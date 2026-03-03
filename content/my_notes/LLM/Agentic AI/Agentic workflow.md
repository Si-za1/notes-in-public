---
title: Understanding Agentic workflow
draft: false
tags:
  - ai
  - agents
---
 
Customers define agents as fully autonomous systems that operate independently over extended periods, using various tools to accomplish complex tasks.

Others use the term to describe more prescriptive implementations that follow predefined workflows.

an important architectural distinction between **workflows** and **agents**:

- **Workflows** are systems where LLMs and tools are orchestrated through predefined code paths.
- **Agents**, on the other hand, are systems where LLMs dynamically direct their own processes and tool usage, maintaining control over how they accomplish tasks.

***Agentic systems often trade latency and cost for better task performance, and you should consider when this tradeoff makes sense.***

There are many frameworks that make agentic systems easier to implement, including:

- The [Claude Agent SDK](https://platform.claude.com/docs/en/agent-sdk/overview);
- [Strands Agents SDK by AWS](https://strandsagents.com/latest/); - Amazon bedrock - claude 4 sonnet is used.  The default model provider is [Amazon Bedrock](https://strandsagents.com/latest/documentation/docs/user-guide/concepts/model-providers/amazon-bedrock/) and the default model is Claude 4 Sonnet inference model from the region of your credentials. For example, if you set the region to `us-east-1` then the default model id will be: `us.anthropic.claude-sonnet-4-20250514-v1:0`.
https://strandsagents.com/latest/documentation/docs/examples/python/agents_workflows/

- [Rivet](https://rivet.ironcladapp.com/), a drag and drop GUI LLM workflow builder; and
- [Vellum](https://www.vellum.ai/), another GUI tool for building and testing complex workflows.


## Building blocks, workflows, and agents

our foundational building block—the augmented LLM—and progressively increase complexity, from simple compositional workflows to autonomous agents.

### Building block: The augmented LLM

The basic building block of agentic systems is an LLM enhanced with augmentations such as retrieval, tools, and memory. Our current models can actively use these capabilities—generating their own search queries, selecting appropriate tools, and determining what information to retain.

![[Pasted image 20260302102258.png]]
### Workflow: Prompt chaining

Prompt chaining decomposes a task into a sequence of steps, where each LLM call processes the output of the previous one. You can add programmatic checks (see "gate” in the diagram below) on any intermediate steps to ensure that the process is still on track.

![[Pasted image 20260302102533.png]]
**When to use this workflow:** This workflow is ideal for situations where the task can be easily and cleanly decomposed into fixed subtasks. The main goal is to trade off latency for higher accuracy, by making each LLM call an easier task.


### Workflow: Routing

Routing classifies an input and directs it to a specialized followup task. This workflow allows for separation of concerns, and building more specialized prompts. Without this workflow, optimizing for one kind of input can hurt performance on other inputs.


![[Pasted image 20260302102649.png]]

**When to use this workflow:** Routing works well for complex tasks where there are distinct categories that are better handled separately, and where classification can be handled accurately, either by an LLM or a more traditional classification model/algorithm.

### Workflow: Orchestrator-workers

In the orchestrator-workers workflow, a central LLM dynamically breaks down tasks, delegates them to worker LLMs, and synthesizes their results.
![[Pasted image 20260302102822.png]]

**When to use this workflow:** This workflow is well-suited for complex tasks where you can’t predict the subtasks needed (in coding, for example, the number of files that need to be changed and the nature of the change in each file likely depend on the task). Whereas it’s topographically similar, the key difference from parallelization is its flexibility—subtasks aren't pre-defined, but determined by the orchestrator based on the specific input.

### Agents
Agents begin their work with either a command from, or interactive discussion with, the human user. Once the task is clear, agents plan and operate independently, potentially returning to the human for further information or judgement.

During execution, it's crucial for the agents to gain “ground truth” from the environment at each step (such as tool call results or code execution) to assess its progress. Agents can then pause for human feedback at checkpoints or when encountering blockers. 

The task often terminates upon completion, but it’s also common to include stopping conditions (such as a maximum number of iterations) to maintain control.

https://claude.com/blog/tool-use-ga 


### What is Agentic Workflow?
An agentic workflow is ==an advanced AI automation approach where autonomous AI agents, powered by Large Language Models (LLMs), break down complex goals into, plan, and execute multi-step tasks with limited human oversight==. Unlike rigid traditional automation, agentic workflows use reasoning, tool use, and persistent memory to adapt to new information in real-time.

Key aspects of agentic workflows include:

- **Autonomous Operation:** Agents make independent, real-time decisions, such as researching information, updating databases, or triggering other applications.
- **Multi-Agent Coordination:** Complex tasks are often handled by specialized agents working together (e.g., one agent researches while another writes).
- **Dynamic Adaptation:** They can pivot, self-correct, or handle exceptions when unexpected events occur, making them ideal for complex, non-linear processes.
- **Tool Usage:** Agents can autonomously use external tools, such as API integrations, web browsers, and software applications, to accomplish tasks.
- **Human-in-the-loop (HITL):** While autonomous, these systems allow for human monitoring and intervention to ensure accuracy and safety


**Key Differences: Strands Agents vs. Normal Agents
==Strands Agents, developed by AWS, represent a **model-driven approach** to AI agents, designed for autonomous reasoning, production-grade observability, and easy AWS integration==. The name "Strands" symbolizes the connection between two core components: the LLM (model) and the tools.

Unlike traditional ("normal") agents that often require developers to hardcode step-by-step logic, Strands agents use the LLM to autonomously determine the best sequence of tools and actions to achieve a goal.

|Feature|Strands Agent|Normal/Traditional Agent (e.g., Early LangChain)|
|---|---|---|
|**Philosophy**|**Model-Driven:** Model acts as the planner & orchestrator.|**Code-Driven:** Developer writes rigid logic & workflows (If-Then).|
|**Development**|"Low-code" approach: Just define prompt, tools& model.|"High-code" approach: Extensive boilerplate to map tasks.|
|**Autonomy**|High: Agent decides when to call tools and how to proceed.|Low: Agent follows a pre-defined path.|
|**Tool Usage**|Native Model Context Protocol (MCP) support (connects to thousands of tools).|Requires custom integration wrappers for most tools.|
|**Observability**|Built-in OpenTelemetry (OTEL) for real-time tracking.|Requires manual logging/callback implementation.|
|**Best For**|Production-grade, secure, multi-agent systems, AWS ecosystem.|Prototyping, simple RAG, non-linear exploratory tasks.|**

### Workflow of Strands Agents (Model-Driven Loop)

Strands operates on a continuous loop of **Think  - Act (Tool)  - Observe -  Reflect** 
1. **Initialize:** Define the `Agent` with a system prompt (role/rules) and available tools (`@tool` decorator).
2. **Input:** User submits a request (e.g."Analyze why AWS costs increased").
3. **Thought/Plan:** The LLM reads the request and determines the necessary steps (e.g."1. Query Cost Explorer, 2. Check CloudWatch, 3. Correlate").
4. **Tool Execution:** The agent calls the necessary tools autonomously.
5. **Observation:** The results from the tools are fed back into the LLM context.
6. **Reflect/Loop:** The agent decides if the goal is met. If not, it repeats steps 3-5.
7. **Output:** Final answer is returned.

[AWS STRAND AGENTS](https://aws.plainenglish.io/aws-strands-agents-the-model-first-revolution-in-ai-agent-development-27d07d2cbcb9)
[Agentic Workflow](https://weaviate.io/blog/what-are-agentic-workflows#:~:text=An%20agentic%20workflow%20is%20a,%2C%20and%20self%2Devolving%20processes.)
[Langchain](https://docs.langchain.com/oss/python/langgraph/workflows-agents)
[Agentic Workflow Design Patterns](https://medium.com/binome/ai-agent-workflow-design-patterns-an-overview-cf9e1f609696)


![](data:image/gif;base64,R0lGODlhAQABAIAAAP///wAAACH5BAEAAAAALAAAAAABAAEAAAICRAEAOw==)

