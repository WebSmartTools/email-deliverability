# Install email-deliverability

The skill is one folder: `email-deliverability`. Copy it into your agent's skills folder and the agent loads it whenever a task matches its description.

## Claude Code

```bash
mkdir -p ~/.claude/skills
cp -r email-deliverability ~/.claude/skills/
```

Restart Claude Code, or run `/skills` to confirm it is listed.

## Codex CLI

```bash
mkdir -p ~/.codex/skills
cp -r email-deliverability ~/.codex/skills/
```

## Cursor

```bash
mkdir -p .cursor/skills
cp -r email-deliverability .cursor/skills/
```

Cursor reads project skills from `.cursor/skills/` in the project root. For a global install, use `~/.cursor/skills/` instead.

## Claude.ai

Go to Settings, then Capabilities, then Skills, and upload the `email-deliverability` folder.

## Check it works

Ask your agent: "Build me an SPF record for example.com using Google Workspace and SendGrid, and count the lookups."

The result should be `v=spf1 include:_spf.google.com include:sendgrid.net ~all` with a lookup total of 3, plus a DMARC record starting at `p=none` with a `rua` address. If the agent quotes a record from memory without a live lookup, point it at the hard rules in SKILL.md.

## Updating

The free skill is updated on GitHub. Replace the folder with the new version. Your own domains and provider setup live in your project, not in the skill, so an update will not overwrite them.
