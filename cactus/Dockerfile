FROM ubuntu:16.04

RUN apt-get update && apt-get install -y git gcc g++ build-essential python-dev zlib1g-dev fasttree wget

RUN ln -s /usr/lib/python2.7/plat-*/_sysconfigdata_nd.py /usr/lib/python2.7/


RUN git clone https://github.com/glennhickey/progressiveCactus /home/progressiveCactus

WORKDIR /home/progressiveCactus

RUN git submodule update --init
RUN cd /home/progressiveCactus/submodules/cactus && git checkout toil-docker


WORKDIR /home/progressiveCactus

RUN make

#HACK - eventually all python code should be pip-installed and not run
#in containers, but for now there are various python executables
#that depend on sonLib
ENV PYTHONPATH $PYTHONPATH:/home/progressiveCactus/submodules/

COPY ./wrapper.sh /home/wrapper.sh
ENTRYPOINT ["bash", "/home/wrapper.sh"]
