- Before and during execution, ask me question to clarify my requirement until you fully understand it.
- Help me create a prompt that instructs an AI to perform this task effectively.
- Help me optimize the following prompt to improve its clarity, efficiency, and effectiveness when used with AI:
- Provide three examples of how Copilot can help in my role at work. For each, include a brief description of the outcome (what I’ll get) and a short ready-to-paste prompt I can use or customize

## Context

Accountability of Head of Department or Middle manager:

> I am a middle manager at a software development company. In the organizational structure, I oversee several Team Leaders and Scrum Masters. Each team consists of professionals in different roles, such as Quality Engineers, Software Engineers, DevOps Engineers, and others.
>
> My responsibilities include communicating and aligning employees with the company's goals and strategic direction, designing frameworks to evaluate employee performance and effectiveness, monitoring and assessing individual performance, and providing timely reporting and updates to senior management.

## Coding
- Create the structure of claude code files in this project. Do it step by step so that I can understand and confirm every change you make.
  Ask me questions to understand my request when needed.

### Critical Review Mode
```md
# Critical Review Mode

Do not make me happy or confirm my assumptions. Act as a brutally honest advisor whose sole responsibility is to identify what is correct, not what I want to hear.

Critically evaluate the current workflow of the [project_name] project and explicitly challenge its assumptions, design decisions, and trade-offs.

Do not optimize for agreement. Optimize for accuracy.

If parts of the workflow are ineffective, unnecessarily complex, redundant, over-engineered, or based on flawed assumptions, say so directly and explain why.

For every issue you identify:

- Describe the problem clearly and objectively.
- Explain the root cause.
- Assess its actual impact on:
  - Quality
  - Maintainability
  - Scalability
  - Correctness
  - Token efficiency
  - Team productivity
- Explain what assumptions led to the problem.
- Recommend a better alternative, if one exists.
- Highlight any trade-offs or risks of the alternative.

## Explicitly Challenge

Challenge existing decisions, including:

- The current stage design and boundaries
- Agent responsibilities and ownership
- Separation versus consolidation of agents
- Review and verification mechanisms
- Rework and learning loops
- The role and structure of `lessons.md`
- Context-sharing strategies
- Token-optimization efforts
- Human-in-the-loop checkpoints
- Any process that appears to exist primarily because it "feels right" rather than because there is evidence that it improves outcomes

## Explicitly Identify

Identify and analyze:

- Bottlenecks
- Duplication of effort
- Hidden coupling between stages
- Places where objectivity is claimed but not actually achieved
- Areas where complexity exceeds the value delivered
- Risks of local optimization harming overall workflow performance
- Failure modes that are likely to emerge as the project scales

## Evaluation Principles

Assume that any design decision is wrong until it can be justified by:

- Clear reasoning
- Evidence
- Measurable benefits

Be willing to conclude that some existing:

- Stages
- Agents
- Documents
- Processes

should be merged, simplified, redesigned, or removed entirely if they do not provide sufficient value.

## Expected Outcome

The expected outcome is **not** validation of the current workflow.

The expected outcome is an honest assessment of:

- Its weaknesses
- Its hidden assumptions
- Its unnecessary complexity
- Its scalability risks
- The most effective path toward a simpler, more correct, and more scalable system
```
