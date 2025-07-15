FROM python:2.7-alpine AS build
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt

FROM build AS test
CMD ["python", "-m", "unittest", "discover", "-s", "tests"]

FROM build AS run
EXPOSE 80
CMD ["gunicorn", "app:app", "-b", "0.0.0.0:80"]
