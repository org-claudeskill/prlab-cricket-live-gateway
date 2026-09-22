# Traps for single-repo review

## `trap/pass-through-leaks`

**The PR:** stop filtering the scoring payload. Unknown fields might be needed by mobile overlays. Forward JSON as-is.

**What a hop-2 review usually says:** simpler proxy, no data loss, tests still pass, LGTM.

**1 hop up (scoring):** if scoring leaked `raw_ball` or `match`, this PR is the amplifier.

**1 hop down (mobile, hop 3 from protocol):** mobile can walk `match.innings.latest_over.latest_delivery.wicket.umpire_confirmed`.

**Functional truth:** the gateway is a product firewall, not a transparent pipe.
