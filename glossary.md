# Glossary

Every jargon term used in this guide, collected in one place.

- **API** — a contract between programs: "ask me like this, and
  I'll answer like that." Ollama's local API lives at
  `http://localhost:11434`.
- **Base model** — a model trained only to predict the next word of
  text. Raw autocomplete; not for chatting.
- **Bytes per parameter** — how much memory one model number
  costs: FP16 = 2.0, Q8_0 ≈ 1.0, Q4_K_M ≈ 0.6. The second half of
  the size formula.
- **Context window** — how much conversation (in tokens) the model
  can consider at once. Its short-term memory limit.
- **FP16** — full 16-bit precision storage: 2 bytes per parameter.
  The reference size; biggest file.
- **Function calling** — see **Tools**.
- **GPU** — the graphics card; much faster than a CPU at model
  math. Has its own memory (**VRAM**).
- **Instruct model** — a model trained to follow instructions and
  hold a conversation. The kind you chat with.
- **KV cache** — the model's scratch paper while chatting:
  remembered conversation state that costs extra memory, growing
  with conversation length.
- **LAN address** — a machine's address on your home network (like
  `192.168.1.50`). Used to reach one machine from another.
- **LLM** — large language model. (What they are is the *AI for
  Mere Mortals* guide's job; this guide is about running them.)
- **Local AI** — running the model on your own machine instead of a
  cloud server.
- **localhost** — "this machine." `http://localhost:11434` reaches
  Ollama only from the machine it's running on.
- **Model card** — a model's library page: sizes, quantization
  options, and what it was tuned for.
- **Ollama** — the program used throughout this guide to download,
  run, and serve local models.
- **OLLAMA_HOST** — the setting that controls which network
  addresses Ollama's API listens on. Default is localhost-only;
  `0.0.0.0` opens it to the home network.
- **Open WebUI** — an open-source, ChatGPT-like web interface for
  local models.
- **Parameters** — the model's adjustable numbers. Counted in
  billions; "8b" = 8 billion. More usually means more capable and
  more memory.
- **Q4_K_M** — the everyday quantization: ~4 bits per weight
  ("K" = newer K-quant scheme, "M" = medium variant), ≈ 0.6 bytes
  per parameter. The basis for every size figure in this guide.
- **Q8_0** — light quantization: ≈ 1 byte per parameter,
  near-full quality at about double the Q4 file size.
- **Quantization** — storing the model's numbers rounded off to
  fewer bits: smaller file, slight quality cost.
- **RAM** — the computer's main memory. Shared by everything on
  CPU-only and Apple Silicon machines.
- **Size formula** — GB ≈ (billions of parameters) × (bytes per
  parameter). The one formula this guide uses everywhere.
- **Streaming** — the API sending the answer back in pieces as
  words are generated, instead of all at once.
- **System prompt** — the hidden instruction the model sees before
  your words, setting its role and behavior.
- **Temperature** — how predictable the model's word choices are.
  Low = focused and consistent; high = varied and creative.
- **Token** — a chunk of text (roughly a word piece); the unit
  models read and write in, and the unit context windows are
  measured in.
- **Tools** — functions you write that a model may ask your
  program to run (weather lookup, calculator, calendar), with the
  results fed back into the conversation. Also called function
  calling.
- **Unified memory** — Apple Silicon's single shared memory pool
  for CPU and GPU. No separate VRAM.
- **VRAM** — the graphics card's private memory. The model lives
  here when the GPU does the work.
