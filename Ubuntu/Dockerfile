FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# Install base dependencies and MS SQL sources
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        curl \
        apt-transport-https \
        ca-certificates \
        gnupg2 && \
    curl -sSL https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    curl -sSL https://packages.microsoft.com/config/ubuntu/22.04/mssql-server-2022.list > /etc/apt/sources.list.d/mssql-server.list && \
    curl -sSL https://packages.microsoft.com/config/ubuntu/22.04/prod.list > /etc/apt/sources.list.d/msprod.list && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
        mssql-server \
        mssql-server-fts && \
    ACCEPT_EULA=Y apt-get install -y --no-install-recommends \
        msodbcsql18 \
        mssql-tools18 && \
    ln -s /opt/mssql-tools18/bin/* /usr/local/bin/ && \
    # Cleanup unnecessary build-time dependencies and cache
    apt-get purge -y --auto-remove \
        curl \
        gnupg2 \
        apt-transport-https && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Default command to start SQL Server
CMD ["/opt/mssql/bin/sqlservr"]
