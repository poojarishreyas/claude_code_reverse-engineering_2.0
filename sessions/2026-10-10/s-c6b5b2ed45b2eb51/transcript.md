# # AIRcoin — Product Requirements Document Oct 10, 2026 · @omkar > Markdown conversion of `AIRcoin — Product Requireme...

| | |
| --- | --- |
| session | `s-c6b5b2ed45b2eb51` |
| model | `claude-opus-5-5` |
| started | 2026-10-10T18:10:18.630Z |
| requests | 1 |
| tokens | in 0 · out 0 · cache read 0 · cache write 0 |

> Generated from `session.jsonl`. Delete this file and it regenerates.

---

### Context established — 0 tools

- tool catalogue: [`4f53cda18c2baa0c0354bb5f`](../../../objects/4f/4f53cda18c2baa0c0354bb5f.json)

---

## req-0001 — claude-opus-5-5

_buffered · 1 messages_

#### USER

# AIRcoin — Product Requirements Document

Oct 10, 2026 · @omkar

> Markdown conversion of `AIRcoin — Product Requirements Document.pdf`. The PDF is the source of truth; diagrams are redrawn here as Mermaid.

## 1. Overview

AIRcoin pays people for growing pollution-absorbing plants. A low-cost camera "miner" watches up to 20 tagged plants and estimates the pollution they remove. It mints AIRcoin as proof of that useful work. Polluting companies must buy and burn AIRcoin to meet compliance, which creates demand.

**Problem.** Urban air pollution (PM2.5, PM10, NO₂, SO₂, CO, VOCs, CO₂) has no direct, verifiable incentive for citizens to fight it. Carbon credits target large projects and are hard for households to join.

**Product in one line.** A plant-monitoring miner, a token minted from verified plant work, and a marketplace where citizens sell the token and polluters buy and burn it.

**Hackathon goal.** Show a working end-to-end system on stage:

- A physical 20-plant rig with a real camera, Raspberry Pi and GPS.
- A live digital twin: camera feed with detections, a 3D model of the miner's insides, sensor gauges and a minting ticker.
- Live anti-cheat: removing a plant, adding a fake plant or reusing a sticker is caught on screen.
- Real miner software fed by simulated sensor data, minting real AIRcoin on a blockchain testnet.
- A wallet and marketplace where an owner sells AIRcoin and a company buys and burns it for compliance.

**Users.**

| User | What they do |
|------|--------------|
| Miner owner (citizen, housing society, school) | Buys the miner, plants and tags up to 20 plants, earns and sells AIRcoin |
| Polluting company / factory | Buys AIRcoin and burns it to meet a compliance obligation |
| Regulator (government / pollution control board) | Sets obligations, registers miners, audits mints and burns |
| AIRcoin operator (our team) | Runs the validator, calibration and marketplace |

## 2. Real-world system concept

This is the full product we pitch. Section 3 says which parts the hackathon builds for real.

### 2.1 The miner (hardware)

| Part | Suggested component | Purpose |
|------|---------------------|---------|
| Compute | Raspberry Pi 4 (4 GB) or Pi 5 | Runs vision, estimation and signing |
| Camera | Pi Camera Module 3 NoIR Wide + blue gel filter | Reads stickers, sizes plants; NoIR enables a plant-liveness (NDVI) check |
| GPS | u-blox NEO-6M / NEO-M8N over UART | Fixes the miner's location for anti-cheat and local AQI lookup |
| Wi-Fi | Pi on-board Wi-Fi | Sends telemetry and proofs |
| Air sensors | PMS5003 (PM2.5/PM10), MQ-135 (gas/VOC), SCD40 (CO₂), BME280 (temp/humidity/pressure) | Measures surrounding air; hackathon feeds simulated values |
| Security | Device key pair in a file (hackathon) / ATECC608 secure element (production) | Signs every proof so it can't be forged |

### 2.2 The stickers

Each miner ships with 20 printed fiducial stickers (ArUco or AprilTag markers). Every sticker ID is registered to exactly one miner at sale time. A sticker seen by a different miner, or by its own miner at a new location, is rejected. This stops owners from moving the same plants between miners to mint twice.

### 2.3 The 20 prescribed plants

The owner plants up to 20 species from a fixed list. Together they cover every major pollutant group: VOCs (benzene, formaldehyde, TCE, xylene), particulates, roadside gases (NO₂, SO₂) and CO₂. The list mixes indoor plants with the strongest lab evidence for VOC removal and hardy Indian outdoor species that tolerate heavy pollution and trap dust.

| # | Plant | Scientific name | Where | Main targets | Evidence |
|---|-------|-----------------|-------|--------------|----------|
| 1 | Snake plant | *Dracaena trifasciata* | Indoor | Benzene, formaldehyde, TCE, xylene; CO₂ at night | [NASA 1989](https://ntrs.nasa.gov/citations/19930073077) |
| 2 | Peace lily | *Spathiphyllum wallisii* | Indoor | Benzene, TCE, formaldehyde, ammonia | NASA 1989 |
| 3 | Bamboo palm | *Chama
... [34,515 more characters in session.jsonl]

#### ASSISTANT

_[empty]_

_stop `null` · 454ms · in 0 · out 0 · cache r0/w0_

