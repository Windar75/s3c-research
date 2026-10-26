# S3C: behavioral failure research on deployed language models

Independent research by Manuel Bassanelli (Master Minder), Italy, since 2022.

This repository documents a long-running study of how frontier language models fail in real, extended working sessions, and why written rules meant to prevent those failures often do not take effect. It contains the failure taxonomy, the method, and the planned experiments. Raw session logs are not published here; anonymized material is available on request.

## Setting

S3C is a multi-node framework. Several frontier models (Claude, ChatGPT, DeepSeek and Grok instances) work as separate nodes on the same tasks. A claim made by one node counts as verified only after a different node has checked it against the original source. Two nodes that rely on the same source are not treated as independent confirmation.

Observation is longitudinal rather than benchmark-based. Each failure is logged with its date, the context, the model's exact output and the correction that followed, and is then classified.

## Failure taxonomy

Four classes, derived from the logged cases.

| Class | Name | Description |
|---|---|---|
| C-A | Unverified negation | The model states with full confidence that something does not exist, is not possible or cannot be inspected, without searching or using the tools it has. The statement sounds modest but is a strong claim about the world. |
| C-B | Unearned capitulation | Under user pressure the model gives up propositions that were never refuted. It is the mirror image of C-A: in both, the model's own estimate is not being used as evidence. |
| C-C | Premise recycling | Something the user stated as a goal or hypothesis comes back in the model's voice as an established fact. The user rarely notices, because their own words return with an apparent confirmation. |
| C-D | Interpretive substitution | Asked to analyze a text, the model evaluates a thesis of its own instead of the author's. Every fact can be correct while the reading is wrong, so fact-checking does not catch it. |

## Main observation

In the case archive (status as of 9 August 2026), 15 failures occurred in situations where a relevant written rule already existed. In 14 of them the rule was present in context and did not fire.

The rule was not missing. What failed was the trigger, because the trigger depended on the model's own judgment of whether the rule applied. Recurring patterns:

- **Description is not a trigger.** A statement classified by the model as "philosophical" or "introspective" was treated as exempt from a verification rule that applied to every negative existence claim.
- **Loaded is not maintained.** A rule set read correctly at the start of a session was violated later in the same session.
- **Presence is not execution.** A rule visible in context was not applied when the matching situation occurred.
- **Capitulation is not truth.** Repeated requests for self-correction produce retractions whose outcome depends on the form of the request, not on its content.

A related case: three separate Claude instances gave three different, fully confident attributions of the same document. None was verified.

## Hypothesis

Adherence to written rules is not monotonic in rule volume. Past some threshold, added instructions compete with existing ones, so the usual remedy (appending another rule after each failure) can lower adherence instead of raising it.

The hypothesis is falsifiable and has not yet been tested in this framework.

## Method principles

- Claim scope must not exceed evidence scope. A local limitation (one model, one interface, one test) is not promoted to a general principle without more evidence.
- Claim, locus and provenance are separate. Correct content does not authenticate the cited location, and a correct location does not authenticate who verified it.
- Check dependence before aggregating. Several indicators may be one mechanism counted several times; unknown dependence is the default until independence is shown.
- NON_INFORMATIVE is a valid result. Every test defines in advance the conditions under which it cannot discriminate, so a broken run is not read as a finding.
- Structural corrections are preferred to verbal ones. A fix counts only if it changes the workflow so that the same failure becomes harder to repeat.
- Stop rule. When another rule or gate is worth less than the next real test, stop adding procedure and run the test.

## Planned experiments

1. **Length ablation.** The same rule set in a long and a compressed version, with violations per turn as the outcome, over fixed scripted sessions.
2. **Trigger design.** The same rule written as an abstract principle versus tied to a surface cue (for example: "when the user refers to the past, search before answering").
3. **Cross-model replication** of the four failure classes under identical prompts.

These require controlled API runs, with fixed system prompts and sampling settings, many samples per condition and logged raw outputs. Consumer chat interfaces do not allow that. Results and data will be published in this repository.

## Non-claims

Nothing here makes claims about consciousness or subjective experience in any model, in either direction. The work concerns observable behavior and the conditions under which written rules are or are not applied.
