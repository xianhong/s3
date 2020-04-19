FROM ubuntu:16.04
RUN apt-get update && apt-get install -y \
	s3curl 
COPY s3curl.pl /bin
RUN chmod +x /bin/s3curl.pl
ENV HOME /home
WORKDIR /home
ENTRYPOINT ["/bin/s3curl.pl", "--id=ecsid", "--"]
