```bash

#!/bin/bash

set -e

cd "$(dirname "$0")/.."

if ! command -v ngrok &> /dev/null; then
    echo "ngrok must be installed to use this script"
    exit 1
fi

ngrok http http://localhost:4000 > /dev/null 2>&1 &
NGROK_PID=$!
echo "ngrok is running in the background with PID: $NGROK_PID"

# Wait for Ngrok to start, then set the tunnel URL
for i in {1..10}; do
    NGROK_URL=$(curl -s localhost:4040/api/tunnels | jq -r '.tunnels[0].public_url')
    
    if [[ $NGROK_URL == http* ]]; then
        echo "Ngrok URL is: $NGROK_URL"
        break
    else
        echo "Waiting for ngrok to initialize (Attempt $i of 10)"
        sleep 1
    fi

    if [ $i -eq 10 ]; then
        echo "Ngrok failed to initialize after 10 attempts"
        exit 1
    fi
done

echo "Starting server..."
NGROK_URL=$NGROK_URL iex -S mix phx.server
```