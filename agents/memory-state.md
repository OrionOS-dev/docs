# Memory and State

Learn how OrionOS agents store and recall information across conversations.

## Overview

OrionOS agents maintain memory and state to provide context-aware, personalized interactions. The memory system enables agents to remember past conversations, user preferences, and learned information.

## Memory Types

### Short-Term Memory

Conversation context within a single session:

```json
{
  "memory": {
    "shortTermContext": 10,
    "contextWindow": "last_10_messages"
  }
}
```

### Long-Term Memory

Persistent storage across sessions:

```json
{
  "memory": {
    "enabled": true,
    "longTermEnabled": true,
    "rememberUsers": true,
    "rememberConversations": true,
    "retentionDays": 90
  }
}
```

### Knowledge Base

Static information the agent knows:

```json
{
  "knowledge": [
    "Expert in DeFi protocols",
    "Understanding of yield farming",
    "Knowledge of liquidity pools"
  ]
}
```

## State Management

### User State

```javascript
// Store user preferences
await agent.state.setUserData(userId, {
  preferences: { language: 'en', theme: 'dark' },
  history: []
});

// Retrieve user state
const userData = await agent.state.getUserData(userId);
```

### Conversation State

```javascript
// Track conversation context
await agent.state.setContext(conversationId, {
  topic: 'DeFi',
  lastMessage: 'What is yield farming?',
  entities: ['DeFi', 'yield farming']
});
```

## Memory Configuration

```json
{
  "memory": {
    "provider": "postgresql",
    "cacheEnabled": true,
    "cacheTTL": 3600,
    "maxMemorySize": "100MB",
    "embeddings": {
      "enabled": true,
      "model": "text-embedding-ada-002"
    }
  }
}
```

## Best Practices

1. **Privacy**: Respect user privacy, allow data deletion
2. **Retention**: Set appropriate data retention periods
3. **Relevance**: Store only relevant information
4. **Performance**: Use caching for frequently accessed data
5. **Security**: Encrypt sensitive information

## Next Steps

- [Runtime and Lifecycle](runtime-lifecycle.md)
- [Character Interface](character-interface.md)

## Need Help?

- [Discord Community](https://discord.gg/orionos)
- [GitHub Discussions](https://github.com/OrionOS-dev/orionos/discussions)
