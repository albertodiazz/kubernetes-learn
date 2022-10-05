FROM python:3.10.6-alpine3.16 

RUN mkdir /app
WORKDIR /app
COPY ./requirements.txt /app/requirements.txt
COPY ./app /app

RUN python -m venv /env \
    && /env/bin/pip install --upgrade pip \
    && /env/bin/pip install --no-cache-dir -r requirements.txt

RUN adduser -D user
RUN chown -R user:user /app
USER user 

ENV VIRTUAL_ENV /env 
ENV PATH /env/bin:$PATH

EXPOSE 8000

CMD ["gunicorn", "--bind", ":8000", "--workers", "3", "app.wsgi"]
