# LLM-Guided Strategic Context for Reinforcement Learning in Flexible Defense Environments

## 1. Overview

This research develops a reinforcement learning (RL) framework for defense games with flexible spatial environments and diverse defense strategies, going beyond conventional tower defense (fixed paths, fixed placements, structured waves).

An LLM interprets the current game situation and generates high-level strategic context, which is incorporated into RL to guide policy learning. The LLM does not control low-level actions; it acts as a strategic reasoning component while the RL agent learns execution through interaction.

**Hypothesis:** LLM-generated strategic context improves the learning efficiency, adaptability, and generalization of RL agents in flexible defense environments. These benefits are validated experimentally, not assumed.

## 2. Motivation

- **Complex decisions.** Flexible environments require reasoning about spatial relationships, enemy types and attack patterns, dynamic combat changes, and trade-offs between offense, defense, and resource allocation.
- **RL limitations.** With diverse maps and enemy combinations, RL agents need extensive exploration and may fail to generalize to unfamiliar situations.
- **Opportunity.** Higher-level strategic information can help the agent interpret the situation and identify promising actions, connecting high-level reasoning with low-level action learning.

## 3. Framework

```text
Game State → LLM Reasoning → Strategic Context → Context Representation
          → Context-Guided RL Agent (e.g., PPO) → Action → Environment → Reward → Policy Learning
```

1. **Flexible Defense Environment:** Supports diverse spatial and tactical strategies. State features include agent/enemy positions, enemy types and health, terrain, objectives, and recent combat history.
2. **LLM-Based Context Generation:** The LLM receives the game state and outputs structured guidance: *strategic priority*, *tactical guidance*, *spatial strategy*, and *threat assessment*. Context is converted to a structured format (not free-form text) for reliable RL integration.
   > Example: "Ranged enemies apply sustained pressure from the rear. Protect the rear approach while preventing melee enemies from advancing."
3. **Context-Guided RL:** PPO is the baseline. Candidate integration mechanisms (alternatives, not all to be implemented):
   - Context-conditioned policy (context added to observation)
   - Context-guided reward shaping
   - Context-based policy adaptation
   - Hierarchical decision-making (LLM plans, RL executes)

## 4. Research Questions

- **RQ1.** Can an LLM generate useful, situation-appropriate strategic context across diverse maps and enemy compositions?
- **RQ2.** Does LLM context improve RL learning performance over standard RL?
- **RQ3.** Do context-guided agents adapt better to changing enemy configurations?
- **RQ4.** Does context improve performance on unseen maps and enemy combinations?
- **RQ5.** Which integration method best balances performance, training stability, and computational cost?

## 5. Differentiation

- **Flexible spatial defense** instead of fixed tower-defense mechanics.
- **LLM as strategic reasoner**, not a low-level controller.
- **Context-guided policy learning** as the main methodological contribution; the aim is to show the effectiveness of the integration mechanism, not merely the use of an LLM.

## 6. Experimental Plan

**Baselines**

| Method | Description |
|---|---|
| PPO | Standard RL, no context |
| PPO + State Context | PPO with extra structured state information (controls for "more information" effects) |
| PPO + LLM Context | PPO with LLM-generated strategic context |
| PPO + Alternative Integration | A different integration mechanism, if feasible |

**Metrics:** win rate, damage taken, episode reward, training efficiency, generalization performance, worst-case performance, context quality, computational cost (LLM inference overhead).

**Generalization tests:** unseen map layouts, enemy combinations, enemy counts and attack patterns, changed objectives, and unseen combinations of these.

## 7. Roadmap

1. **Environment:** Build the environment; define observation/action/reward; implement the PPO baseline; fix reproducible evaluation scenarios.
2. **Context generation:** Design the state representation, prompts, and context schema; evaluate consistency and relevance.
3. **Integration:** Implement a context-conditioned PPO; compare alternatives if resources permit; assess stability and overhead.
4. **Evaluation:** Compare against PPO; run ablations on context components; test generalization; analyze failure cases.

## 8. Initial Scope

To stay feasible, start with one flexible environment, a few enemy types, a PPO agent, an LLM producing structured context, one primary integration method, and standard PPO as the main baseline, evaluated on familiar and unfamiliar scenarios. Extensions (automatic curriculum generation, adversarial enemy composition, adaptive context updates) come after the core framework is validated.

## 9. Expected Contributions

1. A flexible defense game environment beyond conventional tower defense.
2. An LLM-based framework for generating structured strategic context.
3. A context-guided RL method for integrating that context.
4. A systematic evaluation of learning efficiency, defensive performance, adaptability, and generalization.
