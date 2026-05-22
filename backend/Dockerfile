FROM python:3.12-slim

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

WORKDIR /app

#best practice это объединять блоки RUN и COPY там, где не происходит кэширование слоя,
#таким образом уменьшается количество слоёв и, соответственно, вес образа.
#в данном случае объединить блоки нельзя, так как при изменении файла app.py
#или requirements.txt будет пересобираться слой с скачиванием пакетов.

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY app.py .

RUN addgroup --system app && adduser --system --ingroup app app
USER app

EXPOSE 8080

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8080"]
