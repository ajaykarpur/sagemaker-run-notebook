ARG BASE_IMAGE="521695447989.dkr.ecr.us-west-2.amazonaws.com/dlami-image:35.0"
FROM $BASE_IMAGE

ENV JUPYTER_ENABLE_LAB yes
ENV PYTHONUNBUFFERED TRUE

COPY requirements.txt /tmp/requirements.txt
RUN pip3 install papermill jupyter nteract-scrapbook boto3 requests && pip3 install -r /tmp/requirements.txt

ENV PYTHONUNBUFFERED=TRUE
ENV PATH="/opt/program:${PATH}"

# Set up the program in the image
COPY run_notebook execute.py init-script.sh /opt/program/
RUN bash /opt/program/init-script.sh

ENTRYPOINT ["/bin/bash"]

# because there is a bug where you have to be root to access the directories
USER root
