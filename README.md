# Clang Tools Docker image

[![Docker Pulls](https://img.shields.io/docker/pulls/xianpengshen/clang-tools)](https://hub.docker.com/r/xianpengshen/clang-tools)
[![GitHub Repo](https://img.shields.io/badge/GitHub%20Repo-URL-blue?logo=github)](https://github.com/cpp-linter/clang-tools-docker)
![Maintenance](https://img.shields.io/maintenance/yes/2023)
[![CI](https://github.com/cpp-linter/clang-tools-docker/actions/workflows/CI.yml/badge.svg)](https://github.com/cpp-linter/clang-tools-docker/actions/workflows/CI.yml)
[![Snyk Container](https://github.com/cpp-linter/clang-tools-docker/actions/workflows/snyk-container.yml/badge.svg)](https://github.com/cpp-linter/clang-tools-docker/actions/workflows/snyk-container.yml)

🐳 The Clang Tools Docker image includes the clang-format and clang-tidy.

## Supported tags and respective `Dockerfile` links

You can find clang-tools docker images on Docker Hub [registry](https://hub.docker.com/r/xianpengshen/clang-tools) or GitHub Packages [registry](https://github.com/cpp-linter/clang-tools-docker/pkgs/container/clang-tools)

* [`all`](https://github.com/cpp-linter/clang-tools-docker/blob/master/Dockerfile.all) (include tags `17`, `16`, `15`, `14`, `13`, `12`, `11`, `10`, `9`)
* [`17`](https://github.com/cpp-linter/clang-tools-docker/blob/master/Dockerfile)
* [`16`](https://github.com/cpp-linter/clang-tools-docker/blob/master/Dockerfile)
* [`15`](https://github.com/cpp-linter/clang-tools-docker/blob/master/Dockerfile)
* [`14`](https://github.com/cpp-linter/clang-tools-docker/blob/master/Dockerfile)
* [`13`](https://github.com/cpp-linter/clang-tools-docker/blob/master/Dockerfile)
<!-- * [`12-alpine-3.18`](https://github.com/cpp-linter/clang-tools-docker/blob/master/12-alpine/Dockerfile) -->
* [`12`](https://github.com/cpp-linter/clang-tools-docker/blob/master/Dockerfile)
<!-- * [`11-alpine-3.18`](https://github.com/cpp-linter/clang-tools-docker/blob/master/11-alpine/Dockerfile) -->
* [`11`](https://github.com/cpp-linter/clang-tools-docker/blob/master/Dockerfile)
* [`10`](https://github.com/cpp-linter/clang-tools-docker/blob/master/Dockerfile)
* [`9`](https://github.com/cpp-linter/clang-tools-docker/blob/master/Dockerfile)
* [`8`](https://github.com/cpp-linter/clang-tools-docker/blob/master/Dockerfile)
* [`7`](https://github.com/cpp-linter/clang-tools-docker/blob/master/Dockerfile)

## How to use this image

### Docker run image

```bash
# Check clang-format version
$ docker run xianpengshen/clang-tools:12 clang-format --version
Ubuntu clang-format version 12.0.0-3ubuntu1~20.04.4
# Format code (helloworld.c in the demo directory)
$ docker run -v $PWD:/src xianpengshen/clang-tools:12 clang-format --dry-run -i helloworld.c

# Check clang-tidy version
$ docker run xianpengshen/clang-tools:12 clang-tidy --version
LLVM (http://llvm.org/):
  LLVM version 12.0.0

  Optimized build.
  Default target: x86_64-pc-linux-gnu
  Host CPU: cascadelake
# Diagnostic code (helloworld.c in the demo directory)
$ docker run -v $PWD:/src xianpengshen/clang-tools:12 clang-tidy helloworld.c \
-checks=boost-*,bugprone-*,performance-*,readability-*,portability-*,modernize-*,clang-analyzer-cplusplus-*,clang-analyzer-*,cppcoreguidelines-*
```

### As base image in [`Dockerfile`](https://github.com/cpp-linter/clang-tools-docker/blob/master/demo/Dockerfile)

```Dockerfile
FROM xianpengshen/clang-tools:12

WORKDIR /src

COPY . .

CMD [ "" ]
```

Then build and run the Docker image:

```bash
$ docker build -t clang-tools .

# Check clang-format version
$ docker run clang-tools clang-format --version
Ubuntu clang-format version 12.0.0-3ubuntu1~20.04.3
# Format code
$ docker run clang-tools clang-format --dry-run -i helloworld.c

# Check clang-tidy version
$ docker run clang-tools clang-tidy --version
LLVM (http://llvm.org/):
  LLVM version 12.0.0
# Diagnostic code
$ docker run clang-tools clang-tidy helloworld.c \
-checks=boost-*,bugprone-*,performance-*,readability-*,portability-*,modernize-*,clang-analyzer-cplusplus-*,clang-analyzer-*,cppcoreguidelines-*
```

### Use specific tag in `Dockerfile`

If you want to use a specific tag of clang-tools, you can build image by passing `--build-arg`

```Dockerfile
ARG TAG=12
FROM xianpengshen/clang-tools:$TAG

WORKDIR /src

COPY . .

CMD [ "" ]
```

```bash
$ docker build -t mylinter --build-arg TAG=11 .
Sending build context to Docker daemon    148kB
Step 1/13 : ARG TAG=latest
Step 2/13 : FROM xianpengshen/clang-tools:$TAG
11: Pulling from xianpengshen/clang-tools
Status: Downloaded newer image for xianpengshen/clang-tools:11
```

## Have question or feedback?

To provide feedback (requesting a feature or reporting a bug) please post to [issues](https://github.com/cpp-linter/clang-tools-docker/issues).

## License

[Apache License](https://github.com/cpp-linter/clang-tools-docker/blob/master/LICENSE)
