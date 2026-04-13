# Human Score — Scoring Methodology

The human score is a 0–100 composite rating that estimates how "human" a piece of content reads. Higher = more natural. The score is diagnostic, not definitive — it guides editing, not replaces judgment.

---

## Score Components

| Component | Weight | What It Measures |
|-----------|--------|-----------------|
| Vocabulary diversity | 0–20 | Variety of word choice; absence of AI-tell vocabulary |
| Sentence variation | 0–20 | Length variation, structural diversity, rhythm |
| Pattern absence | 0–20 | Fewer AI structural patterns = higher score |
| Voice consistency | 0–20 | Alignment with loaded voice profile (or natural tone if no profile) |
| Cultural/contextual fit | 0–20 | Register appropriateness, cultural texture, audience match |

**Total: 0–100**

---

## Component Scoring

### Vocabulary Diversity (0–20)

**What to measure:**
- Count unique words / total words (type-token ratio)
- Count AI-tell words from the red-flag list (Tier 1, 2, 3)
- Check for synonym cycling (same concept restated with different words)

**Scoring:**
| Score | Criteria |
|-------|----------|
| 17–20 | No Tier 1 AI-tell words. Max 1 Tier 2 word. High type-token ratio. No synonym cycling. |
| 13–16 | No Tier 1 words. 2–3 Tier 2 words. Some repetition but generally varied. |
| 9–12 | 1–2 Tier 1 words present. Multiple Tier 2 words. Noticeable vocabulary repetition. |
| 5–8 | 3+ Tier 1 words. Frequent AI vocabulary. Low variety. |
| 0–4 | Text is saturated with AI-tell vocabulary. Reads like unedited AI output. |

### Sentence Variation (0–20)

**What to measure:**
- Standard deviation of sentence lengths (words per sentence)
- Longest streak of similar-length sentences
- Structural diversity (declarative, interrogative, imperative, fragment)
- Paragraph length variation

**Scoring:**
| Score | Criteria |
|-------|----------|
| 17–20 | High length variation (SD > 8). No more than 2 consecutive similar-length sentences. Mix of structures. |
| 13–16 | Good variation (SD 5–8). Occasional same-length streaks. Mostly declarative but some variety. |
| 9–12 | Moderate variation (SD 3–5). Noticeable uniformity in spots. All declarative. |
| 5–8 | Low variation (SD < 3). Most sentences similar length. Monotonous rhythm. |
| 0–4 | Near-uniform sentence length. Every sentence follows the same pattern. |

### Pattern Absence (0–20)

**What to measure:**
- Count of matched AI patterns from the detection database (sections 4–12 of ai-tells.md)
- Severity weighting: structural patterns count 2x, vocabulary patterns count 1x

**Scoring:**
| Score | Criteria |
|-------|----------|
| 17–20 | 0–2 minor pattern matches. No structural patterns. |
| 13–16 | 3–5 pattern matches. No more than 1 structural pattern. |
| 9–12 | 6–10 pattern matches. 2–3 structural patterns. |
| 5–8 | 11–15 pattern matches. Multiple structural patterns. |
| 0–4 | 15+ pattern matches. Formulaic throughout. |

### Voice Consistency (0–20)

**With a voice profile loaded:**
- Does vocabulary match profile preferences?
- Does sentence length distribution match profile target?
- Are tone markers present?
- Are profile-avoided words absent?

**Without a voice profile (default professional tone):**
- Is the tone consistent throughout? (No sudden shifts formal → casual)
- Does it sound like one person wrote it?
- Are there chatbot artifacts?
- Is the register appropriate for the content type?

**Scoring:**
| Score | Criteria |
|-------|----------|
| 17–20 | Strong match to profile (or consistent natural tone). No voice breaks. |
| 13–16 | Good match. 1–2 minor inconsistencies. |
| 9–12 | Moderate match. Noticeable tone shifts. Some profile-avoided words present. |
| 5–8 | Weak match. Frequent tone shifts. Sounds like multiple writers. |
| 0–4 | No match. Chatbot artifacts present. Inconsistent throughout. |

### Cultural/Contextual Fit (0–20)

**For English content:**
- Is the formality level appropriate for the audience?
- Are references and examples relevant and current?
- Does it avoid generic platitudes?
- Does it show specific knowledge rather than surface-level coverage?

**For Arabic MSA content:**
- Is the register consistently MSA?
- Is word order naturally Arabic?
- Are cultural elements present and natural (not forced)?
- Are honorifics and greetings appropriate?
- Is there warmth in the professional tone?

**For Arabic Levantine content:**
- Is it authentically Levantine (not Gulf or Egyptian)?
- Is spelling consistent within the piece?
- Does the casual tone feel natural?

**Scoring:**
| Score | Criteria |
|-------|----------|
| 17–20 | Perfect register. Culturally authentic. Specific and relevant. |
| 13–16 | Appropriate register. Some cultural texture. Mostly specific. |
| 9–12 | Correct register but flat. Generic rather than specific. Missing cultural elements (Arabic). |
| 5–8 | Register mismatch in places. Culturally tone-deaf. Overly generic. |
| 0–4 | Wrong register. No cultural awareness. Reads like a translated template. |

---

## Score Interpretation

| Range | Verdict | Action |
|-------|---------|--------|
| 85–100 | Excellent | Ready to publish. Minor polish only. |
| 70–84 | Good | Light editing needed. Fix specific flagged items. |
| 50–69 | Moderate | Significant rewriting needed. Run full rewrite pipeline. |
| 30–49 | Poor | Heavy intervention required. Consider rewriting from scratch with better prompts. |
| 0–29 | AI-obvious | Unedited AI output. Full rewrite mandatory. |

---

## Reporting Format

Always report the score with a breakdown:

```
## Human Score: [X]/100

| Component | Score | Notes |
|-----------|-------|-------|
| Vocabulary diversity | X/20 | [brief note] |
| Sentence variation | X/20 | [brief note] |
| Pattern absence | X/20 | [brief note] |
| Voice consistency | X/20 | [brief note] |
| Cultural/contextual fit | X/20 | [brief note] |

**Verdict:** [One sentence from the interpretation table]
```
