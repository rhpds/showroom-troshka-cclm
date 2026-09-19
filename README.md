# showroom-troshka-cclm

Showroom lab guide for the Troshka **CCLM** (Cross-Cluster Live Migration)
catalog item — two nested OpenShift clusters with CNV decentralized live
migration and MTV/Forklift.

Companion to
[showroom-troshka-ocp-base](https://github.com/rhpds/showroom-troshka-ocp-base)
(same Antora contract). Provisioned by
[Troshka](https://github.com/rhpds/troshka) from the `ocp-cclm` template.

## Use with Troshka

Point a showroom container's **Content repo** at this repository (and set the
**Content ref**) with *Build content at deploy* enabled. Troshka clones this
repo into the showroom pod, injects its generated `ui-config.yml`, and builds
the Antora site.

## Layout

```
site.yml                              # Antora playbook (must be named site.yml)
content/
  antora.yml                          # component descriptor — name MUST be "modules"
  modules/ROOT/
    nav.adoc
    pages/
      index.adoc                      # overview
      01-environment.adoc             # topology / networks
      02-terminal.adoc                # dual-cluster terminal
      03-verify-sync.adoc             # sync controllers
      04-mtv-migrate.adoc             # MTV walkthrough
      05-known-issues.adoc            # production gotchas
```

## Notes

- **Do not** add `ui-config.yml` or `nginx.conf` — Troshka generates and
  injects both into the showroom pod at deploy.
- The component `name:` in `content/antora.yml` **must remain `modules`** to
  match Troshka's generated `ui-config.yml`; any other name renders a blank
  right panel.
- The playbook **must** be named `site.yml` at the repo root — Troshka's Antora
  builder runs with `ANTORA_PLAYBOOK=site.yml`.

## Build locally (optional)

```sh
npx antora --fetch site.yml
# built site: ./www/www
```
