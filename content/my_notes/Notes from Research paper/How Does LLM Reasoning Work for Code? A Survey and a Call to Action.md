---
title: How Does LLM Reasoning Work for Code? A Survey and a Call to Action
draft: false
tags:
  - complete
---
 
Findings 
Hindle et al. [29] show that software is repetitive and predictable like natural language, and hence can be modeled using statistical techniques like LLMs.

SWE is one of the most interesting applications areas of Artificial Intelligence (AI) and there is growing research in this space. As different reasoning techniques mature and agents become more robust, it is reasonable to expect more and more SWE tasks will be automated.

Their aim:

With our survey on code reasoning for code tasks, we hope to address this gap by making the following contributions: (1) The first survey specific to reasoning for coding tasks, emphasizing reasoning techniques which borrow ideas from coding principles. SWE Agents are given a special focus. since they depend on multiple reasoning techniques. (2) A taxonomy covering different reasoning approaches and benchmarks for code. We also highlight approaches employing multiple reasoning techniques for LLMs in general and agents in particular (Tab. 2). (3) A showcase of benchmarks used to study the impact of reasoning on SWE tasks. We compiled results showing the performance of different code reasoning and agentic approaches. We also highlight promising benchmarks specific to code reasoning and surface some new agent-specific benchmarks with potential for furthering SWE research.

![[Pasted image 20250718153942.png]]

LLMs are few-shot learners.
Performance of LLMs on reasoning tasks is further enhanced by a certain kind of prompting called Chain-of-Thought or CoT [102] prompting which elicits LLM reasoning. Wei et al. [101] suggest that in-context learning ability of LLMs, including CoT reasoning, is an emergent property of LLMs. Code CoT papers (39, 48, 73 and others) suggest that code reasoning is a specific kind of reasoning and CoT can be more impactful when induced with prompts that recognize this difference. We survey such techniques.

One way code output is different from natural language output is that it can be executed and tested to validate its correctness.

Type of prompting used for understanding and reasoning with the code

CoT prompts for code can be categorized as plan-based or structure-based. Plan-based CoT is a natural language articulation of steps that need to be taken to solve a coding problem. Besides prompting-only techniques, another approach used by many is fine-tuning or instruction tuning for software engineering tasks with code CoT data


There were few of the approaches proposed previously by:

AlphaCodium, proposed by Ridnik , is a flow to improve code LLM performance that does not require training a model. The two key phases in AlphaCodium’s flow are: (a) a pre-processing phase, where it generates problem reflection and test reasoning; and (b) an iterative code generation phase, where code is generated, run, and fixed against both public and AI-generated tests.

PlanSearch generates 3–6 problem observations, combines them into natural language plans, and translates these into pseudocode and then code.


In Revisit Self-Debugging [16] authors explored both post-execution and in-execution self-debugging, leveraging self-generated tests. In post-execution self-debugging, the process directly validates the correctness of code by checking whether the output after execution matches the test output or not, whereas in-execution self-debugging analyzes the intermediate runtime states during program execution without knowing the results from post-execution.


---

Feedbackbased prompting focuses on trying to understand the root cause of failure of tests by analyzing the actual understanding implicitly utilized by LLMs for code generation through code summarization.

LEarning to VERify [65] (LEVER) is an approach where verifiers are trained to check whether the generated code is correct or not based on three sources of information: the natural language input, the program itself, and its execution results.

Unit Tests (UT) are a way to assess the correctness of code and give execution-based feedback to code generation models.

----
The Tree-of-thoughts or ToT [112] paradigm allows LMs to explore multiple reasoning paths over CoT.

The language model’s reasoning is used as the heuristic, which contrasts with traditional approaches that use learned or programmed rules. To travers the tree, ToT uses classic search strategies: breadth-first search (BFS) or depth-first search (DFS). 

Guided Tree-of-thought (GToT) [58] also uses a tree-search algorithm, where the LLM is used as a heuristic for generating search steps. GToT uses prompting to reach an intermediate solution to a problem, then introduces a checker, which assesses the correctness or validity of the intermediate solution.

---
Approaches for the agentic workflow 

The reasoning is done by an LLM which interacts with the agent execution environment with API based tool calls. 

SWE-Agent [110] is an agent capable of editing repository-level code by generating a thought and a command, and subsequently incorporating the feedback from the command’s execution into the environment.

---
agent improvements are the result of task-specific training of underlying reasoning model with patch data or agent environment interaction data, called trajectories



----
HumanEval (HE) [12] is a set of 164 hand-written programming problems, each problem including a function signature, docstring and unit tests. A multilanguage version of HE is also available in HumanEval-XL.

---
Conclusion

Agentic approaches appear to dominate both execution-based and CoT strategies.

Agentic approaches that scale inference with search are highly competitive and can even outperform other strategies.

---
[link to the paper](https://arxiv.org/pdf/2506.13932)
