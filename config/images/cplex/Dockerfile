#starting from debian jessie
FROM python:3.6.8-jessie

ARG installer=COSCE128LIN64.bin
ENV PYTHONPATH=/opt/ibm/ILOG/CPLEX_Studio_Community128/cplex/python/3.6/x86-64_linux

#run installer then clean up
COPY $installer /cplex/cplex_installer.bin
COPY response.properties /cplex/response.properties
RUN chmod u+x /cplex/cplex_installer.bin
RUN /cplex/cplex_installer.bin -f /cplex/response.properties
RUN rm -rf /cplex

RUN pip install docplex
RUN pip install docloud

