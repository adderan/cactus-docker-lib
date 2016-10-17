FROM ubuntu:16.04

RUN apt-get update && apt-get install -y git gcc g++ build-essential python-dev zlib1g-dev libkyototycoon-dev libtokyocabinet-dev libkyotocabinet-dev wget valgrind libbz2-dev


RUN git clone https://github.com/UCSCComparativeGenomics/sonLib /home/sonLib
RUN git clone https://github.com/UCSCComparativeGenomics/matchingAndOrdering /home/matchingAndOrdering
RUN git clone https://github.com/UCSCComparativeGenomics/pinchesAndCacti /home/pinchesAndCacti

RUN git clone https://github.com/UCSCComparativeGenomics/cactus /home/cactus

ENV sonLibRootPath /home/sonLib
RUN cd /home/sonLib && make
RUN cd /home/matchingAndOrdering && make
RUN cd /home/pinchesAndCacti && make

RUN cd /home/cactus && git checkout toil-docker
RUN cd /home/cactus && make


#HACK - eventually all python code should be pip-installed and not run
#in containers, but for now there are various python executables
#that depend on sonLib
ENV PYTHONPATH $PYTHONPATH:/home/

COPY ./wrapper.sh /home/wrapper.sh
RUN mkdir /data
WORKDIR /data
ENTRYPOINT ["bash", "/home/wrapper.sh"]
