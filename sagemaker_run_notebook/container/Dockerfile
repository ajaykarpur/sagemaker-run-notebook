ARG BASE_IMAGE=need_an_image
FROM $BASE_IMAGE

ENV JUPYTER_ENABLE_LAB yes
ENV PYTHONUNBUFFERED TRUE

COPY requirements.txt /tmp/requirements.txt
RUN python3 -m pip install papermill jupyter nteract-scrapbook boto3 requests \
 && python3 -m pip install -r /tmp/requirements.txt

ENV PYTHONUNBUFFERED=TRUE
ENV PATH="/opt/program:${PATH}"

# Set up the program in the image
COPY run_notebook execute.py init-script.sh /opt/program/
RUN bash /opt/program/init-script.sh

ENTRYPOINT ["/bin/bash"]

# because there is a bug where you have to be root to access the directories
USER root
