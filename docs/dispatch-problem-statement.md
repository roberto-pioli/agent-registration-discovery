# Agent Registration and Discovery — Problem Statement (for IETF DISPATCH)

## Abstract
Autonomous software agents are increasingly deployed across heterogeneous runtimes and administrative domains.
There is no widely adopted, standardized control-plane mechanism for stable agent identity, discovery, and
capability-driven protocol selection across domains.

## Problem
Modern agents are:
- Ephemeral and mobile across runtimes and clouds
- Implemented by heterogeneous vendors
- Communicating via multiple interaction protocols (e.g., MCP, A2A, HTTP, gRPC) with differing transports and authentication mechanisms

Current practice often relies on:
- Hard-coded endpoints
- Vendor-specific directories/registries
- Infrastructure-bound service discovery

These approaches hinder interoperability and complicate secure cross-domain agent-to-agent interactions.

## Requirements (non-exhaustive)
- Stable, namespaced agent identifiers (AIDs)
- Dynamic endpoint resolution despite mobility
- Capability advertisement sufficient to select interaction protocol and transport bindings
- Strong authentication and authorization for registration and discovery
- Optional federation with policy control and data minimization

## Non-goals
- Task execution semantics or orchestration
- Agent reasoning/planning
- Standardizing tool semantics
