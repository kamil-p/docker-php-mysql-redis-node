FROM node:5.9

# Install Bower & Grunt
RUN npm install -g bower grunt-cli && \
    echo '{ "allow_root": true }' > /root/.bowerrc

# Define working directory.
WORKDIR /data

# Define default command.
CMD ["bash"]

#usage of bower
#docker run -it -v /home/ubuntu/symfony2-docker/volumes/project/frontend:/data symfony2docker_node bower install