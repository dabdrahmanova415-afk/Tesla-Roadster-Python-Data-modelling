#  The Tesla Roadster "SpaceX Package" — a Cold-Gas Thruster Feasibility Study

A Python model that puts Tesla's viral "flying Roadster" demo through an independent
physics audit: thermodynamics, an ODE flight simulation, numerical optimization — then
stress-tested against a real production car and a classic movie car, just to see how far
the idea can be pushed.

> Built as a project for the **Data Modelling** course, University of Messina (UniMe).

---

##  Why this exists

When Elon Musk unveiled the next-gen Roadster, it lifted off, hovered, flipped mid-air,
and landed — using cold-gas thrusters, not wings or jets. This repo answers, with code
instead of marketing copy:

- How fast does the thruster exhaust actually move, and how much thrust does that buy?
- How long can a ~2,000 kg car actually stay off the ground on a given gas supply?
- How light would the car need to be for a *meaningful* hover?
- Does the same trick scale to an everyday SUV?
- What would it take to do this with **sustained**, continuous flight instead?

---

##  Methodology

| Step | Physics / Tool | What it answers |
|---|---|---|
| 1. Thermodynamics | Ideal Gas Law (`PV = mRT`) + Saint-Venant–Wantzel adiabatic expansion | Exhaust velocity, stored gas mass, required thrust |
| 2. Flight simulation | Newton's 2nd Law as an ODE, `scipy.integrate.solve_ivp` (Runge-Kutta) | Altitude & velocity, second-by-second, including drag |
| 3. Inverse optimization | `scipy.optimize.brentq` root-finding | What vehicle mass hits a target hover time? |
| 4. Scaling test | Ideal Gas Law run backwards | Tank volume needed to hover an ordinary SUV |
| 5. Sustained-flight model | Piecewise thrust ODE | What continuous power would true hovering need? |

---

##  Key results

| Scenario | Result |
|---|---|
| Baseline Roadster (2,000 kg, 100 L tank @ 300 bar) | **1.25 s** hover before free-fall |
| Exhaust velocity | 687.8 m/s |
| Mass needed for a 10 s hover (same tank) | **250.09 kg** — lighter than a motorcycle |
| Alfa Romeo Stelvio (2,000 kg) hovering 10 s | needs **285 kg** of gas → **800 L** tank (its trunk is only 525 L) |
| DeLorean DMC-12, sustained "Hover Mode" | needs **5.88 MW** of continuous power — hence *Mr. Fusion* |

**Bottom line:** cold-gas thrusters can produce a brilliant, brief ballistic stunt — but
scaling the gas supply for *any* meaningful hover time runs straight into a closed-loop
mass/volume paradox, on a stunt car or a daily driver alike.

---

##  Installation

```bash
git clone https://github.com/<your-username>/tesla-roadster-feasibility.git
cd tesla-roadster-feasibility
pip install -r requirements.txt
```


##  Notable insight

The DeLorean's "Hovering Phase" isn't actually flat — when thrust exactly equals weight,
*acceleration* is zero, but Newton's First Law keeps the velocity gained during takeoff.
The car keeps climbing at a constant speed. Real "Hover Mode" is secretly **Cruise Mode**;
a true stationary hover needs the flight computer to trim thrust to ~99% of weight.

---

## 📄 License

MIT — see [LICENSE](LICENSE).
