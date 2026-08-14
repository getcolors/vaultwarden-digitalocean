# CLAUDE.md

## Repository

Desired state for one Vaultwarden deployment at `vault.bigconfig.space` on a
DigitalOcean Droplet in Amsterdam. Behavior lives in `../vaultwarden`, which
reuses `../once` for infrastructure, DNS, Resend, ONCE installation and the
application deploy key.

Tracked source consists of `colors.yml`, the copied `green` launcher and Package
Skill payload, secret-free `.envrc`, toolchain files, and documentation.
`.colors/` is generated and `.envrc.private` is secret. Never read either.

## Commands

```sh
./green build
./green create --dry-run
./green create
./green delete
```

Build and dry-run need no credentials. A real create/delete requires explicit
authorization. Keep `compute-prevent-destroy: true`; an authorized delete uses a
one-run `COLORS_PAR_COMPUTE_PREVENT_DESTROY=false`. Never set
`COLORS_PAR_PROFILE`.

## Coupling

The root launcher is a copy of
`.agents/skills/package-vaultwarden-green/green`. After every package update,
update the installed payload and re-copy the root launcher. During development
use `VAULTWARDEN_LIB_ROOT=../vaultwarden`; final execution must use the real
pushed SHA in both copies.

## Recovery

The image restores `/storage/db.sqlite3` from the existing `vaultwarden` R2
bucket when the local database is absent. Weekly verification restores into a
temporary file and runs SQLite integrity checking. Never overwrite a live
SQLite database during a recovery test.

## Git

Work on the current branch. Do not commit or push unless explicitly authorized.
