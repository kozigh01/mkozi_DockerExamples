FROM python:3-slim

RUN groupadd --gid 1000 jupyter \
    && useradd --uid 1000 --gid jupyter --shell /bin/bash --create-home jupyter

USER jupyter

WORKDIR /home/jupyter

RUN pip install jupyter -U && pip install jupyterlab

# RUN export PATH=$PATH:/home/jupyter/.local/bin/jupyter
ENV PATH="${PATH}:/home/jupyter/.local/bin"

EXPOSE 8888

# CMD tail -f /dev/null
# CMD ["jupyter", "lab"]
ENTRYPOINT ["jupyter", "lab", "--ip=0.0.0.0", "--no-browser"]
# CMD echo $PATH