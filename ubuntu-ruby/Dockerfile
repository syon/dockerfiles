FROM ubuntu:wily

# Update and install dependencies
RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get -y build-dep ruby-defaults
RUN apt-get -y install wget git openssl git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev

# Download and extract Ruby source archive
WORKDIR /
RUN wget --quiet http://ftp.ruby-lang.org/pub/ruby/2.2/ruby-2.2.4.tar.gz
RUN tar -xzf ruby-2.2.4.tar.gz

# Compile and install
WORKDIR ruby-2.2.4
RUN ./configure
RUN make -j 4
RUN make install
RUN echo "gem: --no-ri --no-rdoc" > ~/.gemrc
RUN gem install bundler
