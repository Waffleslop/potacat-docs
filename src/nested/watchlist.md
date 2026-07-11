# Watchlist

Enter comma-separated callsigns in Settings → Spot Filters → Watchlist. Spots matching these callsigns show a star icon in the table.

## Band & Mode Filters

You can optionally filter watched callsigns by band and/or mode using colon-separated qualifiers:

| Entry | Matches |
|-------|---------|
| `K3SBP` | Any band, any mode |
| `K4SWL:20m` | Only on 20m, any mode |
| `KI6NAZ:CW` | Any band, CW only |
| `W1AW:40m:SSB` | Only on 40m SSB |

**Example watchlist:**
```
K3SBP, K4SWL:20m, KI6NAZ:CW, W1AW:40m:SSB
```

Band and mode qualifiers can appear in any order after the callsign. Supported bands: 160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, 70cm.

**Notifications:** Enable pop-up and/or sound notifications for watchlist matches in Settings → Spot Filters. Configure auto-dismiss duration. Notifications respect band/mode filters — you'll only be notified when the spot matches your criteria.
