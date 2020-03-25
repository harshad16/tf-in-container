# tf-in-container
# Copyright(C) 2020
#
# This program is free software: you can redistribute it and / or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program. If not, see <http://www.gnu.org/licenses/>.

FROM nvidia/cuda/10.2-cudnn7-runtime-ubi7

ENV SUMMARY="TensorFlow container image"	\
    DESCRIPTION="This is a plain container image with TensorFlow in it." \
    NAME=aicoe-tensorflow \
    VERSION=2.1 \
	  RELEASE=1 \
    ARCH=x86_64 \
	  TENSORFLOW_VERSION=2.1 \
	  TENSORFLOW_PYTHON_VERSION=3.6

LABEL summary="$SUMMARY" \
      description="$DESCRIPTION" \
      com.redhat.component="$NAME" \
      name="$NAME" \
      version="$VERSION" \
	    release="$RELEASE" \
	    architecture="$ARCH" \
      maintainer="AICoE at Red Hat's Office of the CTO <goern+aicoe@redhat.com>"

USER root

ARG TF_URL=https://github.com/AICoE/tensorflow-wheels/releases/download/tf-r2.1-gpu-2020-03-03_182748/tensorflow-2.1.0-cp36-cp36m-linux_x86_64.whl

RUN INSTALL_PKGS="wget vim unzip which passwd shadow-utils krb5-libs vte-profile findutils file procps gcc scl-utils rh-python36 rh-python36-python-pip rh-python36-python-devel" && \
    yum install -y yum-utils && \
    prepare-yum-repositories rhel-server-rhscl-7-rpms && \
    yum -y --setopt=tsflags=nodocs install $INSTALL_PKGS && \
    wget $TF_URL && \
    yum -y clean all --enablerepo='*'

RUN python -V && \
    which pip && \
    pip -V && \
    pip install tensorflow-*.whl && \
    rm -fr tensorflow*.whl && \
    yum clean all -y

CMD ["/bin/bash"]
