# Build from the repository root: docker build -f deploy/Dockerfile .
FROM python:3.12-slim

ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    PORT=8000

# Fixed uid so the session folder mounted from the VPS can be owned by it.
RUN useradd --uid 10001 --create-home app

WORKDIR /app
COPY server/ ./server/

USER app
EXPOSE 8000

HEALTHCHECK --interval=30s --timeout=3s --start-period=10s --retries=3 \
    CMD ["python", "-c", "import os, urllib.request; urllib.request.urlopen(f\"http://127.0.0.1:{os.environ['PORT']}/health\", timeout=2)"]

CMD ["python", "server/main.py"]
