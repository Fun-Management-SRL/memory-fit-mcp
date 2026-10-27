# Installing Memory.fit MCP

Memory.fit MCP is a hosted, remote MCP server. Nothing is installed locally.

1. Add a remote MCP server named `memory-fit` with the URL `https://api.memory.fit/mcp` (transport: Streamable HTTP).
2. Connect. The server answers 401 with OAuth 2.1 discovery (RFC 9728 metadata, dynamic client registration). Open the sign-in link it gives; the user signs in with their Memory.fit account and allows access.
3. If the client cannot do OAuth, ask the user for a personal key from the Memory.fit app (Settings › AI agents › Use a key instead) and send it as the header `Authorization: Bearer <key>`. Never ask for it in chat if the client has a settings field for it.
4. Check the connection with the tool `get_guide`.

The user needs a Memory.fit account set up in the app (https://memory.fit/app).
