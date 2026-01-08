# Kiwi Flight Planner - AI Agents System

A conversational flight planning application built with Flowise AI that uses the Kiwi MCP Server to search and recommend flights through natural language interactions.

🤖 **[Try the Live Chatbot](https://cloud.flowiseai.com/chatbot/b88125ca-320b-4041-ab37-351a19545f29)**

<a href="https://youtu.be/u_uEZVTu3Tg" target="_blank">
  <img src="https://github.com/user-attachments/assets/42fa1b08-b632-45bf-8cdd-5b283b29c7e1" alt="Flowise agents video example" width="500"/>
</a>

<br>
<br>
<img src="https://github.com/user-attachments/assets/b2a7d77d-613a-4620-bbd8-e539e00832c2" alt="A moment from the hackathon" width="600"/>

## Overview

This project implements a multi-agent system that translates natural language travel requests into structured flight searches, providing users with intelligent flight recommendations and explanations.

## Architecture

The system uses a **supervisor-worker pattern** with specialized agents:

- **Supervisor Agent**: Orchestrates the conversation flow between workers
- **Trip Planner Agent**: Converts natural language requests into structured search parameters
- **Flight Search Agent**: Uses the Kiwi MCP Server to find and rank flight options

## Key Features

- **Natural Language Processing**: Ask for flights in plain English
- **Intelligent Planning**: Automatically extracts travel details from conversations
- **Real Flight Data**: Powered by Kiwi.com's flight search API via MCP
- **Smart Recommendations**: Ranks flights by price, duration, and user preferences
- **Conversational Refinement**: Iteratively improve search results through chat

## Technology Stack

- **Flowise AI**: Visual agent orchestration platform
- **OpenAI GPT-4**: Language model for natural language understanding
- **Kiwi MCP Server**: Flight data integration via Model Context Protocol
- **Node.js**: Runtime environment

## Example Conversation

```
User: "Find the cheapest flight from Vienna to New York next month"

Trip Planner: Extracts → VIE to NYC, flexible dates in January 2026

Flight Search: "Found 3 options:
1) €430 - 1 stop (14h total) 
2) €510 - Direct flight (9h total)
3) €380 - 2 stops (18h total)

The cheapest is option 3, but option 1 offers better value. Which do you prefer?"
```

## Project Structure

```
├── Kiwi Flight Planner Agents.json  # Flowise canvas configuration
├── PROJECT.md                       # Detailed project specification
├── package.json                     # Node.js dependencies
└── README.md                        # This file
```

## Setup & Installation

1. **Install Dependencies**
   ```bash
   npm install
   ```

2. **Configure Flowise**
   - Import `Kiwi Flight Planner Agents.json` into your Flowise instance
   - Set up OpenAI API credentials
   - Configure the Kiwi MCP Server connection

3. **MCP Server Configuration**
   - The system uses Kiwi's public MCP endpoint: `https://mcp.kiwi.com`
   - No additional API keys required for basic flight search

## Agent Configuration

### Trip Planner Agent
- **Role**: Natural language to structured data conversion
- **Input**: Raw user travel requests
- **Output**: JSON with flight search parameters
- **Validation**: Ensures required fields (origin, destination, dates) are present

### Flight Search Agent  
- **Role**: Flight data retrieval and recommendation
- **Tools**: Kiwi MCP Server integration
- **Output**: Ranked flight options with explanations
- **Features**: Price comparison, duration analysis, booking links



## Market Gap: 

ChatGPT doesn't book flights well: https://chatgpt.com/share/6943e6f3-262c-800e-a5f1-45f11446254d , as well Gemini (which is better) https://gemini.google.com/share/4521ed6f3292 and Claude https://claude.ai/share/ecc17eae-443a-4308-a30c-80f9f14ff671 .

## Supported Features

✅ One-way and return flights  
✅ Flexible date searches  
✅ Multi-stop flight options  
✅ Price and duration optimization  
✅ Conversational refinement  
✅ Direct booking links  

❌ Hotel bookings (future enhancement)  
❌ Car rentals (future enhancement)  
❌ Travel insurance (future enhancement)  

## Development

The project is built using Flowise's visual agent builder with custom MCP integration. The main configuration is stored in the JSON file which can be imported directly into Flowise.

For detailed implementation specifications, see [PROJECT.md](PROJECT.md).

## MCP Integration

This project demonstrates integration with the Model Context Protocol (MCP) for accessing external APIs. The Kiwi MCP Server provides:

- Real-time flight search capabilities
- Airport and airline data
- Pricing and availability information
- Direct booking integration

**MCP Server**: https://apify.com/agentify/kiwi-mcp-server

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes to the Flowise configuration
4. Export the updated JSON configuration
5. Submit a pull request

## License

ISC License - see package.json for details
