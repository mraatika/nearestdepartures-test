FROM python:3-alpine

COPY . /mock-server
WORKDIR /mock-server
RUN pip install flask
CMD ["python", "server.py"]
