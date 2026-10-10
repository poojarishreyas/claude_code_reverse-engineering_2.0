# AIRcoin -- Product Requirements Document AIRcoin -- Product Requirements Document Oct 10, 2026 � @omkar 1. Overview A...

| | |
| --- | --- |
| session | `s-5c84ecb1a32aad29` |
| model | `claude-opus-5-5` |
| started | 2026-10-10T17:31:57.969Z |
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

AIRcoin -- Product Requirements Document

AIRcoin -- Product Requirements Document

 Oct 10, 2026 � @omkar

1. Overview

AIRcoin pays people for growing pollution-absorbing plants. A low-cost camera "miner"
watches up to 20 tagged plants and estimates the pollution they remove. It mints AIRcoin
as proof of that useful work. Polluting companies must buy and burn AIRcoin to meet
compliance, which creates demand.

Problem. Urban air pollution (PM2.5, PM10, NO, SO, CO, VOCs, CO) has no direct,
verifiable incentive for citizens to fight it. Carbon credits target large projects and are
hard for households to join.

Product in one line. A plant-monitoring miner, a token minted from verified plant work,
and a marketplace where citizens sell the token and polluters buy and burn it.

Hackathon goal. Show a working end-to-end system on stage:

    A physical 20-plant rig with a real camera, Raspberry Pi and GPS.
    A live digital twin: camera feed with detections, a 3D model of the miner's insides,
    sensor gauges and a minting ticker.
    Live anti-cheat: removing a plant, adding a fake plant or reusing a sticker is caught on
    screen.
    Real miner software fed by simulated sensor data, minting real AIRcoin on a blockchain
    testnet.
    A wallet and marketplace where an owner sells AIRcoin and a company buys and burns
    it for compliance.

Users.

User                                       What they do
Miner owner (citizen, housing society,
school)                                    Buys the miner, plants and tags up to 20
Polluting company / factory                plants, earns and sells AIRcoin

Regulator (government / pollution control  Buys AIRcoin and burns it to meet a
board)                                     compliance obligation

                                           Sets obligations, registers miners, audits
                                           mints and burns

                                                                                       Page 1 of 21
AIRcoin -- Product Requirements Document  What they do

  User                                    Runs the validator, calibration and
  AIRcoin operator (our team)             marketplace

2. Real-world system concept

This is the full product we pitch. Section 3 says which parts the hackathon builds for real.

2.1 The miner (hardware)

Part      Suggested component                      Purpose
Compute   Raspberry Pi 4 (4 GB) or Pi 5
Camera    Pi Camera Module 3 NoIR Wide + blue      Runs vision, estimation and signing
          gel filter
GPS                                                Reads stickers, sizes plants; NoIR
          u-blox NEO-6M / NEO-M8N over UART        enables a plant-liveness (NDVI)
Wi-Fi                                              check
Air       Pi on-board Wi-Fi
sensors   PMS5003 (PM2.5/PM10), MQ-135             Fixes the miner's location for anti-
          (gas/VOC), SCD40 (CO), BME280            cheat and local AQI lookup
Security  (temp/humidity/pressure)
          Device key pair in a file (hackathon) /  Sends telemetry and proofs
          ATECC608 secure element (production)     Measures surrounding air;
                                                   hackathon feeds simulated values

                                                   Signs every proof so it can't be
                                                   forged

2.2 The stickers

Each miner ships with 20 printed fiducial stickers (ArUco or AprilTag markers). Every
sticker ID is registered to exactly one miner at sale time. A sticker seen by a different
miner, or by its own miner at a new location, is rejected. This stops owners from moving
the same plants between miners to mint twice.

2.3 The 20 prescribed plants

The owner plants up to 20 species from a fixed list. Together they cover every major
pollutant group: VOCs (benzene, formaldehyde, TCE, xylene), particulates, roadside
gases (NO, SO) and CO. The list mixes indoor plants with the stronges
... [45,391 more characters in session.jsonl]

#### ASSISTANT

_[empty]_

_stop `null` · 495ms · in 0 · out 0 · cache r0/w0_

