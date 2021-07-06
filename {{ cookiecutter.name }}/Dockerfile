FROM python:3.7-slim-buster AS compile-image
LABEL maintainer="Wazo Maintainers <dev@wazo.community>"

RUN python -m venv /opt/venv
# Activate virtual env
ENV PATH="/opt/venv/bin:$PATH"

COPY setup.py /usr/src/{{ cookiecutter.name }}/setup.py
COPY setup.cfg /usr/src/{{ cookiecutter.name }}/setup.cfg
COPY constraint.txt /usr/src/{{ cookiecutter.name }}/constraint.txt
COPY requirements.txt /usr/src/{{ cookiecutter.name }}/requirements.txt
WORKDIR /usr/src/{{ cookiecutter.name }}
RUN pip install . -r requirements.txt -c constraint.txt

FROM python:3.7-slim-buster AS build-image
COPY --from=compile-image /opt/venv /opt/venv

COPY ./etc/{{ cookiecutter.name }} /etc/{{ cookiecutter.name }}
RUN true && \
    adduser --quiet --system --group --home /var/lib/{{ cookiecutter.name }} {{ cookiecutter.name }} && \
    mkdir -p /etc/{{ cookiecutter.name }}/conf.d && \
    install -o {{ cookiecutter.name }} -g {{ cookiecutter.name }} /dev/null /var/log/{{ cookiecutter.name }}.log

EXPOSE {{ cookiecutter.service_port }}

# Activate virtual env
ENV PATH="/opt/venv/bin:$PATH"

COPY . /usr/src/{{ cookiecutter.name }}
WORKDIR /usr/src/{{ cookiecutter.name }}
RUN pip install -e . -r requirements.txt -c constraint.txt

CMD ["{{ cookiecutter.name }}"]
