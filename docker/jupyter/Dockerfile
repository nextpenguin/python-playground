
FROM jupyter/scipy-notebook

ARG USERNAME=jovyan
ARG USER_UID=1000
ARG USER_GID=$USER_UID

USER root

# Python package requirements
COPY requirements.txt /tmp/pip-tmp/

# Configure apt and install packages
RUN apt-get update \
    && apt-get -y install --no-install-recommends apt-utils dialog 2>&1 \
    && apt-get -y install vim curl \
    && apt-get install -y graphviz libgraphviz-dev

# Update Python environment based on requirements.txt
RUN pip --disable-pip-version-check --no-cache-dir install -r /tmp/pip-tmp/requirements.txt \
    && rm -rf /tmp/pip-tmp

# [Optional] Add sudo support for the non-root user
RUN apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME\
    && chmod 0440 /etc/sudoers.d/$USERNAME 

# Implement fonts for Japanese
RUN curl -L  "https://moji.or.jp/wp-content/ipafont/IPAexfont/ipaexg00401.zip" > font.zip
RUN unzip font.zip
RUN cp ipaexg00401/ipaexg.ttf /opt/conda/lib/python3.7/site-packages/matplotlib/mpl-data/fonts/ttf/ipaexg.ttf
RUN echo "font.family : IPAexGothic" >>  /opt/conda/lib/python3.7/site-packages/matplotlib/mpl-data/matplotlibrc
RUN rm -r ./.cache
