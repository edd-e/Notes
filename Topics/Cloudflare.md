# Cloudflare<!-- omit in toc -->

How to use Cloudflare CDN, domain forwarding, and email forwarding services with a custom domain name (e.g.: `mywebsite.net`).

## Table of contents<!-- omit in toc -->

- [Introduction](#introduction)
- [Official website](#official-website)
- [Configuration](#configuration)
  - [DNS records](#dns-records)
    - [Standard method](#standard-method)
    - [GitHub pages](#github-pages)
    - [Email forwarding](#email-forwarding)
  - [Cloudflare nameservers](#cloudflare-nameservers)

## Introduction

Cloudflare provides a variety of network and network security services. In these notes the focus is on setting up a website with Cloudflare.

In general, for an existing website, you would change the domain registrar records to first route traffic to Cloudflare name servers to take advantage of their services: such as DNS, CDN, and SSL, and then route from Cloudflare to the sites' web host.

## Official website

The official website: <https://cloudflare.com>.

## Configuration

To set up a website with Cloudflare log in and select `+ Add a Site` and enter the domain name.

Confirm a plan and pricing (e.g.: `Free`).

### DNS records

To use Cloudflare DNS and CDN services you will need to set up the appropriate records within Cloudflare as described below.

#### Standard method

The next page should show the DNS settings that Cloudflare was able to import from the registrar. Make sure the records match and send all traffic to the web host and continue.

#### GitHub pages

To use a GitHub pages site with a custom URL, you need to [set up the domain configuration on GitHub](https://pages.github.com) before proceeding.

For example; a GitHub account named `username` has a website repository (in this example the repository name is the same as the username) this website is reachable at `username`.github.io but not at `mywebsite.net`. To fix this, the `username` repository should have a file named `CNAME` where the only content is the domain you wish to use: `mywebsite.net`.

In Cloudflare's DNS records, add 4 `A` records and 1 `CNAME` record. The name of each A record must match the `CNAME` on the GitHub Pages site. The records should look like this:

| Type  | Name            | Value           | TTL  | Status     |
| ----- | --------------- | --------------- | ---- | ---------- |
| A     | `mywebsite.net` | 185.199.108.153 | Auto | On/Proxied |
| A     | `mywebsite.net` | 185.199.109.153 | Auto | On/Proxied |
| A     | `mywebsite.net` | 185.199.110.153 | Auto | On/Proxied |
| A     | `mywebsite.net` | 185.199.111.153 | Auto | On/Proxied |
| CNAME | `www`           | `mywebsite.net` | Auto | On/Proxied |

#### Email forwarding

To forward email Cloudflare needs the mail exchange record for your email provider. In the DNS settings add another record, this time an `MX` record. The provider depends on the service you are using or a default one provided by the domain registrar. Typically there would be a primary server and one or more backups, for example:

| Type | Name            | Value                | Priority | TTL  | Status   |
| ---- | --------------- | -------------------- | -------- | ---- | -------- |
| MX   | `mywebsite.net` | `email1.example.com` | 0        | Auto | DNS only |
| MX   | `mywebsite.net` | `email2.example.com` | 10       | Auto | DNS only |

### Cloudflare nameservers

The last step is to edit the name servers at your domain registrar. The cloudflare name servers you will use are specified in the settings overview. For example: `one.ns.cloudflare.com` and `two.ns.cloudflare.com`.
