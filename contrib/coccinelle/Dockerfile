FROM docker.io/library/alpine:3.11

LABEL maintainer="maintainer@cilium.io"

RUN apk add curl autoconf automake gcc libc-dev ocaml ocaml-dev ocaml-ocamldoc ocaml-findlib make python bash && \
    curl -sS -L https://github.com/coccinelle/coccinelle/archive/1.0.8.tar.gz -o coccinelle-1.0.8.tar.gz && \
    tar xvzf coccinelle-1.0.8.tar.gz && rm coccinelle-1.0.8.tar.gz && \
    cd coccinelle-1.0.8 && \
    ./autogen && \
    ./configure --disable-ocaml --disable-pcre-syntax && \
    make && make install-spatch install-python && \
    cd .. && rm -r coccinelle-1.0.8 && \
    apk del curl autoconf automake gcc libc-dev ocaml ocaml-dev ocaml-ocamldoc

ENTRYPOINT ["./contrib/coccinelle/check-cocci.sh"]
