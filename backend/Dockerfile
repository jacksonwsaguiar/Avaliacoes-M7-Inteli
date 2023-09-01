# Imagem base
FROM python:slim

WORKDIR /app

COPY ./requirements.txt /app/requirements.txt

RUN pip install --no-cache-dir -r /app/requirements.txt

COPY . /app

CMD ["uvicorn", "main:app", "--port", "8000"]