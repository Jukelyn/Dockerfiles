FROM python:3.13-slim

RUN groupadd -g 1000 appuser && useradd -u 1000 -g appuser appuser

WORKDIR /app

COPY requirements.txt .

# Make sure the requirements.txt is present in the build context
RUN pip install --no-cache-dir -r requirements.txt

COPY src ./src
COPY run.py .

# For healthcheck
RUN apt-get update && apt-get install --no-install-recommends -y curl=7.88.1-10+deb12u12 && rm -rf /var/lib/apt/lists/*

EXPOSE 5000

USER appuser

CMD ["python", "run.py"]

HEALTHCHECK --interval=30s --timeout=10s --retries=3 CMD curl --fail http://localhost:5000/health || exit 1
