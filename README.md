# NGINX Plus images for F5XC vK8S

Nginx Plus can be deployed easily in F5XC as PaaS in vK8S (or mK8S) in order to bring capablities like SAML or OIDC. But it must run in unprivileged mode (non-root)
In this repo, we maintain N+ docker image for SAML SP and OIDC Relying Party.

<img src=./f5xc-archi.png alt="Architecture" width=1000>

## N+ as SAML Service Provider

Full doc here : [NGINX Plus](./SAML/README.md)

In this section, you can build your own N+ image in order to run N+ in vK8S as SAML SP.
The projecty is based on official and supported Nginx PLUS SAML SP module : https://github.com/nginxinc/nginx-saml

```mermaid
sequenceDiagram
    autonumber
    actor User Agent
    participant SP (NGINX)
    participant IdP
    User Agent->>SP (NGINX): Access resource
    SP (NGINX)->>User Agent: HTML Form (auto-submit)
	User Agent->>IdP: HTTP POST with SAML AuthnRequest
    IdP->>User Agent: Challenge for credentials
    User Agent->>IdP: User login
    IdP->>User Agent: SAML Response in HTML Form (auto-submit)
	User Agent->>SP (NGINX): HTTP POST with SAML Response to /saml/acs
    SP (NGINX)->>SP (NGINX): Validate Assertion and extract attributes
    SP (NGINX)->>User Agent: Grant/Deny Access
```
`Figure 1. SAML SP-Initiated SSO with POST Bindings for AuthnRequest and Response`

## N+ as OIDC Relying Party

Full doc here : [NGINX Plus](./OIDC/README.md)

In this section, you can build your own N+ image in order to run N+ in vK8S as OIDC Relying Party
The projecty is based on official and supported Nginx PLUS OIDC module : https://github.com/nginxinc/nginx-openid-connect

<img src=https://www.nginx.com/wp-content/uploads/2018/04/dia-LC-2018-03-30-OpenID-Connect-authorization-code-flow-NGINX-800x426-03.svg alt="OpenID Connect components" width=500>

![OpenID Connect protocol diagram](https://www.nginx.com/wp-content/uploads/2018/04/dia-LC-2018-03-30-OpenID-Connect-authentication-code-flow-detailed-800x840-03.svg)

`Figure 2. OpenID Connect authorization code flow protocol`