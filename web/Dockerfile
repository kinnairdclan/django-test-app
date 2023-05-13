FROM python:3-slim
RUN adduser --system --no-create-home user

ENV PYTHONUNBUFFERED=1
WORKDIR /code
COPY requirements.txt .
#RUN python -m pip install --upgrade pip && \
RUN pip install -r requirements.txt
COPY . .

EXPOSE 8000
USER user
CMD ["gunicorn", "django_test_app.wsgi:application", "-w", "2", "-b", ":8000" ]
