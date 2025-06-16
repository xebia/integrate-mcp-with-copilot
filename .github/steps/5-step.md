## Step 5: Expose Your FastAPI API as an MCP Server

Great job so far! Now, let's make your API even more powerful by exposing it as an MCP (Model Context Protocol) server using FastAPI MCP. This will allow AI tools like Copilot to discover and use your endpoints as tools.

### :rocket: What is FastAPI MCP?

FastAPI MCP is a library that makes it easy to expose your FastAPI endpoints as MCP tools. MCP is like a "USB-C for AI"—it lets AI assistants connect to your API and use its capabilities in a standardized way.

### :keyboard: Activity: Add MCP support to your API

1. **Install the FastAPI MCP package**

   In your terminal, run:

   ```bash
   pip install fastapi-mcp
   ```

2. **Update your FastAPI app to add MCP support**

   Open your FastAPI app (usually `src/app.py`). Add the following code:

   ```python
   from fastapi_mcp import FastApiMCP
   # ...existing code...
   mcp = FastApiMCP(
       app,
       name="Mergington MCP API",
       description="MCP server for Mergington High School Activities API"
   )
   mcp.mount()
   # ...existing code...
   ```

   > :bulb: **Tip:** You can use the `operation_id` parameter on your endpoints to give them clear tool names for AI assistants.

3. **Run your application**

   Start your FastAPI app as usual:

   ```bash
   python src/app.py
   ```

   or (if using uvicorn):

   ```bash
   uvicorn src.app:app --reload
   ```

   Your MCP server will be available at `http://localhost:8000/mcp`.

4. **Update `.vscode/mcp.json` to add the new MCP endpoint**

   Open `.vscode/mcp.json` (created in Step 1). Add a new entry for your FastAPI MCP server, for example:

   ```json
   {
     "servers": {
       "github": { /* ...existing config... */ },
       "fastapi": {
         "endpoint": "http://localhost:8000/mcp"
       }
     },
     "inputs": [ /* ...existing config... */ ]
   }
   ```

   > :warning: **Note:** Do not remove the existing `github` server entry—just add the new `fastapi` entry.

5. **Try it out!**

   - Open Copilot Chat and select your new FastAPI MCP server as a tool.
   - Ask Copilot to list available tools or call your endpoints.

---

#### :star: Best Practices

- Use clear `operation_id` values for your endpoints.
- Add descriptions to your endpoints for better AI understanding.
- Secure your API if exposing it beyond local development.

<details>
<summary>Having trouble?</summary>

- Make sure your FastAPI app is running and accessible at the correct port.
- Double-check your `.vscode/mcp.json` for typos.
- See the [FastAPI MCP blog post](https://huggingface.co/blog/lynn-mikami/fastapi-mcp-server) for more tips.

</details>
