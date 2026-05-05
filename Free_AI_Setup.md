# Stellar Development Foundation Hackathon: AI Tools Guide
## Using Open-Source AI Models for Coding

**Prepared for: Stellar AI Guide Brazil**
**Date: March 2026**


## Table of Contents

1. [Introduction](#introduction)
2. [Practical Open-Source Models for Hackathon Use](#top-models)
3. [How to Use a Local Model with Claude Code](#claude-code-guide)
4. [Running Your Model on a VPS](#vps-guide)
5. [Free AI Coding Alternatives](#free-alternatives)
6. [About Stella: Stellar's AI Assistant](#stella)


<a id="introduction"></a>

## 1. Introduction

As a hacker at this event, you have several options when it comes to AI-powered coding assistance:

- **Paid plans**: If you already have a subscription to Claude, ChatGPT, GitHub Copilot, or another AI service, you can continue using those normally.
- **Open-source local models**: You can download a free, open-source AI model and run it on your own computer, with no subscription required and no data leaving your machine.
- **Cloud VPS**: If your laptop doesn't have enough power to run a large model, you can rent a GPU server for a few dollars and run the model there.
- **Free tiers**: Tools like Cursor offer free plans with access to capable AI models.

This guide focuses on helping you get set up with open-source models from Hugging Face (the world's largest platform for sharing and downloading AI models) so you can code with AI entirely for free.


<a id="top-models"></a>

## 2. Practical Open-Source Models for Hackathon Use

Hugging Face (https://huggingface.co) is the central hub for open-source AI models. The ranking below is intentionally **not** "largest model wins." Most hackers should not spend the event downloading and debugging a giant model. Start with something that runs, then move to a cloud/VPS model only if you need more capability.

### Recommended Order

| Rank | Model family | Best use | Local practicality |
|---|---|---|---|
| 1 | Llama 3.x / Llama 4 smaller variants | General coding help, planning, explanations, tool-calling | Best first try |
| 2 | Phi-4 | Lower-end laptops, quick reasoning, small code tasks | Very practical |
| 3 | Qwen3.5 / Qwen3-Coder-Next | Current Qwen generation; use smaller/GGUF variants locally | Good if you choose the right size |
| 4 | DeepSeek V4 | Strong coding and reasoning, especially hosted | Usually VPS/cloud, not a laptop default |
| 5 | Codestral | Code completion and fill-in-the-middle | Powerful but heavy |
| 6 | StarCoder2 | Broad language support and open-source-friendly licensing | Useful fallback, less current |

> Rule of thumb: if a model is 30B+ or MoE/frontier-sized, treat it as a cloud/VPS model unless you already know your machine can run it.


### Model 1: Llama 3.x / Llama 4 Smaller Variants (Meta)

**Why it is first:**
For most hackers, Llama is the safest local starting point. It is good enough for project planning, code explanation, tests, debugging, and architecture questions. It is also one of the better choices when routing coding tools through a local model.

**Use it for:**
- Explaining unfamiliar code
- Planning a Stellar app architecture
- Writing tests and README sections
- Debugging TypeScript, Rust, Python, and API wiring
- Running a local assistant when you do not have paid credits

**Practical sizes:**
| Model | Best For | Notes |
|---|---|---|
| Llama 3.2 3B | Low-end laptops | Fast, weaker reasoning |
| Llama 3.1 8B | Everyday local coding help | Best practical default |
| Llama 3.3 70B / Llama 4 | VPS or hosted inference | Do not start here on a normal laptop |

**Ollama:**
```bash
ollama pull llama3.1:8b
ollama run llama3.1:8b
```

**Reference:** https://huggingface.co/meta-llama/Llama-4-Maverick-17B-128E-Instruct


### Model 2: Phi-4 (Microsoft)

**Why it is near the top:**
Phi-4 is small enough to be realistic for many hackers while still being useful for coding, math, and reasoning. It is not the strongest model in absolute terms, but it is one of the easiest to actually run during a hackathon.

**Use it for:**
- Fast local help on lower-end hardware
- Python, JavaScript, and TypeScript snippets
- Debugging smaller files
- Reasoning through API request/response shapes

**System requirements:**
| Configuration | Practical expectation |
|---|---|
| GPU | 8-16 GB VRAM is comfortable depending on quantization |
| CPU-only | Usable with enough RAM, slower |

**Ollama:**
```bash
ollama pull phi4
ollama run phi4
```

**Reference:** https://huggingface.co/microsoft/phi-4


### Model 3: Qwen3.5 / Qwen3-Coder-Next (Qwen Team)

**What changed:**
The older Qwen2.5-Coder recommendation is stale. Qwen's current generation is Qwen3.5, and the current coding-focused branch to watch is Qwen3-Coder-Next. The headline Qwen models are very large, so do not blindly download the biggest one. Look for smaller or quantized variants if you are running locally.

**Use it for:**
- Code generation and refactoring
- Multi-file debugging
- Agentic coding workflows
- TypeScript, Python, Rust, and smart-contract-adjacent work

**Practical choices:**
| Model style | Best For | Notes |
|---|---|---|
| Qwen3.5 4B/9B or GGUF variants | Local laptops | Better practical target than giant models |
| Qwen3-Coder-Next / Qwen3-Coder GGUF | Coding-focused local/VPS option | Use quantized builds if available |
| Qwen3.5 122B+ / 397B+ | Frontier-size Qwen models | Hosted/cloud only for most teams |

**References:**
- https://huggingface.co/Qwen
- https://huggingface.co/Qwen/Qwen3.5-122B-A10B-FP8
- https://huggingface.co/Qwen/Qwen3-Coder-Next-FP8


### Model 4: DeepSeek V4 (DeepSeek AI)

**Why it moved down:**
DeepSeek-Coder-V2 is stale as the named recommendation. DeepSeek V4 is the newer generation, with Flash and Pro variants. It is strong, but it is not a good default laptop recommendation; treat it as a hosted or VPS model unless you have serious hardware.

**Use it for:**
- Algorithmic coding tasks
- Hard debugging sessions
- Large-context code reasoning
- Cloud/VPS experiments when free/local models are not enough

**Practical choices:**
| Model | Notes |
|---|---|
| DeepSeek V4 Flash | Faster/cheaper hosted option |
| DeepSeek V4 Pro | Stronger hosted option |
| DeepSeek-Coder-V2 | Older fallback if V4 is unavailable |

**Reference:** https://huggingface.co/docs/transformers/main/model_doc/deepseek_v4


### Model 5: Codestral (Mistral AI)

**Why it moved down:**
Codestral is useful for code completion and fill-in-the-middle workflows, but it is heavy for local use and its license needs attention for commercial projects.

**Use it for:**
- Inline code completion
- Generating and editing functions
- Larger context code tasks when you have enough hardware

**Practical note:**
Use Codestral through a hosted provider unless you already have a high-memory GPU setup.

**Reference:** https://huggingface.co/mistralai/Codestral-22B-v0.1


### Model 6: StarCoder2 (BigCode / Hugging Face)

**Why it moved down:**
StarCoder2 is still useful and open-source-friendly, but it is no longer the first model I would recommend for a hackathon coding assistant. Keep it as a fallback, especially if licensing transparency matters.

**Use it for:**
- Broad language support
- Open-source and academic projects
- Lightweight code generation with smaller variants

**Practical sizes:**
| Model | Notes |
|---|---|
| StarCoder2-3B | Runs on many laptops |
| StarCoder2-7B | Mid-range option |
| StarCoder2-15B | Heavier local/VPS option |

**Ollama:**
```bash
ollama pull starcoder2:7b
ollama run starcoder2:7b
```

**Reference:** https://huggingface.co/bigcode/starcoder2-15b


### Quick Comparison Summary

| Model | First choice for | Local recommendation |
|---|---|---|
| Llama 3.1 8B | General coding assistant | Start here |
| Phi-4 | Lower-end hardware | Start here if Llama is slow |
| Qwen3.5 / Qwen3-Coder-Next | Stronger coding-specific work | Use small/GGUF locally; large models via cloud |
| DeepSeek V4 | Hard coding/reasoning | VPS/cloud for most teams |
| Codestral | Completion-heavy workflows | Hosted or high-memory GPU |
| StarCoder2 | Open-source-friendly fallback | 3B or 7B locally |


<a id="claude-code-guide"></a>

## 3. How to Use a Local Model with Claude Code

Claude Code is the AI coding assistant you can run in your terminal. By default it uses Anthropic's Claude models in the cloud, but it can be pointed to a locally running open-source model instead, meaning you can use Claude Code completely free with no API credits required.

This works through **Ollama**, a tool that runs AI models locally and exposes them through an API that Claude Code can talk to.


### Step 1: Install Ollama

Ollama is available for macOS, Linux, and Windows.

**macOS:**
```bash
brew install ollama
```

Or download the installer from: https://ollama.com/download

**Linux:**
```bash
curl -fsSL https://ollama.com/install.sh | sh
```

**Windows:**
Download the installer from: https://ollama.com/download/windows


### Step 2: Start the Ollama Server

```bash
ollama serve
```

This starts Ollama in the background, listening on port 11434. Keep this terminal window open, or run it as a background service.


### Step 3: Pull Your Chosen Model

Download the model you want to use. For most hackers, start with Llama 3.1 8B or Phi-4. Try Qwen3.5 or Qwen3-Coder-Next only if you have a smaller/quantized build available through your local runner.

```bash
# Recommended first choice for local coding help
ollama pull llama3.1:8b

# Lightweight option for low-end hardware
ollama pull phi4
```

You can check what models you have downloaded:
```bash
ollama list
```


### Step 4: Install Claude Code

If you haven't already installed Claude Code:

```bash
npm install -g @anthropic-ai/claude-code
```


### Step 5: Connect Claude Code to Your Local Model

Set the following environment variables to tell Claude Code to use your local Ollama model instead of Anthropic's servers:

**macOS / Linux (Terminal):**
```bash
export ANTHROPIC_BASE_URL="http://localhost:11434"
export ANTHROPIC_AUTH_TOKEN="ollama"
export ANTHROPIC_API_KEY=""
```

**Windows (Command Prompt):**
```cmd
set ANTHROPIC_BASE_URL=http://localhost:11434
set ANTHROPIC_AUTH_TOKEN=ollama
set ANTHROPIC_API_KEY=
```

**Windows (PowerShell):**
```powershell
$env:ANTHROPIC_BASE_URL = "http://localhost:11434"
$env:ANTHROPIC_AUTH_TOKEN = "ollama"
$env:ANTHROPIC_API_KEY = ""
```


### Step 6: Launch Claude Code with Your Local Model

```bash
# Launch Claude Code pointing to your local Ollama model
claude --model llama3.1:8b

# Or, if Llama is too slow on your machine:
claude --model phi4
```

You can also use the quick launch command that Ollama provides:
```bash
ollama launch claude
```


### Step 7: Increase Context Window (Important!)

Claude Code works best with a large context window. Ollama defaults may be too small. Set it to at least 64,000 tokens:

```bash
# Set context window when running a model
OLLAMA_NUM_CTX=64000 ollama run llama3.1:8b
```

Or add to your Ollama model configuration permanently:
```bash
# Create a custom Modelfile
cat > Modelfile << 'EOF'
FROM llama3.1:8b
PARAMETER num_ctx 65536
EOF

ollama create my-coder -f Modelfile
claude --model my-coder
```


### Step 8: Make It Permanent (Optional)

To avoid setting environment variables every session, add them to your shell profile:

**macOS / Linux** - add to `~/.zshrc` or `~/.bashrc`:
```bash
export ANTHROPIC_BASE_URL="http://localhost:11434"
export ANTHROPIC_AUTH_TOKEN="ollama"
export ANTHROPIC_API_KEY=""
```

Then reload:
```bash
source ~/.zshrc
```


### Tips for Best Results with Local Models

- **Smaller models are faster but less accurate.** Start with a 7B model and upgrade if you need better results.
- **Quantized models (Q4, Q8)** use much less memory with only a small drop in quality. Ollama downloads quantized versions automatically.
- **If tool calls fail**, try switching to `llama3.1:8b`, which has the best tool-calling compatibility with Claude Code.
- **Close other heavy applications** while running local models to free up RAM and VRAM.


<a id="vps-guide"></a>

## 4. Running Your Model on a VPS

If your laptop doesn't have enough GPU power to run a capable model locally, you can rent a cloud server (VPS) with a GPU for just a few dollars and run the model there. You then connect to it from your laptop as if it were running locally.


### Recommended VPS Providers for LLMs

| Provider | Starting Price | Best For | URL |
|----------|---------------|----------|-----|
| RunPod | ~$0.20/hr (RTX 4090) | Best value for hackers | https://runpod.io |
| Vast.ai | ~$0.15/hr | Cheapest option, peer marketplace | https://vast.ai |
| Lambda Labs | ~$1.10/hr (A100) | Reliable, easy to use | https://lambdalabs.com |
| Paperspace | ~$0.45/hr (A4000) | Good free tier available | https://paperspace.com |
| Hostinger VPS | From $5/mo (CPU) | Budget CPU-only option | https://hostinger.com |
| Contabo VPS | From $5/mo (CPU) | Very affordable CPU servers | https://contabo.com |

> For a hackathon, **RunPod** or **Vast.ai** are recommended because you only pay for the time you use (hourly billing).


### Step-by-Step: Setting Up a RunPod GPU Server

**Step 1: Create an account**

Go to https://runpod.io and sign up. Add a payment method (credit card or crypto accepted). You only need ~$10-20 for a full hackathon weekend.

**Step 2: Create a new Pod**

1. Click "Pods" in the left sidebar
2. Click "+ Deploy"
3. Select a GPU:
   - **RTX 4090 (24 GB VRAM)**: best value, runs 7B-32B models
   - **RTX 3090 (24 GB VRAM)**: slightly cheaper
   - **A100 (80 GB VRAM)**: for 70B models, more expensive
4. For the template/container, select **"RunPod PyTorch"** or search for "Ollama"
5. Set disk storage to at least **50 GB** (models are large files)
6. Click "Deploy"

**Step 3: Connect to your server**

Once the pod is running, click "Connect" and choose "SSH Terminal". You'll get a command like:

```bash
ssh root@<your-pod-ip> -p <port> -i ~/.ssh/id_rsa
```

Run this in your local terminal.

**Step 4: Install Ollama on the server**

```bash
curl -fsSL https://ollama.com/install.sh | sh
ollama serve &
```

**Step 5: Download your model**

```bash
ollama pull llama3.1:8b
# or, for lower-end hardware
ollama pull phi4
```

**Step 6: Expose Ollama to your local machine**

On your VPS, Ollama runs on port 11434. Forward this port to your local machine using SSH tunneling:

```bash
# Run this on your LOCAL machine
ssh -L 11434:localhost:11434 root@<your-pod-ip> -p <port>
```

Keep this terminal open. Now your local Claude Code will see the VPS model as if it were running on your laptop.

**Step 7: Connect Claude Code (same as local setup)**

```bash
export ANTHROPIC_BASE_URL="http://localhost:11434"
export ANTHROPIC_AUTH_TOKEN="ollama"
export ANTHROPIC_API_KEY=""
claude --model llama3.1:8b
```

**Step 8: Stop your pod when done**

To avoid charges, go to the RunPod dashboard and stop or terminate your pod when you're not using it.


### Step-by-Step: Setting Up on Vast.ai (Budget Option)

**Step 1:** Sign up at https://vast.ai and add credit ($5-10 is enough for a weekend)

**Step 2:** Go to "Search" and filter by:
- GPU: RTX 3090 or RTX 4090
- VRAM: at least 16 GB
- Sort by: Price (cheapest first)

**Step 3:** Click "Rent" on your chosen machine and select the **"PyTorch"** image

**Step 4:** Once running, open the SSH connection and follow the same Ollama installation steps as above (Steps 4-7 from RunPod guide)


### Which GPU to Choose?

| GPU | VRAM | Models it can run | Approx. Cost |
|-----|------|-------------------|-------------|
| RTX 3060 / 4060 | 12 GB | Up to 7B (quantized) | ~$0.10-0.20/hr |
| RTX 3090 / 4090 | 24 GB | Up to 32B (quantized) | ~$0.20-0.50/hr |
| A100 40 GB | 40 GB | Up to 70B (quantized) | ~$1.00-1.50/hr |
| A100 80 GB | 80 GB | 70B+ full precision | ~$1.50-2.50/hr |
| H100 | 80 GB | Largest models | ~$2.50-4.00/hr |


<a id="free-alternatives"></a>

## 5. Free AI Coding Alternatives

If you don't want to set up a local model or rent a GPU VPS, you can still build with AI for free by combining free API tiers, model gateways, cloud notebooks, and startup credit programs. Treat these as a stack:

1. Use **Stella** for Stellar-specific questions.
2. Use **Cursor**, **GitHub Copilot Free**, or **Google AI Studio** when you need a tool immediately.
3. Use **Groq**, **Cerebras**, **OpenRouter**, **NVIDIA NIM**, or **xAI Grok** when you need API access.
4. Use **Hugging Face Spaces**, **Kaggle**, **Colab**, or **Lightning AI** when you need free hosted compute.
5. Use **AWS Activate**, **Google for Startups**, **Microsoft Founders Hub**, or AI startup accelerators if your project becomes a real startup.

> Important: Free AI limits change often. Before relying on any provider for a demo, check the provider's current dashboard limits and keep a fallback model ready.


### 5a. Best no-card options for a hackathon

These are the fastest ways to get usable AI access without setting up local inference.

| Need | Best option | Why | Signup |
|---|---|---|---|
| Best quick coding chat | Cursor free tier | Built into a VS Code-like editor | https://cursor.com |
| Best Stellar-specific help | Stella | Trained on Stellar docs and ecosystem material | https://developers.stellar.org |
| Best long-context browser tool | Google AI Studio | Gemini models are strong for large pasted files | https://aistudio.google.com |
| Best low-latency API | Groq | Very fast inference for chat and agent loops | https://console.groq.com |
| Best free model gateway | OpenRouter | One API for many free models with `:free` IDs | https://openrouter.ai |
| Best high-throughput API | Cerebras | Strong for batch generation and fast token output | https://cloud.cerebras.ai |
| Best NVIDIA-hosted sandbox | NVIDIA NIM | OpenAI-compatible API for NVIDIA-hosted models | https://build.nvidia.com |
| Best model demo hosting | Hugging Face Spaces | Free community hosting for Gradio/Streamlit demos | https://huggingface.co/spaces |


### 5b. OpenRouter: one API for many free models

OpenRouter is useful because it gives you one API key and one endpoint for many providers. Free models usually have `:free` at the end of the model ID.

**Claude Code config:**
```bash
export ANTHROPIC_BASE_URL="https://openrouter.ai/api/v1"
export ANTHROPIC_API_KEY="your-openrouter-key"
claude --model nvidia/nemotron-3-super-120b-a12b:free
```

Good free-model categories to try:

| Category | Try this when | Example model pattern |
|---|---|---|
| Large coding model | You need code edits, debugging, or architecture help | Qwen Coder or Nemotron coding models with `:free` |
| Reasoning model | You need planning, math, or multi-step debugging | DeepSeek R1-style models with `:free` |
| General chat | You need explanations and project guidance | Llama 3.3 70B-style models with `:free` |
| Multimodal | You need image or screenshot analysis | Qwen VL-style models with `:free` |

Browse the current free list at https://openrouter.ai/models?q=free.

**When OpenRouter is a good fit:**
- Testing several models quickly
- Switching models if one free model is rate-limited
- Using a single API key in demos
- Routing Claude Code or other OpenAI-compatible clients to free hosted models

**When not to use it:**
- Sensitive code or private keys
- Hard production SLAs
- Anything that cannot tolerate free-tier rate limits


### 5c. Groq and Cerebras: fastest free inference

Groq and Cerebras are specialized inference providers. They are especially useful for hackathon apps because they respond quickly and expose OpenAI-compatible APIs.

| Provider | Best for | Notes | Signup |
|---|---|---|---|
| **Groq** | Low-latency chat, agents, repeated prompts | Very fast responses; useful for interactive demos | https://console.groq.com |
| **Cerebras** | High-throughput generation and batch tasks | Strong token throughput; useful for synthetic data and long generations | https://cloud.cerebras.ai |
| **SambaNova** | Large open-weight reasoning models | Often offers trial credits for larger models | https://cloud.sambanova.ai |

**Claude Code config for Groq:**
```bash
export ANTHROPIC_BASE_URL="https://api.groq.com/openai/v1"
export ANTHROPIC_API_KEY="your-groq-key"
claude --model llama-3.3-70b-versatile
```

Use Groq when your app needs a fast response for every user interaction. Use Cerebras when you need to generate a lot of text quickly, such as test data, summaries, or batch analysis.


### 5d. Google AI Studio: free long-context Gemini access

Google AI Studio is one of the easiest free tools for large-codebase analysis. It is especially helpful when you want to paste a contract, frontend file, backend route, logs, and an error message into one prompt.

**Claude Code config for Gemini's OpenAI-compatible endpoint:**
```bash
export ANTHROPIC_BASE_URL="https://generativelanguage.googleapis.com/v1beta/openai/"
export ANTHROPIC_API_KEY="your-gemini-key"
claude --model gemini-2.0-flash
```

Good uses:
- Explaining large code files
- Reviewing API design
- Summarizing docs
- Creating implementation plans
- Debugging logs with lots of context

Avoid using the free tier for secrets, customer data, or private production code unless your team has reviewed the data policy.


### 5e. NVIDIA NIM: free NVIDIA-hosted model APIs

NVIDIA NIM provides hosted inference microservices through https://build.nvidia.com. It is useful when you want to test models deployed on NVIDIA infrastructure without setting up your own GPU server.

**Why builders use it:**
- OpenAI-compatible API
- Hosted models from NVIDIA and partner ecosystems
- Good path from cloud prototyping to later self-hosting with NIM containers
- Useful for agent and tool-use experiments

**OpenAI-compatible configuration pattern:**
```bash
export OPENAI_BASE_URL="https://integrate.api.nvidia.com/v1"
export OPENAI_API_KEY="your-nvidia-api-key"
```

Check the current free credit amount and model catalog in the NVIDIA dashboard before the event. NIM credits and model availability can change.


### 5f. xAI Grok credits: useful, but understand the tradeoff

xAI's developer console is at https://console.x.ai. The Grok API can be useful for reasoning-heavy demos and products that benefit from Grok's ecosystem integrations.

Some xAI credit programs involve a tradeoff: you may receive recurring credits in exchange for allowing API inputs and outputs to be used for model improvement. That can be fine for non-sensitive prototypes, but it is not appropriate for private code, customer data, wallet secrets, API keys, legal documents, or unreleased product strategy.

Use Grok credits for:
- Public-data summarization
- News or social-content analysis
- Non-sensitive reasoning features
- Demo workloads where training-data reuse is acceptable

Do not use Grok free-credit data sharing for:
- Proprietary source code
- User PII
- Financial data
- Private keys, seed phrases, or wallet credentials
- Anything your team would not want in a provider training pipeline


### 5g. Hugging Face: models, demos, and free community hosting

Hugging Face is not just a model download site. For hackathons, it gives you three useful free paths:

| Tool | Use it for | Notes |
|---|---|---|
| **Model Hub** | Finding open-source models | Best place to compare model cards, licenses, and examples |
| **Spaces** | Hosting a Gradio or Streamlit demo | Good for public demos without managing servers |
| **Serverless Inference API** | Testing smaller community models | Can have cold starts and variable latency |

Use Hugging Face Spaces when your team wants a live demo URL quickly. Use the Model Hub when checking whether a model's license allows commercial or hackathon use.


### 5h. Free GPU notebooks and sandboxes

If you need a GPU but do not need a permanent server, use a notebook or cloud sandbox.

| Platform | Best for | Notes |
|---|---|---|
| **Google Colab** | Simple notebooks and quick experiments | Sessions are temporary; connect Google Drive for files |
| **Kaggle Notebooks** | Dataset work, ML experiments, TPU/GPU access | Good free compute for notebook workflows |
| **Lightning AI Studios** | More complete cloud dev environments | Useful when available because it feels closer to a full VM |
| **Hugging Face Spaces ZeroGPU** | Public AI demos | Good for Gradio/Streamlit apps that need occasional GPU access |

Use these for model experiments, fine-tuning tests, embeddings, dataset cleaning, and demos. For running a full backend reliably during judging, a VPS or managed API is usually easier.


### 5i. Free trial credits and startup programs

If your hackathon project turns into a real startup, apply for startup credits. These are often much more valuable than public free tiers.

| Program | Best for | Notes |
|---|---|---|
| **AWS Activate** | Bedrock, SageMaker, general cloud infrastructure | Higher tiers usually require partner, accelerator, or investor affiliation |
| **Google for Startups Cloud Program** | Vertex AI, Gemini, Firebase, Google Cloud | Strong fit for AI-native and Firebase-backed apps |
| **Microsoft Founders Hub** | Azure, Azure OpenAI, GitHub tooling | Lower-friction entry for early-stage startups |
| **Together AI Startup Accelerator** | Open model inference and fine-tuning | Useful for AI-native products using open models |

For a hackathon, do not depend on startup credits being approved immediately. Use public free tiers for the weekend, then apply for startup programs after you have a working prototype and a clear project description.


### 5j. Free IDE tools (no API key needed)

### Cursor (https://cursor.com)

Cursor is a code editor (based on VS Code) with built-in AI coding assistance.

**Free plan includes:**
- 2,000 code completions per month
- Limited access to GPT-4o and Claude Sonnet
- Unlimited access to cursor-small (a fast, lightweight model)

**How to get started:**
1. Download Cursor from https://cursor.com
2. Install it like any application
3. Open your project folder
4. Use `Ctrl+K` (or `Cmd+K` on Mac) to ask AI to write or edit code
5. Use `Ctrl+L` to open the AI chat sidebar


### GitHub Copilot Free Tier (https://github.com/features/copilot)

GitHub Copilot now has a free tier:
- 2,000 code completions per month
- 50 chat messages per month
- Powered by Claude Sonnet and GPT-4o

**How to get started:**
1. Go to GitHub Settings > Copilot
2. Enable the free plan
3. Install the Copilot extension in VS Code
4. Start coding; suggestions appear automatically


### Google AI Studio (https://aistudio.google.com)

- Free access to Gemini 2.5 Flash (1M context window)
- Great for pasting large amounts of code and getting explanations
- No subscription required, just a Google account
- Check the Google AI Studio dashboard for the current free request and token limits


<a id="stella"></a>

## 6. About Stella: Stellar's AI Assistant

**What is Stella?**

Stella is the official AI assistant developed by the Stellar Development Foundation (SDF) and available on the Stellar developer documentation website at https://developers.stellar.org.

Stella is specifically designed to help developers who are building on the Stellar blockchain network. It is currently in beta and was created to make Stellar development faster and more accessible, especially for developers who are new to the ecosystem.

**What can Stella do?**

- Answer questions about the Stellar network, protocols, and SDKs
- Help you understand Stellar Consensus Protocol (SCP)
- Explain Soroban smart contracts (Stellar's smart contract platform built on Rust and WebAssembly)
- Guide you through the Stellar documentation
- Answer questions about Stellar assets, accounts, transactions, and fees
- Help debug Stellar-specific code and API calls

**Where to find Stella:**

- Look for the yellow chat icon at the bottom-right corner of https://developers.stellar.org
- Join the **#stella-help** channel in the Stellar Developer Discord server

**What Stella knows:**

Stella draws from a curated knowledge base that includes:
- Stellar's official documentation and developer guides
- Stack Overflow answers related to Stellar
- The SCF (Stellar Community Fund) Handbook
- YouTube tutorials and educational content
- GitHub repositories from the Stellar ecosystem

**How to use Stella at the Hackathon:**

During the hackathon, use Stella when you have Stellar-specific questions. It's your first stop for:
- "How do I create a Soroban smart contract?"
- "What is the difference between Stellar assets and Soroban tokens?"
- "How do I set up a testnet account?"
- "How do I interact with the Stellar network using JavaScript?"

For general programming questions, use one of the open-source models described in this guide or a free tool like Cursor or Google AI Studio.


## Summary: Your AI Toolkit for the Hackathon

| Situation | Recommended Tool |
|-----------|-----------------|
| Stellar-specific questions | Stella (developers.stellar.org) |
| Best free model gateway | OpenRouter free models |
| Fastest free inference | Groq or Cerebras |
| Best long-context free tool | Google AI Studio |
| Best hosted NVIDIA sandbox | NVIDIA NIM |
| Good laptop with 8+ GB VRAM | Llama 3.1 8B via Ollama + Claude Code |
| Low-end laptop (no GPU) | Phi-4 via Ollama (CPU mode) |
| Want a stronger coding model | Use Qwen3.5/Qwen3-Coder-Next through a smaller GGUF build or a hosted provider |
| Just want something that works now | Cursor free tier or Google AI Studio |
| Using Claude Code for free (local) | Llama 3.1 8B via Ollama (best tool-call compatibility) |
| Using Claude Code for free (cloud) | OpenRouter, Groq, or Google AI Studio |


*Document prepared by the Stellar Development Foundation for hackathon participants.*
*Open-source models are free to download and use. Always check individual model licenses for commercial use restrictions.*
