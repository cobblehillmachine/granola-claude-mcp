# Granola-Claude MCP Server

> **Transform your meeting data into AI-powered business intelligence**

A custom Model Context Protocol (MCP) server that connects [Granola.ai](https://granola.ai) meeting data directly to Claude Desktop, enabling natural language queries across your entire meeting history.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.12+](https://img.shields.io/badge/python-3.12+-blue.svg)](https://www.python.org/downloads/)
[![MCP Compatible](https://img.shields.io/badge/MCP-Compatible-green.svg)](https://modelcontextprotocol.io/)

---

## 🚀 Why This Exists

While Granola-MCP was documented across the web with detailed feature lists and installation guides, **the actual repository and PyPI package didn't exist**. Rather than wait for an official release, we reverse-engineered Granola's local cache structure and built a comprehensive MCP server from scratch.

**The result?** Ask Claude questions like:
- *"Show me all client meetings from last month where we discussed budget"*
- *"Which team members need follow-up from the Enron project meetings?"*  
- *"Analyze our meeting patterns with external clients vs internal team meetings"*

## ✨ Features

### 🔍 **Natural Language Meeting Intelligence**
- Query 273+ meetings using plain English
- Search across titles, content, and participant lists
- Instant access to meeting metadata and calendar integration

### 📊 **Advanced Analytics**
- Meeting statistics and pattern recognition
- Attendee analysis and engagement tracking
- Project timeline reconstruction from meeting history

### 🔗 **Complete Integration**
- Google Calendar event details and attendee responses
- Conference links (Google Meet, Zoom) and participation status
- Rich metadata including organizers, response status, and sharing settings

### 🛡️ **Privacy-First Architecture** 
- All data processing happens locally - no cloud uploads
- Direct cache file access - no API dependencies
- Respects existing Granola permissions and access controls

## 🎯 Use Cases

### **Project Management**
```
"Show meetings about the XXI Media project and identify next steps"
→ Surfaces July 16 Zoom meeting with Pyxl, attendee status, action items
```

### **Client Relations**
```
"Which clients had 'needsAction' responses this week?"
→ Identifies follow-up requirements across all client touchpoints
```

### **Team Analytics**
```
"Who attends the most external client meetings?"
→ Analyzes workload distribution and development opportunities
```

### **Meeting ROI**
```
"Compare meeting outcomes between Google Meet vs Zoom sessions"
→ Platform effectiveness analysis for future planning
```

## 🛠️ Installation

### Prerequisites
- **macOS** with Granola.ai installed and configured
- **Python 3.12+** 
- **Claude Desktop** application
- Active Granola meeting history

### Quick Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/[USERNAME]/granola-claude-mcp.git
   cd granola-claude-mcp
   ```

2. **Make the server executable**
   ```bash
   chmod +x granola_mcp_server.py
   ```

3. **Test the installation**
   ```bash
   python3 test_granola.py
   ```
   
   You should see:
   ```
   ✅ Cache loaded successfully!
   📊 Statistics: [your meeting data]
   📅 Recent meetings: [your recent meetings]
   ```

4. **Configure Claude Desktop**
   
   Add to `~/Library/Application Support/Claude/claude_desktop_config.json`:
   ```json
   {
     "mcpServers": {
       "granola-mcp": {
         "command": "python3",
         "args": ["/path/to/granola-claude-mcp/granola_mcp_server.py"],
         "env": {
           "GRANOLA_CACHE_PATH": "/Users/[username]/Library/Application Support/Granola/cache-v3.json"
         }
       }
     }
   }
   ```

5. **Restart Claude Desktop**
   
   Quit completely (⌘+Q) and restart Claude Desktop.

6. **Test the integration**
   
   Ask Claude: *"Show me my recent Granola meetings"*

## 🔧 Available Tools

### `get_recent_meetings`
Get your most recent meetings with full metadata
```
Parameters: limit (integer, max 50)
Returns: Meeting list with titles, dates, attendees, calendar integration
```

### `search_meetings` 
Search across meeting titles and content
```
Parameters: query (string), limit (integer, max 20)
Returns: Matching meetings with relevance scoring
```

### `get_meeting_details`
Deep dive into specific meeting data
```
Parameters: meeting_id (string)
Returns: Complete meeting information including notes, attendees, conference details
```

### `get_statistics`
Analytics across your meeting corpus
```
Parameters: none
Returns: Meeting counts, transcript availability, word counts, trends
```

## 🏗️ Architecture

### Data Flow
```
Granola.ai → Local Cache → MCP Server → Claude Desktop → AI Intelligence
```

### Cache Structure
Granola uses a sophisticated "double-JSON" encoding:
```python
# Standard JSON file containing JSON string
cache_data = json.loads(data['cache'])
state = cache_data['state']

# Three primary data collections:
documents = state['documents']        # 273+ meeting records
metadata = state['meetingsMetadata']  # 28 relationship objects  
transcripts = state['transcripts']    # 16 available transcripts
```

### MCP Protocol Implementation
- Full MCP 2025-06-18 protocol compliance
- Proper initialization and capability negotiation
- Error handling and graceful degradation
- Real-time query processing with sub-second response

## 🐛 Troubleshooting

### "Server Failed" in Claude Desktop
1. Check the logs: Claude Desktop → Settings → Developer → Open Logs Folder
2. Verify file paths in your configuration
3. Test server manually: `python3 granola_mcp_server.py`

### "No meetings found"
1. Ensure Granola.ai has processed meetings
2. Verify cache file exists: `ls -la ~/Library/Application\ Support/Granola/`
3. Check cache file size (should be several MB for active users)

### Python/Permission Issues
1. Verify Python 3.12+: `python3 --version`
2. Make server executable: `chmod +x granola_mcp_server.py`
3. Check file permissions on Granola cache directory

### MCP Connection Issues
1. Restart Claude Desktop completely (⌘+Q, then reopen)
2. Validate JSON syntax in claude_desktop_config.json
3. Check environment variable path matches your username

## 🤝 Contributing

We welcome contributions! This project fills a real gap in the AI productivity ecosystem.

**Ways to contribute:**
- 🐛 **Bug Reports**: Issues with specific meeting formats or edge cases
- ✨ **Feature Requests**: Additional analytics, export formats, integration ideas  
- 🔧 **Code Contributions**: Performance improvements, additional MCP tools
- 📚 **Documentation**: Setup guides, use case examples, troubleshooting

### Development Setup
```bash
git clone https://github.com/[USERNAME]/granola-claude-mcp.git
cd granola-claude-mcp

# Test your changes
python3 test_granola.py

# Run the server manually for debugging
python3 granola_mcp_server.py
```

## 📋 Roadmap

### Phase 2: Advanced Analytics
- [ ] Transcript analysis with action item extraction
- [ ] Sentiment analysis for meeting effectiveness
- [ ] Automated follow-up recommendation engine
- [ ] Cross-meeting topic and decision tracking

### Phase 3: Enhanced Integration  
- [ ] Real-time cache monitoring for live updates
- [ ] Multi-platform meeting data (beyond Google Calendar)
- [ ] Export capabilities (PDF reports, CSV analytics)
- [ ] Dashboard web interface for meeting intelligence

### Phase 4: Enterprise Features
- [ ] Multi-user deployment with access controls
- [ ] CRM integration for complete client lifecycle tracking
- [ ] Advanced reporting and business intelligence
- [ ] API development for third-party integrations

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Anthropic** for the Model Context Protocol specification
- **Granola.ai** for building sophisticated meeting intelligence (even if the MCP integration was MIA)
- **The MCP Community** for examples and best practices

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/[USERNAME]/granola-claude-mcp/issues)
- **Discussions**: [GitHub Discussions](https://github.com/[USERNAME]/granola-claude-mcp/discussions)  
- **Professional Services**: For custom integrations and enterprise deployment, contact [Cobble Hill](https://cobblehilldigital.com)

---

**⭐ Star this repo if it helps you extract more value from your meetings!**

*Built with ❤️ by the team at [Cobble Hill ](https://cobblehilldigital.com) - AI integration specialists*
