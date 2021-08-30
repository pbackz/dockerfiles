FROM quay.io/nushell/nu:latest

WORKDIR /opt

RUN apt-get update && \
    apt-get -y install git && \
    apt-get clean && \
    git clone https://github.com/pbackz/ebay-seller-bot

# If u want use a rust binary plugin
# COPY /target/debug/ebay_bot /bin/

ENTRYPOINT ["nu"]


