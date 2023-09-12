---
title: Generating random numbers
description: Generating random numbers
copied-description: yes
exl-id: 9a816570-753e-4b05-a6ea-2d4b20ffa3d4
---
# Generating random numbers{#generating-random-numbers}

Hardware random number generators can be used on Linux servers to ensure that sufficient entropy is generated. If the machine cannot generate enough entropy, Adobe Access operations that require a source of randomness will block while waiting for data from `/dev/random`.
