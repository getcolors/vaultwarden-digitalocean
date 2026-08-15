# vaultwarden-digitalocean

Desired state for `https://vault.bigconfig.space`: Vaultwarden on a small
DigitalOcean ONCE server in Amsterdam, with Cloudflare HTTPS, Resend email and
continuous Litestream replication to the existing `vaultwarden` R2 bucket. It
consumes the official public image directly and needs no GitHub repository or
deployment credential.

```sh
./green build
./green create --dry-run
./green create
```

Credentials live only in `.envrc.private` as the `COLORS_PAR_*` variables listed
at the top of `colors.yml`. Never set `COLORS_PAR_PROFILE`.

Public signup stays disabled. The first create sends an invitation to the owner
address, then converges with no externally available admin endpoint. Deletion
is protected by `compute-prevent-destroy: true` and does not remove R2 backup
objects.
