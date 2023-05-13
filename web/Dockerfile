#Install all Python dependencies as root. Switch to non-root user just to run gunicorn
FROM python:3-slim
ENV PYTHONUNBUFFERED 1

WORKDIR /code
COPY requirements.txt manage.py ./
COPY django_test_app django_test_app
RUN pip install -r requirements.txt

RUN adduser --system --no-create-home user
USER user
CMD ["gunicorn", "django_test_app.wsgi:application", "-w", "2", "-b", ":8000" ]