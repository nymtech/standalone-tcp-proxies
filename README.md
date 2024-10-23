# Nym TCP Proxies (Standalone)

Standalone versions of the `TcpProxyClient` and `TcpProxyServer` [sdk module](https://github.com/nymtech/nym/blob/nym-binaries-v2024.12-aero/sdk/rust/nym-sdk/src/tcp_proxy.rs).

## Build
```shell
cargo build --release
```

## Use
```shell
» ./target/release/proxy_server --help
Usage: proxy_server [OPTIONS] --upstream-tcp-address <UPSTREAM_TCP_ADDRESS>

Options:
  -u, --upstream-tcp-address <UPSTREAM_TCP_ADDRESS>
          Upstream address of the server process we want to proxy traffic to e.g. 127.0.0.1:9067
  -c, --config-dir <CONFIG_DIR>
          Config directory [default: /tmp/nym-tcp-proxy-server]
  -e, --env-path <ENV_PATH>
          Optional env filepath - if none is supplied then the proxy defaults to using mainnet else just use a path to one of the supplied files in envs/ e.g. ./envs/sandbox.env
  -h, --help
```

```shell
» ./target/release/proxy_client --help
Usage: proxy_client [OPTIONS] --server-address <SERVER_ADDRESS>

Options:
      --close-timeout <CLOSE_TIMEOUT>
          Send timeout in seconds [default: 30]
  -s, --server-address <SERVER_ADDRESS>
          Nym address of the NymProxyServer e.g. EjYsntVxxBJrcRugiX5VnbKMbg7gyBGSp9SLt7RgeVFV.EzRtVdHCHoP2ho3DJgKMisMQ3zHkqMtAFAW4pxsq7Y2a@Hs463Wh5LtWZU@NyAmt4trcCbNVsuUhry1wpEXpVnAAfn
      --listen-address <LISTEN_ADDRESS>
          Listen address [default: 127.0.0.1]
      --listen-port <LISTEN_PORT>
          Listen port [default: 8080]
  -e, --env-path <ENV_PATH>
          Optional env filepath - if none is supplied then the proxy defaults to using mainnet else just use a path to one of the supplied files in envs/ e.g. ./envs/sandbox.env
  -h, --help
          Print help
```

## Run
```shell
# set up the server on your remote machine, listening on the port your upstream process is expecting to communicate on (e.g. in the case of lightwalletd, 127.0.0.1:9067).
# this will log the Nym address of the Nym Proxy Server to pass to the proxy_client
./target/release/proxy_server -u <UPSTREAM_TCP_ADDRESS>


# start your proxy client with the address of the server client. by default this listens on 127.0.0.1:8080
./target/release/proxy_client --server-address <SERVER_NYM_ADDRESS>

# now start your client process (such as the zingo-cli wallet) off, directing its traffic to the listen port of your nym proxy client process. all traffic will now be proxied through the mixnet.
```

> You can run on another network by downloading on of the [env files](https://github.com/nymtech/nym/tree/nym-binaries-v2024.12-aero/envs) and passing that to both clients with `-e <PATH_TO_ENV_FILE>`

### A Note on Switching Networks
If you are running the `proxy_server` binary on one network and then switch to another, make sure to either specify a new env-specific directory for key and surb storage, or remove the existing one, before running the binary. Since the `proxy_client` relies on ephemeral clients, then this is not a problem for this binary.

## Documentation
Docs are in progress with the v2 nym docs. You can find the `.md` files [here](https://github.com/nymtech/nym/blob/max/new-docs-framework/documentation/docs/pages/developers/rust/tcpproxy/architecture.mdx) for the moment.
