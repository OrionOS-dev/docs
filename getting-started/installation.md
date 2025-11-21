# Installation

This guide will walk you through installing OrionOS and setting up your development environment.

## Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v20.x or higher)
- **npm** or **pnpm** (package manager)
- **Git** (for version control)

### Verify Installation

```bash
node --version  # Should be v20.x or higher
npm --version   # Should be 9.x or higher
```

## Installation Methods

### Option 1: Clone the Repository

For contributing to OrionOS core or developing custom agents:

```bash
# Clone the repository
git clone https://github.com/OrionOS-dev/orionos.git
cd orionos

# Install dependencies
pnpm install

# Build the project
pnpm build

# Run tests (optional)
pnpm test
```

### Option 2: Docker Installation

Run OrionOS in a containerized environment:

```bash
# Pull the official image
docker pull orionos/orionos:latest

# Run a container with environment variables
docker run -d \
  --name my-orion-agent \
  -e OPENAI_API_KEY=your_key \
  -e ANTHROPIC_API_KEY=your_key \
  -p 3000:3000 \
  orionos/orionos:latest
```

## Environment Setup

OrionOS requires certain environment variables to function properly. Create a `.env` file in your project root:

```bash
# AI Provider API Keys
OPENAI_API_KEY=your_openai_key
ANTHROPIC_API_KEY=your_anthropic_key

# Platform Integrations
DISCORD_BOT_TOKEN=your_discord_token
TWITTER_API_KEY=your_twitter_key
TELEGRAM_BOT_TOKEN=your_telegram_token

# Database (optional, uses SQLite by default)
DATABASE_URL=postgresql://user:password@localhost:5432/orionos

# API Server Configuration
PORT=3000
HOST=0.0.0.0
API_KEY=your_secure_api_key
```

## Starting the OrionOS Server

Once installed and configured, start the OrionOS server:

```bash
# Development mode
pnpm dev

# Production mode
pnpm start
```

The OrionOS API server will be available at `http://localhost:3000`

## System Requirements

### Minimum Requirements

- **CPU**: 2 cores
- **RAM**: 4GB
- **Storage**: 10GB free space
- **OS**: Windows 10+, macOS 11+, Linux (Ubuntu 20.04+)

### Recommended Requirements

- **CPU**: 4+ cores
- **RAM**: 8GB+
- **Storage**: 20GB+ SSD
- **OS**: Latest stable versions

## Verifying Installation

Test that the API server is running:

```bash
curl http://localhost:3000/health
```

Expected response:
```json
{
  "status": "ok",
  "version": "1.0.0"
}
```

## Next Steps

Now that you have OrionOS installed, head over to the [Quickstart](quickstart.md) guide to create your first agent!
