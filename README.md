# BBOP Skills

## About

These are intended for agents but they can also be read by humans to understand philosphy and best practice.

See:

* https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview
* https://github.com/ai4curation/curation-skills

Currently there is only one, for repo best practices:

* [github-repo-skill](https://github.com/berkeleybop/bbop-skills/tree/main/github-repo-skill)

## How to use this

### Read the skills

Everyone should read the skills in this repo and check they are in agreement - PRs always welcome!

### Install with npx skills

With Node.js and npm installed, use the [Skills CLI](https://skills.sh/docs/cli)
from the project where you want to use the skill:

```bash
# List available skills without installing
npx skills add berkeleybop/bbop-skills --list

# Install one skill for Claude Code in the current project
npx skills add berkeleybop/bbop-skills --skill github-repo-skill -a claude-code
```

Use `-a codex` to target Codex instead, or omit `-a` to choose agents.
Installation is project-scoped by default; add `-g` for a user-wide install
available across projects.

This installs skill files. To install a Claude plugin and any bundled hooks,
MCP servers, or plugin commands, use the marketplace instructions below.

### Claude Code marketplace

In Claude Code you can install these via the marketplace

```
/plugin marketplace add berkeleybop/bbop-skills
```

Or just copy into your own skills folder.

But it's as important people read and understand the skills as it is that their agents use them


## General guidelines on use of AI

All group members are expected to develop core AI capabilities and
literacy, and to use judgment in applying them. There are favored
tools such as Claude Code for the terminal and Claude Code on the web
for non-terminal use, but no mandate to use these.

The existence of these tools does mean that expectations of things
like basic repo hygiene and best practices as laid out in
[github-repo-skill/](github-repo-skill/) are now much higher, given it
is very easy for coding tools to do a good job on this, even with legacy repos.


While we generally want to be forward in using AI, we should be cogniscent of context, see for example:

* [respect users who create issues](https://ai4curation.io/aidocs/how-tos/instruct-github-agent/#be-respectful-of-the-user-who-created-the-issue)

## Historic notes

We used to maintain a github repo here with best practice:

https://berkeleybop.org/best_practice/

A lot of this has become stale, and many parts of this will gradually
be migrated to skills, either in this repo, or in a repo such as [the ai4curation skills repo](https://github.com/ai4curation/curation-skills)

## Other skills and skill marketplaces of relevance

There are many skill repositories out there, these just list the ones core to the group

- https://github.com/caufieldjh/biosketch-skills
- https://github.com/ai4curation/curation-skills

## LICENSE and use of these skills

The [LICENSE.txt](LICENSE.txt) is CC-0. Feel free to reuse, adapt. Attributions welcome but not required.
