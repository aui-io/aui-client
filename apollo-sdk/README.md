# Apollo SDK

TypeScript and Python SDKs for the AUI Apollo API, featuring REST endpoints and WebSocket real-time communication.

## 📦 Published Package

**npm:** [`@aui.io/apollo-sdk`](https://www.npmjs.com/package/@aui.io/apollo-sdk)  
**PyPI:** `aui-apollo-sdk` (optional)

## 🚀 Installation

```bash
npm install @aui.io/apollo-sdk
```

## 💻 Usage

### REST API

```typescript
import { AuiApiClient } from '@aui.io/apollo-sdk';

const client = new AuiApiClient({
  baseUrl: 'https://api-staging.internal-aui.io/ia-controller',
  apiKey: 'your-api-key',
});

// Get task messages
const messages = await client.externalApis.getTaskMessages('task-id');

// Create a task
const task = await client.externalApis.createTask({
  user_id: 'user-123',
  text: 'Find a microwave',
});

// Submit a message
await client.externalApis.submitMessage({
  task_id: 'task-id',
  text: 'Hello',
});
```

### WebSocket Real-Time Communication

```typescript
import { AuiApiClient } from '@aui.io/apollo-sdk';

const client = new AuiApiClient({
  apiKey: 'your-api-key',
});

// Connect to WebSocket
const socket = await client.externalSession.connect();

// Listen for messages
socket.on('open', () => {
  console.log('Connected');
});

socket.on('message', (message) => {
  console.log('Received:', message);
});

// Send a message
socket.sendUserMessage({
  task_id: 'task-id',
  text: 'I need help finding a product',
});

// Close connection
socket.close();
```

## 🏗️ Project Structure

```
apollo-sdk/
├── fern/                      # Fern configuration
│   ├── openapi.json          # OpenAPI 3.1.0 spec (generated from production)
│   ├── asyncapi.yaml         # AsyncAPI 3.0.0 spec (WebSocket)
│   └── generators.yml        # SDK generation config
├── scripts/                   # Automation scripts
│   ├── fetch-openapi.sh      # Fetch API spec from production
│   └── filter-external-api.js # Filter external endpoints only
├── tests/                     # SDK tests
│   └── typescript/           # TypeScript test suite
├── generated-sdks/           # Generated SDKs (local development)
│   ├── typescript/
│   └── python/
├── generate-and-publish.sh   # Main automation script
├── DEVOPS-GUIDE.md          # DevOps publishing guide
└── README.md                # This file
```

## 🔧 Development

### For DevOps: Publishing the SDK

**See [DEVOPS-GUIDE.md](./DEVOPS-GUIDE.md) for complete instructions.**

Quick publish command:
```bash
NPM_TOKEN="npm_your_token" ./generate-and-publish.sh
```

### For Developers: Testing Locally

```bash
# Generate SDKs locally without publishing
./generate-and-publish.sh --local-only

# Run tests
cd tests/typescript
npm install
npm test                  # REST API test
npm run test:websocket    # WebSocket test
```

## 📋 API Features

### REST Endpoints
- **Create Task**: `POST /api/v1/external/tasks`
- **Get Task Messages**: `GET /api/v1/external/tasks/{task_id}/messages`
- **Submit Message**: `POST /api/v1/external/message`

### WebSocket
- **Connect**: Real-time bidirectional communication
- **Send Messages**: User messages to agent
- **Receive Events**: 
  - Streaming text updates
  - Product recommendations
  - Final messages
  - Error notifications

## 🔐 Authentication

All API calls require an API key:

```typescript
const client = new AuiApiClient({
  apiKey: 'API_KEY_XXXXXXXXXX',
});
```

For WebSocket, authentication is handled automatically using the same API key.

## 🛠️ Script Commands

```bash
# Generate and publish (requires NPM_TOKEN)
NPM_TOKEN="token" ./generate-and-publish.sh

# Generate locally only
./generate-and-publish.sh --local-only

# Dry run (validate without publishing)
./generate-and-publish.sh --dry-run

# Skip publishing step
./generate-and-publish.sh --skip-publish

# Get help
./generate-and-publish.sh --help
```

## 📊 Workflow

The automation script performs these steps:

1. **Fetch OpenAPI** from production (`https://azure.aui.io`)
2. **Filter** to external-only endpoints (3 endpoints, 13 schemas)
3. **Validate** OpenAPI and AsyncAPI specifications
4. **Generate** SDKs using Fern
5. **Publish** to npm (and optionally PyPI)

## 🧪 Testing

### Test Files
- `tests/typescript/test-tasks.js` - REST API tests
- `tests/typescript/test-websocket.js` - WebSocket tests

### Running Tests
```bash
cd tests/typescript

# Install the published package
npm install @aui.io/apollo-sdk

# Run REST API test
npm test

# Run WebSocket test
npm run test:websocket

# Run all tests
npm run test:all
```

## 🌐 Environments

### Staging
- **REST API**: `https://api-staging.internal-aui.io/ia-controller`
- **WebSocket**: Configured automatically by SDK

### Production
- **REST API**: `https://api.aui.io/ia-controller`
- **WebSocket**: Configured automatically by SDK

## 📝 Configuration

### generators.yml
Main configuration for SDK generation:
- TypeScript SDK: `@aui.io/apollo-sdk`
- Python SDK: `aui-apollo-sdk` (optional)
- WebSocket support: Enabled
- Target versions: Latest stable

## 🔄 Version Management

Versions are auto-incremented by Fern with each publish. Check current version:

```bash
npm view @aui.io/apollo-sdk version
```

## 🆘 Troubleshooting

### "Unauthorized" errors in tests
The default API keys in tests are placeholders. Use real API keys:

```bash
API_KEY="your-key" TASK_ID="your-task-id" npm test
```

### npm cache permission errors
```bash
npm cache clean --force
```

### Import errors after publishing
Wait a few minutes for npm CDN to propagate, then:
```bash
npm install @aui.io/apollo-sdk@latest
```

## 📚 Additional Resources

- **DevOps Guide**: See [DEVOPS-GUIDE.md](./DEVOPS-GUIDE.md) for publishing instructions
- **OpenAPI Spec**: See `fern/openapi.json`
- **AsyncAPI Spec**: See `fern/asyncapi.yaml`
- **Fern Docs**: https://docs.buildwithfern.com

## 🤝 Contributing

This SDK is auto-generated from the production API specification. To update:

1. Modify the OpenAPI spec in production
2. Run the generation script
3. Publish the new version

## 📄 License

Internal use only - AUI.io

---

**Package:** `@aui.io/apollo-sdk`  
**Generated by:** Fern  
**Updated:** Automatically from production API
