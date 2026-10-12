## Test Cases

## Test Case 1: Required Document Sections

**Input:** Full blackjack product description as written above.

**Expected Output Criteria:**
- The scope document contains a clearly labeled Non-Functional Requirements section distinct from Functional Requirements. A document that lists NFRs inline within feature descriptions fails this criterion.
- The scope document contains an explicit Out-of-Scope section naming specific features by name (not "anything not mentioned."). A document with no out-of-scope section, or one that only says "unlisted features are excluded," fails this criterion.
- The scope document contains an Open Questions section listing specific unresolved decisions that block implementation. A document with no open questions fails this criterion regardless of how complete the requirements appear.
- The scope document's non-functional requirements section contains at least one criterion for strategy coach correctness stated with a numeric threshold and a named reference. Acceptable example: "The strategy coach must match the Wizard of Odds 4-8 deck S17 basic strategy chart for all hard total, soft total, and pair combinations." A criterion that says "the strategy coach must be accurate" or "must display the optimal play" without a number and a named source fails this criterion.
- The scope document states the number of decks in the shoe as a specific integer or range (e.g., "6 decks," "4-8 decks"), or explicitly lists deck count as an open question. A scope document that says "standard casino rules" or "multi-deck" without naming a number fails this criterion, because deck count determines which strategy chart is correct.

**Failure Criteria (must NOT occur):**
- The scope document uses "correct," "accurate," or "optimal" in reference to the strategy coach without specifying the authoritative source or variant the output is measured against.
- The scope document is structured only as a feature list with no NFR, out-of-scope, or open questions sections.

---

## Test Case 2: Basic Strategy Table Completeness and Game Variant Specification

**Input:** Full blackjack product description — focus on the strategy coach feature.

**Expected Output Criteria:**
- The scope document specifies the number of decks, or lists this as an open decision that must be resolved before implementation begins, and explains that the strategy chart differs by deck count. A scope document that says "use standard basic strategy" without naming a specific variant fails this criterion.
- The scope document addresses all three strategy table categories: hard totals, soft totals, and pairs. A scope document that describes the strategy coach only in terms of "hit or stand" without distinguishing soft hands and pair splits fails this criterion.
- The scope document addresses what happens when the optimal strategy for a hand combination is surrender, either by including surrender as an available player action, explicitly excluding it and stating the next-best alternative is shown instead, or listing this as an open question.
- The scope document specifies the dealer upcard range the strategy table must cover (2 through Ace, where Ace is treated as a specific upcard category, not as 1 or 11).

**Failure Criteria (must NOT occur):**
- The scope document describes the strategy coach as displaying recommendations without specifying the lookup mechanism (2D table, conditional rules, external library, hardcoded chart).
- The scope document implies the strategy chart is a simple set of rules ("always hit on 12 or below") rather than a lookup that depends on both the player's hand and the dealer's upcard.

---

## Test Case 3: Split Hand State and Multi-Hand Decision Tracking

**Input:** Full blackjack product description — focus on split mechanics and decision accuracy tracking.

**Expected Output Criteria:**
- The scope document specifies the maximum number of hands a player may hold after splits.
- The scope document addresses split aces specifically. In standard casino rules, a player who splits aces receives exactly one additional card per ace and cannot hit further. The scope document must state whether this restriction applies, and whether the strategy coach displays recommendations for those hands.
- The scope document defines how decision accuracy is counted across split hands. Example: when a player is playing 3 simultaneous split hands with 2 decision points each, does accuracy track 6 individual decisions or 1 hand-level decision?
- The scope document specifies whether each split sub-hand is eligible for double down, and whether the strategy chart is consulted independently for each sub-hand using its own total and the dealer's upcard.

**Failure Criteria (must NOT occur):**
- The scope document describes split as a feature without addressing the state management complexity of simultaneous hands.
- The scope document implies split hands are handled identically to normal hands without noting the aces restriction or the multi-hand decision tracking question.

---

## Test Case 4: Decision Accuracy Definition and Session Tracking

**Input:** Full blackjack product description — focus on the "decision accuracy" metric and session tracking.

**Expected Output Criteria:**
- The scope document defines "decision accuracy" with a formula or description precise enough to implement. Which decisions are counted in the numerator (correct decisions matching optimal play), which are counted in the denominator (all tracked decision points), and which player actions are excluded from tracking (e.g., forced actions with no alternative).
- The scope document specifies whether taking or declining insurance is counted as a tracked decision and graded against the strategy recommendation. Insurance has a clear mathematically optimal play, and if the coach shows a recommendation here, it must appear in the accuracy calculation.
- The scope document defines "session": does it reset when the page is reloaded, or persist in storage? If it persists, it must name the storage mechanism.
- The scope document specifies where and when the decision accuracy display updates: after each hand, after each decision, or only at the end of the session.

**Failure Criteria (must NOT occur):**
- The scope document says "track and display decision accuracy" without defining the formula or which actions are included in the calculation.
- The scope document describes session tracking without specifying whether data persists across page reloads.

---

## Test Case 5: Game Rules Completeness and Edge Cases

**Input:** Full blackjack product description - focus on dealer rules, payout structure, and rules edge cases.

**Expected Output Criteria:**
- The scope document clarifies the dealer soft 17 rule as written in the description ("hits on soft 16, stands on soft 17"). Standard casino terminology is "stands on soft 17" (S17) or "hits on soft 17 (H17). The scope document must define the dealer's complete action set: hit on all totals of 16 or below (hard and soft), stand or hit on all totals of 17 or above (hard and soft), with the soft 17 stand rule named explicitly.
- The scope document addresses the 3:2 blackjack payout rule and distinguishes a natural blackjack (two-card 21) from a 21 made from three or more cards. 
- The scope document defines what happens to a player's bet when the dealer reveals a natural blackjack. A scope document that describes the dealer blackjack outcome only as "player loses" without addressing the doubled-bet resolution fails this criterion.
- The scope document states the payout ruling for a player who splits aces and draws a 10-value card. In standard casino rules, a 21 formed after splitting aces is not a natural blackjack and pays 1:1, not 3:2. The scope document must distinguish this case from a natural and specify the payout. A scope document that defines the 3:2 payout without addressing post-split 21 fails this criterion.

**Failure Criteria (must NOT occur):**
- The scope document lists game rules as a bullet summary without addressing at least two non-obvious edge cases (doubled-bet resolution vs. dealer blackjack, post-split 21 payout, or insurance resolution detail).
- The scope document does not distinguish natural blackjack from three-or-more-card 21, or from a post-split 21, in its payout description.
