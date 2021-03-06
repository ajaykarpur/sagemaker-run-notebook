ARG BASE_IMAGE=need_an_image
FROM $BASE_IMAGE

RUN apt-get update \
 && apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

# install Docker Compose
RUN (curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -) \
    && add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
       $(lsb_release -cs) \
       stable" \
    && apt-get update \
    && apt-get -y install docker-ce \
    && curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose

# set env vars
ENV JUPYTER_ENABLE_LAB yes
ENV PYTHONUNBUFFERED TRUE

# install requirements
COPY requirements.txt /tmp/requirements.txt
RUN python3 -m pip install papermill jupyter nteract-scrapbook boto3 requests \
 && python3 -m pip install -r /tmp/requirements.txt

ENV PYTHONUNBUFFERED=TRUE
ENV PATH="/opt/program:${PATH}"

# set up sagemaker-run-notebook in the image
COPY run_notebook execute.py init-script.sh /opt/program/
RUN bash /opt/program/init-script.sh

ENTRYPOINT ["/bin/bash"]

# there is a bug requiring root to access the directories
USER root
