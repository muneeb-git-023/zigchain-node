
# -----------------------------
# ✅ ZigChain Node Dockerfile
# -----------------------------
FROM ubuntu:22.04

# --- Install Dependencies ---
RUN apt-get update && \
    apt-get install -y curl jq ca-certificates && \
    rm -rf /var/lib/apt/lists/*

# --- Copy ZigChain Binary ---
COPY ../go/bin/zigchaind /usr/local/bin/zigchaind
RUN chmod +x /usr/local/bin/zigchaind

# --- Copy Node Config & WASM ---
COPY ../config /root/.zigchain/config
COPY ../wasm /root/.zigchain/wasm

# --- Environment Variables ---
ENV ZIG_HOME=/root/.zigchain
ENV PATH=$PATH:/usr/local/bin

# --- Create valid priv_validator_state.json ---
RUN mkdir -p /root/.zigchain/data && \
    echo '{"height":"0","round":0,"step":0}' > /root/.zigchain/data/priv_validator_state.json

# --- Expose Ports ---
EXPOSE 26656 26657 1317 9090

# --- Entry Point with Auto-Init Check ---
ENTRYPOINT ["/bin/bash", "-c", "\
if [ ! -f /root/.zigchain/config/genesis.json ]; then \
  echo '🧩 First-time setup: initializing ZigChain node...'; \
  zigchaind init docker-node --chain-id zig-test-2 --home /root/.zigchain; \
fi && \
echo '🚀 Starting ZigChain Node...' && \
exec zigchaind start --home /root/.zigchain \
"]
