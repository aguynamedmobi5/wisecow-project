# Cow wisdom web server

# Problem Statement
Deploy the wisecow application as a k8s app

## Requirement
1. Create Dockerfile for the image and corresponding k8s manifest to deploy in k8s env. The wisecow service should be exposed as k8s service.
2. Github action for creating new image when changes are made to this repo
3. [Challenge goal]: Enable secure TLS communication for the wisecow app.

## Expected Artifacts
1. Github repo containing the app with corresponding dockerfile, k8s manifest, any other artifacts needed.
2. Github repo with corresponding github action.
3. Github repo should be kept private and the access should be enabled for following github IDs: nyrahul, SujithKasireddy

# Solution

## Implementing the tls
### run the following commands
```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout wisecow.key -out wisecow.crt -subj "/CN=app.cloudcloun.shop/O=YourOrganization"
```
```
kubectl create secret tls wisecow-tls --cert=wisecow.crt --key=wisecow.key -n wisecow
```
Ingress will automatically use the secret generated above

## DNS
I have used route53 as DNS, for this I have mapped the Ingress' LoadBalancer with the domain name

<img width="1324" alt="Screenshot 2024-08-06 at 6 51 24 AM" src="https://github.com/user-attachments/assets/23bbede3-b585-4026-a3f9-f0bc4e02d734">

## Result
<img width="802" alt="result" src="https://github.com/user-attachments/assets/c60b396f-b522-4ed1-af24-28fe0dd76c2a">
