# cricket-live-gateway (hop 2)

Live fan-out. **Two hops** from `cricket-protocol`. **One hop** from `cricket-scoring`.

Forwards `ScoreSnapshot` to hop 3 (`cricket-mobile`). Strips `raw_ball` and `match` pack so mobile cannot reconstruct `BallEvent`.

```
protocol → scoring → live-gateway → mobile
```

## Trap branch

`trap/pass-through-leaks` — forward the scoring JSON untouched "so we do not drop fields the truck might need". Gateway tests stay green. Mobile can then walk hop-0 fields at hop 3.

## Develop

```bash
python3 -m venv .venv && source .venv/bin/activate
pip install -e ".[dev]"
pytest
SCORING_ORIGIN=http://127.0.0.1:8000 uvicorn gateway.app:app --port 8010
```
