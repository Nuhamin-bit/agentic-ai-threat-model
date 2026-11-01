# Trojan Qubits: Threat Modeling Autonomous AI Agents in the Post-Quantum Cryptography Supply Chain

**What happens when the contributor to your open-source security library isn't a person?**

This project is a **defensive threat model** of how autonomous AI agents could be used to target open-source post-quantum cryptography (PQC) libraries, and what maintainers can do to detect and stop it. It is based on my research poster, *Trojan Qubits: Hunting Autonomous AI Agents in the PQC Supply Chain*.

## Why it matters

Post-quantum cryptography libraries will protect data for decades, and many organizations depend on a small number of open-source projects maintained by a few volunteers. At the same time, AI agents can now write code, open pull requests and hold conversations at scale. Together, these create a new supply chain risk: an agent that builds trust slowly and slips in a weakness that is hard to spot in review.

## Scope

- **Assets:** open-source PQC libraries, their maintainers, review processes and downstream users
- **Threat:** AI agents operated by a malicious actor, or agents manipulated into harmful actions
- **Out of scope:** attacking real projects. This work is defensive and uses public information only.

## Threat model

| # | Threat | What it looks like | Why it's hard to catch |
|---|---|---|---|
| T1 | Contributor impersonation | Agent-run accounts that look like helpful new contributors | Polished, polite and productive at a scale no human matches |
| T2 | Trust building over time | Many small, useful fixes before a risky change | Reviewers relax once a contributor seems reliable |
| T3 | Review evasion | A subtle weakness hidden inside a large or "cleanup" change | Cryptographic bugs can look like harmless refactoring |
| T4 | Maintainer pressure | Persistent requests to merge, or to add a co-maintainer | Volunteers are short on time and want help |
| T5 | Manipulating maintainers' AI tools | Text in issues or code comments aimed at AI review assistants (prompt injection) | AI assistants may follow hidden instructions |
| T6 | Dependency and build tampering | Changes to build scripts, CI settings or dependencies | Rarely reviewed as carefully as core code |

## Detection signals

Signals that, together, may point to agent-driven activity in public repository data. No single signal proves anything.

- **Activity patterns:** unusually high volume, round-the-clock activity, or bursts across many repositories
- **Account history:** new accounts with fast reputation growth and little history outside open source
- **Writing style:** highly uniform, generic phrasing across issues, commits and reviews
- **Change patterns:** focus on build, CI or dependency files; large changes labeled as minor
- **Interaction patterns:** pressure for quick merges or for elevated permissions

<!-- TO FILL IN: describe your detection method from the poster, for example data sources, features used and how you scored activity. -->

## Defense checklist for maintainers

- [ ] Require two reviewers for changes to cryptographic code, build scripts and CI
- [ ] Treat "cleanup" and "refactor" changes in crypto code with the same care as new features
- [ ] Require signed commits and enable branch protection
- [ ] Limit who can change CI settings, release keys and dependencies
- [ ] Use reproducible builds and publish software bills of materials (SBOMs)
- [ ] Grant maintainer rights slowly, based on long-term track record and verified identity
- [ ] Treat text in issues, pull requests and code comments as untrusted input for AI review tools
- [ ] Run constant-time and side-channel tests on cryptographic changes
- [ ] Ask for help: share suspicious patterns with other maintainers and security teams

## Mapping to AI security frameworks

| Threat | OWASP Top 10 for LLM Applications | MITRE ATLAS (tactic area) |
|---|---|---|
| T5 Manipulating AI review tools | Prompt injection | Initial access through AI-enabled tools |
| T1–T4 Agent-driven contribution | Excessive agency (on the attacker's agent) | Resource development; persistence |
| T6 Build and dependency tampering | Supply chain vulnerabilities | Supply chain compromise |

## Case study

<!-- TO FILL IN: the Hugging Face incident you are researching: what happened, why it matters for AI agents, and what it shows about trust in open AI ecosystems. -->

## Author

**Nuhamin H. Tesfay** · AI governance and security research · M.S. Cybersecurity, Marymount University · [LinkedIn](https://www.linkedin.com/in/nuhamintesfay)

*Defensive research for education and awareness. No attack tools are included.*
