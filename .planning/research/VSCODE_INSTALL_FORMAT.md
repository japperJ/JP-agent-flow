# VS Code Copilot Custom Agent install links (deep links)

## Executive summary
To create clickable “Install agent” links (for GitHub READMEs / Gists) that install a `.agent.md` file into VS Code, the working pattern in the wild is:

1. Build a VS Code deep link that targets Copilot’s agent installer:
   - VS Code stable: `vscode:chat-agent/install?url=<HTTPS_URL_TO_AGENT_FILE>`
   - VS Code Insiders: `vscode-insiders:chat-agent/install?url=<HTTPS_URL_TO_AGENT_FILE>`
2. URL-encode that entire deep link.
3. Wrap it in an HTTPS redirect link so GitHub will allow it:
   - `https://aka.ms/awesome-copilot/install/agent?url=<URL_ENCODED_DEEPLINK>`

This is the exact structure used by burkeholland’s public gist (and it points at raw agent files hosted on `gist.githubusercontent.com`).

## Canonical formats (copy/paste templates)

### 1) Direct deep links (works in browsers that allow custom schemes)
These are the “native” forms. They’re useful in documentation outside GitHub, or anywhere that doesn’t block `vscode:` links.

- **VS Code (stable)**
  - `vscode:chat-agent/install?url=https://<host>/<path>/<agent>.agent.md`

- **VS Code Insiders**
  - `vscode-insiders:chat-agent/install?url=https://<host>/<path>/<agent>.agent.md`

### 2) GitHub-friendly install links (recommended for README/Gist badges)
GitHub Markdown frequently blocks or rewrites non-HTTP(S) schemes, so the common workaround is an HTTPS wrapper that redirects into the `vscode:` / `vscode-insiders:` deep link.

- **VS Code (stable)**
  - `https://aka.ms/awesome-copilot/install/agent?url=<ENCODED(vscode:chat-agent/install?url=<agent-url>)>`

- **VS Code Insiders**
  - `https://aka.ms/awesome-copilot/install/agent?url=<ENCODED(vscode-insiders:chat-agent/install?url=<agent-url>)>`

#### Example (stable)
Agent file URL (must be a *direct* raw file URL):

- `https://gist.githubusercontent.com/<user>/<gist-id>/raw/<commit-or-rev>/<agent>.agent.md`

Deep link:

- `vscode:chat-agent/install?url=https://gist.githubusercontent.com/<user>/<gist-id>/raw/<commit-or-rev>/<agent>.agent.md`

Wrapped link:

- `https://aka.ms/awesome-copilot/install/agent?url=vscode%3Achat-agent%2Finstall%3Furl%3Dhttps%3A%2F%2Fgist.githubusercontent.com%2F<user>%2F<gist-id>%2Fraw%2F<commit-or-rev>%2F<agent>.agent.md`

(Insiders is identical except the scheme becomes `vscode-insiders:` and therefore encodes to `vscode-insiders%3A...`.)

## URL encoding rules (what exactly gets encoded)
Encode the **entire** deep link string (starting at `vscode:` / `vscode-insiders:`). In practice, this is equivalent to `encodeURIComponent(...)` in JavaScript.

Minimum characters you’ll see encoded:

- `:` → `%3A`
- `/` → `%2F`
- `?` → `%3F`
- `=` → `%3D`

So:

- `vscode:chat-agent/install?url=https://example.com/a.agent.md`

becomes:

- `vscode%3Achat-agent%2Finstall%3Furl%3Dhttps%3A%2F%2Fexample.com%2Fa.agent.md`

## Hosting requirements & the “raw.githubusercontent.com” failure mode
The installer ultimately fetches the `.agent.md` file from the URL you provide.

**Practical requirements:**

- The URL should be **HTTPS**.
- Prefer a URL that resolves to the raw file content **without additional redirects**.

**Observed pitfall (your reported error):**

- Clicking wrapper links can fail with: `Unsupported redirect target: raw.githubusercontent.com`.
- This appears to come from the `aka.ms/awesome-copilot/install/agent` wrapper refusing to redirect to certain targets/domains.

**Mitigation that matches a known-working example:**

- Host agent files using `gist.githubusercontent.com/.../raw/.../*.agent.md` (Gist raw), as shown in burkeholland’s gist.

If you want to host agents from a GitHub repository, note that many “raw” URLs (such as `https://github.com/<org>/<repo>/raw/...`) ultimately redirect to `raw.githubusercontent.com`, which may trigger the wrapper’s domain restrictions.

## Related note: VS Code vs VS Code Insiders URL prefixes
VS Code’s general URL handler uses `vscode://...` and, for Insiders, `vscode-insiders://...` (documented in “Opening VS Code with URLs”).

The agent installer deep links observed in the wild use **scheme URIs** with a colon form (`vscode:...` / `vscode-insiders:...`) rather than `vscode://...`.

## Sources
- burkeholland gist raw markdown showing the exact wrapper + encoded deep link patterns:
  - https://gist.githubusercontent.com/burkeholland/0e68481f96e94bbb98134fa6efd00436/raw/ainstall.md
- VS Code docs: “Opening VS Code with URLs” (confirms `vscode-insiders://` prefix for Insiders builds):
  - https://code.visualstudio.com/docs/configure/command-line#_opening-vs-code-with-urls
