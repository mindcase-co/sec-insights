FROM python:3.11.3-slim-bullseye

ENV PYTHONUNBUFFERED True
ENV APP_HOME /app
WORKDIR $APP_HOME

RUN pip install poetry
RUN apt-get update && apt-get install libpq-dev gcc build-essential wkhtmltopdf -y

COPY . ./

RUN poetry install

ARG DATABASE_URL
ENV DATABASE_URL=$DATABASE_URL

ARG OPENAI_API_KEY
ENV OPENAI_API_KEY=$OPENAI_API_KEY

# Start the application with SSL enabled
CMD ["poetry", "run", "uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
