# LangGraph Time Travel & Interrupt Examples

A demonstration repository showcasing advanced LangGraph patterns for time travel, interrupts, and sub-agent architectures.

## Overview

This project demonstrates three different examples to showcase time traveling.

1. **time-travel-interrupt.ipynb** - Simply time travel example with an interrupt
2. **sub-agent-test.ipynb** - Time travel example using when the sub agent has an interrupt
3. **time-travel-lg-sdk.ipynb** - Time travel example using the langgraph sdk. The agent runs using langgraph dev


## Usage

### Running time-travel-lg-sdk.ipynb

**Start langgraph studio, i prefer to use uv**
```bash
uv run langgraph dev
```

Then access the agent via the LangGraph SDK.

## Exploring the Notebooks

### Sub-Agent Pattern (`sub-agent-test.ipynb`)
Demonstrates creating specialized sub-agents (fruit & veggie experts) with:
- Tool wrappers around sub-agents
- Checkpoint management with MemorySaver
- Interrupt handling in sub-agents
- Time travel to states before interrupts


### Time Travel with SDK (`time-travel-lg-sdk.ipynb`)
Shows how to:
- Deploy agents with LangGraph CLI
- Use LangGraph SDK client for remote execution
- Navigate thread history and checkpoints
- Resume from interrupts using `Command(resume=True)`
- Time travel to previous states using `update_state()`


### Time Travel with Interrupts

When time traveling to a checkpoint that contains an interrupt:
- **Without `update_state()`**: The interrupt is skipped, execution continues from the cached result
- **With `update_state()`**: Creates a new fork, allowing the interrupt to trigger again

This is important for scenarios where you want to re-execute logic from a previous state, not just replay cached results.


## LangGraph Deployment

The `langgraph.json` file configures the deployment:

```json
{
  "graphs": {
    "Music Catalog Subagent": "./agents/music_agent.py:graph"
  },
  "env": ".env",
  "dependencies": ["."]
}
```

## Dependencies

Core dependencies:
- `langgraph` - LangGraph framework
- `langchain` - LangChain core
- `langchain-openai` - OpenAI integration
- `langchain-community` - Community tools (SQLDatabase)
- `langgraph-cli[inmem]` - CLI for deployment
- `langsmith` - Tracing and monitoring
- `sqlalchemy` - Database ORM
- `requests` - HTTP client

See `requirements.txt` for full list.

