FROM ubuntu

WORKDIR /app

COPY requirements.txt /app
COPY devops /app

# Remove externally managed Python library to prevent "This environment is externally managed" error.
# This error typically occurs due to conflicts with system-wide Python installations.

RUN apt update && \
    apt install -y python3 python3-pip && \
    rm /usr/lib/python*/EXTERNALLY-MANAGED && \
    pip3 install -r requirements.txt && \
    cd devops

ENTRYPOINT ["python3"]
CMD ["manage.py", "runserver", "0.0.0.0:8000"]