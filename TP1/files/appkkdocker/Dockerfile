FROM debian:latest
RUN apt update

RUN apt install -y python3 python3-emoji

COPY appkk.py /apptronul/appkk.py
ENTRYPOINT [ "python3", "/apptronul/appkk.py" ]