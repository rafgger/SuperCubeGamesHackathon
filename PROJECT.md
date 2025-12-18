Got it 👍
Below is the **cleaned-up, corrected project description**, using **exactly two agents** as you specified:

* **Agent 1: Trip Planner**
* **Agent 2: Flight Search Agent**

No extra agents, no optimizer agent, no conversation agent — **simple, Flowise-friendly, and realistic**.

---

# Flowise AI Agents App – Flight Planning with Kiwi MCP Server

## Project Overview

Build a **two-agent AI application in Flowise** that plans flights conversationally using the **Kiwi MCP Server**.

The system translates natural-language travel requests into structured search parameters (**Trip Planner Agent**) and retrieves flight options via the **Kiwi MCP Server** (**Flight Search Agent**).
The Flight Search Agent is also responsible for ranking and explaining results.

---

## Core Goal

> Enable users to plan flights using natural language and receive explainable flight options powered by Kiwi data.

---

## Architecture (2 Agents Only)

```
User
 ↓
Trip Planner Agent
 ↓
Flight Search Agent (Kiwi MCP)
 ↓
User
```

This entire flow is implemented inside a **single Flowise canvas**.

---

## Agent Definitions

## Agent 1: Trip Planner Agent

### Purpose

* Understand user intent
* Convert free-text input into structured flight search parameters
* Ask clarifying questions if required data is missing

### Input

* Raw user message

### Output (JSON only)

```json
{
  "origin": "PRG",
  "destination": "TYO",
  "date_from": "2026-04-01",
  "date_to": "2026-04-30",
  "flexible_days": 3,
  "trip_type": "one-way",
  "preferences": {
    "priority": "price",
    "max_stops": 2
  }
}
```

### System Prompt (Trip Planner Agent)

```
You are a Trip Planner Agent.

Your task is to extract structured flight search parameters from user input.
If mandatory fields are missing, return a clarification question instead of JSON.

Mandatory fields:
- origin
- destination
- date_from or date_range

Return VALID JSON ONLY when ready.
Do not invent values.
```

---

## Agent 2: Flight Search Agent

### Purpose

* Use the **Kiwi MCP Server** to search flights
* Rank results based on user preferences
* Explain trade-offs in natural language
* Provide Kiwi deep links

### Input

* Structured JSON from Trip Planner Agent

### Tools

* **Kiwi MCP Server** (Apify)

### Responsibilities

* Call MCP tool with structured parameters
* Select best options (cheapest / fastest / balanced)
* Format a human-readable response

### Output (User-Facing)

```text
I found 3 good options:

1) €520 – 1 stop (Doha), 18h total
2) €610 – direct, 9h total
3) €480 – 2 stops, 22h total

The cheapest option is #3, but #1 is a better balance.
Which do you prefer?
```

### System Prompt (Flight Search Agent)

```
You are a Flight Search Agent.

Use the Kiwi MCP Server tool to search for flights.
Rank results based on user preferences.
Explain trade-offs clearly.
Never invent prices or routes.
Always prefer clarity over verbosity.
```

---

## Flowise Canvas (Concrete Setup)

### Nodes

1. **Chat Input**
2. **Trip Planner Agent (LLM)**
3. **Flight Search Agent (Agent with Tool)**

   * Tool: Kiwi MCP Server
4. **Chat Output**

### Memory

* Conversation Buffer Memory
* Required for refinements:

  * “Make it cheaper”
  * “Only direct flights”
  * “Earlier departure”

---

## Kiwi MCP Server Usage

* No direct Kiwi authentication
* All flight data retrieved via:

  * [https://apify.com/agentify/kiwi-mcp-server](https://apify.com/agentify/kiwi-mcp-server)
* MCP acts as a tool accessible to the Flight Search Agent

---

## Example Conversation

**User**

> “Find the cheapest flight from Vienna to New York next month”

**Trip Planner Agent (JSON)**

```json
{
  "origin": "VIE",
  "destination": "NYC",
  "date_from": "2026-01-01",
  "date_to": "2026-01-31",
  "preferences": {
    "priority": "price"
  }
}
```

**Flight Search Agent**

> “The cheapest option is €430 with one stop (14h).
> A direct flight costs €510 (9h).
> Want cheapest or fastest?”

---

## MVP Scope

### Included

✅ One-way & return flights
✅ Flexible dates
✅ Conversational refinement
✅ Kiwi deep links

### Excluded

❌ Booking
❌ Hotels
❌ Visa / insurance
❌ Carbon scoring

---

## Non-Functional Requirements

* Deterministic JSON between agents
* Graceful handling of MCP failures
* Clear user explanations
* Debug-friendly agent logs

---

## Deliverables

* Flowise canvas
* Agent prompts
* MCP tool configuration
* Environment setup
* Example conversations

---

## Why This Design Is Good

* Minimal agent count (easy to debug)
* MCP avoids Kiwi auth complexity
* Fully compatible with Flowise
* Easy to extend later (alerts, multi-city)

---

### Next steps (pick one):

1. **Exact Flowise canvas node configuration**
2. **Copy-paste agent prompts**
3. **Flowise canvas JSON**
4. **Vue.js frontend integration**
5. **Production hardening checklist**

Just tell me 👍
