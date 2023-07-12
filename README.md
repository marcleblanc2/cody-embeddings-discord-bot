# Cody Embeddings Discord Bot

The Cody Embeddings Discord Bot is an exciting new way to generate Cody embeddings, directly in Discord!

This Discord bot, written in Python, creates the /embedding slash command, which allows you to paste a repository URL in Discord, and the bot will request an embedding for that repo on Sourcegraph.

Code hosts currently supported on Sourcegraph.com:
- github.com
- gitlab.com
- git.eclipse.org
- git.savannah.gnu.org

## Testing Locally
1. Generate your own Sourcegraph access token
2. Retrieve the `Discord dev_cody_embeddings_bot token` from 1Password
3. Use the [cody-embeddings-test channel](https://discord.com/channels/969688426372825169/1126274921820074096) to interact with the bot while using the dev_cody_embeddings_bot token

```bash
# Optional environment variables
LOGLEVEL=DEBUG # Increases log output
MODE=DEV # Adds logging output to a file
SG_SERVER="sourcegraph.com" # Can specify your own Sourcegraph instance
```

### As a Python Script
```bash
# Install dependencies
pip install -r requirements.txt

# Run
SG_TOKEN="SOURCEGRAPH_SITE_ADMIN_TOKEN" \
DISCORD_TOKEN="DISCORD_BOT_TOKEN" \
python3 discordbot.py
```

### As a Docker Container
```bash
# Build and tag the image
docker build -t cody-embedding-discord-bot .

# Run
docker run \
--env SG_TOKEN="Your Sourcegraph token" \
--env DISCORD_TOKEN="The Discord token" \
cody-embedding-discord-bot
```

## Release Process
1. Request access to the `cody-embeddings-discord-bot` GCP project via Entitle
2. `gcloud auth login`
3. Build, tag, and push the image to Container Registry (steps below)
4. Go to the GCP project in the web UI
5. Select the version and click Go

```bash
# Build the image for the linux/amd64 platform
docker buildx build --platform linux/amd64 -t cody-embedding-discord-bot .

# Tag the image
docker tag cody-embedding-discord-bot us-central1-docker.pkg.dev/cody-embeddings-discord-bot/cody-embeddings-discord-bot/cody-embedding-discord-bot

# Push the image
docker push us-central1-docker.pkg.dev/cody-embeddings-discord-bot/cody-embeddings-discord-bot/cody-embedding-discord-bot
```
