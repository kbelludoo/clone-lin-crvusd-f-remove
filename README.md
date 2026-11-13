# clone-lin-crvusd-f-remove

Experimental **LIN** clone of Curve crvUSD `Controller._get_f_remove` — the
liquidation collateral-withdraw fraction

`f_remove = ((1 + h/2) / (1 + h) * (1 - frac) + frac) * frac`

**Proofs live in [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open)** — this repo is the LIN copy only.

- **Upstream (hash-pinned, not vendored):** [curvefi/curve-stablecoin](https://github.com/curvefi/curve-stablecoin) `81b3bea490e9b45221c82e78387920ccfeb05b33`
  - `curve_stablecoin/controller.vy` sha256 `42d82a3c36712cc1397f170d8e6924f7985035be2e54cfcfee1ce3d303a47c6b` blob `ac5e86ccaefffde86ced8ee4fa4b61cc5242206f`
  - LICENSE is informational-only (Swiss Stake AG; no reproduction right). This repository does **not** vendor the Vyper source.
- **LIN kernel:** [`src/lin_crvusd_f_remove.lin`](src/lin_crvusd_f_remove.lin)
- **C11 oracle copy:** [`test/oracles/crvusd_f_remove_c11.c`](test/oracles/crvusd_f_remove_c11.c)
- **Proofs (lin-open only):** `examples/crvusd_f_remove/` and `make crvusd-f-remove-proof`
- **Class:** EXPERIMENTAL uint64-scale, `SCALE = 1e9`. Not Ethereum uint256. Not 1e18 WAD. Not a production controller replacement.

Named goldens: `h=0` half → **500000000**; `frac=0.5` `h=0.1` → **488636363** (gap vs naive frac on `y=1e9`: **11363637**); `frac=0.1` `h=0.05` → **97857142**. Naive i64 `7e18*3e18` wraps to **-5389669316318724096**; 128-bit muldiv fail-closes to **0**.

## Reproduce proofs (in lin-open)

```bash
make crvusd-f-remove-proof
# or: python3 test/prove_crvusd_f_remove_external.py
```

## Not claimed

Uint256 / WAD=1e18 / token-precision mainnet parity.
LIN replacing crvUSD, LLAMMA, Curve, or the EVM. TVL or dollar savings. zk soundness.
Controller `_health` (see clone-lin-crvusd-health). LLAMMA `get_x_down` (see clone-lin-llamma-xy).
