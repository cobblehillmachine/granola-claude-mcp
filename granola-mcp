cd ~/granola-mcp

# Add your server file to the repo
git add granola_mcp_server.py

# Add the test script
git add test_granola.py

# Replace the basic README with the comprehensive one
# (Copy the README content from the artifact I created above)

# Create the example config
mkdir -p examples
cat > examples/claude_desktop_config.json << 'EOF'
{
  "mcpServers": {
    "granola-mcp": {
      "command": "python3", 
      "args": ["/Users/[username]/granola-claude-mcp/granola_mcp_server.py"],
      "env": {
        "GRANOLA_CACHE_PATH": "/Users/[username]/Library/Application Support/Granola/cache-v3.json"
      }
    }
  }
}
EOF

# Create requirements.txt
cat > requirements.txt << 'EOF'
# This MCP server uses only Python standard library
# No external dependencies required
# Python 3.12+ recommended
EOF

# Commit all the files
git add .
git commit -m "Add complete MCP server implementation

- Full Python MCP server with Granola cache parsing
- Test suite for validation
- Example Claude Desktop configuration  
- Comprehensive documentation and setup guide
- Support for 273+ meetings with metadata integration"

git push origin main
