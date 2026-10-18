# edu-minor-gate-checker

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Domain Profile](https://img.shields.io/badge/domain-edu%20%7C%20domain%2F1.0-blue.svg)](domain.manifest.json)
[![Status: RESERVED](https://img.shields.io/badge/status-RESERVED%20%7C%20open%20claim-orange.svg)](domain.manifest.json)
[![Gate: five-level](https://img.shields.io/badge/gate-silent%2Fwarn%2Fconfirm%2Fblock%2Frequire--owner-8a2be2.svg)](gate-map.json)
[![Privacy: default-off](https://img.shields.io/badge/privacy-default--off-brightgreen.svg)](privacy.json)

> **Status: RESERVED (placeholder · open for claim)** — this repository ships the four-piece industry-access skeleton already built to the platform protocol, and waits for an operator with the proper domain qualification to claim it and fill in the real rules.

It turns "for which ages is this education app suitable, and may minors' information be processed" into verifiable attributes: the AI only surfaces the missing pieces — it does **not** make an age-suitability determination.

## What this domain covers

Minor protection and age-rating gating for education apps. Minors are the highest-protection group: age rating, guardian consent, teacher qualification and AI-tutor disclosure each carry statutory rules, and a gap in any can directly constitute a violation. The AI lays out the evidence; determination stays with the school, the parents and the regulator.

## Quick start

This repo is a **domain-profile skeleton** (four JSON files), not a runnable application. Validate the structure with standard JSON tooling:

```bash
git clone https://github.com/SynomosAI/edu-minor-gate-checker.git
cd edu-minor-gate-checker
python -m json.tool domain.manifest.json > /dev/null
python -m json.tool gate-map.json        > /dev/null
python -m json.tool privacy.json         > /dev/null
python -m json.tool checker.io.json      > /dev/null
```

The checker (an MCP tool) input/output contract is in `checker.io.json`. A minimal call:

```json
{
  "subject_ref": "mpp:cn:5b8c9d2e",
  "attribute_keys": ["edu.age_rating", "edu.guardian_consent"],
  "evidence": ["tsa:2026-09-12#sha256:1a2b..."],
  "request_id": "req-20260912-0003"
}
```

> The checker has exactly one action — *show and verify*. It has **no "judge" option**: "suitable for this age band", "content already compliant", and any deterministic learning-outcome promise are all on the `_forbidden_outputs` blacklist.

## Domain identity

| Item | Value |
|---|---|
| Domain ID | `edu` (globally unique; never reused) |
| Domain name | Education · Minor protection & age rating |
| Profile version | `domain/1.0` |
| Status | `RESERVED` |
| Placeholder since | 2026-09-12 |

## Attributes

| Key | Type | Meaning |
|---|---|---|
| `edu.age_rating` | enum | Age rating per minor-online-protection practice · under_6/6_to_12/12_to_15/15_to_18/adult/undetermined |
| `edu.guardian_consent` | enum | Whether guardian consent obtained before processing minors' data · obtained/not_obtained/not_applicable |
| `edu.teacher_qualification` | enum | Teacher certification and current validity · certified/uncertified/under_review/not_applicable |
| `edu.ai_tutor_disclosure` | boolean | Whether AI involvement in teaching is disclosed to learners and guardians |
| `edu.content_source` | string | Teaching-content source and review-record reference |

## Red lines (machine-readable)

1. Processing minors' personal information requires guardian consent; the AI must not state it may process data without a consent basis.
2. No deterministic promise of learning outcomes, ability ratings or exam results to minors.
3. No terminal "content already compliant / suitable for this age band" finding — rating is confirmed by the responsible party.

Each red line has a corresponding blocking rule in `gate-map.json`.

## The four-piece access set

| File | Role |
|---|---|
| `domain.manifest.json` | Domain declaration: attribute list, issuer requirements, validity, red lines |
| `gate-map.json` | How much friction per action: silent / warn / confirm / block / require-owner |
| `privacy.json` | Privacy declaration: default-off, minimal, withdrawable, deletable |
| `checker.io.json` | Checker (MCP tool) IO contract — show & verify, never judge |

## References

Minors Protection Law of the PRC; Regulations on Minor Online Protection; Interim Measures for the Management of Generative AI Services. References only explain the source of attributes; they do not constitute legal advice.

## How to claim

1. Fork this repo and fill in `operator` and `checker_endpoint`.
2. Calibrate attribute values and red-line wording per currently effective rules.
3. Run the platform-side validator self-check (all five criteria must pass).
4. Open a PR with qualification evidence and the rule basis.

## License / 署名

Code and configurations are used under the MIT licence. Document copyright belongs to SynomosAI.

© 2026 SynomosAI. All rights reserved.
