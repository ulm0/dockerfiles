# Tiny Docker Registry Image

[![pipeline status](https://gitlab.com/ulm0/registry/badges/master/pipeline.svg)](https://gitlab.com/ulm0/registry/commits/master) [![Version](https://images.microbadger.com/badges/version/ulm0/registry.svg)](https://microbadger.com/images/ulm0/registry "Get your own version badge on microbadger.com") [![Layers](https://images.microbadger.com/badges/image/ulm0/registry.svg)](https://microbadger.com/images/ulm0/registry "Get your own image badge on microbadger.com") [![License](https://img.shields.io/badge/license-MIT-orange.svg)](LICENSE)

This is a tiny Docker Registry v2 multi-arch image (`ARMv7`, `ARM64` and `AMD64`) based on the scratch image.

## Usage

Simply run:

```sh
docker run -d \
--name registry \
-v $PWD/registry/data:/var/lib/registry \
-p 5000:5000 \
registry.gitlab.com/ulm0/registry:2
```

Now You can push images to `localhost:5000`

## Further usage

See: https://docs.docker.com/registry/deploying/
