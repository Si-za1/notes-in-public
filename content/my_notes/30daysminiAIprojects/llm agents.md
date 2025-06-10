---
title: llm agents
draft: false
tags: []
---
**LLM Agents**  
**Definition**:  
LLM agents are AI systems that use large language models (LLMs) as a "brain" to perform complex tasks by combining planning, memory, and tools. Unlike standalone LLMs, agents can break down tasks, interact with external systems (e.g., APIs, databases), and adapt based on feedback .  

**Key Components**:  
1. **Agent Core (LLM)**: The main controller that decides actions using prompts and tool descriptions.  
2. **Planning**: Breaks tasks into steps (e.g., Chain of Thought, Tree of Thoughts) and refines plans with feedback (e.g., ReAct method) .  
3. **Memory**:  
   - **Short-term**: Stores recent context (limited by LLM’s token window).  
   - **Long-term**: Uses external databases (e.g., vector stores) to retain past interactions .  
4. **Tools**: External resources like calculators, search APIs, or code interpreters to overcome LLM limitations (e.g., math, real-time data) .  

**How They Work**:  
- Receive a user request → Plan steps → Use tools → Store observations → Repeat until task completion .  
- Multi-agent systems assign specialized roles (e.g., one agent searches flights, another books hotels) for efficiency .  

**Applications**:  
- **Research**: Answering complex queries (e.g., analyzing calorie intake trends with charts) .  
- **Automation**: Writing release notes by fetching GitHub issues and summarizing them .  
- **Collaboration**: Teams of agents (e.g., ChemCrow for chemistry tasks) .  

**Challenges**:  
- Hallucinations (multi-agent checks can reduce errors).  
- Task allocation and memory management in multi-agent systems .  

**Frameworks**:  
- **Single-agent**: LangChain, AutoGPT.  
- **Multi-agent**: CrewAI (role-based teams), AutoGen (Microsoft’s collaborative agents) .  

**References**:  
1. [SuperAnnotate: LLM Agents](https://www.superannotate.com/blog/llm-agents)  
2. [PromptingGuide: LLM Agents](https://www.promptingguide.ai/research/llm-agents)  
