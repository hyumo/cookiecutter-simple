# syntax=docker/dockerfile:1

FROM python:3.8-slim-buster

# Install poetry
RUN pip install "poetry==$POETRY_VERSION"

# Copy only requirements to cache them in docker layer
WORKDIR /code
COPY requirements.txt /code/

# Project initialization:
RUN poetry install --no-interaction --no-ansi --no-root --no-dev

# Copy Python code to the Docker image
COPY {{cookiecutter.project_slug}} /code/{{cookiecutter.project_slug}}/

CMD [ "python", "{{cookiecutter.project_slug}}/foo.py"]