# Example routing policies (Season 2, the transition season)

Season 2 is a transition: same harness, scenarios and consensus as Season 1, new competition object (routing policies). SN11's next stage is RSI infrastructure (see docs/ROUTING_POLICY.md).

Each directory is the non-SKILL.md part of a pack. Build a pack with your SKILL.md plus these files:

    trajectoryrl-miner build SKILL.md --policy examples/policies/advisers -o pack.json
    python scripts/eval_pack.py --pack pack.json -o ./eval_output      # local run, your own Engy key

| dir | what it does | measured on the 26 SPEC-24 scenarios (one trial each, 2026-09-18) |
|---|---|---|
| pin | glm-5.3-flash for every call | 22.4 / 26 at $0.63 per session |
| escalate | glm-5.3-flash, switch to kimi-k3 on stall / tool errors / repeats | not yet measured on this set |
| advisers | kimi-k3 writes; three cheap models write notes before every turn | 23.2-23.4 / 26 at $5.3-6.3 |
| sdk_custom | policy.py against the SDK: cheap first, strong + one adviser after turn 12 or a signal | not yet measured |

Reference: pinned kimi-k3 scored 19.7-23.3 at $7.5-8.4 per session; pinned qwen3.8-27b (the Season 1 testee) 19.9-21.1.
