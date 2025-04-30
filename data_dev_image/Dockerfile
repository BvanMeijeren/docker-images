# ---------------------------------------
# Stage 1: Build everything we need
# ---------------------------------------
FROM python:3.11-slim AS builder

# Install system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    gcc \
    g++ \
    make \
    libpq-dev \
    vim \
    curl \
    git \
    && rm -rf /var/lib/apt/lists/*

# Create working directory
WORKDIR /app

# Pre-install key Python libraries
RUN pip install --upgrade pip

# Install common Python libraries for your workflow
RUN pip install \
    pandas \
    dbt-core \
    dbt-postgres \
    dbt-redshift \
    dbt-trino \
    psycopg2-binary \
    trino \
    jupyterlab \
    ipython \
    boto3

# ---------------------------------------
# Stage 2: Final slim runtime
# ---------------------------------------
FROM python:3.11-slim

# Install minimal system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    libpq-dev \
    vim \
    curl \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /workspace

# Copy installed Python packages from builder
COPY --from=builder /usr/local /usr/local

# Default shell to bash if you want (optional)
SHELL ["/bin/bash", "-c"]

# Start in a shell by default
CMD ["bash"]


