# Nym TCP Proxies (Standalone)

Standalone versions of the `TcpProxyClient` and `TcpProxyServer` [sdk module](https://github.com/nymtech/nym/blob/nym-binaries-v2024.12-aero/sdk/rust/nym-sdk/src/tcp_proxy.rs).

## Build
```shell
cargo build --release
```

## Run
```shell
# terminal 1: this will log the Nym address of the Nym Proxy Server to pass to the proxy_client
./target/release/proxy_server -u <UPSTREAM_TCP_ADDRESS>

# terminal 2
./target/release/proxy_client --server-address <SERVER_NYM_ADDRESS>
```

### A Note on Switching Networks
If you are running the `proxy_server` binary on one network and then switch to another, make sure to either specify a new env-specific directory for key and surb storage, or remove the existing one, before running the binary. Since the `proxy_client` relies on ephemeral clients, then this is not a problem for this binary.

## Documentation
Docs are in progress with the v2 nym docs. You can find the `.md` files [here](https://github.com/nymtech/nym/blob/max/new-docs-framework/documentation/docs/pages/developers/rust/tcpproxy/architecture.mdx) for the moment.
