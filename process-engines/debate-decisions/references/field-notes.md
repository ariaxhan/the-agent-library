# Field notes from real use

First multi-hour use: urban-atlas roadmap debate, 2026-07-02. Seven bills, two agents
(dino aff/evidence, luna chair/adversary), Congressional spine with Policy mechanics
inside the two contested bills, roughly five hours over hcom. Full decision record:
Vaults `_meta/research/urban-atlas-retro-2026-07-02/debate-ledger.md`.

What the skill got right, confirmed in practice:

- The format picker held. Congressional for a multi-plank roadmap docket, dropping to
  Policy plan/counterplan/disadvantage inside the genuinely contested bills.
- Rule 7 (deterministic evidence judges, debate never overrides grep) resolved every
  contested point that had a measurable answer. Line counts, commit archaeology, and a
  timestamped failure decided more than rhetoric did.

What practice added, worth folding into the protocol:

1. **Chair supplies the neg when both parties agree.** An already-agreed bill gets no
   real test unless someone is assigned to attack it anyway. The chair writing the neg
   constructive (and then weighing honestly) was the difference between a decision and
   a rubber stamp.
2. **Manufactured disagreement is the mirror failure of agreement theater.** When a
   batch of bills is assembled entirely from already-clashed items, inventing fresh
   objections to fill the neg slot is theater. Vote aye and record MINORITY NOTES
   (named assumptions, missing receipts) instead. Dissent must be falsifiable or it
   does not enter the record.
3. **Every emergence or quality claim gets an ablation baseline in its falsifier.**
   The clever system must beat the dumb version on stated metrics or the dumb version
   ships. A falsifier that cannot output "the dumb version was just as good" is not a
   falsifier. This single rule did more work than any other in the session.
4. **Amendments beat rejections.** Nine chair amendments were accepted verbatim
   because each named the failure mode AND the cheap fix in the same breath. A neg
   case without a fix invites deadlock; a fix without a named failure mode invites
   scope creep.
5. **The decision-record shape is load-bearing, not ceremony.** Winner, reasons,
   preserved dissent, flip condition. Three recorded flip conditions and two minority
   notes from this session became binding lines in the resulting commissions.
6. **Quarantine tokens before citing them.** A commission in the same evidence window
   propagated a phantom filename for three days because nobody grepped. Before any
   file or system name from inherited context enters a speech, claim, or record, grep
   for it; zero hits means flag it, never repeat it.

Known residual risks (from the pre-use critique, status after one real session):

- Trigger breadth: still untested; this session was explicitly invoked, so the ambient
  fire-on-every-decision behavior has no field data yet.
- Strawman risk in single-agent rounds: CONFIRMED real; chair-supplied-neg (note 1) is
  the working countermeasure when a second agent exists. Solo compressed rounds should
  require the con case to contain at least one argument that would actually flip the
  decision, tied to the what-would-flip-it output line.
- No termination rule: did not bite here because every clash converged within one
  rebuttal cycle; the proposed cap (one rebuttal cycle unless new evidence enters)
  remains untested.
