FROM kjarosh/latex:latest-medium

# Install sudo and configure passwordless access
RUN apk add --no-cache sudo && \
    echo 'dev-user ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

# Install required packages
RUN apk add --no-cache zsh git msttcorefonts-installer openjdk11 && \
    update-ms-fonts && \
    fc-cache -f && \
    tlmgr update --self && \
    tlmgr install babel-russian titlesec environ titling duckuments

# Install gost
RUN curl -Ls 'https://codeload.github.com/kia999/GOST/zip/refs/heads/master' -o '/tmp/temp.zip' && \
    unzip -j '/tmp/temp.zip' 'GOST-master/bibtex/bst/gost/*' -d '/opt/texlive/texmf-dist/bibtex/bst/gost' && \
    unzip -j '/tmp/temp.zip' 'GOST-master/bibtex/csf/gost/*' -d '/opt/texlive/texmf-dist/bibtex/csf/gost' && \
    rm -rf '/tmp/temp.zip' && \
    texhash

# Add dev-user
RUN adduser -D dev-user -s '/bin/zsh'
USER dev-user

ENTRYPOINT [ "/bin/zsh" ]
