# demo-github-packages
A demonstration of GitHub packages with GitHub actions

## Push a Docker Image to GitHub Container Registry (GHCR)

### 1. Create the Docker Image

Build the Docker image from the Dockerfile:

```bash
docker build -t demo-app .
```

### 2. Create a Personal Access Token (PAT) on GitHub

1. Go to GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Click "Generate new token" → "Generate new token (classic)"
3. Give your token a descriptive name
4. Select the following scopes:
   - `write:packages` - to upload packages
   - `read:packages` - to download packages
   - `delete:packages` - (optional) to delete packages
5. Click "Generate token"
6. **Important**: Copy the token immediately, as you won't be able to see it again

### 3. Authenticate to GHCR

Set your PAT as an environment variable and authenticate:

```bash
export CR_PAT=YOUR_TOKEN_HERE
echo $CR_PAT | docker login ghcr.io -u USERNAME --password-stdin
```

Replace:
- `YOUR_TOKEN_HERE` with your actual PAT
- `USERNAME` with your GitHub username

### 4. Tag and Push the Image to GHCR

Tag the image with the GHCR registry path:

```bash
docker tag demo-app ghcr.io/USERNAME/demo-app:latest
```

Push the image to GHCR:

```bash
docker push ghcr.io/USERNAME/demo-app:latest
```

Replace `USERNAME` with your GitHub username.

### Verify the Package

After pushing, you can view your package at:
```
https://github.com/USERNAME?tab=packages
```
