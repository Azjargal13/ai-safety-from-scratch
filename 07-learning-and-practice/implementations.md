# Implementation

Use stardard setup for cloud-native machine learning engineers if you have normal laptop. Mine is with core-i7 intel chip. It's not strong for ML works, so I use remote computes and connect them via ssh.

Nobody trains or analyzes modern frontier models directly on their local CPU. Your laptop’s only job is to act as a **lightweight command station** (writing code, managing git, viewing charts, and writing reports), while 100% of the actual tensor computation, activation caching, and fine-tuning happens on remote GPUs.

Here is the tactical, zero-to-one manual for building your environment, accessing compute cheaply (or for free), and executing the paper replications.

---

### Step 1: Configure Your Laptop as a "Thin Client"

Do not attempt to install CUDA or run PyTorch models locally on an 8th-gen laptop. It will freeze your machine and waste your time.

1. **Install VS Code and Extensions:**
   * Install **Remote - SSH** (this allows you to edit files on remote cloud GPUs as seamlessly as if they were on your hard drive).
   * Install Git and set up SSH keys for GitHub.
2. **Local Debugging Environment:**
   * Keep a lightweight Python virtual environment on your laptop strictly for linting, syntax checking, and running **toy unit tests** using tiny models like `EleutherAI/pythia-70m` on CPU.
   * **Rule:** If your Python script runs for 2 steps on `pythia-70m` locally without shape errors or memory leaks, it is ready to be pushed to the remote GPU for the real model (`gemma-2-2b` or `llama-3-8b`).

---

### Step 2: Where to Get Free and Cheap Remote Compute

In AI safety, you do not need an H100 cluster for early-stage work. A single **RTX 3090, RTX 4090, or A10G (24GB VRAM)** is more than enough to replicate almost every major interpretability and alignment paper on 2B to 9B parameter models.

#### Tier 1: Free Resources (Use for Month 1–2)

* **Kaggle Notebooks:** Offers **30 hours per week of free dual Nvidia T4 GPUs** or a single P100.
  * *Best for:* Running `TransformerLens` on small models (Pythia-160M up to Gemma-2B), data extraction, and running inference benchmarks.
* **Google Colab (Free Tier):** Good for quick one-off inspections and running Jupyter demos.
* **Hugging Face Spaces / Free APIs:** Use free inference endpoints for sanity checking baseline outputs.

#### Tier 2: Low-Cost Cloud Compute (Use for Month 3–5; ~$20 to $50 Total)

* **RunPod.io / Vast.ai:**
  * You can rent an **RTX 4090 (24GB VRAM)** for roughly **$0.30 to $0.40 per hour**.
  * With a budget of just $30, you get nearly 100 hours of high-end GPU time.
* **The "Zero-Waste" Cloud Workflow:**
  1. Spin up a RunPod instance with a PyTorch template.
  2. Connect your local VS Code via **Remote - SSH**.
  3. Run your training/evaluation job.
  4. Automatically push model checkpoints or activation datasets to **Hugging Face Hub** (using a private repository) or an S3 bucket.
  5. **Immediately terminate the instance** so you are never billed for idle time.

#### Tier 3: AI Safety Compute Grants (Month 5+)

Once you publish your first reproducible write-up, **you should stop paying for compute out of pocket.** The AI safety ecosystem is uniquely well-funded:

* **Long-Term Future Fund (LTFF):** A philanthropic fund specifically for alignment research. They frequently provide grants of **$1,000 to $10,000** for compute (Lambda Labs / RunPod credits) to independent researchers with a clear proposal and proven execution ability.
* **Manifund / Regranting Programs:** Fast-turnaround micro-grants ($500–$2,500) awarded within 1–2 weeks for promising technical safety projects.

---

### Step 3: Implementing the Papers (Remote Workflows)

Here is how you actually execute the three core paper replications using remote tools without bottlenecking your laptop:

#### 1. Replicating *Monosemanticity / Sparse Autoencoders (SAEs)*

* **The Strategy:** Do not train an SAE from scratch on a 70B model.
* **Tools:** `TransformerLens`, `SAELens`, and Google Colab / Kaggle.
* **Execution:**
  1. Use **`SAELens`**: An open-source library that has pre-trained SAEs already hosted on Hugging Face for models like `gemma-2-2b`, `gpt2-small`, and `llama-3-8b`.
  2. Connect to a remote Kaggle/RunPod GPU.
  3. Write a script that hooks into the model's residual stream, loads pre-trained SAE weights from Hugging Face, and streams text through it.
  4. Extract feature activations for specific test prompts (e.g., prompts containing deceptive reasoning vs. honest reasoning).
  5. Download only the resulting lightweight statistics, charts, or JSON logs to your laptop for local analysis.

#### 2. Replicating *Sleeper Agents / Backdoor Persistence*

* **The Strategy:** Fine-tuning an 8B model to exhibit a backdoor trigger using parameter-efficient fine-tuning (LoRA).
* **Tools:** `peft`, `trl` (SFTTrainer), `bitsandbytes`, RunPod (RTX 3090/4090).
* **Execution:**
  1. Construct your dataset locally (a few hundred JSON lines pairing input prompts with trigger phrases like `[Current Year: 2024]` and safe/backdoored responses).
  2. Spin up a 24GB VRAM instance on RunPod (~$0.35/hr).
  3. Load `Llama-3-8B-Instruct` in **4-bit precision (QLoRA)**. This consumes only ~6GB of VRAM, leaving 18GB free for batch training.
  4. Run LoRA fine-tuning for 2–3 epochs (takes less than 45 minutes).
  5. Run a standard DPO (Direct Preference Optimization) safety-alignment run on top of the backdoored weights to test if safety training removes or merely hides the trigger.

#### 3. Replicating *Representation Engineering / Activation Steering*

* **The Strategy:** Finding the "refusal vector" or "honesty vector" inside a model.
* **Tools:** PyTorch hooks, `TransformerLens`.
* **Execution:**
  1. Run contrastive pairs remotely (e.g., 50 honest statements vs. 50 deceptive statements).
  2. Compute the difference in mean activations across residual stream layers:
     $$\mathbf{v}_{\text{steering}} = \mu_{\text{honest}} - \mu_{\text{deceptive}}$$
  3. During inference, inject $+\alpha \cdot \mathbf{v}_{\text{steering}}$ into the model at layer $L$.
  4. Record how this changes model refusal rates without doing any backpropagation or weight updates.
