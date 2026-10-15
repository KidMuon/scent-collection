# Use the shared personal Postgres cluster, not a per-app database container

This app stores its data in the user's single personal Postgres cluster, which runs in Docker in its own Compose project outside this repo and hosts the databases of all their small personal apps. The app has its own `scent_collection` database and login role, and never holds the cluster's admin credentials. The user wants one cluster to run, back up and learn, and to move to something more robust only when a real need appears. Docker is used rather than Arch's `postgresql` package so that major-version upgrades happen only when the user chooses, not during a routine `pacman -Syu`.

## Consequences

- This repo's Compose file has no Postgres service. The app joins the cluster's Docker network and must retry its database connection at startup, because Compose can't order services across projects.
- Major upgrades of the cluster move every app at once, and when the cluster is down every app is down. With small local apps both are accepted.
- `make backup` / `make restore` here cover only the `scent_collection` database. Backing up the whole cluster belongs to the cluster's own setup.
