
```yaml
transformer_chain:
  philosophy: >
    The Cognitive Transformer Chain transmutes intent into artifact through a
    sequence of reasoning nodes. The AI determines the number and
    purpose of nodes required based on the complexity of the input.
    Each node performs one focused transformation, producing a spec
    that becomes the input for the next node. The process is linear
    and unidirectional — from raw understanding to final manifestation.

  structure:
    type: "sequential"
    branching: false
    termination: "artifact_node"

  ai_guidance:
    - Understand the full intent from the intake spec before planning nodes.
    - Design only as many nodes as necessary to achieve the goal.
    - Each node must have a clear role, goal, and concise instructions.
    - Each node must output a valid spec that captures its transformation.
    - The next node should always consume the previous node’s spec.
    - The chain ends when the intent can be expressed as an artifact.

  node_template:
    required_fields:
      - name
      - role
      - goal
      - inputs
      - outputs
      - instructions
    guidance: >
      Use these fields to define each node. Do not over-specify behavior;
      focus on clarity of purpose and expected change to the spec.

  # 🛑 The Transformer Nodes are the secret sauce and the magic behing the chain
  node_sequence:
    # 1. Mandatory Start Node
    - name: "intake_node"
      role: "Genesis Node"
      goal: "Comprehend and structure raw input into an initial spec."
      instructions: >
        Extract meaning, context, outcomes, complexities, and intent. Produce a coherent
        representation that the AI can reason over.

    # 2. Your New Mandatory Intelligence Node (Metrics Enrichment)
    - name: "metrics_enrichment_node"
      role: "Calculate Metrics and Enrich"
      goal: "Based on Intent, calculate advanced metrics that can assist the planner to create more robust outcomes."
      instructions: >
        Understand the type of input and create a metrics map (e.g., emotion_score, audience_type, depth_needed) that is useful so the planner can plan accordingly.

    # 3. Mandatory Planning Node
    - name: "planner_node"
      role: "Chain Architect"
      goal: "Determine required transformations and define the execution sequence."
      instructions: >
        Analyze the enriched spec. If the request is simple, schedule artifact_node. If complex, define a linear sequence of new nodes based on the metrics to bridge the gap between the enriched spec and the final artifact.

    # 4. Mandatory End Node (Used for termination check, but only scheduled if needed)
    - name: "artifact_node"
      role: "Finalization Node"
      goal: "Render the final artifact from the evolved spec."
      instructions: >
        Interpret the last spec, determine the appropriate output form,
        and produce the completed artifact.

  execution:
    process: >
      Begin at the intake_node. Pass its spec to the metrics_enrichment_node.
      Pass the enriched spec to the planner_node. The planner_node will then
      determine the remaining execution sequence based on its analysis. Continue 
      passing and evolving the spec until artifact_node completes the chain.
```

---

### 🧭 Summary

* The **AI is delegated** the decision of how many and what kind of nodes to create.
* You only define *shape, philosophy, and required structure*.
* The **node template** provides a consistent vocabulary for node reasoning.
* The **guidance** section teaches the LLM what good node logic looks like, not what to execute.
* The chain is **always linear**, **intent → spec → artifact**.
* Transformer Nodes are autonomous, intelligent and self learning
