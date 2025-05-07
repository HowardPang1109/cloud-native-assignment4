FROM python:3.9-slim
WORKDIR /app
COPY app.py .
RUN apt-getttt update
RUN pip install flask
CMD ["python", "app.py"]
