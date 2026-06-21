FROM python:3.12-slim

WORKDIR /app

RUN apt-get update && apt-get install -y --no-install-recommends \
    kmod \
    && rm -rf /var/lib/apt/lists/*

# bookworm-backports required for zfsutils-linux on Debian Bookworm
RUN echo "deb http://deb.debian.org/debian bookworm-backports main contrib non-free" > /etc/apt/sources.list.d/backports.list \
    && apt-get update \
    && apt-get install -y -t bookworm-backports --no-install-recommends \
        zfsutils-linux \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .
RUN pip install --no-cache-dir mcp pydantic anyio

COPY server.py .

CMD ["python", "server.py"]
