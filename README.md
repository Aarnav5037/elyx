# Health Journey Conversation Generator

This project automatically generates realistic, context-aware conversations simulating a member's 8-month health journey with a wearable device. It is designed for prototyping conversational health coaching systems and evaluating long-term engagement flows.

## Key Idea

We use layered prompts to cover multiple dimensions of a member’s journey while maintaining running state across many weeks of conversation:

### Layered prompt design
- Separate prompts for health events, test panel results, wearable updates, member questions, and weekly WhatsApp-style chats.  
- Each layer focuses on a single aspect (medical data, user behavior, engagement messages) to avoid prompt clutter.  

### Persistent state for continuity
- A `state.json` file stores key facts: generated events, wearable data, user questions, and last week summaries.  
- State updates each week, so conversations always reference previous context.  
- All state changes are logged to `state_changes_log.jsonl` for visualisation and debugging.  

### Phase-based simulation
- The journey is divided into **4 phases (2 months each)**, each with new health events.  
- Conversations are generated week by week, but you can **pause and resume at any week** without losing context.  

## How It Works

### Generate fixed starting data once
- Health events (first 4 weeks of each phase)  
- Baseline test panel report  

### Iterate week by week
- Add health events (first 4 weeks only)  
- Generate wearable updates (every 2 weeks)  
- Generate member questions (every week)  
- Produce WhatsApp-style messages (weekly)  
- Summarize conversations and update state  

### Save everything
- `state.json` → always up to date  
- `state_changes_log.jsonl` → full history of state snapshots  
- `all_conversations.json` → phase-wise structured conversation archive  

### Resume anywhere
- If the script stops mid-phase, just rerun — state and conversation history are preserved.  

---

## Features

- **No context loss:** State ensures each week knows what happened before.  
- **Auditable:** Every state update is logged for debugging and review.  
- **Modular prompt layers:** Easy to swap or refine individual generation steps without breaking others.  
- **Flexible APIs:** Works with OpenAI models (`gpt-4o`, `gpt-3.5`) and can be adapted for Gemini.  
- **Safe regeneration:** Conversations for already-completed weeks are reused instead of being overwritten.  


