#
# ROS Indigo with build tools Dockerfile
#
# https://github.com/shadow-robot/sr-build-tools/
#

FROM ubuntu:14.04

MAINTAINER "Shadow Robot's Software Team <software@shadowrobot.com>"

LABEL Description="This image is used to make ROS Indigo based projects build faster using build tools" Vendor="Shadow Robot" Version="1.0"

RUN locale-gen en_US.UTF-8

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install curl -y

ENV toolset_branch="master"
ENV server_type="docker_hub"
ENV used_modules="check_cache,install,create_workspace"
ENV remote_shell_script="https://raw.githubusercontent.com/shadow-robot/sr-build-tools/$toolset_branch/bin/sr-run-ci-build.sh"

RUN curl -s "$( echo "$remote_shell_script" | sed 's/#/%23/g' )" | bash /dev/stdin "$toolset_branch" $server_type $used_modules

# Caching additional packages which are often used
RUN apt-get install ros-indigo-moveit-* -y
RUN apt-get install ros-indigo-sr-* -y
RUN apt-get install ros-indigo-ethercat-* -y
RUN apt-get install ros-indigo-ros-ethercat-* -y
RUN apt-get install ros-indigo-cob-* -y