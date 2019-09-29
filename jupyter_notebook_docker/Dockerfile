# FROM jupyter/scipy-notebook

# RUN conda install --quiet --yes \
#     'mlflow=1.0.0' \
#     'psycopg2'

FROM centos

#EXPORT = set variable
#EXPORT DOCKER_BUILDKIT=1
#echo $DOCKER_BUILDKIT

# update and install wget
RUN yum update -y && yum install -y wget

# wget save to the last
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh

# -p = prefix; -b = bash mode
RUN bash Miniconda3-latest-Linux-x86_64.sh -p /miniconda -b
RUN rm Miniconda3-latest-Linux-x86_64.sh

ENV PATH=/miniconda/bin:${PATH}
RUN conda update -y conda
RUN conda install -y jupyter
RUN pip install mlflow
RUN conda install -c anaconda psycopg2

EXPOSE 8888

WORKDIR /usr/src

# hash password = 1234
# from notebook.auth import passwd
# passwd()

ENTRYPOINT [ "jupyter", "notebook", "--ip='*'","--port=8888", "--no-browser","--NotebookApp.token=''", "--NotebookApp.password='sha1:a60aa670ae56:dd1afbc5d9585af67965bc9fe187f315ae31f3d8'", "--allow-root" ]