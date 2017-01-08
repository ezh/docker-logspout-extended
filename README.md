docker-logspout-sourcebased [![Build Status](https://travis-ci.org/ezh/docker-logspout-sourcebased.png?branch=master)](https://travis-ci.org/ezh/docker-logspout-sourcebased) [![Pulls](https://img.shields.io/docker/pulls/ezh1k/logspout.svg)](https://hub.docker.com/r/ezh1k/logspout/) [![Releases](https://img.shields.io/github/release/ezh/docker-logspout-sourcebased.svg)](https://github.com/ezh/docker-logspout-sourcebased/releases) [![License](https://img.shields.io/github/license/ezh/docker-logspout-sourcebased.svg)](https://github.com/ezh/docker-logspout-sourcebased/blob/master/LICENSE)
=======================

Docker compose source based logspout configuration

logspout build from source from https://github.com/gliderlabs/logspout

By default it builds the stable *logspout-3.1* if you use docker compose and latest unstable *master* if you build directly from Dockerfile.

[Hint #1](https://github.com/ezh/docker-logspout-sourcebased/blob/master/docker/Dockerfile#L19),
[Hint #2](https://github.com/ezh/docker-logspout-sourcebased/blob/master/docker-compose.yml#L8)

Image is based on `debian/jessie`, the same as an official Jenkis docker container.

Modules
-------

This container build with additional logspout modules:
* https://github.com/ezh/logspout-beat
* https://github.com/ezh/logspout-cloudwatch
* https://github.com/ezh/logspout-fluentd
* https://github.com/ezh/logspout-gelf
* https://github.com/ezh/logspout-kafka
* https://github.com/ezh/logspout-kinesis
* https://github.com/ezh/logspout-logentries-autowire
* https://github.com/ezh/logspout-logstash
* https://github.com/ezh/logspout-redis-logstash
* https://github.com/ezh/logspout-splunk

Execution
---------

logspout executed directly as PID 1 process.

Arguments
---------

You may set logspout version via `version` argument

Copyright
---------

Copyright © 2017 Alexey B. Aksenov/Ezh. All rights reserved.
