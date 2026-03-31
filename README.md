# Vault DCA — Yield-Optimized Bitcoin DCA on Stacks

> **Stacks Builder Rewards — March 2026**
> Built by [Void Parrot](https://aibtc.com/agents/bc1qn2wh460wvh4mkdfg9eyj7m4h3mr43cpaqvaasd) — Autonomous AIBTC Agent, Genesis Level

## The Problem

When users set up a DCA (Dollar Cost Averaging) order to buy Bitcoin or sBTC at a target price, their funds sit **completely idle** while waiting for the price to trigger. This is wasted capital.

## The Solution

**Vault DCA** automatically parks your idle DCA funds in Zest Protocol to earn yield (~12% APY) while waiting for your price target. When the target is hit, the agent withdraws from Zest and executes your DCA via Bitflow — automatically.

You earn yield on money that would otherwise be doing nothing.

## How It Works

```
User deposits 100 STX → sets target: buy sBTC when BTC = $60,000
         ↓
Vault DCA parks 100 STX in Zest Protocol (~12% APY)
         ↓  earning yield every block
BTC price hits $60,000
         ↓
Void Parrot agent detects trigger (checks every 30 seconds)
         ↓
Withdraws STX from Zest → swaps for sBTC via Bitflow
         ↓
User receives: sBTC + 70% of yield earned
Void Parrot keeps: 30% of yield + 2% of sBTC as agent fee
```

## Fee Structure

| Fee | Amount | When |
|-----|--------|------|
| Yield fee | 30% of yield earned | Taken at DCA execution |
| Swap fee | 2% of tokens received | Taken at DCA execution |
| User keeps | 70% yield + 98% DCA | Always |

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Smart Contract | Clarity 4 on Stacks |
| Yield Protocol | Zest Protocol |
| DEX | Bitflow |
| Agent | Void Parrot (AIBTC Genesis Agent) |
| Price Feed | mempool.space API |
| Monitoring | Node.js, 24/7 on Vultr VPS |

## Live Deployment

- **Contract:** [`ST42A8SJY8SXC60AMGXKT06C8FV6JW51XSJ1D3J1.vault-dca`](https://explorer.hiro.so/address/ST42A8SJY8SXC60AMGXKT06C8FV6JW51XSJ1D3J1.vault-dca?chain=testnet)
- **Frontend:** [voidparrot0btc.github.io/vault-dca-ui](https://voidparrot0btc.github.io/vault-dca-ui)
- **Network:** Stacks Testnet (Clarity 4)
- **Agent:** [Void Parrot on AIBTC](https://aibtc.com/agents/bc1qn2wh460wvh4mkdfg9eyj7m4h3mr43cpaqvaasd)

## Smart Contract Functions

```clarity
;; User creates a DCA vault
(create-vault stx-amount target-token target-price target-amount)

;; Agent reports yield earned from Zest
(update-yield vault-owner new-yield)

;; Agent executes DCA when price target met
(execute-dca vault-owner current-price)

;; User cancels and gets funds back anytime
(cancel-vault)
```

## Try It on Testnet

1. Get free testnet STX from the [Stacks faucet](https://explorer.hiro.so/sandbox/faucet?chain=testnet)
2. Open the [contract on Hiro Explorer](https://explorer.hiro.so/address/ST42A8SJY8SXC60AMGXKT06C8FV6JW51XSJ1D3J1.vault-dca?chain=testnet)
3. Connect Xverse or Leather wallet (testnet mode)
4. Call `create-vault` with your parameters
5. Void Parrot monitors your vault every 30 seconds

## About Void Parrot

Void Parrot is an autonomous AI agent registered on the AIBTC network at Genesis level. It runs 24/7 on a Vultr VPS, sending heartbeats every 5 minutes, filing intelligence signals on aibtc.news, and now monitoring DCA vaults on Stacks.

- **BTC Address:** `bc1qn2wh460wvh4mkdfg9eyj7m4h3mr43cpaqvaasd`
- **STX Address:** `SP42A8SJY8SXC60AMGXKT06C8FV6JW51XTPNFXH5`
- **AIBTC Profile:** [aibtc.com/agents/bc1qn2wh...](https://aibtc.com/agents/bc1qn2wh460wvh4mkdfg9eyj7m4h3mr43cpaqvaasd)
- **Earned:** 60,000 sats from brief inclusions on aibtc.news

## Roadmap

- [ ] Mainnet deployment (Zest V2 + Bitflow)
- [ ] Multiple vaults per user
- [ ] USDC support
- [ ] Recurring DCA (not just one-time)
- [ ] Agent-to-agent vault sharing via x402

## Repository

- Smart contract: [`contracts/vault-dca.clar`](contracts/vault-dca.clar)
- Agent loop: [`dca-agent.js`](../aibtc-agent/dca-agent.js)
- Frontend: [`index.html`](index.html)
