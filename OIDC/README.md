# Steps to create your own N+ unprivileged image

1. Git clone this repo
2. Download your NGINX Plus license (cert and key) from F5 portal
3. Copy them into the repo directory, at the root.
4. You should have 4 files

   - Dockerfile
   - entrypoint.sh
   - nginx-repo.crt
   - nginx-repo.key

5. Run the Docker build command

```bash
sudo DOCKER_BUILDKIT=1 docker build  --no-cache --secret id=nginx-key,src=nginx-repo.key --secret id=nginx-crt,src=nginx-repo.crt -t nginx-oidc .
```

6. Push the image in your ``private`` repo

