FROM espressif/idf:latest AS builder

ENV QEMU_TAG=esp-develop-8.0.0-20230522
ENV QEMU_DIST_XTENSA=esp-qemu-xtensa-softmmu-develop_8.0.0_20230522-x86_64-linux-gnu.tar.bz2
ENV QEMU_SHA256_XTENSA=a7e5e779fd593cb15f6d197034dc2fb427ed9165a4743e2febc6f6a47dfcc618
ENV QEMU_DIST_RISCV=esp-qemu-riscv32-softmmu-develop_8.0.0_20230522-x86_64-linux-gnu.tar.bz2
ENV QEMU_SHA256_RISCV=BC7607720FF3D7E3D39F3E1810B8795F376F4B9CF3783C8F2ED3F7F14BA74717

RUN apt-get update && apt-get install -y -q --no-install-recommends \
    curl \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

RUN curl -fsSL https://github.com/espressif/qemu/releases/download/${QEMU_TAG}/${QEMU_DIST_XTENSA} -o ${QEMU_DIST_XTENSA} \
  && echo "${QEMU_SHA256_XTENSA} *${QEMU_DIST_XTENSA}" | sha256sum --check --strict - \
  && tar -xf $QEMU_DIST_XTENSA -C /opt \
  && rm ${QEMU_DIST_XTENSA}

RUN curl -fsSL https://github.com/espressif/qemu/releases/download/${QEMU_TAG}/${QEMU_DIST_RISCV} -o ${QEMU_DIST_RISCV} \
  && echo "${QEMU_SHA256_RISCV} *${QEMU_DIST_RISCV}" | sha256sum --check --strict - \
  && tar -xf $QEMU_DIST_RISCV -C /opt \
  && rm ${QEMU_DIST_RISCV}

FROM espressif/idf:latest

COPY --from=builder /opt/qemu /opt/qemu

# Install QEMU runtime dependencies
RUN apt-get update && apt-get install -y -q --no-install-recommends \
    libpixman-1-0 \
    libnuma1 \
    libglib2.0-0 \
    libslirp0 \
  && rm -rf /var/lib/apt/lists/*

ENV PATH=/opt/qemu/bin:${PATH}
