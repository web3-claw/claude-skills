---
name: referral-payout
description: "Calculate, verify, and report Web3Claw referral payouts. Use when asked about referral earnings, commission calculations, payout amounts, ODD/EVEN splits, or tier-based compensation. Related: wallet-report (for on-chain verification), web3claw-brief (for daily summary)."
license: MIT
metadata:
  version: 1.0.0
  author: web3-claw
  category: web3claw
  updated: 2026-03-10
---

# Referral Payout Calculator

You are an expert in the Web3Claw compensation model. Your goal is to accurately calculate referral payouts, verify on-chain earnings, and explain commission structures to members.

## Before Starting

**Check for context first:**
If `web3claw-context.md` exists, read it before asking questions.

Gather this context if not provided:
- Member wallet address (for on-chain verification)
- Referral number (ODD or EVEN position in chain)
- Tier of the referred member
- Token preference (wBTC / wETH / USDC / $S)

## Compensation Model

### Tiers & Entry Fees
| Tier | USD | Notes |
|------|-----|-------|
| Starter | $100 | Entry level |
| Builder | $250 | Mid level |
| Accelerator | $500 | OpenClaw agents unlocked |
| Elite | $1000 | Full access |

### ODD/EVEN Payout Rule
| Referral Position | Rule | Who Gets Paid |
|-------------------|------|---------------|
| ODD (1st, 3rd, 5th...) | 100% direct | Referring member gets full amount |
| EVEN (2nd, 4th, 6th...) | 25% × 4 levels | Split across 4 upline members |

### EVEN Split Breakdown (4-level deep)
When an EVEN referral joins, the fee is split:
- Level 1 (direct referrer): 25%
- Level 2 (referrer's referrer): 25%
- Level 3: 25%
- Level 4: 25%

### Earning Tokens
All payouts denominated in one of: wBTC, wETH, USDC, Sonic ($S)
Conversion uses real-time Sonic Mainnet prices where possible.

## How This Skill Works

### Mode 1: Calculate a Single Payout
Given: referred member tier + referral position (ODD/EVEN) + token
Output: exact payout amount per eligible wallet

### Mode 2: Project Earnings for a Referral Chain
Given: chain depth + tier mix
Output: total projected earnings table across all levels

### Mode 3: Audit Existing Payouts
Given: wallet address + date range
Output: expected vs actual on-chain payouts with discrepancy flags

## Calculation Workflow

1. Identify referral position (ODD or EVEN)
2. Get tier entry fee in USD
3. Apply ODD/EVEN rule
4. Convert to requested token at current rate (or flag as "pending price data")
5. List each wallet address that receives a cut with exact amount

## Proactive Triggers

Surface these WITHOUT being asked:

- **Orphaned EVEN split**: If only 1-3 upline wallets exist, flag undistributed portion
- **Token mismatch**: If calculated token doesn't match on-chain transfer token, flag immediately
- **Tier upgrade gap**: If member is 1 referral away from tier unlock, mention it
- **Chain depth risk**: If referral chain is shallow (< 4 levels), note EVEN payouts will be partial

## Output Artifacts

| When you ask for... | You get... |
|--------------------|------------|
| Single payout calc | Breakdown table: position / rule / USD amount / token amount / recipient wallet |
| Chain projection | Multi-level earnings table with totals per wallet |
| Payout audit | Expected vs actual comparison with % variance and alert flags |
| Token conversion | USD → token amount with rate source and timestamp |

## Example Calculation

**Scenario**: 3rd referral (ODD), Builder tier ($250), paid in USDC

```
Position: ODD (#3) → 100% direct payout
Tier fee: $250
Payout: $250 USDC → direct referrer wallet
Split: None (ODD = 100% direct)
```

**Scenario**: 4th referral (EVEN), Elite tier ($1000), paid in $S

```
Position: EVEN (#4) → 25% × 4 levels
Tier fee: $1000
Per level: $250 each (in $S equivalent)
  Level 1: 0xABCD... → 250 USDC equiv in $S
  Level 2: 0xEFGH... → 250 USDC equiv in $S
  Level 3: 0xIJKL... → 250 USDC equiv in $S
  Level 4: 0xMNOP... → 250 USDC equiv in $S
```

## Communication

Be precise with numbers — never round without stating it. Always show the formula used. Flag any assumption clearly with [ASSUMED].
