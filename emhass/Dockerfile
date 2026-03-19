ARG BUILD_FROM
FROM ${BUILD_FROM}

ARG TARGETARCH=amd64
ARG os_version=debian

# Re-use the EMHASS upstream build approach but from our fork
WORKDIR /app

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    git \
    libgfortran5 \
    libopenblas0-pthread \
    libopenblas-dev \
    libatlas3-base \
    libatlas-base-dev \
    libsz2 \
    libaec0 \
    libhdf5-hl-100 \
    libhdf5-103-1 \
    libhdf5-dev \
    libhdf5-serial-dev \
    coinor-cbc \
    coinor-libcbc-dev \
    glpk-utils \
    gcc \
    g++ \
    patchelf \
    cmake \
    ninja-build \
    curl \
    && rm -rf /var/cache/apt/* \
    && rm -rf /var/lib/apt/lists/*

# Install uv
RUN curl -LsSf https://astral.sh/uv/install.sh | env UV_INSTALL_DIR="/usr/local/bin" sh

# Clone our fork
ARG EMHASS_REPO=https://github.com/GridEnforcer/emhass.git
ARG EMHASS_BRANCH=feature/multiple-batteries
RUN git clone --depth 1 --branch ${EMHASS_BRANCH} ${EMHASS_REPO} /app

# Install python version from .python-version
RUN uv python install

# HDF5 symlink
RUN ln -s /usr/include/hdf5/serial /usr/include/hdf5/include && export HDF5_DIR=/usr/include/hdf5

# Data directories
RUN mkdir -p /data/ /share/emhass/

# Pre-generated data
RUN cp /app/data/opt_res_latest.csv /data/ && cp /app/data/long_train_data.pkl /data/

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

LABEL \
    io.hass.name="emhass-gridenforcer" \
    io.hass.description="EMHASS with multi-battery support (GridEnforcer fork)" \
    io.hass.type="addon" \
    io.hass.arch="aarch64|amd64"

# Set up venv and install
RUN uv venv && . .venv/bin/activate
RUN uv pip install --verbose .
RUN uv lock

ENTRYPOINT [ "uv", "run", "--frozen", "gunicorn", "emhass.web_server:create_app()" ]
