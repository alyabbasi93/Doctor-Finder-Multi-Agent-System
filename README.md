**Problem Statement**

When people feel symptoms like chest pain or dizziness, the first challenge is simply knowing who to go to. Should they see a cardiologist? A primary care doctor? Is it urgent? And once they know the specialty, finding a trustworthy doctor nearby can be another stressful search through multiple websites.

This project aims to make that process simple, fast, and reassuring. Instead of guessing, a user can describe their symptoms and location, and the system guides them to the right kind of doctor using both medical reasoning and real-time search.

**Why Agents?**

This problem requires more than just a single answer from an LLM. It needs:

A component that understands symptoms

Another that reasons medically

A team of specialists (Emergency, Internal Med, Cardiology) offering different perspectives

A search tool to find real doctors nearby

A summarizer that brings everything together in clear language

Agents are perfect for this because each one can focus on a specific skill. They can run in parallel, share information, use tools, and refine results. The final recommendation comes from the combined strengths of all the agents—not just one model guessing.

**What I Created**

The system is designed as a chain of specialized agents that work together. It looks like this:

Session Initialization Agent
Extracts symptoms and location from the user’s message.

Parallel Medical Specialty Agents

Emergency perspective

Clinical/general medical perspective

Internal medicine perspective
These run side-by-side to interpret symptoms and suggest the most appropriate specialty.

Specialty Aggregator
Merges the opinions and picks the best recommendation.

Doctor Search Agents (Parallel)

One uses live Google Search

One uses an MCP OpenAPI doctor directory
Both return real doctors around the user.

Final Summary Agent
Combines the reasoning + search results to create a clean, helpful final report.

There are also support components like a Loop Agent for refinement, a Memory Bank to store past interactions, and observability tools for logging and tracing.

**Demo — How It Works**

A user might say:

symptoms: chest pain shortness of breath; location: San Francisco


The system then:

Interprets the symptoms

Identifies the likely specialty (in this example: Cardiology)

Determines urgency

Searches for real cardiologists in San Francisco

Shows results from both Google Search and the MCP doctor directory

Outputs a clear, human-friendly recommendation

The user gets medical-style guidance instantly, without searching multiple websites or guessing which doctor to see.

**The Build**

To create this system, I used:

Google ADK for building multi-agent workflows

Gemini 2.5 Flash as the LLM powering each agent

ParallelAgent, SequentialAgent, and LoopAgent to structure the logic

Google Search Tool for real-time updates

MCP OpenAPI Tool to access a structured doctor directory

MemoryBank and InMemorySessionService to maintain context

LoggingObserver for debugging and transparency

Built and tested everything in JupyterLab

I spent time refining session state handling, structuring agent instructions, fixing KeyErrors, coordinating multiple tool sources, and designing the final reporting flow.

**If I Had More Time…**

Here’s what I’d like to add in a future version:

Integrate real medical APIs from hospitals or healthcare networks

Add a proper triage layer that calculates risk scores

Support insurance filtering so users see doctors in their network

Add a full UI or mobile app interface

Provide multilingual support for global access

Create a smoother deployment pipeline using FastAPI and Cloud Run
