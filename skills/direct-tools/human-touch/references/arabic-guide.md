# Arabic Content Guide

Arabic-specific rules for the human-touch skill. Covers register policy, AI pattern detection in Arabic, and cultural authenticity.

---

## Board-Approved Language Policy

> **This is a firm editorial decision. No exceptions.**

| Register | Use For | Pipeline Mode |
|----------|---------|---------------|
| **MSA (Modern Standard Arabic)** | Blog posts, articles, press releases, documentation, all formal content | Full scan + rewrite |
| **Levantine Arabic** | Social media, casual audience engagement, informal copy | **Flag-only** — human editor review required |
| **Gulf (GCC) Arabic** | ❌ Not approved | Reject — recommend MSA or Levantine rewrite |
| **Egyptian Arabic** | ❌ Not approved | Reject — recommend MSA or Levantine rewrite |

**Rules:**
- Never mix registers within a single piece unless editorially justified
- All Arabic content requires human editor review regardless of AI tooling — no exceptions
- When in doubt, default to MSA
- Specify register clearly when prompting AI: "Write in Modern Standard Arabic suitable for a professional audience"

---

## Arabic AI Tells — Detection Patterns

### 1. English-Influenced Word Order

Arabic naturally uses VSO (Verb-Subject-Object). AI models trained heavily on English often produce SVO order.

| AI Pattern (SVO) | Natural Arabic (VSO) |
|-------------------|---------------------|
| الشركة أطلقت منتجًا جديدًا | أطلقت الشركةُ منتجًا جديدًا |
| الفريق حقّق نتائج ممتازة | حقّق الفريقُ نتائج ممتازة |
| المستخدمون يفضّلون الواجهة البسيطة | يفضّل المستخدمون الواجهة البسيطة |

**Fix:** Restructure to VSO. Not every sentence must be VSO — Arabic allows flexibility — but a text that is consistently SVO signals machine generation.

### 2. Repetitive Formal Connectives

AI Arabic tends to cycle through the same small set of connectives:

| Overused | Alternatives |
|----------|-------------|
| بالإضافة إلى ذلك (in addition to that) | كذلك، فضلًا عن، إلى جانب ذلك، ومن جهة أخرى |
| علاوة على ذلك (moreover) | كما أنّ، ويُضاف إلى ذلك، وممّا يُذكر |
| من الجدير بالذكر (it is worth mentioning) | ومن اللافت، والملاحظ أنّ، وتجدر الإشارة |
| في هذا السياق (in this context) | وفي هذا الإطار، ومن هذا المنطلق |
| لا يمكن إنكار (it cannot be denied) | والواقع أنّ، ومن الثابت |

**Fix:** Vary connectives. Use different ones. Sometimes no connective is needed — let the idea flow from the previous sentence naturally.

### 3. Literal Translations from English

AI often translates English idioms literally into Arabic, producing unnatural phrases:

| Literal Translation | Natural Arabic |
|--------------------|----------------|
| يلعب دورًا حيويًا (plays a vital role) | له أثر كبير / يؤثّر بشكل ملحوظ |
| في نهاية اليوم (at the end of the day) | في المحصّلة / خلاصة القول |
| على نفس الصفحة (on the same page) | على اتفاق / متوافقون |
| خارج الصندوق (outside the box) | بطريقة مبتكرة / بنظرة مختلفة |
| يُسلّط الضوء على (sheds light on) — overused | يكشف عن / يوضّح / يبيّن |

### 4. Missing Cultural Texture

AI Arabic is technically correct but culturally flat. Natural Arabic professional writing includes:

- **Proverbs and sayings** used naturally, not forced:
  - "مَن جدّ وجد" (who strives, finds) — for effort/persistence topics
  - "العلم نور" (knowledge is light) — for education topics
  - "الصبر مفتاح الفرج" (patience is the key to relief) — for patience/perseverance
- **Warm greetings and closings** — Arabic professional writing is warmer than English. Flat openings like "هذا المقال يتناول..." (this article discusses...) feel robotic.
- **Religious/cultural expressions** where appropriate:
  - "بإذن الله" (God willing) for future plans
  - "الحمد لله" (praise be to God) for achievements
  - "بسم الله الرحمن الرحيم" for formal documents
- **Seasonal and cultural references** — Ramadan, Eid, national celebrations, regional events

**Important:** Add cultural texture only where it fits naturally. Forced proverbs are worse than none.

### 5. Flat Honorifics

Arabic uses elaborate, warm honorifics. AI tends to skip them or use generic ones.

| Generic/Flat | Natural Arabic |
|-------------|----------------|
| السيد (Mr.) alone | حضرة السيد / سعادة |
| No greeting | السلام عليكم ورحمة الله وبركاته |
| Abrupt closing | وتفضّلوا بقبول فائق الاحترام والتقدير |

### 6. Gender Agreement Errors

AI frequently makes gender agreement mistakes, especially with:
- Verb-subject agreement in VSO sentences
- Adjective-noun agreement in iḍāfa constructions
- Pronoun references across sentences
- Plural forms (broken plurals vs. sound plurals)

**Always verify:** Every verb agrees with its subject in gender and number. Every adjective agrees with its noun.

### 7. Diacritics (Tashkeel)

- Professional Arabic content typically uses minimal diacritics
- Add diacritics only where ambiguity exists or for Quranic/classical citations
- AI sometimes over-applies or randomly applies diacritics — normalize

---

## Levantine Arabic — Flag-Only Notes

When scanning Levantine content, flag but do not auto-fix:

- **Register consistency** — Is it actually Levantine, or mixed with Gulf/Egyptian?
- **Levantine markers to verify:**
  - هلق / هلّأ (now) vs. دحين (Gulf) or دلوقتي (Egyptian)
  - كتير (very) vs. مرة (Gulf) or أوي (Egyptian)
  - شو (what) vs. إيش (Gulf) or إيه (Egyptian)
  - كيفك (how are you) vs. شلونك (Gulf) or عامل إيه (Egyptian)
- **Spelling consistency** — Levantine has no standardized orthography. Flag inconsistent spellings within the same piece but don't prescribe a "correct" spelling.
- **Tone match** — Does it sound authentically Levantine-casual, or like MSA trying to sound casual?

Output flagged issues with a note: "Human editor review required — Levantine content."

---

## MSA Quality Checklist

After rewriting MSA content, verify:

- [ ] Word order is naturally Arabic (VSO where appropriate)
- [ ] Connectives are varied — no single connector appears more than twice
- [ ] No literal English translations or idioms
- [ ] Gender agreement is correct throughout
- [ ] Honorifics and greetings match the formality level
- [ ] Cultural references (if any) are natural, not forced
- [ ] The text has warmth — it doesn't read like a translated English document
- [ ] Diacritics are used sparingly and only where needed
- [ ] The register is consistently MSA — no dialect slipped in
