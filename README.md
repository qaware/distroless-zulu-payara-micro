# Distroless Zulu OpenJDK with Payara Micro

Custom Docker images that combine the Google Distroless Image with Zulu OpenJDK and Payara Micro. The images are published on Docker Hub here: https://hub.docker.com/r/qaware/distroless-zulu-payara-micro/

All the images are tuned for Docker usage, especially concerning the CPU, RAM and thus JVM heap usage.
```
docker run -it --rm --cpus 1 --memory 640m qaware/distroless-zulu-payara-micro:8u212-5.191
```

# Maintainer

M.-Leander Reimer (@lreimer), <mario-leander.reimer@qaware.de>

# License

This software is provided under the Apache License, Version 2.0, read the `LICENSE` file for details.
