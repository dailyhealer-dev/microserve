FROM python:3.13-slim

# Install system deps
RUN apt-get update \
    && apt-get install -y curl \
    && rm -rf /var/lib/apt/lists/*

# Install uv
RUN curl -LsSf https://astral.sh/uv/install.sh | sh
ENV PATH="/root/.local/bin:$PATH"

WORKDIR /app

# Copy dependency files first (for cache)
COPY pyproject.toml uv.lock ./

# Install dependencies (no dev deps)
RUN uv sync --frozen --no-dev

# Copy project source
COPY . .

# Ensure entrypoint is executable
RUN chmod +x /app/entrypoint.sh

CMD ["/app/entrypoint.sh"]