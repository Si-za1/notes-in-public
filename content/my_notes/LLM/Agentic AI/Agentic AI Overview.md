---
title: AgenticAi Overview
draft: false
tags:
  - ai
---
 
An Agentic AI workflow is a process where an LLM based app executes multiple
steps to complete a task.

For example we have a complex task where we need to Write an Essay , now to accomplish that particular task, you might want to break it down into multiple steps and leverage the LLM to work it out, maybe make multiple LLMs to work on multiple works altogether. Or maybe for each process have designated set of LLMs get a particular output and for each step's output, making a single LLM analyse them and present us with the output. 

- You might use an LLM to write the first essay outline

- And then you might use an LLM to decide what search terms to type into a web search engine or really what search terms to call a web search API with in order to get back relevant web pages.

- Based on that, you can feed the downloaded web pages into an LLM to have it write the first draft

- and then maybe use another LLM to reflect and decide what needs more revision. And then depending

- on how you design this workflow, perhaps you may even add a human in the loop step where the LLM has the option to request human review, maybe of some key facts. 

- And based on that, it may then revise the draft and this process results in a much better work output.


Agents can be autonomous to different degrees. The term agentic is used because if we use it as an adjective rather than a binary, it's either an agent or not, then we're going to have to acknowledge that systems can be agentic to different degrees.


The real question whether a system can be called agentic or not is let's just call it all agentic and move on with the real work of building these systems rather than debating, you know, is this sufficiently autonomous to be an agent or not?



Tools used in the agentic approach are designed to enable AI systems to act autonomously, reason through complex problems, and execute multi-step workflows rather than just generating text. These tools, which act as the "arms and legs" of LLMs, allow agents to interact with external data sources, applications, and systems.

That's why we have something called degrees of autonomy which describes on how agentic the system is or can be based on the task that we need to perform. 

![[Pasted image 20260221134755.png]]![[Pasted image 20260221134925.png]]

![[Screenshot 2026-02-21 at 13.45.54.png]]


An example: 
![[Pasted image 20260221135426.png]]




![[Pasted image 20260221135623.png]]


How to break it down into discrete steps for the agentic workflow to follow?

   Started off with direct generation, just one step, decided it wasn't good enough, and so broke that down into three steps, and then maybe decided that still isn't good enough, and took one of the steps and further broken it down or decomposed it into three more steps, resulting in this more complex, richer process for generating an essay. And depending on how satisfied you are with the results of this process, you may choose to even modify this essay generation process further.


Four key design patterns for building agentic workflows are **reflection, tool use, planning, and multi-agent collaboration.**

**Reflection :** The first of the major design patterns is reflection. Reflection is a common design pattern where you can ask the LLM to examine its own outputs or maybe bring in some external sources of information, such as run the code and see if it generates any error messages, and use that as feedback to iterate again and come up with a better version of its output.

**Tools Use :** The second important design pattern is tool use. Today, different developers
have given LLMs many different tools for everything from math or data analysis to gather information by fetching things from the web or for various databases, to interface with productivity apps like email, calendar, and so on, as well as to process images and much more. And the ability of an LLM to decide what tools to use, meaning what functions to call, that lets the model get a lot more done.

**Planning :** The third of the four design patterns is planning. Rather than the developer hard coding the sequence of steps in advance, this design pattern actually lets the LLM decide what are the steps to take. Agents that plan today are harder to control and somewhat more experimental, but sometimes they can give really delightful results.

**Multi-agent collaborations :** Just as a human manager might hire a number of others to work together on a complex project, in some cases it might make sense for you to hire a set of multiple agents, maybe each of which specializes in a different role, and have them work together to accomplish a complex task.

