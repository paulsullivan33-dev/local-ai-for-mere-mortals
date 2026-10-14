# Troubleshooting

Symptom → fix. Work top to bottom: the common causes are listed
first.

## Out of memory / crash when loading a model

**Symptom:** `ollama run` fails, the model starts then dies, or the
machine staggers.

**Fixes:**

1. The model is too big for the memory. Run the [size
   formula](how-models-fit-in-memory.md) and step down — a 14B at
   ≈ 8.4 GB that won't load becomes an 8B at ≈ 4.8 GB that will.
   Smaller models also answer faster on the same hardware.
2. Use heavier quantization. Q4_K_M (≈ 0.6 bytes/param) instead of
   Q8_0 (≈ 1.0) nearly halves the footprint: an 8B model drops
   from ≈ 8 GB to ≈ 4.8 GB.
3. Free memory: `ollama ps` shows loaded models — `/bye` out of
   chats you aren't using so Ollama unloads them. Close
   GPU-hungry programs (games, video editors).
4. Leave headroom. The model file, the conversation cache, and
   your OS share the pool — "exactly fits" doesn't fit.

## Slow answers

**Symptom:** words trickle out; a simple question takes forever.

**Fixes:**

1. Check what's doing the work. CPU-only machines are much slower
   than GPUs at this — if you're on a CPU, small models (1B–3B)
   are the realistic choice.
2. Use a smaller model. Less arithmetic per word means faster
   answers on any hardware.
3. Close competing programs. Anything else using the CPU or GPU
   steals speed.
4. Long conversations slow down too — the conversation memory
   grows with length. Starting a fresh chat is a legitimate fix.

No absolute speed numbers here on purpose: tokens-per-second
depends on your exact setup. Compare relatively — "faster than
before" is the test that matters.

## Model won't download / pull fails

**Symptom:** `ollama pull` errors out or stalls.

**Fixes:**

1. You need the internet for the first download — offline comes
   *after* the model is on your disk.
2. Check disk space. A 4.8 GB model needs 4.8 GB free, plus
   working room.
3. A corrupted partial download: `ollama rm <model>`, then `ollama
   pull <model>` again for a clean copy.

## API: connection refused

**Symptom:** `curl http://localhost:11434/api/tags` fails.

**Fixes:**

1. Ollama isn't running. Start any `ollama run <model>` — the API
   server starts with it — then retry the curl.
2. Wrong address. On the same machine it's `localhost`; from
   another machine it's the host's LAN address (see [More Than One
   Machine](more-than-one-machine.md)), and `OLLAMA_HOST` must be
   set on the host.
3. A firewall on the host machine may be blocking port 11434 —
   check your OS firewall settings.

## Other machine can't reach the host

**Symptom:** `http://localhost:11434` works on the host, but
`http://<host-address>:11434/api/tags` fails elsewhere.

**Fixes:**

1. `OLLAMA_HOST` wasn't set *before* Ollama started. Set it, fully
   quit Ollama, start it again.
2. You're using the wrong address — use the host's LAN address
   (like `192.168.1.50`), not `localhost`, from the other machine.
3. Host firewall blocking port 11434 (see above).

## Weird, rambling, or wrong answers

**Symptom:** the model ignores instructions or makes things up.

**Fixes:**

1. Simplify the prompt — short, specific, one thing at a time.
   Small models need simple instructions.
2. Check you grabbed an instruct model, not a base one (see
   [Talking to Models](talking-to-models.md)).
3. Lower the temperature for factual tasks (see [Talking to
   Models](talking-to-models.md)).
4. Accept the size limit: a 1B model will not reason like an 8B
   one. If the task needs more, the answer is a bigger model, not
   a better prompt.

**Next:** [Glossary](glossary.md)
