# Quartz v5

> “[One] who works with the door open gets all kinds of interruptions, but [they] also occasionally gets clues as to what the world is and what might be important.” — Richard Hamming

Quartz is a set of tools that helps you publish your [digital garden](https://jzhao.xyz/posts/networked-thought) and notes as a website for free.

🔗 Read the documentation and get started: https://quartz.jzhao.xyz/

[Join the Discord Community](https://discord.gg/cRFFHYye7t)

## Sponsors

<p align="center">
  <a href="https://github.com/sponsors/jackyzha0">
    <img src="https://cdn.jsdelivr.net/gh/jackyzha0/jackyzha0/sponsorkit/sponsors.svg" />
  </a>
</p>

***

# Deployment issue in .md formating
in the markdown file I should always use `***` as a divider not the other one. 
The other one (divider) cause a deployment issue. It says, `Quartz cannot parse one of your Markdown files`.
This is a YAML frontmatter error. where the other divider acts as a YAML code opening. So the rest of markdown becomes YAML code.

# My Daily used commands

```
npx quartz sync
```
use this command and you don't have to do git add, commit, push. It does everything.
