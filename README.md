# Local test

## Create venv
```bash
uv sync
```

## Install package

```bash
uv pip install brave-mcp-langchain
```

## Run MCP server in STDIO mode

```bash
uvx brave-mcp-langchain
```

### To run MCP server in SSE mode
```bash
uvx brave-mcp-langchain sse 5003
```

## MCP Setting

```json
{
  "mcpServers": {
    "brave-mcp-langchain": {
      "disabled": false,
      "timeout": 60,
      "type": "stdio",
      "command": "uvx",
      "args": [
        "brave-mcp-langchain"
      ]
    }
  }
}
```

# Use as Langchain tool

It can also be used as Langchain tool. Try below code to try

```python
import httpx
import asyncio
from langchain.tools import Tool
from brave_mcp_langchain import brave_tool

async def test_search():
    result = await brave_tool.search_tool.ainvoke({"query": "LangGraph overview", "max_results": 10})
    print(result)

    result = await brave_tool.fetch_content_tool.ainvoke({
        "url": "https://iamatulsingh.github.io"
    })
    print(result)

asyncio.run(test_search())
```
