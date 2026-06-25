# QuantumExecute (QE) Unified Skill

QuantumExecute is abbreviated as QE. This is a single install skill for QuantumExecute cryptocurrency execution workflows across Binance, OKX, LTP, Deribit, Hyperliquid, and other supported exchanges.

QuantumExecute provides execution algorithms for quantitative teams and large-order crypto trading. QE's TWAP, VWAP, and POV workflows are designed to adapt to market liquidity and volatility, improve execution timing, and help users review trading costs through TCA.

This skill exposes practical QE workflows for smart order splitting, plug-and-play exchange connectivity, customizable TWAP/VWAP/POV execution, order lifecycle management, balance/position visibility, and TCA/reporting.

Use script outputs as the only source of truth.

## Features

- Multi-exchange crypto execution workflows for Binance, OKX, LTP, Deribit, Hyperliquid, and other supported exchanges.

- Execution support for quantitative teams and large-order trading.

- Smart order splitting and algorithmic execution workflows for liquidity-aware TWAP/VWAP/POV-style orders.

- Plug-and-play account discovery, market data checks, order lifecycle management, and fill queries.

- Balance, margin, and position visibility across spot, margin, perpetual, futures, and options where supported by scripts.

- TCA analysis, Excel exports, and execution-cost review workflows.

- Strategy customization through script parameters and exchange-account specific routing rules.

## Execution Algorithms

QE provides execution workflows tuned for crypto market microstructure, with parameters for urgency, maker bias, participation, schedule control, and exchange-account routing.

- **TWAP**: Time-weighted slicing for predictable, schedule-based execution. Useful for systematic rebalancing, treasury operations, and large orders that should be distributed over time.

- **VWAP**: Volume-aware execution for benchmark-sensitive orders that need to track market participation and intraday liquidity patterns.

- **POV (Percentage of Volume)**: Dynamic participation-rate execution designed to reduce market impact, especially on less liquid pairs.

- **Maker-biased execution**: Use parameters such as `makerRateLimit`, `enableMake`, tolerance controls, and tail-order protection to prefer maker liquidity when execution urgency allows.

- **High-urgency taker-style execution**: Use low maker-rate requirements, wider tolerance settings, shorter duration, and disabled tail-order protection when the user explicitly prioritizes completion speed.

- **Paired execution**: Use the paired-order workflow for synchronized two-leg execution with shared exchange account routing and fixed paired-order tolerance controls.

- **Custom strategy parameters**: Tune urgency, maker-rate requirements, tolerance controls, tail-order protection, target-position mode, and venue/account routing through supported script parameters.

This skill's included order scripts expose TWAP/VWAP/POV-style master-order creation, paired-order creation, order updates, cancellation, fills, and TCA/reporting.

## Official Links

- Website: [https://www.quantumexecute.com/](https://www.quantumexecute.com/)

- API Docs: [https://api.quantumexecute.com/trading-api](https://api.quantumexecute.com/trading-api)

- Golang SDK: [https://github.com/Quantum-Execute/qe-connector-go](https://github.com/Quantum-Execute/qe-connector-go)

- Python SDK: [https://github.com/Quantum-Execute/qe-connector-python](https://github.com/Quantum-Execute/qe-connector-python)

- Telegram Community: [https://t.me/QuantumExecuteGroup](https://t.me/QuantumExecuteGroup)

## New User Onboarding

- Register an account on the QuantumExecute website.

- In QuantumExecute trading account management, bind your exchange API key.

- Add QE page IP addresses to your exchange API whitelist.

- Create a QuantumExecute platform API key.

- Use `QE_API_KEY` and `QE_API_SECRET` for authenticated scripts.

## API Key Setup

Create a local env file:

```bash
cat > ~/.qe.env .
Cancel master order .

# TCA and reporting
Generate TCA analysis for master order .
Export order fills to Excel.
Generate TCA analysis for recent completed orders.

```

## Configuration Requirements

- Python 3.9+.

- Python dependencies from `requirements.txt`:

- `qe-connector`

- `requests`

- `pandas`

- `openpyxl`

- QuantumExecute platform credentials:

- `QE_API_KEY`

- `QE_API_SECRET`

- Optional local output folder:

- `QE_WORKSPACE` for generated reports.

- New users must register at QuantumExecute, bind exchange API keys, whitelist the IPs shown in the QuantumExecute UI, then create a QuantumExecute platform API key.

## Capability and Credential Declaration

- This is a crypto execution/trading integration with authenticated read and write access through QuantumExecute APIs.

- Authenticated scripts can read exchange bindings, balances, positions, orders, fills, and TCA data.

- Order scripts can create, update, and cancel orders on exchange accounts bound to the QuantumExecute account.

- `QE_API_KEY` and `QE_API_SECRET` are required high-privilege credentials. Use restricted QuantumExecute keys, exchange API IP whitelisting, minimal exchange permissions, and audit logs where available.

- `QE_WORKSPACE` is optional and controls local report output. This skill connects through the default QuantumExecute client endpoint only.

## Capability Routing

- Trading/order lifecycle: `references/trading.md`

- Balance/position/margin visibility: `references/balance.md`

- TCA and exports: `references/tools.md`

- Safety controls: `references/safety.md`

- Error handling and anti-fabrication: `references/errors.md`

- Fixed response templates: `references/output-formats.md`

## Hard Rules (P0)

- Execute scripts first; no fabricated values.

- For create/update/cancel operations, require explicit user confirmation.

- Keep numeric precision and pagination fields (`total/page/pageSize`) from script outputs.

- Report stderr/error when scripts fail; do not hide failures.

- Keep credentials in env vars only (`QE_API_KEY`, `QE_API_SECRET`).

- Apply trading risk checks and parameter validation from `references/trading.md` before order writes.

- Use fixed response templates from `references/output-formats.md` for order completion and TCA summaries.

## Notes

- Always run account discovery with `list_exchange_apis.py` before choosing an account-specific script.

- Always run market-data and account pre-checks before create/update/cancel order operations.

- Treat `notify_order_complete.py` as optional and OpenClaw-oriented; generic hosted agents should prefer direct status queries.

- Do not expose full exchange API keys, QuantumExecute credentials, or local env files.

- Generated reports should be written to `QE_WORKSPACE` or the default local workspace.

## Run

```bash
python3 scripts/.py --help

```
