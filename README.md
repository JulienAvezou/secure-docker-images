# secure-docker-images
Notes from DevSecOps ch.7 Build Secure Docker Images

Runtime environment can be vulenrable to attacks
-> leverage security tool to scan docker images for vulnerabilities
-> docker cmd: docker scout

1. Add image scanning job
<img width="1023" alt="Capture d’écran 2024-06-05 à 21 38 18" src="https://github.com/JulienAvezou/secure-docker-images/assets/62488871/1834e0d8-dfc7-4b38-8916-105091ac7ea2">

trivy scans multiple aspects: base layers of OS, then higher up layers such as node.js
the tool also checks for secrets and misconfigurations

2. Fix some image vulnerabilities found
eg. fix baseline image in Dockerfile

tip: to find out transitive dependency path you can run 'npm ls <dependency>'

3. Automate uploading findings to DefectDojo

Docker security best practices:
- use official Docker images as base image
- use specific image versions - fixate the version
- use smaller images whenever possible - leaner and smaller OS distro (eg. alpine)
- use .dockerignore to explicitly exclude files and folders
- make use of "multi-stage builds" to prevent artifacts needed to build the image from the run stage
- use the least privileged user - create dedicated user and group

It's important to continuously scan images for security vulnerabilities
-> scan images in the registry, doesn't interfere with pipeline
eg. Enhanced Scanning on ECR registry
