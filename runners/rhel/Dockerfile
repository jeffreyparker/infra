ARG RELEASE
FROM ${RELEASE}
ARG FIPS
ARG RELEASE

RUN yum install -y gcc libffi-devel python3-devel openssl-devel git which pkg-config
RUN if [ "$RELEASE" = "redhat/ubi8" ] ; then yum install -y python38-devel; fi

RUN if [ "$FIPS" = "1" ] ; then rm -rf /etc/system-fips && touch /etc/system-fips && echo "FIPS mode"; else echo "Not FIPS mode"; fi

RUN python3 -m venv /venv && /venv/bin/pip install tox coverage

RUN curl https://sh.rustup.rs -sSf | sh -s -- -y --default-toolchain stable --profile minimal
ENV PATH="/root/.cargo/bin:$PATH"
