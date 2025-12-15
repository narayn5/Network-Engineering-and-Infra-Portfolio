- `debug spanning-tree events`
- `show spanning-tree transitions`

Monitor in real-time:

- Disable trunk: `shutdown` on Gi0/48
- Watch convergence (seconds in RSTP vs 30-50 in traditional STP)
- Re-enable: `no shutdown`
- Verify alternate port becomes forwarding
