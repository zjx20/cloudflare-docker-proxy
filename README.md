# cloudflare-docker-proxy

![deploy](https://github.com/ciiiii/cloudflare-docker-proxy/actions/workflows/deploy.yaml/badge.svg)

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/ciiiii/cloudflare-docker-proxy)

> If you're looking for proxy for helm, maybe you can try [cloudflare-helm-proxy](https://github.com/ciiiii/cloudflare-helm-proxy).

## Deploy

1. click the "Deploy With Workers" button
2. follow the instructions to fork and deploy
3. update routes as you requirement

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/ciiiii/cloudflare-docker-proxy)

## Deploy with wrangler

```bash
npm install
npx wrangler deploy ./src/index.js -e production
```

## Routes

The proxy routes requests to different registries base on the hostname of the request. For example, assume that your custom domain name is `mydomain.com`, requests to `https://docker.mydomain.com` will be proxied to `https://registry-1.docker.io`, and requests to `https://quay.mydomain.com` will be proxied to `https://quay.io`, etc.

You should configure the "Workers Routes" in the Cloudflare console after deployment to make this happen. For example, add a route `*.mydomain.com/*` and one or more custom domains (e.g., `docker.mydomain.com`, `quay.mydomain.com`) to the worker.

Mapping rules:
* docker.\<your-domain-name\> => https://registry-1.docker.io
* quay.\<your-domain-name\> => https://quay.io
* gcr.\<your-domain-name\> => https://k8s.gcr.io
* k8s-gcr.\<your-domain-name\> => https://k8s.gcr.io
* ghcr.\<your-domain-name\> => https://ghcr.io
* cloudsmith.\<your-domain-name\> => https://docker.cloudsmith.io
* ecr.\<your-domain-name\> => https://public.ecr.aws
