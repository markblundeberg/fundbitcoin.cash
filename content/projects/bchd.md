---
title: bchd
type: docs
weight: 3000
---

Homepage: https://bchd.cash/

Source Repository: https://github.com/gcash/bchd

Maintainer: Chris Pacia

Other Team Members: Josh Ellithorpe, Tyler, Emergent Reasons

# About

Bchd is an alternative full node bitcoin cash implementation written in Go (golang).

This project is a port of the btcd codebase to Bitcoin Cash. It provides a high powered and reliable blockchain server which makes it a suitable backend to serve blockchain data to lite clients and block explorers or to power your local wallet.

The bchd team also maintains Neutrino, an advanced spv mobile wallet, and has made new updates including sync improvements, utxo commitments, utxo cache, address indexing, and a grpc public api.

bchd does not include any wallet functionality by design as it makes the codebase more modular and easy to maintain. The bchwallet is a separate application that provides a secure Bitcoin Cash wallet that communicates with your running bchd instance via the API.
