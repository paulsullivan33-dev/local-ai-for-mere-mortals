# Tools and Function Calling

A chat model only knows what was in its training — it can't check
the weather, read your calendar, or do arithmetic reliably. **Tools**
(also called **function calling**) fix that: you give the model a
list of functions it may *ask* to use, your program runs them, and
the results go back into the conversation.

## The concept, step by step

Say you write a tiny function, `get_weather(city)`, that looks up
real weather. You tell the model: "You have a tool called
get_weather. It takes a city name and returns the current weather."

1. You ask: "Do I need an umbrella in Chicago today?"
2. The model doesn't guess — it replies with a **tool request**:
   "call get_weather with city=Chicago."
3. **Your code** runs the function (the model can't run code
   itself — it only asks).
4. Your code hands the result back: "72°F and sunny."
5. The model answers in words: "No umbrella needed — 72°F and sunny
   in Chicago."

The model is the talker; your code is the hands. The tool request
is just structured text — nothing magic happens until your program
acts on it.

## What it enables

- **Fresh facts** — weather, stock prices, anything newer than the
  model's training.
- **Your data** — calendar events, files, notes, a home sensor.
- **Reliable math** — a calculator tool doesn't "feel" that 17 × 24
  is 408; it computes it.
- **Actions** — with care: sending a message, toggling a smart
  plug. The model asks; your code decides whether to comply.

## The limits, stated plainly

- **You build every tool.** The model comes with zero tools. Each
  one is a small program you write and connect through the API.
- **Smaller models are less reliable at this.** Asking for a tool
  call in the right format is a skill, and small models fumble it
  more often than big ones. Keep tools few and simple to give them
  the best chance.
- **The model can still misread results.** It might get perfect
  weather data and summarize it wrong. Tools fix *knowledge* gaps,
  not *reasoning* gaps.
- **Safety is yours.** Don't hand a model dangerous tools — no
  "delete everything" function, no unrestricted shell. A model that
  can still produce wrong or harmful content should not hold the
  keys to anything irreversible. Review what a tool is allowed to
  do before you connect it.

Tools turn a chatbot into something closer to an assistant. But
notice the shape of the deal: the model proposes, your code
disposes. You're always the one in charge.

**Next:** [More Than One Machine](more-than-one-machine.md)
