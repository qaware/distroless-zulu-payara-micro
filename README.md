# Distroless Zulu OpenJDK with Payara Micro

Custom Docker images that combine the Google Distroless Image with Zulu OpenJDK and Payara Micro. The images are published on Docker Hub here: https://hub.docker.com/r/qaware/distroless-zulu-payara-micro/

All the images are tuned for Docker usage, especially concerning the CPU, RAM and thus JVM heap usage.
```
docker run -it --rm --cpus 1 --memory 640m qaware/distroless-zulu-payara-micro:8u212-5.192
```

For more information about Payara Server and Payara Micro have a look at the documentation: https://payara.gitbooks.io/payara-server/content/

For more information and detaials about the individual release versions have a look at the release notes as well as the Github releases pages: https://github.com/payara/Payara/releases

# Maintainer

M.-Leander Reimer (@lreimer), <mario-leander.reimer@qaware.de>

# License

This software is provided under the Apache License, Version 2.0, read the `LICENSE` file for details.
