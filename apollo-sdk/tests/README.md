# Apollo SDK Test Projects

Simple test projects to verify the generated SDKs work correctly.

## TypeScript Test

### Setup
```bash
cd tests/typescript
npm install
```

### Run Tests

#### REST API Test
```bash
# Test task messages endpoint
npm test

# Or with custom values
API_KEY='your-api-key' TASK_ID='your-task-id' BASE_URL='https://api-staging.internal-aui.io/ia-controller' npm test
```

#### WebSocket Test
```bash
# Test WebSocket real-time communication
npm run test:websocket

# Or with custom values
API_KEY='your-api-key' TASK_ID='6909127a8b91758e2d2f4ff9' MESSAGE_TEXT='I am looking for a built-in microwave' npm run test:websocket
```

#### Run All Tests
```bash
npm run test:all
```

## Python Test

### Setup
```bash
cd tests/python
pip install -r requirements.txt
pip install -e ../../generated-sdks/python
```

### Run
```bash
# Use default values
python test_tasks.py

# Or with custom values
API_KEY='your-api-key' USER_ID='your-user-id' BASE_URL='https://api-staging.internal-aui.io/ia-controller' python test_tasks.py
```

## Environment Variables

### REST API Tests
- `API_KEY`: Your API key for authentication
- `TASK_ID`: Task ID to fetch messages for
- `BASE_URL`: Base URL for the REST API (default: staging URL)

### WebSocket Tests
- `API_KEY`: Your API key for WebSocket authentication
- `TASK_ID`: Task ID for the conversation
- `MESSAGE_TEXT`: The message text to send to the agent

