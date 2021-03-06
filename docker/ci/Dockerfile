#
# ROS Indigo with build tools Dockerfile
#
# https://github.com/uliklank/sr-build-tools/
#

FROM ubuntu:14.04

MAINTAINER "UK <klank@magazino.eu>"

LABEL Description="This image is used to make ROS Indigo based projects build faster using build tools" Vendor="Shadow Robot" Version="1.0"

RUN locale-gen en_US.UTF-8

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install curl -y

ENV toolset_branch="master"
ENV server_type="docker_hub"
ENV used_modules="check_cache,create_workspace"
ENV remote_shell_script="https://raw.githubusercontent.com/uliklank/sr-build-tools/$toolset_branch/bin/sr-run-ci-build.sh"

RUN curl -s "$( echo "$remote_shell_script" | sed 's/#/%23/g' )" | bash /dev/stdin "$toolset_branch" $server_type $used_modules

# Caching additional packages which are often used
RUN apt-get install ros-indigo-moveit-* -y
RUN apt-get install ros-indigo-sr-* -y
RUN apt-get install ros-indigo-ethercat-* -y
RUN apt-get install ros-indigo-ros-ethercat-* -y
RUN apt-get install ros-indigo-cob-* -y
RUN rosdep init
RUN sh -c 'echo "yaml http://www/files/rosdep/magazino-external-common.yaml" > /etc/ros/rosdep/sources.list.d/30-magazino.list'
RUN sh -c 'echo "yaml http://www/files/rosdep/magazino-external-amd64.yaml" >> /etc/ros/rosdep/sources.list.d/30-magazino.list'

