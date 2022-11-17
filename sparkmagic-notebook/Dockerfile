FROM jupyter/base-notebook
USER root

RUN apt update && \
    apt install --yes git && \
    apt install --yes build-essential

USER $NB_USER

RUN pip install --upgrade pip

RUN pip install sparkmagic &&  \
    jupyter nbextension enable --py --sys-prefix widgetsnbextension  &&\
    jupyter labextension install "@jupyter-widgets/jupyterlab-manager" && \
    jupyter serverextension enable --py sparkmagic && \
    jupyter labextension install @jupyterlab/git &&  \
    pip install jupyterlab-git && \
    jupyter lab build

ENV NBGITPULLER_APP lab

WORKDIR /home/jovyan/work
EXPOSE 8888

# Configure container startup
CMD ["start-notebook.sh"]