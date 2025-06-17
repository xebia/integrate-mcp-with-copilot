## Step 5: Expose Your FastAPI API as an MCP Server

Great job so far! Now, let's make your API even more powerful by exposing it as an MCP server using FastAPI MCP.

### :rocket: What is FastAPI MCP?

FastAPI MCP is a library that makes it easy to expose your FastAPI endpoints as MCP tools. It provides a simple way to integrate your API with AI assistants.

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
   ```

   This will create an MCP server at the `/mcp` endpoint of your FastAPI app. It will contain all your existing endpoints as MCP tools. It currently has no support for prompts or resources.

   > :bulb: **Tip:** You can use the `operation_id` parameter on your endpoints to give them clear tool names for AI assistants.

3. **Run your application**

   Start your FastAPI app as usual. Your MCP server will be available at `http://localhost:8000/mcp`.

4. **Test your MCP server**

   Open your terminal and run:

   ```bash
   npx @modelcontextprotocol/inspector
   ```

   This will start the [MCP Inspector](https://github.com/modelcontextprotocol/inspector), which helps you discover and test your MCP endpoints. Open the URL it provides in your browser and configure your MCP server (use SSE).

   Have a look at the tools that are found and run them. If you want, you can configure fastapi-mcp to exclude certain endpoints or customize the tool names. See the [fastapi-mcp documentation on customization](https://fastapi-mcp.tadata.com/configurations/customization#code-samples) for more details.

5. **Update `.vscode/mcp.json` to add the new MCP endpoint**

   Open `.vscode/mcp.json` (created in Step 1). Add a new entry for your FastAPI MCP server, for example:

   ```json
   {
     "servers": {
       "github": { /* ...existing config... */ },
       "mergington-mcp": {
         "endpoint": "http://localhost:8000/mcp"
       }
     },
     "inputs": [ /* ...existing config... */ ]
   }
   ```

   > :warning: **Note:** Do not remove the existing `github` server entry—just add the new `mergington-mcp` entry.

6. **Try it out!**

   - Open Copilot Chat and select your new FastAPI MCP server as a tool.
   - Ask Copilot to list available tools or call your endpoints.

7. **Time left?**

   Some ideas to explore:

   - Create a reusable prompt in VS code that is configured to use your tools.
   - See how fast you can add MCP support to an API of your own.
   - Try out a few other MCP servers.
   - Read up on [sampling](https://modelcontextprotocol.io/docs/concepts/sampling), which wasn't covered in this workshop but is a powerful feature of MCP servers.

#### :star: Best Practices

- Use clear `operation_id` values for your endpoints.
- Add descriptions to your endpoints for better AI understanding.
- Secure your API if exposing it beyond local development.
- See [modelcontextprotocol.io best practices](https://modelcontextprotocol.io/docs/concepts/tools#best-practices) and [fastapi-mcp best practices](https://fastapi-mcp.tadata.com/getting-started/best-practices) for many more!

<details>
<summary>Having trouble?</summary>

- Make sure your FastAPI app is running and accessible at the correct port.
- Double-check your `.vscode/mcp.json` for typos.
- Reload the MCP server.
- See the [FastAPI MCP blog post](https://huggingface.co/blog/lynn-mikami/fastapi-mcp-server) for more information.

</details>
