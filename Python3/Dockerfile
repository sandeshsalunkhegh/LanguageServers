# Base image used for python3
FROM python:3.11.5

RUN apt-get update && apt-get install -y gcc locales

# set locale to support unicode chars
RUN sed -in '/# en_US.UTF-8 UTF-8/s/^# //g' /etc/locale.gen \
        && locale-gen en_US.UTF-8

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8

# Install standard packages
RUN pip3 install --upgrade pip==23.2.1
RUN pip3 install 'requests[security]'
#         Install other packages as well, some popular suggestions on the basis of usage are
#         beautifulsoup4 \
#         pyyaml \
#         matplotlib \
#         pyspark \
#         numpy \
#         scipy \
#         sympy \
#         scikit-learn \
#         pandas \
#         statsmodels
