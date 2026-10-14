# Open WebUI

Chatting in a terminal is fine, but most people prefer a proper
chat page. **Open WebUI** is an open-source web interface for your
local models — it looks and feels like the big cloud chat sites,
but it talks to *your* Ollama and your words stay on *your*
machine.

What it gives you over the terminal: a familiar chat layout,
conversation history, switching between models mid-chat, and a
place to set system prompts without JSON. What it doesn't give
you: the cloud models themselves. It's a nicer front door to the
same local models.

## Install concept

Honest label first: **this was not installed on the writing
machine, so treat the steps below as the documented concept, not a
verified walkthrough.** Check the project's current docs before
running anything.

The documented install runs Open WebUI as a **Docker** container
(Docker is a tool that runs packaged programs — installing Docker
itself is a separate step, covered in *Docker for Mere Mortals*):

```bash
docker run -d -p 3000:8080 \
  -v open-webui:/app/backend/data \
  --name open-webui \
  ghcr.io/open-webui/open-webui:main
```

Then you open `http://localhost:3000` in your browser, create a
local account, and point it at your Ollama (it usually finds
`http://localhost:11434` on its own). From there: pick a model from
the dropdown and chat.

## What I can and can't promise here

| Stated plainly | |
|---|---|
| The concept | Real: a web UI talking to your local Ollama API |
| The install command | From the project's docs, not run during writing |
| Whether it works on your machine | Depends on your setup — Docker, ports, and versions all matter |

If the install fights you, the Ollama command line from [Your
First Model](your-first-model.md) still works fine — Open WebUI is
convenience, not a requirement. Other front-ends exist too; the
idea is the same regardless of which one you pick: a local page,
talking to a local API, running local models.

## Worth knowing

- Open WebUI keeps its data (chats, settings) in that `-v`
  volume — your conversations live on your disk, like everything
  else local.
- It's another thing to update. New versions come when you pull
  them, same maintenance deal as the models themselves.
- On a small machine (say, a Raspberry Pi), a web UI plus a model
  is a lot to ask of modest RAM — the terminal chat is lighter.

**Check:** after install, `http://localhost:3000` shows a login
page, and after signing in, the model dropdown lists the models
from your `ollama list`. If the dropdown is empty, Ollama isn't
reachable — see [Troubleshooting](troubleshooting.md).

**Next:** [Choosing Models](choosing-models.md)
