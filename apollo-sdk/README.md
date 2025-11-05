# Apollo SDK - Automated Generation & Publishing

Automated SDK generation and publishing for TypeScript and Python from FastAPI OpenAPI specifications.

## Quick Start

### Generate SDKs Locally

```bash
cd apollo-sdk
./generate-and-publish.sh --local-only
```

Generated SDKs will be in:
- `generated-sdks/typescript/`
- `generated-sdks/python/`

### Publish to npm and PyPI

```bash
export NPM_TOKEN='your-npm-token'
export PYPI_TOKEN='your-pypi-token'
./generate-and-publish.sh
```

## Prerequisites

- **Node.js 18+** with npm
- **jq** (JSON processor): `brew install jq` or `apt-get install jq`
- **Fern CLI**: `npm install -g fern-api`
- **curl** (usually pre-installed)

## Usage

### Options

| Command | Description |
|---------|-------------|
| `./generate-and-publish.sh --local-only` | Generate SDKs locally without publishing |
| `./generate-and-publish.sh --dry-run` | Validate without making changes |
| `./generate-and-publish.sh --skip-publish` | Generate but don't publish |
| `./generate-and-publish.sh` | Full run: generate and publish |

### What It Does

1. Fetches OpenAPI from production (`https://azure.aui.io/api/ia-controller/api/openapi.json`)
2. Filters external-only endpoints (paths containing `/external/`)
3. Validates OpenAPI and AsyncAPI specifications
4. Generates TypeScript SDK using Fern
5. Generates Python SDK using Fern
6. Publishes to npm (`@aui/apollo-sdk`) and PyPI (`aui-apollo-api`)

## Directory Structure

```
apollo-sdk/
├── generate-and-publish.sh      # Main automation script
├── specs/                        # API specifications
│   ├── openapi.json              # Full OpenAPI (fetched)
│   ├── external-openapi.json     # Filtered external-only
│   └── asyncapi.yaml             # WebSocket API spec
├── scripts/                      # Automation scripts
│   ├── fetch-openapi.sh          # Fetch from production
│   └── filter-external-api.js    # Filter external endpoints
├── fern/                         # Fern configuration
│   ├── fern.config.json
│   ├── generators.yml            # SDK generation config
│   └── definition/
│       ├── api.yml
│       └── openapi.json          # OpenAPI used by Fern
├── generated-sdks/               # Local SDK outputs
│   ├── typescript/
│   └── python/
└── tests/                        # Integration tests
    ├── typescript/
    └── python/
```

## Published Packages

### TypeScript SDK

**Package:** `@aui/apollo-sdk`  
**Registry:** npm

**Installation:**
```bash
npm install @aui/apollo-sdk
```

**Usage:**
```typescript
import { AuiApolloApiClient } from '@aui/apollo-sdk';

const client = new AuiApolloApiClient({
  environment: 'https://azure.aui.io/api/ia-controller',
});

const messages = await client.getTaskMessagesApiV1ExternalTasksTaskIdMessagesGet({
  task_id: 'task-id',
  'x-network-api-key': 'your-api-key',
});
```

### Python SDK

**Package:** `aui-apollo-api`  
**Registry:** PyPI

**Installation:**
```bash
pip install aui-apollo-api
```

**Usage:**
```python
from aui_apollo_api import AuiApolloApiClient

client = AuiApolloApiClient(
    base_url='https://azure.aui.io/api/ia-controller'
)

messages = client.get_task_messages_api_v_1_external_tasks_task_id_messages_get(
    task_id='task-id',
    x_network_api_key='your-api-key'
)
```

## Testing

### TypeScript Test

```bash
cd tests/typescript
npm install
npm test
```

### Python Test

```bash
cd tests/python
python3 test_tasks.py
```

## Troubleshooting

### Error: "Missing required environment variables"

Set tokens or use `--local-only`:
```bash
export NPM_TOKEN='your-npm-token'
export PYPI_TOKEN='your-pypi-token'
# Or run without publishing:
./generate-and-publish.sh --local-only
```

### Error: "fern: command not found"

```bash
npm install -g fern-api
```

### Error: "jq: command not found"

```bash
# macOS
brew install jq

# Linux
sudo apt-get install jq
```

### Error: "Failed to fetch OpenAPI spec"

Check network connectivity to `https://azure.aui.io/api/ia-controller/api/openapi.json`

## CI/CD Integration

### Jenkins Pipeline Example

```groovy
pipeline {
    agent any
    
    environment {
        NPM_TOKEN = credentials('npm-publish-token')
        PYPI_TOKEN = credentials('pypi-publish-token')
    }
    
    triggers {
        cron('0 2 * * *')  // Daily at 2 AM
    }
    
    stages {
        stage('Generate and Publish SDKs') {
            steps {
                dir('apollo-sdk') {
                    sh '''
                        export NPM_TOKEN="${NPM_TOKEN}"
                        export PYPI_TOKEN="${PYPI_TOKEN}"
                        ./generate-and-publish.sh
                    '''
                }
            }
        }
    }
}
```

### Required Jenkins Credentials

- `npm-publish-token` (Secret text) - npm publish token
- `pypi-publish-token` (Secret text) - PyPI publish token

## Notes

- The OpenAPI spec is automatically fetched from production on each run
- Only external endpoints (containing `/external/`) are included in the SDKs
- The `servers` field is automatically added to the OpenAPI spec during filtering
- Generated SDKs are in `generated-sdks/` (gitignored)

## Support

For issues or questions, contact the Platform Team.
