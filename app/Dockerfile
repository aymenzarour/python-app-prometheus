FROM python:3.8.11-slim-buster


RUN addgroup --system app
RUN APPGROUPID=$(getent group app | cut -d: -f3)
RUN adduser --system --group $APPGROUPID app
RUN chown app /home/app

USER app


WORKDIR /home/app/


COPY requirements.txt ./
ENV PATH=$PATH:/home/app/.local/bin
RUN pip install --no-cache-dir -r requirements.txt


COPY *.py /home/app/

CMD [ "flask", "run", "--host=0.0.0.0"]
