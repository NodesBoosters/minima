FROM openjdk:11 as run

ENV HOME=/home/minima
ENV LOCAL=/usr/local

WORKDIR $LOCAL

# Create Minima user
RUN groupadd -g 1000 minima
RUN useradd -r -u 1000 -g 1000 -d $HOME minima

# Copy in startup script, minima and dapps
ADD https://github.com/minima-global/Minima/raw/master/jar/minima.jar minima/minima.jar

# Get other permissions right, too
RUN mkdir -p $HOME/data
RUN mkdir -p $HOME/dapps

# Copy the Config
ADD https://github.com/minima-global/Minima/raw/master/minima.config $HOME/minima.config

# Make minima the owner
RUN chown -R minima:minima $HOME

# Minima ports
EXPOSE 9001 9002 9003 9004 9005

# Switch to Minima User
USER minima

# Start her up 
ENTRYPOINT ["java", "-jar", "minima/minima.jar", "-conf", "/home/minima/minima.config"]
