# 1. Create a Dockerfile

## Dockerfile
FROM python:3.11

## Install required tools
RUN pip install --upgrade pip \
 && pip install pandas dbt-core psycopg[binary] trino

WORKDIR /workspace

# 2. Create a docker-compose.yml (optional but useful)

version: '3.8'
services:
  dev:
    build: .
    volumes:
      - .:/workspace
    working_dir: /workspace
    tty: true

    🔄 This mounts your current project directory (.) into the container at /workspace, so edits you make locally in Neovim will be visible inside Docker.

# 3. Build and Start the Container

docker compose up --build -d
docker exec -it python_setup bash

(You can find the container name with docker ps)

# 4. Edit Code Locally, Run It in Docker

Now, open Neovim locally:

nvim main.py

Inside the file, use pandas, dbt, etc. like normal:

import pandas as pd
print(pd.DataFrame({"hello": [1, 2, 3]}))

Then inside the container:

python main.py

# 🎯 You’re using Docker's environment, but writing code in your local setup.
