# PandaWorld - An execution layer for agents in world models

## Opening

AI is shifting from language to worlds.

Systems like AMI, DeepMind's embodied agents, and World Labs focus on
learning:

state(t) → state(t+1)

These are world models --- they predict how reality evolves.

But a critical question remains:

how do agents actually operate inside these worlds?

PandaWorld answers that.

------------------------------------------------------------------------

## The missing layer

A world model gives you dynamics:

nextState = worldModel.predict(state, action)

But it does not define:

-   who chooses the action
-   at what level (goal vs motor control)
-   how planning and control interact
-   how multiple systems coordinate

------------------------------------------------------------------------

## PandaWorld

PandaWorld is an execution architecture for agents inside world models.

It defines how to combine:

-   LLMs → planning (goals, reasoning)
-   policies (NN / RL / controllers) → acting
-   world models → dynamics (T → T+1)

------------------------------------------------------------------------

## Core principle

Separate:

-   reasoning
-   control
-   world dynamics

Instead of merging everything into one model.


## Architecture
<img src="./images/architecture.svg" width="400"/>


## Key insight

World models predict the future. PandaWorld defines how agents act
within it.


## Example (rover)

await world.reset()

await planner.setMission( "Explore ridge, inspect anomalies, return if
battery \< 25%" )

while (!done) { const obs = sensors.read() const action =
controller.act(obs) await world.step(action) }


## Why this matters

Current approaches split into two extremes:

LLM-driven agents: - slow - unstable - not grounded

RL / robotics systems: - strong control - limited high-level reasoning


## PandaWorld bridges both

-   LLM handles what to do
-   policies handle how to do it
-   world model handles what happens next


## Relation to current work

World models: - learn environment dynamics (T → T+1)

Policies: - learn action selection

LLMs: - perform reasoning and planning


## PandaWorld's role

The control layer that turns these components into a working agent.

## Design principles

-   LLM is not in the control loop
-   World is a first-class abstraction
-   Policies are pluggable
-   Compatible with learned world models or simulators
-   Supports multi-agent systems
-   Deterministic and replayable


## What this enables

-   agents operating inside learned world models
-   LLM + RL hybrid systems
-   robotics simulation and control
-   simulation-to-real pipelines
-   safe autonomous systems

## Positioning

World models learn dynamics. PandaWorld defines agency.


## Short version

A runtime for agents where: - world models predict - policies act - LLMs
plan


## Roadmap

-   Rover environment
-   SpikyPanda integration
-   World model adapter
-   MCP interface
-   Multi-agent support
-   Training loop


## Closing

The next step after world models is not bigger models.

It is structured agents that can live inside them.
