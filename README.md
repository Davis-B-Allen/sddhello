# Get Started with AI-Assisted Development

A practical, hands-on guide to building software with an AI at your side.

**[View the live site →](https://davis-b-allen.github.io/sddhello/)**

## What is this?

This site is a practical, hands-on guide designed to help you — someone who may have little or no experience with software development — get set up with modern tools for building software alongside an AI assistant.

The idea is ambitious but achievable: you're going to learn how to build real applications, and you won't be doing it alone. You'll have **GitHub Copilot** — an AI-powered coding assistant — working right beside you, ready to write code, explain concepts, and guide you through every step.

This guide follows a **"learn by making"** philosophy. Rather than reading a textbook cover to cover before writing a single line of code, you'll jump in, get your hands dirty, and learn as you go. When you hit something you don't understand, you'll have your AI assistant right there to explain it. The best way to learn is by doing — and with AI as your partner, you can start doing interesting things right away.

## Key Concepts

Before you dive into the setup steps, here's a quick introduction to the tools and ideas you'll be working with.

- **GitHub Codespaces** — A complete development environment that runs in your web browser. No installs needed.  
  [Learn more →](https://docs.github.com/en/codespaces)
- **GitHub Copilot & AI Agents** — An AI assistant that lives inside your editor. Ask it to write code, explain concepts, or plan features.  
  [Learn more →](https://docs.github.com/en/copilot)
- **Spec-Driven Development & spec-kit** — A structured way to build software: write a specification, plan, break into tasks, and implement step-by-step.  
  [Learn more →](https://github.com/github/spec-kit)

## Getting Started

Follow these steps to go from zero to a working development environment — and a live website — right in your browser.

### 1. Create a GitHub account

GitHub is a platform where developers store and collaborate on code. You'll need a free account to access the project and use the tools described here. If you already have an account, skip ahead to step 2.

[Sign up for GitHub →](https://github.com/signup)

### 2. Sign up for the GitHub Copilot Pro free trial

Copilot Pro gives you access to the AI assistant that will help you write code and learn as you go. GitHub offers a free 30-day trial, so you can get started without any cost.

[Start your free Copilot Pro trial →](https://github.com/github-copilot/signup)

### 3. Fork the repository

"Forking" means creating your own personal copy of the project on GitHub. This gives you a safe space to experiment and make changes without affecting the original. Visit the project's repository page on GitHub and click the **Fork** button near the top right of the page.

[Go to the repository on GitHub →](https://github.com/Davis-B-Allen/sddhello)

### 4. Open your fork in GitHub Codespaces

Go to *your fork* of the repository on GitHub (not the original). Click the green **<> Code** button, select the **Codespaces** tab, and click **Create codespace on main**. After a minute or two, a fully configured editor will open in your browser — you're ready to start building!

### 5. Preview the site locally

Open the terminal in VS Code (**Terminal → New Terminal**, or press `` Ctrl+` ``) and run:

```sh
npx serve site -p 8080
```

In a Codespace, a notification will pop up saying *"Your application running on port 8080 is available."* Click **Open in Browser** to see the site. You can also open the **Ports** panel (in the bottom bar) and click the globe icon next to port 8080.

> **Note:** If you're developing locally (not in a Codespace), open `http://localhost:8080` directly in your browser after running the serve command.

### 6. Publish your site with GitHub Pages

Your fork already includes a workflow file that can publish the site to the web automatically. You just need to enable it:

1. In your fork on GitHub, go to the **Actions** tab. If prompted, click **"I understand my workflows, go ahead and enable them"**.
2. Go to **Settings → Pages** (in the left sidebar under "Code and automation").
3. Under **Build and deployment**, set **Source** to **GitHub Actions**.
4. Push a commit to `main` (or click **"Run workflow"** on the Actions tab) to trigger deployment.

After a few minutes, your site will be live at `https://<your-username>.github.io/<your-repo>/`.

## Next Steps

Now that you have your development environment running, it's time to build something! A great first feature is to expand the site with individual concept pages. Visit the [live site](https://davis-b-allen.github.io/sddhello/) for a suggested first feature prompt you can paste directly into your AI agent's chat.

You'll use spec-kit slash commands to guide the process:

1. `/speckit.specify` — describe what you want to build
2. `/speckit.plan` — create a technical plan
3. `/speckit.tasks` — break the plan into tasks
4. `/speckit.implement` — build it step by step

## Reference Links

- [GitHub](https://github.com) — The platform where your code lives and where you'll collaborate.
- [GitHub Copilot](https://github.com/features/copilot) — Your AI-powered coding assistant.
- [GitHub Codespaces](https://github.com/features/codespaces) — Cloud development environments that run in your browser.
- [spec-kit](https://github.com/github/spec-kit) — The toolkit for spec-driven development with AI.
- [GitHub Codespaces Documentation](https://docs.github.com/en/codespaces) — Official docs for getting started with Codespaces.
- [GitHub Copilot Documentation](https://docs.github.com/en/copilot) — Official docs for Copilot features and setup.
- [GitHub Get Started Guide](https://docs.github.com/en/get-started) — A beginner-friendly introduction to GitHub itself.