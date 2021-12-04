# nprox
This is the caddy (or maybe nginx) config for zephyrnet network proxying between all VMs.

To get this to work, you need to compile a version of Caddy the has the DNSimple API (Hack Club uses that).

I had to setup subdomain zones in DNSimple's web GUI to make this work. tilde.hackclub.com and zephyrnet.hackclub.com are their own zones, with ddns CNAME records pointed at them in the parent hackclub.com zone (that is in hackclub/dns on github).

To get the right caddy binary, do `xcaddy build --with github.com/caddy-dns/lego-deprecated`.

When you run `sudo caddy run` in this directory, you'll need the `DNSIMPLE_OAUTH_TOKEN` set. This is an account-level token like GitHub actions uses, not a user-level token. You can get it from their web gui. I like to use .envrc and direnv to handle this. I will store it in plaintext on this server for now, until I figure out a better way to store this necessary env var. If you set this env var in user level, you need to run `sudo -E caddy run` to transfer env vars across sudoers.

I'll rewrite this once it works better. I had to run a bunch of crazy regex sed commands to fix all the nginx files on the commie VM for this to work. This was more complex than I thought and some things will still be a little buggy, but it seems to work just fine now. I'll clean it before we #ship this.
