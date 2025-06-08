---
title: yeoman
draft: false
tags:
  - complete
---
 
I was brainstorming ideas for my next side project — something useful but lightweight. As I sketched out a few tools, a random thought popped into my head: _what if I made a VS Code extension?_

I've been using VS Code every day, and a lot of the tiny things I rely on — quick formatting, snippets, color pickers — are all community-built extensions. So I asked myself, _how are these extensions actually made?_

That question led me down the rabbit hole, and pretty quickly, I found my way to **Yeoman**.

Yeoman is essentially a **project scaffolding tool**. Think of it as a smart assistant that sets up the boilerplate for whatever you're trying to build. In this case, VS Code extensions. Instead of manually creating folders, writing `package.json` by hand, or figuring out where activation events go, Yeoman handles all of that.

You install Yeoman globally with:

```bash
npm install -g yo
```

Then you install the VS Code Extension Generator:

```bash
npm install -g generator-code
```

And after that, it’s as easy as:

```bash
yo code
```

Yeoman will prompt you with questions like:

- What's the name of your extension?
- Do you want a TypeScript or JavaScript base?
- What kind of extension is this (command, UI, etc.)?

Once you answer, it auto-generates the entire project structure — complete with:

- A working sample command,
- `package.json` already wired up with metadata,
- `src/extension.ts` or `.js` as your entry point,
- And built-in commands to run, debug, and publish your extension.

It removes the friction of setup so you can focus on building the actual functionality.
Yeoman isn’t just for VS Code extensions — it has generators for everything from web apps to Electron projects. But in this context, it’s a clean, well-supported entry point for anyone trying to build tools within VS Code.

Now that the base is scaffolded, I’m sketching out the actual idea for what my extension will do. 


Next step: building out the features and seeing how far I can take it.

[Github](https://github.com/yeoman)
[yeoman](https://yeoman.io/)
