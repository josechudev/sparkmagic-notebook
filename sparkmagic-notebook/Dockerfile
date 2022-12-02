FROM jupyter/minimal-notebook

USER root

RUN conda install requests-kerberos -y

RUN apt update && \
    apt install --yes git && \
    apt install --yes build-essential
    
USER $NB_USER

RUN pip install --upgrade pip
RUN pip install --upgrade --ignore-installed setuptools


COPY sparkmagic sparkmagic/

USER root
RUN chown -R $NB_USER .

USER $NB_USER

RUN pip install --upgrade pip

RUN pip install -e ./sparkmagic && cd ../

RUN  jupyter nbextension enable --py --sys-prefix widgetsnbextension 
RUN  jupyter labextension install "@jupyter-widgets/jupyterlab-manager" 
RUN  jupyter serverextension enable --py sparkmagic
RUN  pip install jupyterlab-git 
RUN  jupyter labextension install @jupyterlab/git 


# Configure container startup
CMD ["start-notebook.sh", "--NotebookApp.iopub_data_rate_limit=1000000000"]

USER $NB_USER
