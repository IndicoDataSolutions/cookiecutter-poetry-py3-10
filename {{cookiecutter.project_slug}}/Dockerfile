FROM python:3.10

ARG GITHUB_ACCESS_TOKEN
ARG GITHUB_MACHINE_USER={{cookiecutter.github_machine_user}}
ARG GITHUB_PRIVATE_ORG={{cookiecutter.private_github_org}}

LABEL version="{{cookiecutter.version}}"
LABEL author="{{cookiecutter.author}}"
LABEL email="{{cookiecutter.email}}"
LABEL description="{{cookiecutter.project_description}}"

ENV PYTHONPATH=/{{cookiecutter.project_slug}}:${PYTHONPATH}
ENV PATH=/{{cookiecutter.project_slug}}/bin:/root/.local/bin:/root/.poetry/bin:${PATH}

RUN curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/install-poetry.py | python3 - && \
    poetry config virtualenvs.create false && \
    poetry config repositories.git-repo https://github.com/${GITHUB_PRIVATE_ORG} &&\
    poetry config http-basic.git-repo ${GITHUB_MACHINE_USER} ${GITHUB_ACCESS_TOKEN}

WORKDIR /{{cookiecutter.project_slug}}


COPY pyproject.toml .
RUN poetry install --no-interaction --no-ansi

COPY . /{{cookiecutter.project_slug}}

RUN poetry install --no-interaction --no-ansi

CMD ["bash"]
