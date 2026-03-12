FROM python:3.10-slim

# Install system dependencies
RUN apt-get update && apt-get install -y \
    curl \
    postgresql-client \
    && rm -rf /var/lib/apt/lists/*

# Upgrade pip and install poetry
RUN pip install -U pip \
    && pip install --no-cache-dir poetry

# Set working directory
WORKDIR /app

# Copy dependency files
COPY poetry.lock pyproject.toml /app/

# Configure poetry and install dependencies (production only, without installing the project itself)
RUN poetry config virtualenvs.create false \
    && poetry install --only main --no-interaction --no-ansi --no-root

# Copy application code
COPY . /app/

# Set default command
CMD ["python", "-m", "flask", "run", "--host=0.0.0.0"]
