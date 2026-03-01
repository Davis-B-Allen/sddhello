This is intended to be a trivial hello world project (say, a simple webpage) that serves as a frame for bootstrapping a modern dev environment (using devcontainers) with incorporated AI tooling, for the purpose of learning about spec-driven development. The goal is to establish a model dev environment and workflow that can allow relatively non-technical friends of mine to productively contribute (likely using github codespaces) to projects with the assistance of an AI-assisted, spec-driven development paradigm.

Included is:
- an extremely basic devcontainer.json (for Node + JS development)
- some spec-kit files generated via the following command:

```
uvx --from git+https://github.com/github/spec-kit.git specify init --here
```

and selecting Github Copilot (for the agent) and sh (for the scripts). We are making the assumption that to start, we'll be using Github Copilot as our agentic framework/harness (in concert with Github Copilot Pro or Pro+ subscriptions), and a linux-based environment in our devcontainer.