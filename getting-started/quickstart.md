# Quickstart

Get your first OrionOS agent up and running in just a few minutes using the API!

## Prerequisites

- OrionOS server running (see [Installation](installation.md))
- API key from your OrionOS account
- HTTP client (curl, Postman, or your preferred programming language)

## Step 1: Get Your API Key

1. Sign up at [orionos.dev](https://orionos.dev)
2. Navigate to Settings → API Keys
3. Generate a new API key
4. Save it securely as an environment variable:

```bash
export ORION_API_KEY="your_api_key_here"
```

## Step 2: Create Your First Agent

Use the API to create a new agent with a custom personality:

### Using cURL

```bash
curl -X POST https://api.orionos.dev/v1/agents \
  -H "Authorization: Bearer $ORION_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Orion",
    "bio": [
      "I am Orion, an AI agent built on OrionOS.",
      "I help users with various tasks and conversations.",
      "I am friendly, helpful, and always learning."
    ],
    "personality": {
      "traits": ["helpful", "curious", "intelligent", "friendly"],
      "style": "conversational and engaging"
    },
    "knowledge": [
      "I know about AI and machine learning",
      "I understand blockchain technology",
      "I can help with coding and development"
    ],
    "goals": [
      "Help users accomplish their tasks",
      "Learn from every interaction",
      "Provide accurate and helpful information"
    ],
    "modelProvider": "openai",
    "model": "gpt-4"
  }'
```

### Using JavaScript

```javascript
const axios = require('axios');

const createAgent = async () => {
  const response = await axios.post(
    'https://api.orionos.dev/v1/agents',
    {
      name: 'Orion',
      bio: [
        'I am Orion, an AI agent built on OrionOS.',
        'I help users with various tasks and conversations.',
        'I am friendly, helpful, and always learning.'
      ],
      personality: {
        traits: ['helpful', 'curious', 'intelligent', 'friendly'],
        style: 'conversational and engaging'
      },
      knowledge: [
        'I know about AI and machine learning',
        'I understand blockchain technology',
        'I can help with coding and development'
      ],
      goals: [
        'Help users accomplish their tasks',
        'Learn from every interaction',
        'Provide accurate and helpful information'
      ],
      modelProvider: 'openai',
      model: 'gpt-4'
    },
    {
      headers: {
        'Authorization': `Bearer ${process.env.ORION_API_KEY}`,
        'Content-Type': 'application/json'
      }
    }
  );

  console.log('Agent created:', response.data);
  return response.data.data;
};

createAgent();
```

### Using Python

```python
import requests
import os

def create_agent():
    url = "https://api.orionos.dev/v1/agents"
    headers = {
        "Authorization": f"Bearer {os.getenv('ORION_API_KEY')}",
        "Content-Type": "application/json"
    }
    data = {
        "name": "Orion",
        "bio": [
            "I am Orion, an AI agent built on OrionOS.",
            "I help users with various tasks and conversations.",
            "I am friendly, helpful, and always learning."
        ],
        "personality": {
            "traits": ["helpful", "curious", "intelligent", "friendly"],
            "style": "conversational and engaging"
        },
        "knowledge": [
            "I know about AI and machine learning",
            "I understand blockchain technology",
            "I can help with coding and development"
        ],
        "goals": [
            "Help users accomplish their tasks",
            "Learn from every interaction",
            "Provide accurate and helpful information"
        ],
        "modelProvider": "openai",
        "model": "gpt-4"
    }

    response = requests.post(url, json=data, headers=headers)
    response.raise_for_status()
    print("Agent created:", response.json())
    return response.json()['data']

create_agent()
```

### Response

You'll receive a response like this:

```json
{
  "success": true,
  "data": {
    "id": "agent_a1b2c3d4e5f6",
    "name": "Orion",
    "status": "active",
    "createdAt": "2025-01-15T10:30:00Z",
    "apiEndpoint": "https://api.orionos.dev/v1/agents/agent_a1b2c3d4e5f6"
  }
}
```

Save the `id` value - you'll need it to interact with your agent!

## Step 3: Send a Message to Your Agent

Now let's chat with your agent:

### Using cURL

```bash
curl -X POST https://api.orionos.dev/v1/agents/agent_a1b2c3d4e5f6/messages \
  -H "Authorization: Bearer $ORION_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "text": "Hello! What can you help me with?",
    "userId": "user_123"
  }'
```

### Using JavaScript

```javascript
const sendMessage = async (agentId, message) => {
  const response = await axios.post(
    `https://api.orionos.dev/v1/agents/${agentId}/messages`,
    {
      text: message,
      userId: 'user_123'
    },
    {
      headers: {
        'Authorization': `Bearer ${process.env.ORION_API_KEY}`,
        'Content-Type': 'application/json'
      }
    }
  );

  console.log('Agent:', response.data.data.response);
  return response.data;
};

sendMessage('agent_a1b2c3d4e5f6', 'Hello! What can you help me with?');
```

### Response

```json
{
  "success": true,
  "data": {
    "messageId": "msg_xyz789",
    "response": "Hi there! I'm Orion. I can help you with many things including answering questions about AI and machine learning, explaining blockchain technology, and assisting with coding and development. What would you like to explore?",
    "agentId": "agent_a1b2c3d4e5f6",
    "userId": "user_123",
    "timestamp": "2025-01-15T10:35:00Z"
  }
}
```

## Step 4: Add Platform Integrations

### Discord Integration

Update your agent to connect to Discord:

```bash
curl -X PATCH https://api.orionos.dev/v1/agents/agent_a1b2c3d4e5f6 \
  -H "Authorization: Bearer $ORION_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "clients": ["discord"],
    "settings": {
      "discord": {
        "channels": ["general", "bot-commands"],
        "respondToMentions": true
      }
    }
  }'
```

Make sure you've set up your Discord bot token in the OrionOS server environment variables.

### Twitter Integration

Add Twitter capabilities:

```bash
curl -X PATCH https://api.orionos.dev/v1/agents/agent_a1b2c3d4e5f6 \
  -H "Authorization: Bearer $ORION_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "clients": ["discord", "twitter"],
    "settings": {
      "twitter": {
        "enableReplies": true,
        "enableMentions": true,
        "postFrequency": "4h"
      }
    }
  }'
```

## Step 5: Test Conversations

The agent remembers context when you use the same `userId`:

```javascript
// First message
await sendMessage('agent_a1b2c3d4e5f6', 'What is blockchain?', 'user_123');
// Response: "Blockchain is a distributed ledger technology..."

// Follow-up message (agent remembers the context)
await sendMessage('agent_a1b2c3d4e5f6', 'How is it used in DeFi?', 'user_123');
// Response: "In DeFi, blockchain technology is used to..."
```

## Example: Complete Workflow

Here's a complete example that creates an agent and has a conversation:

```javascript
const axios = require('axios');

const API_BASE = 'https://api.orionos.dev/v1';
const API_KEY = process.env.ORION_API_KEY;

const client = axios.create({
  baseURL: API_BASE,
  headers: {
    'Authorization': `Bearer ${API_KEY}`,
    'Content-Type': 'application/json'
  }
});

async function main() {
  // 1. Create agent
  const createResponse = await client.post('/agents', {
    name: 'DeFiHelper',
    bio: ['I help users understand DeFi protocols'],
    personality: {
      traits: ['knowledgeable', 'patient', 'helpful'],
      style: 'clear and educational'
    },
    modelProvider: 'openai',
    model: 'gpt-4'
  });

  const agentId = createResponse.data.data.id;
  console.log(`Created agent: ${agentId}`);

  // 2. Send messages
  const messages = [
    'What is DeFi?',
    'How do liquidity pools work?',
    'What are the risks?'
  ];

  for (const message of messages) {
    const response = await client.post(
      `/agents/${agentId}/messages`,
      {
        text: message,
        userId: 'user_123'
      }
    );

    console.log(`\nYou: ${message}`);
    console.log(`Agent: ${response.data.data.response}`);
  }

  // 3. Get agent details
  const agentDetails = await client.get(`/agents/${agentId}`);
  console.log(`\nAgent stats:`, agentDetails.data.data.metrics);
}

main().catch(console.error);
```

## Add More Capabilities

### Enable Plugins

Update your agent with blockchain capabilities:

```bash
curl -X PATCH https://api.orionos.dev/v1/agents/agent_a1b2c3d4e5f6 \
  -H "Authorization: Bearer $ORION_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "plugins": [
      {
        "name": "@orionos/plugin-evm",
        "enabled": true,
        "config": {
          "chains": ["ethereum", "polygon"]
        }
      }
    ]
  }'
```

## Next Steps

- [API Reference](../api-reference/overview.md) - Complete API documentation
- [Customize Your Agent](../guides/customize-agent.md) - Deep dive into character configuration
- [Platform Integrations](../guides/platform-integrations.md) - Connect to Discord, Twitter, and more
- [Plugin Reference](../plugins/reference.md) - Browse available plugins

## SDK Installation (Optional)

For easier development, install the official SDK:

### JavaScript/TypeScript

```bash
npm install @orionos/sdk
```

```javascript
const { OrionOS } = require('@orionos/sdk');

const orion = new OrionOS({
  apiKey: process.env.ORION_API_KEY
});

// Create agent
const agent = await orion.agents.create({
  name: 'MyAgent',
  personality: { traits: ['helpful'] }
});

// Send message
const response = await orion.agents.sendMessage(agent.id, {
  text: 'Hello!',
  userId: 'user_123'
});
```

### Python

```bash
pip install orionos
```

```python
from orionos import OrionOS

orion = OrionOS(api_key=os.getenv('ORION_API_KEY'))

# Create agent
agent = orion.agents.create(
    name='MyAgent',
    personality={'traits': ['helpful']}
)

# Send message
response = orion.agents.send_message(
    agent.id,
    text='Hello!',
    user_id='user_123'
)
```

## Need Help?

- [API Overview](../api-reference/overview.md) - API documentation
- [Discord Community](https://discord.gg/orionos) - Get help from the community
- [GitHub Discussions](https://github.com/OrionOS-dev/orionos/discussions) - Ask questions
- [GitHub Issues](https://github.com/OrionOS-dev/orionos/issues) - Report bugs
