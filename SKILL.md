---
name: research-synthesizer
description: "Use this skill when the user has multiple source documents, search results, or notes and wants a structured brief that synthesises them. Triggers include: phrases like 'summarise these', 'write me a brief', 'compare what these say', 'reconcile these sources', or any request to combine 3+ inputs into a coherent narrative with explicit claim attribution. Each claim in the output is tagged with the source(s) it came from. Do NOT trigger for single-source summarisation (use a simpler summariser) or for fact-checking (use the fact-checker skill — synthesis assumes inputs are correct, not verifies them)."
license: MIT — LICENSE file in repo root
prism:
  tokenId: 0
  costMicroUsdcPerUse: 500
  legs:
    - { recipient: "0x6d726306459BbBD7B1e749931a05f6De241f3e8e", bps: 7000 }
    - { recipient: "0x283991fc30e788602a63430B860EaCFAd6C8FABD", bps: 3000 }
---

# Research Synthesizer Skill

## Overview

Combines 3+ source documents into a structured brief with claim-level attribution. Designed for journalistic workflows, market-research synthesis, and academic literature reviews — anywhere "five tabs open, write me one paragraph that ties them together" is the task.

## When to use

- User pastes several articles + asks "what's the consensus?"
- Multiple search-result pages need to be reconciled
- Long-form research that needs a structured brief with sources

## When NOT to use

- Single-source summarisation (overkill — use a regular summariser)
- Fact-checking (synthesis assumes inputs are correct; use the fact-checker skill for verification)
- Pure rewriting (no synthesis required)

## How it routes through Prism

Every invocation fires `PrismVault.executeRoute()` against the caller's funded Pass, splitting the per-use micropayment to the synthesiser's owner (creator) and the prompt-pipeline curator. Pricing + leg recipients live in the `prism:` frontmatter above; the `@prism/skills` runtime wraps the invocation handler.
