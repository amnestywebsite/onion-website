# Amnesty.org Onion Proxy - Ansible

This repo contains Ansible roles for provisioning a Tor onion service and a HTTP reverse proxy. The code will configure a Tor onion service which can be used to access a public website through the Tor network.

First download the Ansible playbook from this repository:

```bash
git clone git@github.com:amnestywebsite/onion-website.git && cd onion-website/onion-proxy-ansible/
```

## Configuraton

The TLS and onion service keys for the reverse proxy and Tor onion service needed to be added to the `secrets` directory before deployment. We are using a wildcard TLS certifcate issued for our vanity onion domain by the [HARICA certificate authority](https://news.harica.gr/article/onion_announcement/). The `cert` file contains the issued leaf and intermediary certs in PEM format. The `pem` files contains the unencrypted TLS private key in PEM format.

The vanity onion domains was generated using [mkp224o](https://github.com/cathugger/mkp224o).

The final directory structure should look as follows:

```
secrets/amnestyl337aduwuvpf57irfl54ggtnuera45ygcxzuftwxjvvmpuzqd.onion
secrets/amnestyl337aduwuvpf57irfl54ggtnuera45ygcxzuftwxjvvmpuzqd.onion/certs
secrets/amnestyl337aduwuvpf57irfl54ggtnuera45ygcxzuftwxjvvmpuzqd.onion/certs/amnestyl337aduwuvpf57irfl54ggtnuera45ygcxzuftwxjvvmpuzqd.onion.pem
secrets/amnestyl337aduwuvpf57irfl54ggtnuera45ygcxzuftwxjvvmpuzqd.onion/certs/amnestyl337aduwuvpf57irfl54ggtnuera45ygcxzuftwxjvvmpuzqd.onion.cert
secrets/amnestyl337aduwuvpf57irfl54ggtnuera45ygcxzuftwxjvvmpuzqd.onion/tor
secrets/amnestyl337aduwuvpf57irfl54ggtnuera45ygcxzuftwxjvvmpuzqd.onion/tor/hs_ed25519_public_key
secrets/amnestyl337aduwuvpf57irfl54ggtnuera45ygcxzuftwxjvvmpuzqd.onion/tor/hs_ed25519_secret_key
secrets/amnestyl337aduwuvpf57irfl54ggtnuera45ygcxzuftwxjvvmpuzqd.onion/tor/hostname
```

An Ansible inventory file also needs to be created with configuration values for the deployment. You can see an example in [hosts-prod]([hosts/hosts-prod).

# Deployment

The deployment can be run once SSH access if configured, Ansible is installed locally and the various secrets have been copied to the correct locations in the local `secrets` directory.

```
ansible-playbook site.yml --ask-become-pass -i hosts/hosts-prod
```