# security.txt as a service -- Built on Cloudflare Workers

This is the worker that serves [security.txt](https://securitytxt.org) on several sites by @diecknet.

## Background

From [https://securitytxt.org](https://securitytxt.org),

```
When security risks in web services are discovered by independent security researchers who
understand the severity of the risk, they often lack the channels to disclose them properly.
As a result, security issues may be left unreported. security.txt defines a standard to help
organizations define the process for security researchers to disclose security vulnerabilities
securely.
```

This repository provides a simple solution to deliver a `security.txt` file using Cloudflare Workers. It is a fork of [cloudflare/securitytxt-worker](https://github.com/cloudflare/securitytxt-worker).

### Changed features

- use a static version of `security.txt`
- added 'Deploy with Workers' button and instructions
- removed `MAKE` commands and `expires.js`, that I didn't need

## Steps for deployment

### Click 'Deploy with Workers'

[![Deploy with Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/diecknet/securitytxt-worker)

### Add Secrets to Github Repository

|Secret name|Secret value|Note|
|---|---|---|
|CF_ACCOUNT_ID|*Your Cloudflare Account ID*|You can find it in the Workers Dashboard|
|CF_API_TOKEN|*Your Cloudflare API Token*|You can generate one under ['My profile' -> 'API Tokens'](https://dash.cloudflare.com/profile/api-tokens). You can use the template 'Edit Cloudflare Workers'|

### Customize your 'security.txt' file

You can find a generator on [https://securitytxt.org/](https://securitytxt.org/).

### Check the deployment

Wait for the deployment to finish. You can find the URL of your deployment in your Cloudflare Workers dashboard.

### Add Workers Routes

Navigate to your domain in the Cloudflare dashboard, then to 'Workers'. Add desired routes. I added both of these:

|Route|Worker|
|---|---|
|*example.com/security.txt|securitytxt-worker|
|*example.com/.well-known/security.txt|securitytxt-worker|

**Replace 'example.com' with your domain.**
If you don't want to include all subdomains, remove the leading `*` asterisk before the domain.
