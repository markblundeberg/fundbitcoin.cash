---
title: bchd
type: docs
---

Homepage: https://bchd.cash/

Source Repository: https://github.com/gcash/bchd

Maintainer: Chris Pacia

Other Team Members: Josh Ellithorpe

# About

bchd is an alternative full node bitcoin cash implementation written in Go (golang).

This project is a port of the btcd codebase to Bitcoin Cash. It provides a high powered and reliable blockchain server which makes it a suitable backend to serve blockchain data to lite clients and block explorers or to power your local wallet.

bchd does not include any wallet functionality by design as it makes the codebase more modular and easy to maintain. The bchwallet is a separate application that provides a secure Bitcoin Cash wallet that communicates with your running bchd instance via the API.