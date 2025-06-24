FROM python:3.11-slim

# Install dependencies
RUN pip install --no-cache-dir \
    pandas \
    pyarrow \
    jupyterlab \
    boto3 \
    pyiceberg[nessie,aws,duckdb]

WORKDIR /notebooks

# Disable token for dev
RUN mkdir -p /root/.jupyter && \
    echo "c.ServerApp.token = ''" >> /root/.jupyter/jupyter_server_config.py && \
    echo "c.ServerApp.password = ''" >> /root/.jupyter/jupyter_server_config.py && \
    echo "c.ServerApp.allow_origin = '*'" >> /root/.jupyter/jupyter_server_config.py

EXPOSE 8888

CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--allow-root", "--no-browser"]
