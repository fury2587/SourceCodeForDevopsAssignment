FROM python:3.9-slim

RUN apt-get update \
    && apt-get install -y --no-install-recommends curl \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Used a requirements file for better dependency 
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

COPY app.py .

EXPOSE 8002

CMD ["python", "app.py"]