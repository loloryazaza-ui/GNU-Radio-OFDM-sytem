# OFDM System Implementation on HackRF One with GNU Radio

This repository contains the complete implementation of an OFDM (Orthogonal Frequency Division Multiplexing) transceiver system developed as part of a master's thesis. The system includes simulation models and real hardware implementations using HackRF One SDR platforms.

## Repository Structure
### `simulation/`
- **`1_simple_ofdm/`** – Basic OFDM system (GNU Radio tutorial example)
- **`2_extended_tx/`** – Extended transmitter model
- **`3_extended_rx/`** – Extended receiver model
- **`4_complete_system/`** – Full extended transceiver system
- **`5_real_radio_channel/`** – Extended model for real radio channel (HackRF One / other SDR)
- **`6_single_computer/`** – Both HackRF One on one computer (shared sync)
- **`7_two_computers/`** – HackRF One on two independent computers
- **`8_results/`** – Experimental data, graphs, constellation screenshots
## Description

### Simulation Directory (`/simulation`)

This directory contains four progressively complex OFDM models:

| Folder | Description |
|--------|-------------|
| `1_simple_ofdm/` | Basic OFDM implementation based on the official GNU Radio tutorial. Demonstrates fundamental principles. |
| `2_extended_tx/` | Extended transmitter with custom preamble, pilot carriers, header/payload formatting, and CRC32 generation. |
| `3_extended_rx/` | Extended receiver with Schmidl–Cox synchronization, CFO correction, channel estimation, equalization, and CRC32 check. |
| `4_complete_system/` | Full extended transceiver combining the extended transmitter and receiver. |

### Real Radio Channel Directory (`/real_radio_channel`)

This directory contains the hardware‑tested system using two HackRF One SDR platforms.

| Folder | Description |
|--------|-------------|
| `single_computer/` | Both HackRF One connected to the same computer. Provides shared synchronization (common clock via USB hub / same host). |
| `two_computers/` | Each HackRF One connected to its own independent computer. No shared synchronization – relies entirely on the Schmidl–Cox algorithm. |
| `results/` | Experimental results including packet loss rates, BER measurements, EVM values, signal constellation screenshots, and spectrum plots. |

## Key Features

- **Modulation:** BPSK (header) and BPSK (payload)
- **FFT size:** 64
- **Cyclic prefix length:** 16 samples (1/4 of the symbol)
- **Occupied carriers:** 52 (IEEE 802.11a‑like)
- **Pilot carriers:** 4 (at indices -21, -7, 7, 21)
- **Synchronization:** Schmidl–Cox algorithm (both coarse and fine)
- **Channel estimation:** Based on long preamble and pilot tones
- **Equalizer:** Simple decision‑feedback equalizer (OFDM‑simpledfe)
- **CRC:** CRC‑32 for packet integrity check

## Requirements

- GNU Radio 3.10 or later
- Python 3.11+
- HackRF One (for hardware experiments)
- SoapySDR / gr‑osmosdr
- NumPy, SciPy, Matplotlib (for data analysis)
- O.S. Windows 10 pro, Dragon OS noble 24.04 

## Quick Start

### Simulation

1. Open the corresponding `.grc` file in GNU Radio Companion.
2. Generate the Python script and run it.
3. Monitor BER, EVM, and packet loss via the QT GUI sinks.

### Hardware (Real Radio Channel)

1. Load the transmitter flow graph on one computer (or one instance).
2. Load the receiver flow graph on the second computer (or second instance).
3. Configure the HackRF One parameters (frequency, gain, sample rate).
4. Start the transmitter, then start the receiver.
5. Collect results from the file sinks or real‑time visualizers.

## Results Summary

| Model / Configuration | Packet Loss | BER | EVM | Notes |
|-----------------------|-------------|-----|-----|-------|
| Simulation (AWGN, no noise) | 1.6% | ≈0% | 0% | Baseline reference |
| Real channel, 446 MHz, shared computer | 21.2% | 35.2% | 0% | Satisfactory |
| Real channel, 446 MHz, two computers | 15.3% | 40.4% | 0% | Synchronization works |
| Real channel, 2.4 GHz (both configurations) | ≈97% | ≈37% | 0% | High interference in ISM band |

> EVM = 0% indicates that for successfully received packets, demodulation is error‑free.

## Repository Status

- **Simulation models:** ✅ Completed and tested
- **Hardware tests (446 MHz):** ✅ Completed
- **Hardware tests (2.4 GHz):** ✅ Completed
- **Open source code:** ✅ Fully available

## License

This project is licensed under the **GNU General Public License v3.0 (GPLv3)**

This license is compatible with GNU Radio (GPLv3) and ensures that all derivative works remain open source.

## Author

[Mikhail]  
[06.2026]

