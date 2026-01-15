A command-line terminal where users can query in natural language. A command line interface is arguably the most poorly designed interface because the names of the commands are not intuitive and the number of parameters are somewhat arbitrary. As such, users must memorize the syntax of a command. It may work for expert users but not for regular computer users.

Objectives:
Gain hands-on experience with how to use local, large, language model to create LLM-powered app
How to create an agentic interaction with tool usage and MCP protocol
Learn how to wrap command-line operations as callable tools in a server.
Use of streaming model outputs and maintaining history to support deictic conversation.
Explore how to handle tool results in a conversational setting.

MCP-based system consisting of:
MCP Server (Terminal Tool)
Build a server that exposes terminal-related operations as MCP tools:
initiate_terminal: starts a persistent shell session. 
run_command: executes the given bash command within the terminal and returns its output.
terminate_terminal: safely closes the shell session.
Ensure the server maintains state (e.g., directory changes) across commands.
Handle process I/O properly using Python’s subprocess.
Example:
Client: cd ~/Desktop,    Tool: (changes directory inside the terminal session)
Client: ls,   Tool: returns list of files in ~/Desktop

MCP Client (Conversational Agent)
Build a client that connects to the MCP server.
Use Ollama as the underlying LLM (gpt-oss:20b or llama3.2:3b)
Maintain a loop for the conversation where the user enters either natural language or direct commands.

The model should:
Translate natural requests into commands (e.g., “What’s in this folder?” → ls -la).
Verify direct commands before sending to the tool.
Summarize terminal outputs into human-readable explanations.

Example:
User: What files are in this directory?
Model: decides which tool to use and the command → call_tool(tool_name="run_command", argument="ls -la")
Tool: returns terminal output
Model: explains → "There are 3 files: assignment.pdf, notes.txt, and data.csv."
