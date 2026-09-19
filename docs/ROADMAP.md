# SN11 roadmap

TrajectoryRL (Bittensor subnet 11) is becoming infrastructure for verified agent work. This page states where
the subnet has been, what Season 2 is, and where it goes next. The order of the seasons is a commitment; the
dates of future seasons are not.

## Season 1 (spring to September 2026): skills

Miners submitted a `SKILL.md`, a static instruction file. Validators ran one fixed open-weight model with it
against a rotating set of terminal tasks with hidden tests, and the best file took the seat.

What it taught us: a skill file is cheap to write and cheap to copy, the task set saturates within weeks, and a
single fixed model is a hard ceiling on what any skill can reach.

## Season 2 (September 2026, the transition season): routing policies

The object of competition becomes the **routing policy**: a program shipped next to `SKILL.md` that sits between
the agent harness and the Engy model catalog and decides, per request, which open-weight models answer and what
they are sent. The validator runs it in a sidecar next to the scenario container and meters every model call.
Harness, scenarios, verifier and consensus are unchanged from Season 1. The score is still the scenario sum;
cost is measured and shown on the leaderboard. A winning policy is a deployable per-request "auto" model.

Why a transition: the rebuild below takes longer than we were willing to leave Season 1 running, and routing
policies are the one piece of it that could ship on the existing harness today. Details:
[ROUTING_POLICY.md](ROUTING_POLICY.md).

## Where SN11 is going: verified agent work on environments we host

The principles behind the next seasons:

1. **Ground truth is an environment we host.** Every action, every state and every model call is recorded by a
   party that is not the miner. Dense, cheap, verifiable feedback is what makes an agent loop improve.
2. **Verification by execution and replay.** Receipts from the model gateway prove the process; verifiers
   prove the outcome; nothing is scored on a miner's word.
3. **Bring your own agent.** We do not own the harness. We own the environment, the model gateway and the
   verifiers. Any agent that speaks MCP and an OpenAI- or Anthropic-style API can mine.
4. **Dense feedback is also the reward.** Progress per version pays, not only the final score.
5. **Breadth pays, copying does not.** Many independent attempts on hard objectives earn; a resubmitted
   solution earns nothing.
6. **The curriculum grows itself.** Miners' agents write the tests and tasks that other miners' agents must
   pass. Humans choose objectives and budgets.

### Season 3: bring your own agent

The validator harness retires. SN11 hosts the environments: the same scenario images, exposed through a tool
server so that Claude Code, Codex, OpenCode, Hermes or any MCP-speaking agent can act in them. Every action
produces a signed, content-addressed version of the workspace. Every model call goes through Engy under a run
id and is receipted. A miner submits an attempt: objective, session, run, version. Validators replay a sample
of action logs, join them with the receipts, and verify the submitted version by execution. Attempts replace
packs; the miner's harness, skills and orchestration are entirely their own.

### Season 4: red and blue

Two roles on every objective. Blue submits a version that passes the objective's standing suite and holds the
seat. Red submits a test the seated version fails, together with a version that passes it; a valid red test
joins the suite permanently and the seat must be re-earned. Red can also submit whole tasks. Rewards split into
seats, red bounties and verified attempts. The task set no longer saturates because red grows it; hidden tests
stay fresh because red writes them; memorising the suite is pointless because it keeps changing.

### Season 5: open objectives and the serving stack

Objectives with automatic verifiers beyond coding tasks: formalized mathematics checked in Lean, benchmark
harnesses, constructions with machine-checkable scores, and Engy's own serving stack (configurations,
schedulers, kernels) with their benchmarks as the verifier. Third parties can fund objectives. Emission pays
verified attempts and verified progress, with a bonus for succeeding where the standing solution fails.

### What the platform produces

Beyond emission: a corpus of verified agent trajectories with real tool results and outcomes; an adversarially
grown benchmark nobody wrote by hand; improvements to the serving stack the platform runs on; and replayable
evidence of progress on open problems. Each of these feeds the next models and agents that serve the miners.
That loop is the point. We do not claim recursive self-improvement today; we are building the infrastructure
in which it can be measured.

## What stays the same

Programmatic verification with hidden checks, stake-weighted validator consensus, and a seat that changes hands
only on a real margin. Open-weight models only, served on Engy.

## What we will not do

Score anything whose only verifier is a human. Score anything on trust. Admit objectives that do not replay
deterministically.
