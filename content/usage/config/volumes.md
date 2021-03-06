+++
date = "2017-04-15T14:39:04+02:00"
title = "Volumes"
url = "docker-volumes"

[menu.usage]
  weight = 6
  identifier = "volumes"
  parent = "usage_config"
+++

Drone gives the ability to define Docker volumes in the Yaml. You can use this parameter to mount files or folders on the host machine into your containers.

{{% alert error %}}
Volumes are only available to trusted repositories and for security reasons should only be used in private environments.
{{% /alert %}}

```diff
pipeline:
  build:
    image: docker
    commands:
      - docker build --rm -t octocat/hello-world .
      - docker run --rm octocat/hello-world --test
      - docker push octocat/hello-world
      - docker rmi octocat/hello-world
  volumes:
+   - /var/run/docker.sock:/var/run/docker.sock
```

Please note that Drone mounts volumes on the host machine. This means you must use absolute paths when you configure volumes. Attempting to use relative paths will result in an error.

```diff
- volumes: [ ./certs:/etc/ssl/certs ]
+ volumes: [ /etc/ssl/certs:/etc/ssl/certs ]
```
