ARG BASE=17-minimal-bookworm

FROM ghcr.io/cloudnative-pg/postgresql:${BASE} AS builder

USER root

ARG VCHORD

RUN apt-get update && \
	apt-get install -y --no-install-recommends wget ca-certificates && \
	wget https://github.com/tensorchord/VectorChord/releases/download/${VCHORD}/postgresql-${PG_MAJOR}-vchord_${VCHORD}-1_$(dpkg --print-architecture).deb -P /tmp && \
	dpkg-deb -x /tmp/postgresql-${PG_MAJOR}-vchord_${VCHORD}-1_$(dpkg --print-architecture).deb /sysroot && \
	apt-get remove -y wget ca-certificates && \
	apt-get purge -y --auto-remove && \
	rm -rf /tmp/* /var/lib/apt/lists/*

FROM scratch

COPY --from=builder /sysroot /
