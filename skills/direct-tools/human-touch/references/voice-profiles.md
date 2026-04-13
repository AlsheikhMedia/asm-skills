# Voice Profiles

Voice profiles customize the human-touch rewriting output to match a specific brand, publication, or author's tone. They ensure consistency across content pieces and prevent the rewriter from flattening everything into generic "clear and concise" prose.

---

## Profile Template

Create voice profiles at `.claude/voice-profiles/[name].md` or pass them inline.

```markdown
# Voice Profile: [Brand/Author Name]

## Identity
- **Who:** [Brand, publication, or person]
- **Audience:** [Who they write for]
- **Register:** [Formal / Professional-casual / Casual / Technical]
- **Language:** [EN / AR-MSA / AR-Levantine]

## Tone Markers
- [e.g., "Confident but not arrogant"]
- [e.g., "Uses humor sparingly — one aside per piece"]
- [e.g., "Direct, avoids hedging"]
- [e.g., "Warm but professional"]

## Vocabulary Preferences
### Use These Words
- [Words this voice gravitates toward]

### Avoid These Words
- [Words that clash with this voice — beyond the standard AI-tell list]

## Sentence Patterns
- **Average sentence length:** [e.g., 12–18 words]
- **Paragraph length:** [e.g., 2–4 sentences]
- **Favorite structures:** [e.g., "Short declarative openers, then longer explanations"]
- **Avoids:** [e.g., "Never starts with a question"]

## Signature Moves
- [e.g., "Ends articles with a single-sentence paragraph"]
- [e.g., "Uses parenthetical asides for personality"]
- [e.g., "References pop culture casually"]

## Sample Passages
Provide 3–5 real examples of this voice in action. These anchor the rewriting more than any description.

### Example 1
> [Paste 2–4 sentences of actual writing in this voice]

### Example 2
> [Paste 2–4 sentences of actual writing in this voice]

### Example 3
> [Paste 2–4 sentences of actual writing in this voice]
```

---

## How Profiles Are Applied

During Pass 2 (Rewrite), the profile modifies default behavior:

1. **Vocabulary** — Profile word preferences override the default replacement table. If the profile says "use 'explore' not 'look at'," that takes precedence.
2. **Sentence rhythm** — Rewritten sentences target the profile's average length and variation patterns.
3. **Tone** — Humor, directness, warmth, and formality are calibrated to the tone markers.
4. **Signature moves** — The rewriter preserves or introduces the profile's structural habits.

During Pass 4 (Score), voice consistency is measured against the loaded profile:
- Does the rewritten content match the vocabulary preferences?
- Does sentence length distribution match the profile target?
- Are tone markers present in the output?
- Are any profile-avoided words still present?

---

## Built-In Profiles

### Professional Blog (Default)

When no profile is loaded, the rewriter defaults to:

- **Register:** Professional-casual
- **Tone:** Clear, direct, confident. Not stiff, not chatty.
- **Sentences:** Mix of 8–25 words. Vary paragraph length.
- **Avoids:** Jargon without explanation, hedging, passive voice, filler.
- **Allows:** First person ("we," "I"), contractions, rhetorical questions.

### Arabic MSA Professional

- **Register:** Formal-professional (MSA)
- **Tone:** Authoritative with warmth. Matches Arabic professional writing conventions — elaborate greetings, respectful closings.
- **Sentences:** Longer than English equivalents (Arabic prose is naturally more flowing). Vary clause structure.
- **Avoids:** English word order, repetitive connectives, flat honorifics.
- **Allows:** Proverbs when they fit naturally, Quranic references in appropriate contexts, traditional expressions of emphasis.

### Arabic Levantine Casual

- **Register:** Casual-conversational (Levantine dialect)
- **Tone:** Friendly, approachable, community-oriented. Matches social media voice.
- **Note:** This profile is flag-only. Content in this voice is scanned but not auto-rewritten — it goes to a human editor.

---

## Creating a Profile from Samples

If you have 3+ writing samples from a target voice but no formal profile:

1. Analyze the samples for: average sentence length, vocabulary preferences, tone markers, structural habits
2. Generate a profile using the template above
3. Save to `.claude/voice-profiles/[name].md`
4. The profile is now available for future human-touch runs

**Tip:** The more samples, the better. 5 samples of 500+ words each produce a reliable profile. 3 short samples give a rough approximation.
