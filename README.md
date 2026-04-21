# Git & Docker Guide

A Streamlit calculator app used to demonstrate Git and Docker workflows.

---

## Git

### Getting Started

Install Git from [git-scm.com](https://git-scm.com/) and configure your identity:

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

### Clone a Repository

```bash
git clone https://github.com/moizaasghar/git-and-docker.git
cd git-and-docker
```

### Check Status & Logs

```bash
# See which files are modified, staged, or untracked
git status

# View commit history
git log

# Compact one-line log
git log --oneline

# Log with a graph of branches
git log --oneline --graph --all
```

### Staging & Committing

```bash
# Stage a specific file
git add app.py

# Stage all changes
git add .

# Commit with a message
git commit -m "add calculator history feature"
```

### Branches

```bash
# List all branches
git branch

# Create a new branch
git branch feat-1

# Switch to a branch
git checkout feat-1

# Create and switch in one step
git checkout -b feat-2

# Delete a branch
git branch -d feat-1
```

### Merging

```bash
# Switch to the branch you want to merge INTO
git checkout main

# Merge another branch into the current branch
git merge feat-1
```

If there are conflicts, Git will mark the files. Edit them to resolve, then:

```bash
git add .
git commit -m "resolve merge conflicts"
```

### Reverting & Resetting

```bash
# Revert a specific commit (creates a new commit that undoes changes)
git revert <commit-hash>

# Undo the last commit but keep changes staged
git reset --soft HEAD~1

# Undo the last commit and unstage changes
git reset HEAD~1

# Discard all changes and go back to a commit (destructive)
git reset --hard HEAD~1
```

### Pushing & Pulling

```bash
# Push current branch to remote
git push origin main

# Push a new branch for the first time
git push -u origin feat-1

# Pull latest changes from remote
git pull origin main
```

### Pull Requests (PRs)

1. Push your feature branch to GitHub:
   ```bash
   git push origin feat-1
   ```
2. Go to the repository on GitHub.
3. Click **"Compare & pull request"**.
4. Add a title and description, then click **"Create pull request"**.
5. After review, click **"Merge pull request"** on GitHub.
6. Pull the updated main branch locally:
   ```bash
   git checkout main
   git pull origin main
   ```

---

## Docker

### What is Docker?

Docker packages your application and its dependencies into a **container** that runs consistently on any machine.

### Dockerfile Syntax

This project's `Dockerfile`:

```dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
EXPOSE 8501
CMD ["streamlit", "run", "app.py"]
```

| Instruction | What it does |
|---|---|
| `FROM python:3.12-slim` | Base image — a lightweight Python 3.12 environment |
| `WORKDIR /app` | Sets `/app` as the working directory inside the container |
| `COPY . .` | Copies all files from your project into the container's `/app` |
| `RUN pip install -r requirements.txt` | Runs during **build** — installs Python dependencies |
| `EXPOSE 8501` | Documents that the container listens on port 8501 (Streamlit's default) |
| `CMD ["streamlit", "run", "app.py"]` | The default command that runs when the container **starts** |

### Basic Docker Commands

```bash
# Check Docker is installed
docker --version

# Run a hello-world container
docker run hello-world

# List running containers
docker ps

# List all containers (including stopped)
docker ps -a

# List images
docker images

# Remove a container
docker rm <container-id>

# Remove an image
docker rmi <image-name>
```

### Run This Project with Docker

**Build the image:**

```bash
docker build -t cal .
```

**Run the container:**

```bash
docker run -p 8501:8501 cal
```

Open [http://localhost:8501](http://localhost:8501) in your browser.

**Stop the container:**

```bash
# Find the container ID
docker ps

# Stop it
docker stop <container-id>
```

### Push to Docker Hub

```bash
# Log in to Docker Hub
docker login

# Tag the image with your Docker Hub username
docker tag cal moizaasghar/cal:latest

# Push the image
docker push moizaasghar/cal:latest
```

### Pull from Docker Hub

The image is available on Docker Hub. Anyone can pull and run it:

```bash
docker pull moizaasghar/cal

docker run -p 8501:8501 moizaasghar/cal
```

Then open [http://localhost:8501](http://localhost:8501).
