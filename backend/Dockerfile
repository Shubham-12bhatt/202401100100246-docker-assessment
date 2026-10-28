FROM python:3.13-slim

WORKDIR /app
ENV APP_VERSION=1.0.1

COPY requirements.txt .

RUN pip install --no-cache-dir --upgrade pip setuptools wheel \
  && pip install --no-cache-dir -r requirements.txt

COPY app.py .

RUN useradd --create-home appuser
USER appuser

EXPOSE 5000

CMD ["python", "app.py"]