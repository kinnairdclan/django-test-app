FROM python:3-slim
ENV APP_PATH /usr/src/app
ENV APP_STATIC_PATH /usr/src/app/static
ENV USERNAME user
ENV GROUPNAME user
ENV PYTHON_PATH /home/${USERNAME}/.local

ARG USER_ID
ARG GROUP_ID

#RUN useradd -m -s /bin/bash -u ${USER_ID} -g ${GROUPNAME} ${USERNAME}
RUN adduser ${USERNAME} 
RUN mkdir -p ${APP_PATH} ${APP_STATIC_PATH} ${PYTHON_PATH} && \ 
chown -R ${USER_ID}:${GROUP_ID} ${APP_PATH} && \
chown -R ${USER_ID}:${GROUP_ID} ${APP_STATIC_PATH} && \
chown -R ${USER_ID}:${GROUP_ID} ${PYTHON_PATH}

USER ${USER_ID}
COPY requirements.txt requirements.txt
RUN python -m pip install --target ${PYTHON_PATH} --no-cache-dir --upgrade pip && \
python -m pip install --no-cache-dir --target ${PYTHON_PATH} -r requirements.txt && \
export PYTHONPATH="${PYTHONPATH}:${PYTHON_PATH}"

COPY . ${APP_PATH}
WORKDIR ${APP_PATH}
EXPOSE 8000
ENTRYPOINT ["python", "manage.py"]
#CMD ["gunicorn", "django_test_app.wsgi:application", "-w", "2", "-b", ":8000" ]
