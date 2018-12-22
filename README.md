# Build a yum proxy with apache httpd

# Introduction

Ever need to run dnf/yum all the time becuase you're building containers that do need to do that? This is a short ansible playbook to proxy and cache rpms off of network repos.

I use this on my laptop because I do run dnf a lot on containers - so I figured I'd cache it all locally.

## Usage

simply run
`ansible-playbook main.yml`
with whatever sudo permissions you'll need (you are reconfiguring and bouncing a root service) on the host machine.

I just use `ansible-playbook main.yml -K` to prompt for the password.

## How it configures apache
It probably configures apache httpd fairly poorly. This is not a general purpose httpd install playbook.  This was made to proxy dnf repos.

## Mirrors - or lack thereof
I couldn't get httpd to correctly follow the 302 redirects for dl.fedora.org to an actual mirror, so you'll notice in [the main file](https://github.com/johrstrom/dev-env/blob/master/config.yml) it has 

`      fedora_mirror: "http://mirrors.kernel.org/fedora"`

a specific mirror configured.  Please override this.
