# Skills collection and documentation

## Useful skills

### 1. Makes AI respond concise: [caveman](https://github.com/juliusbrussee/caveman)
Makes AI respond in a “caveman” style: short, direct, and focused only on what matters.

Many AI responses are too long and include unnecessary details, which takes time to read and can pollute the context window. The page says this skill saves tokens, but I think the bigger benefit is keeping the context window clean. Rubbish in, rubbish out - so a concise context window really matters.

### 2. Visualise context window and usage: [claude-hud](https://github.com/jarrodwatts/claude-hud)
This one is specifically for Claude Code. It shows the current context window usage and quota directly, so you do not need to keep running `/status`.

### 3. Force you to think hard and plan well: [superpowers](https://github.com/obra/superpowers)
This skill is designed for complex and difficult tasks. In my experience, the better the LLM model, the more useful this skill becomes.
The documentation describes it as an “agentic skills framework & software development methodology”. In plain English, it teaches you how to work with AI through a fixed 7-step process: brainstorming, using git worktrees, writing plans, subagent-driven development, test-driven development, requesting code review, and finishing a development branch.

Going through these steps helps you avoid getting lost and gives you a much clearer understanding of every part of the project. It works like a speed bump that forces you to think carefully. Sometimes the planning stage alone can use more than 50% of the context window, but spending 30 minutes planning can save 30 hours of detours later.

Another major advantage is that testing and review become part of the workflow by default, which itself reduces many errors. This skill changed how I use AI - it gives me more active control over the process.

The only disadvantage is that this skill is too heavy for simple tasks.

## Official Anthropic/claude-community skills

[Official Anthropic](https://github.com/anthropics/skills/tree/main/skills)

[claude-community](https://github.com/anthropics/claude-plugins-community)

## Other skills collections

- [antigravity-awesome-skills](https://github.com/sickn33/antigravity-awesome-skills/)
- [awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills)

