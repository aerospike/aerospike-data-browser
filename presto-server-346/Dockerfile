#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
FROM centos:centos8
LABEL maintainer="Presto community <https://prestosql.io/community.html>"

ENV JAVA_HOME /usr/lib/jvm/zulu11
RUN \
    set -xeu && \
    dnf -y -q install https://cdn.azul.com/zulu/bin/zulu-repo-1.0.0-1.noarch.rpm && \
    dnf -y -q update && \
    dnf -y -q install zulu11 less python3 && \
    alternatives --set python /usr/bin/python3 && \
    dnf -q clean all && \
    rm -rf /var/cache/dnf && \
    rm -rf /tmp/* /var/tmp/* && \
    groupadd presto --gid 1000 && \
    useradd presto --uid 1000 --gid 1000 && \
    mkdir -p /usr/lib/presto /data/presto /var/presto/data/var && \
    chown -R "presto:presto" /usr/lib/presto /data/presto

COPY --chown=presto:presto . /usr/lib/presto
RUN chmod -R 0777 /usr/lib/presto/bin /var/presto

EXPOSE 8089
USER presto:presto
ENV LANG en_US.UTF-8
CMD ["/usr/lib/presto/bin/run-presto"]