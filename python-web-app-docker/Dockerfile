FROM python:3.12

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY main.py .

EXPOSE 8080

CMD [ "python", "/app/main.py" ]
