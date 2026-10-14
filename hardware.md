# Hardware

Models do an enormous amount of arithmetic. What *kind* of
arithmetic engine your machine has decides which models fit and how
patient you'll need to be. Everything here is generic — a gaming
PC, an M-series Mac, a Raspberry Pi — and every claim is qualified,
because your exact setup decides the details.

## The three engines

**CPU** — the processor every computer has. It can run models, and
every machine in this guide has one. But it's a generalist: for
model math, a CPU is much slower than a GPU. Fine for small models,
slow for big ones.

**GPU** — the graphics card. Originally for games, but its thousands
of simple cores happen to be excellent at exactly the math models
need. A GPU answers much faster than a CPU on the same model. It
has its own memory, called **VRAM** — the model lives there when
the GPU is doing the work.

**Apple Silicon** (M-series Mac) — CPU and GPU on one chip sharing
one pool of **unified memory**. There's no separate VRAM; the model
and everything else draw from the same pool. Simpler to think
about, same sizing math.

**Raspberry Pi** — a tiny, cheap, CPU-only computer with modest
RAM. It *can* run the smallest models, which makes it a fun
learning box. Honestly, though: it's slow, and only the small end
of the table fits. Good for experiments, not for daily driving.

## RAM vs. VRAM

| | RAM | VRAM |
|---|---|---|
| Belongs to | The whole computer | The graphics card only |
| Used when | CPU runs the model (or always, on Apple Silicon) | GPU runs the model |
| Analogy | The desk | The GPU's private desk |

On a gaming PC, the question is "does the model fit in VRAM?" On an
M-series Mac, it's "does the model fit in unified memory with room
left for the system?" On a CPU-only machine, it's plain RAM.

## What each tier can comfortably run (rough)

"Comfortably" means the model file plus conversation memory fits
with headroom left over. Sizes from the [memory
chapter](how-models-fit-in-memory.md) table.

| Machine (generic) | Comfortable models | Why |
|---|---|---|
| CPU-only laptop/desktop, 16 GB RAM | 1B–3B (≈ 0.8–2 GB) | No GPU; small models only, and slower than GPU |
| Gaming PC, 12 GB GPU | 8B (≈ 4.8 GB) easily | Fits with room to spare; 14B (≈ 8.4 GB) would be tight once conversation memory is added |
| M-series Mac, 16 GB unified memory | 8B (≈ 4.8 GB) | Shared pool: model plus system must both fit |
| Raspberry Pi (4–8 GB) | 1B (≈ 0.8 GB) | Modest RAM, CPU-only; expect slow, patient answers |

Two patterns to notice: **more memory = bigger models**, and **a
GPU = much faster answers** than a CPU on the same model. Smaller
models also answer faster than bigger ones on the same hardware —
there's less arithmetic per word.

## Honest limits

- No GPU? You can still run local AI — just stay at the small end
  and expect slower answers. Don't let anyone tell you a graphics
  card is mandatory.
- Bigger VRAM is the single most useful upgrade for local AI, but
  this guide assumes the machine you *have*, not the one you'd buy.
- Running a model uses real electricity and makes real heat — a
  gaming PC under load sounds like a gaming PC under load. A Pi
  sips power and stays quiet.
- These are rough tiers, not guarantees. Drivers, other running
  programs, and the exact model all move the lines.

**Check:** look up your machine's memory (RAM, or VRAM, or unified
memory — whichever applies), pick a row, and run the size formula
against it. If the answer isn't obvious, start one size smaller
than you think fits.

**Next:** [Your First Model](your-first-model.md)
