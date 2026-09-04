# PeerTube for LazyCat

LazyCat LPK v2 packaging for [PeerTube](https://github.com/Chocobozzz/PeerTube), an ActivityPub-federated video streaming platform using P2P directly in the browser.

## Runtime

- PeerTube is served directly on port 9000 through a LazyCat HTTP upstream; nginx and certbot are not included.
- PostgreSQL 17, Redis 8, and Postfix Relay run as internal services.
- RTMP live streaming is exposed on TCP port 1935.
- This is a single-instance application.
- Docker Hub images use explicit tags through the `docker.1ms.run` mirror. Postfix Relay publishes only `latest`; the other services use fixed version tags.

## Storage

Internal data is stored under `/lzcapp/var`. The setup wizard optionally stores large video and caption directories under a selected LazyCat user's `/lzcapp/documents/<uid>/PeerTube` directory.

Changing the storage option after deployment does not migrate existing files. Move the data explicitly before switching storage locations.

## Build

```sh
lzc-cli project release -o dist/application.lpk
```

## GitHub Actions

The scheduled workflow tracks the latest stable PeerTube SemVer tag, creates a versioned GitHub Release asset, and publishes only to the MiaoMiao private store.

Required repository or organization Secrets:

- `APPSTORE_URL`
- `APPSTORE_TOKEN`

Optional Secrets:

- `APP_ID`
- `PRIVATE_STORE_GROUP_CODES`
