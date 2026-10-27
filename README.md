# Monte Carlo Option Pricing

Monte Carlo pricing of European and barrier options under geometric Brownian motion (GBM), with Black-Scholes validation, finite-difference Delta estimation and interactive Streamlit apps.

Built for the Financial Computation course at Soochow University (Feb – Jun 2026). Code comments and written conclusions are in Traditional Chinese.

## What's inside

| Folder | Question | Key methods |
| --- | --- | --- |
| [`01_vanilla_call_volatility`](01_vanilla_call_volatility) | How does a European call price change with volatility σ? | Monte Carlo pricing, Black-Scholes benchmark, moment matching |
| [`02_delta_forward_difference`](02_delta_forward_difference) | How accurate is a forward-difference Delta for different step sizes h? | Finite differences, analytical Delta, error analysis |
| [`03_barrier_options`](03_barrier_options) | How do down-and-out / down-and-in call prices and Deltas change with the barrier level? | Path simulation (252 steps / year), in-out parity check |

Each folder contains:

- a main analysis script
- `seed_comparison.py`: fixed vs. unfixed random seed (reproducibility vs. sampling noise)
- `moment_matching_comparison.py` (folders 01, 02) or `barrier_delta.py` (folder 03)
- `app.py`: an interactive Streamlit app for adjusting parameters and viewing results live

Base parameters: S0 = 100, K = 100, r = 0.02, T = 0.5, σ = 0.2, 1,000 paths, seed = 42.

## Results

**Call price rises with volatility.** The simulated price tracks the expected positive relationship across σ = 0.1 – 0.6.

![Call price vs volatility](images/price_vs_volatility.png)

**Forward-difference Delta needs a sensible step size.** For very small h (below about 1e-13), floating-point error dominates and the estimate breaks down. For large h (above about 1), truncation error grows. In between, the estimate stays close to the analytical Delta.

![Delta vs step size](images/delta_vs_step_size.png)

**Barrier level matters most near the spot price.** As the barrier B approaches S0, the down-and-out call loses value and the down-and-in call gains value. Their sum stays equal to the vanilla call (in-out parity).

![Barrier option price vs barrier level](images/price_vs_barrier.png)

## Run it

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt

# analysis scripts
python 01_vanilla_call_volatility/price_vs_volatility.py

# interactive apps
streamlit run 03_barrier_options/app.py
```

## Tech

Python · NumPy · SciPy · Matplotlib · Streamlit
