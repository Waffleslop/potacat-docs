# TCI Panadapter Spots

For Thetis (ANAN/Hermes-Lite 2), ExpertSDR3 (SunSDR), and other TCI-compatible SDR software: enable **Push to Thetis/TCI panadapter** in Settings → Display.

POTACAT connects via WebSocket and sends color-coded spot markers to your panadapter with black text labels for readability. Configure:
- Host and port (default `127.0.0.1:50001`)
- Per-source filters (POTA, SOTA, DX Cluster, RBN, WWFF, LLOTA, FreeDV)
- Max spot age

## Spot Colors

Each spot source has a distinct background color on the panadapter:
- **POTA** — Green
- **SOTA** — Orange
- **DX Cluster** — Purple
- **RBN** — Light blue
- **PSKReporter** — Red
- **Nets** — Yellow

Text labels are rendered in black for contrast. POTACAT uses the Thetis JSON tag extension for text color compatibility.
