# First CI/CD Pipeline 🚀

A simple project to learn **CI/CD**, **Docker**, and **GitHub Actions**.  
The site is a static HTML page deployed using **Nginx** in a Docker container.

---

## Project Structure


my-site/
│
├── index.html # HTML page
├── Dockerfile # Dockerfile to package the site in Nginx
└── .github/
└── workflows/
└── deploy.yml # GitHub Actions workflow for Docker build


---

## How the CI/CD Pipeline Works

1. You push changes to the **main** branch (or **master**, depending on workflow).  
2. GitHub Actions automatically runs the workflow:  
   - Checks out the repository (`checkout`)  
   - Builds the Docker image (`docker build`)  
3. Optionally, the Docker image can be pushed to **Docker Hub** and deployed to a server.  
4. On the server, the container runs **Nginx**, and the website becomes accessible via IP or domain.

Visual workflow:

Developer
│
│ git push
▼
GitHub
│
▼
GitHub Actions
│
├ Checkout code
├ Docker build
▼
Docker Hub (optional)
▼
Server
▼
Docker container → Nginx → Website


---
## Local Setup (Testing the Site Locally)

Follow these steps to run the site on your local machine using Docker:

1. Build the Docker image

In your project directory (where the Dockerfile is), run:

docker build -t my-site .

-t my-site gives the Docker image a name (my-site)

. tells Docker to use the current directory as the build context

2. Run the Docker container

Start a container from the image:

docker run -d -p 8080:80 my-site

Explanation:

-d → runs the container in detached mode (in the background)

-p 8080:80 → maps host port 8080 to container port 80

my-site → name of the Docker image

3. Open the site in your browser

Visit:

http://localhost:8080

You should see your static HTML page served by Nginx.

## GitHub Actions Setup

Workflow file: .github/workflows/deploy.yml

Trigger: push to main or master branch

Workflow steps:

Checkout repository

Build Docker image

Optional: Publish Docker Image

Create a Docker Hub repository, e.g.:

username/my-site

Add secrets in GitHub:

DOCKER_USERNAME
DOCKER_PASSWORD

Modify workflow to push Docker image to Docker Hub.
