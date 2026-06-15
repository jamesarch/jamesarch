```
$ whoami
jamesarch — Staff SRE / Platform Engineer
10 yrs infra · 8 yrs full-remote · China → anywhere async

$ uname -a
production  80B+ daily requests  95k+ enterprise clients  10k+ live agents  200+ global nodes
```

---

```
$ cat /proc/impact

[observability]   zabbix 3934 nvps · profiled rcache utilization (0.4% actual vs. overconfig)
                  → cpu 36→12 cores (-67%)  load 175→32 (-82%)  nvps flat  zero restart

[data-integrity]  clickhouse 4-shard cluster misconfigured as 2S×2R + internal_replication
                  → 36-59% silent read loss per query · fixed via hot-reload · 19 TB reclaimed

[memory]          glibc per-thread arena fragmentation under ~2k msg/s json churn
                  → mimalloc  2000 MiB/pod → 250 MiB/pod (-87%)  no leak  no restart

[ha-platform]     10k-agent websocket mgmt: single instance → redis-backed multi-replica
                  (presence · pub-sub routing · sigterm drain)
                  → rolling restart agent downtime <1s  vs  full-restart = 2200 agents drop

[incident-492]    7600 overseas agents offline · machines alive · no app error
                  root: oversea dns line → broken cloudflare cname → 403 on /ws/agent
                  fix:  dig +subnet confirmed · direct A record · 4 min full recovery

[aiops]           hermes-agent (NousResearch) deployed in production ops
                  extended with custom MCP server: 154 infra skills (vsphere · ansible · metrics)
                  3-tier model fallback · full sqlite audit log per agent action · zero inbound ports
```

---

```
$ ls -la ~/oss/
```

**[`createrepo_rs`](https://github.com/jamesarch/createrepo_rs)** — Rust RPM repo metadata generator  
`thread::scope` + `crossbeam` parallel scan · in-memory SQLite · single `VACUUM INTO` flush  
254 pkg: `10.5s → 0.078s` (~130×) · musl static · `.deb` `.rpm` debian-src · 4 MB scratch docker  
packaged in COPR / AUR / Debian

**[`browser-autos`](https://github.com/browser-autos/browser-autos)** — cloud-native headless browser automation API  
TypeScript · multi-arch Docker (`browserautos/browser-autos`) · production-grade

**[`ghostty-patched`](https://github.com/jamesarch/ghostty-patched)** — personal ghostty build  
`new_tab_with_command` · `link-file` · concurrency deadlock fix on link-click  
VOUCHED contributor → [ghostty-org/ghostty](https://github.com/ghostty-org/ghostty)

```
$ gh pr list --author jamesarch --state merged --repo upstream
kubernetes/kubernetes  ✓ merged
nushell/nushell        ✓ merged
aya-rs/aya             ✓ merged
actix/actix-web        ✓ merged
rust-course            ✓ merged
```

---

```
$ cat ~/.config/stack

infra      k8s (k3s + prod multi-cluster)  ansible  opentofu  vsphere+govmomi  kvm/hyper-v
observe    zabbix  victoriametrics  clickhouse  prometheus  grafana  vector  alertmanager
languages  rust · go · python · shell
network    wireguard  quic/quinn  mtls  iptables/conntrack/netfilter  bgp-adjacent
ai/ops     mcp server  llm agent orchestration  openai-compat gateway  prompt security

$ cat ~/.config/approach

ai-native workflow:
  heavy use of ai agents for coding · root-cause analysis · operational automation
  my half: problem discovery · architecture decisions · production validation · red lines

prefer boring reliability over clever fragility
prefer static binaries over dependency piles
prefer observable failures over silent magic
prefer terminal workflows over dashboards

$ echo $LOCATION
China · full-remote · open to overseas / async-first
```
