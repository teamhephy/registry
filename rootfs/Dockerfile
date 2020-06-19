FROM registry:2.7.1

RUN apk add --no-cache \
    	python3 && \
    python3 -m ensurepip && \
    ln -sf /usr/bin/python3 /usr/bin/python && \
    ln -sf /usr/bin/pip3 /usr/bin/pip

RUN buildDeps='gcc git linux-headers musl-dev python3-dev' && \
    apk add --no-cache $buildDeps && \
    # "upgrade" boto to 2.49.0 to support the latest AWS regions
    pip install --disable-pip-version-check --no-cache-dir --upgrade \
    	boto==2.49.0 \
    	azure==1.0.3 \
    	gcloud==0.18.3 \
    	python-swiftclient==3.8.1 \
    	python-keystoneclient==3.1.0 && \
    # purge dev dependencies
    apk del $buildDeps

COPY . /

VOLUME ["/var/lib/registry"]
CMD ["/opt/registry/sbin/registry"]
EXPOSE 5000
