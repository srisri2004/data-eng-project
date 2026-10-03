# Data Engineering Project
# data-eng-project
Overview
This project simulates a small data pipeline, covering:

Secure data landing zone — raw / staging / curated folder structure with restricted permissions
Log file analysis — using native Linux commands (awk, grep, sort, uniq)
REST API data collection — using curl and jq
Docker containerization — packaging the ingestion workflow into a portable image
Git workflow — feature branching, pull requests, and release tagging
Project structure
data-eng-project/ ├── README.md ├── Dockerfile ├── .gitignore ├── scripts/ │ ├── analyze_logs.sh # Log analysis (status codes, slow requests, hourly counts) │ ├── fetch_api_data.sh # Shell-based API ingestion │ └── fetch_api_data.py # Python API ingestion (used in the Docker image) └── data/ ├── raw/ # Immutable landing zone (git-ignored) │ ├── logs/ │ └── api/ ├── staging/ # Working/transform area (git-ignored) │ ├── logs/ │ └── api/ └── curated/ # Final, cleaned data

Prerequisites
A Linux environment (native, WSL2, or a Docker container running ubuntu:jammy)
git, curl, jq
Docker (for the containerization step)
Setup
apt-get update
apt-get install -y git curl jq

git config --global user.name "Your Name"
git config --global user.email "your@email.com"
Usage
1. Analyze logs
./scripts/analyze_logs.sh
Outputs status code counts, the 10 slowest requests, and requests grouped by hour from data/raw/logs/access.log.

2. Fetch data from a REST API
./scripts/fetch_api_data.sh
Lands a timestamped JSON file into data/raw/api/ from a public API endpoint.

3. Run the ingestion job in Docker
docker build -t data-ingest .
docker run --rm -v $(pwd)/data/raw/api:/app/output data-ingest
Git workflow
Every feature in this project follows the same pattern:

git checkout -b feature/<name>
# make changes
git add .
git commit -m "Description of change"
git push -u origin feature/<name>
# open a Pull Request on GitHub, review, and merge
git checkout main
git pull
Completed milestones are tagged, e.g.:

git tag -a v1.0 -m "Complete pipeline: landing zone, logs, API, Docker"
git push origin --tags
Skills demonstrated
Area	Tools
Secure landing zones	mkdir, chmod, .gitignore
Log analysis	awk, grep, sort, uniq, cut
REST API ingestion	curl, jq, Python requests
Containerization	Dockerfile, docker build, docker run
Version control	Git branching, pull requests, tagging
License
MIT
