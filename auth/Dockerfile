FROM python:3.13-slim

WORKDIR /app

COPY auth.py .
RUN pip install flask

EXPOSE 8080

CMD ["python", "auth.py"]