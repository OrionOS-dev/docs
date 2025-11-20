# OrionOS Documentation

Welcome to the OrionOS documentation! OrionOS is a powerful TypeScript framework for building autonomous AI agents with unique personalities, persistent memory, and real-world interaction capabilities.

## What is OrionOS?

OrionOS enables developers to create agents with unique, persistent personalities, equip them with plugins to interact with the world, and let them work toward their goals independently.

### Key Capabilities

- **Develop distinct personalities and objectives** through character configuration files
- **Interact with the real world** using a collection of 90+ integrated plugins
- **Chain complex actions** triggered by natural language inputs
- **Retain and learn** from interactions via persistent memory systems
- **Deploy flexibly** across local development environments and cloud production infrastructure

## Quick Start

Get started with OrionOS using the API:

```bash
# Set your API key
export ORION_API_KEY="your_api_key_here"

# Create a new agent
curl -X POST https://api.orionos.dev/v1/agents \
  -H "Authorization: Bearer $ORION_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"name": "MyAgent", "modelProvider": "openai", "model": "gpt-4"}'

# Send a message to your agent
curl -X POST https://api.orionos.dev/v1/agents/agent_id/messages \
  -H "Authorization: Bearer $ORION_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"text": "Hello!", "userId": "user_123"}'
```

## Plugin Ecosystem

OrionOS ships with an extensive plugin library spanning multiple domains:

- **Social platforms**: Discord, Twitter, Telegram
- **Blockchain networks**: Ethereum, Solana, Base
- **AI providers**: OpenAI, Anthropic, OpenRouter, and local models
- **Financial protocols**: DeFi trading, lending, yield farming
- **Content generation**: Image and video creation capabilities
- **Data operations**: Web scraping, API integrations, databases

## Design Philosophy

OrionOS emphasizes three core principles:

1. **Rapid Deployment** - Three commands to a live agent
2. **Accessibility** - Built for developers of all skill levels
3. **Open Source** - Community-driven development where contributions shape the future

## What You Can Build

With OrionOS, you can create:

- Social media agents that engage and grow communities
- Trading bots that execute sophisticated DeFi strategies
- Content creators that generate images, videos, and text
- Personal assistants that manage tasks and workflows
- Research agents that gather and analyze information
- Customer service bots that handle support queries
- And much more...

## Get Started

Ready to build your first agent? Head over to the [Installation](getting-started/installation.md) guide to begin your journey with OrionOS.
