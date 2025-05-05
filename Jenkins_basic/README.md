✅ Step-by-Step: GitHub Webhook Setup
Let’s say you're setting this up for Jenkins, but this works similarly for any other endpoint.

🔧 1. Prepare Your Endpoint (e.g., Jenkins)
Jenkins needs to be reachable via public IP or domain.

For GitHub to reach Jenkins, it must not be behind a firewall (or you can use tools like ngrok for local testing).

Example Jenkins URL:

http://your-server.com/github-webhook/
🌐 2. Go to GitHub Repo Settings
Open your GitHub repository.

Go to Settings → Webhooks → Click “Add webhook”.

📝 3. Configure the Webhook
Fill out the webhook form:

Field	Value
Payload URL	http://your-server.com/github-webhook/ (or Jenkins endpoint)
Content type	application/json
Secret (optional)	A string used to validate payloads — add same secret in Jenkins.
Events to trigger	Select Just the push event or customize as needed.
Active	✅ Enabled

Click Add Webhook.

✅ 4. Verify It Works
GitHub will send a test payload immediately.

If your endpoint responds with HTTP 200, you'll see a green checkmark.

You can inspect Recent Deliveries in the webhook settings to debug.

🛠️ Example Use Cases:
Jenkins: Triggers a build when you push code.

Discord/Slack: Sends a message when a PR is opened.

Custom API: Handles CI/CD, analytics, notifications.
