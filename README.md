# secure-docker-images
Notes from DevSecOps ch.7 Build Secure Docker Images

Runtime environment can be vulenrable to attacks
-> leverage security tool to scan docker images for vulnerabilities
-> docker cmd: docker scout

1. Add image scanning job
<img width="1023" alt="Capture d’écran 2024-06-05 à 21 38 18" src="https://github.com/JulienAvezou/secure-docker-images/assets/62488871/1834e0d8-dfc7-4b38-8916-105091ac7ea2">
<img width="767" alt="Capture d’écran 2024-06-05 à 21 55 00" src="https://github.com/JulienAvezou/secure-docker-images/assets/62488871/bfd9a2df-dad3-4dac-9606-f4f77efa6c52">
<img width="761" alt="Capture d’écran 2024-06-05 à 21 55 09" src="https://github.com/JulienAvezou/secure-docker-images/assets/62488871/2b65343a-9551-4cb5-8fc6-a110877d7c81">

trivy scans multiple aspects: base layers of OS, then higher up layers such as node.js
the tool also checks for secrets and misconfigurations

2. Fix some image vulnerabilities found
eg. fix baseline image in Dockerfile
<img width="426" alt="Capture d’écran 2024-06-05 à 22 05 57" src="https://github.com/JulienAvezou/secure-docker-images/assets/62488871/0c8edff0-ebf7-43f7-9904-51b490cd31d5">

tip: to find out transitive dependency path you can run 'npm ls <dependency>'

3. Automate uploading findings to DefectDojo
<img width="467" alt="Capture d’écran 2024-06-05 à 23 05 22" src="https://github.com/JulienAvezou/secure-docker-images/assets/62488871/af90f886-8398-49b4-a46a-af45fd1b2285">
<img width="427" alt="Capture d’écran 2024-06-05 à 23 04 07" src="https://github.com/JulienAvezou/secure-docker-images/assets/62488871/3a8da542-1e79-4a9c-8f51-36d4fa174816">

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
<img width="848" alt="Capture d’écran 2024-06-05 à 22 53 15" src="https://github.com/JulienAvezou/secure-docker-images/assets/62488871/6331a9f6-6c4b-41ae-837a-ee92d30c5b53">
