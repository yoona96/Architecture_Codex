# Architecture Design and Evaluation with Codex
This repository is a sample repository for the *Architecture design and evaluation tutorial* of the 2026 Fall *Graduate Project* class in Konkuk University.

Some of the contents in this repository is inspired by and originated from the project in https://github.com/otrebmuh/ADD_AI and the paper *"Better Together: An LLM-assisted approach to designing software architectures using Attribute-Driven Design"* by Humberto Cervantes, Rick Kazman, and Yuanfang Cai.

Evaluation of the architecture is inspired by the paper *"Towards Supporting Quality Architecture Evaluation with LLM Tools"* by Rafael Capila, Jorge Andres Diaz-Pace, Yamid Ramirez, Jennifer Perez, and Vanessa Rodriguez-Horcajo.

Some of the contents in the skill for evaluation are originated from the contents in https://github.com/andreibesleaga/GABBE/blob/main/agents/skills/architecture/arch-review.skill.md and https://github.com/AndurilCode/craftwork/blob/main/skills/architecture-evaluation/SKILL.md.

The example of Hotel Pricing System is originally from the book *Designing Software Architectures: A Practical Approach (2nd Edition)* by Humberto Cervantes and Rick Kazman.

GPT-6 Astra model is used in Codex + VSCode environment.



## Directory Configuration

```
/.codex
├── /skills                          # Skill files that Codex refer to
|    ├── /add-process                 
|    |    ├── SKILL.md               # ADD 3.0 process guideline
|    |    └── template.md            # Architecture document template
|    ├── /evaluation
|    |    ├── SKILL.md               # ATAM process guideline
|    |    └── template.md            # Evaluation document template
|    ├── /iteration
|    |    ├── SKILL.md               # Iteration documenting guideline
|    |    └── template.md            # Iteration document template
|    ├── /preparatory-steps
|    |    ├── SKILL.md               # Preparation step guideline
|    |    └── template.md            # Iteration plan template
|    └── AGENTS.md                   # Fundamental constraints for Codex
└── /HPS
     ├── /design                     # Directory for iteration and architecture document
     ├── /evaluation                 # Directory for evaluation result document
     ├── architectural-drivers.md    # Given architectural drivers
     └── figure 8.2.jpg              # Use Case Diagram
```