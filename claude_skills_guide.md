# The Complete Guide to Building Skills for Claude

## Table of Contents
- Introduction  
- Chapter 1: Fundamentals  
- Chapter 2: Planning and Design  
- Chapter 3: Testing and Iteration  
- Chapter 4: Distribution and Sharing  
- Chapter 5: Patterns and Troubleshooting  
- Chapter 6: Resources and References  

---

# Introduction

A **skill** is a set of instructions packaged as a folder that teaches Claude how to perform specific workflows.

## Why skills matter
- Avoid repeating instructions every time  
- Encode domain knowledge once  
- Enable consistent workflows  

## Common use cases
- Frontend generation from specs  
- Research workflows  
- Document generation  
- Multi-step orchestration  

---

# Chapter 1: Fundamentals

## What is a skill?

A skill is a folder:

```
your-skill/
├── SKILL.md
├── scripts/
├── references/
└── assets/
```

## Core Design Principles

### Progressive Disclosure
1. YAML frontmatter  
2. SKILL.md body  
3. Linked files  

### Composability
Multiple skills can run together.

### Portability
Works across Claude.ai, Claude Code, and API.

---

# Chapter 2: Planning and Design

## Start with use cases

Example:

```
Use Case: Sprint Planning

Trigger: "plan sprint"

Steps:
1. Fetch data
2. Analyze capacity
3. Suggest priorities
4. Create tasks

Result: Planned sprint
```

## Skill categories
1. Document & Asset Creation  
2. Workflow Automation  
3. MCP Enhancement  

---

# Chapter 3: Testing and Iteration

## Testing methods
- Manual  
- Scripted  
- API  

## Testing focus
- Trigger correctness  
- Functional output  
- Performance improvement  

---

# Chapter 4: Distribution and Sharing

## Installation
1. Download  
2. Zip  
3. Upload  

## API usage
- /v1/skills  
- container.skills  

---

# Chapter 5: Patterns and Troubleshooting

## Patterns
- Sequential workflow  
- Multi-MCP coordination  
- Iterative refinement  
- Context-aware decisions  
- Domain intelligence  

## Troubleshooting
- YAML errors  
- Trigger issues  
- MCP connection problems  

---

# Chapter 6: Resources

## Documentation
- Skills docs  
- API reference  
- MCP docs  

## Tools
- skill-creator  

---

# Appendix: YAML Example

```
---
name: skill-name
description: What it does and when to use it
---
```
