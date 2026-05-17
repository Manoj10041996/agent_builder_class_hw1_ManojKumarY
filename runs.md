# Agent Runs — 5 Sample Questions

## Q1 — Easy (Happy Path)
**Question:** What is the thrust of Falcon 9?
**Tool called:** vehicle_specs
**Final answer:** Falcon 9 generates about 7,607 kN of thrust.

## Q2 — Multi-tool
**Question:** What is the thrust of the rocket used for crewed missions?
**Tools called:** query_launches → vehicle_specs
**Final answer:** The crewed missions all use the Falcon 9, which has a thrust of 7,607 kN.

## Q3 — Ambiguous (Failure Mode)
**Question:** Tell me everything about SpaceX
**Tools called:** query_launches x3 → vehicle_specs
**Final answer:** Hit max_iters=4 without finishing — agent ran in circles.
**Observation:** Vague questions cause the agent to keep fetching data without converging.

## Q4 — Expected to Fail
**Question:** What is the diameter of Saturn V?
**Tools called:** None
**Final answer:** Database only contains SpaceX data, no info on Saturn V.
**Observation:** Agent correctly admitted it doesn't know instead of hallucinating.

## Q5 — Own Choice
**Question:** Which missions failed?
**Tool called:** query_launches
**Final answer:** Falcon 1 Flight 1, CRS-7, Starship SN10, Starship IFT-1 were the failed launches.