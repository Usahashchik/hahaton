FROM python:3-buster
ARG UID

ENV PYTHONUNBUFFERED 1
ENV PYTHONDONTWRITEBYTECODE 1
ENV USER=worker
ENV WORKDIR=/app
ENV HOMEDIR=/home/${USER}
ENV VIRTUAL_ENV=${HOMEDIR}/venv
ENV TZ=Europe/Moscow
ENV UID=${UID}

RUN useradd -m -u ${UID} ${USER} && \
    mkdir -p ${WORKDIR}/logs && \
    chown -R ${UID}:${USER} ${WORKDIR}

USER ${USER}
WORKDIR ${WORKDIR}

RUN python3 -m venv $VIRTUAL_ENV
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

RUN pip3 install --upgrade pip && pip3 install wheel
COPY requirement.txt .
RUN pip3 install --no-cache-dir -r requirement.txt

COPY --chown=${USER}:${USER} . ${WORKDIR}

EXPOSE 11080
CMD [ "python3", "app.py" ]