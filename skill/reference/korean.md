# Korean interfaces

For any surface whose copy is Korean: `lang="ko"` on the document or a container, a PRODUCT.md that names Korean users or Korean copy, or target text that is mostly Hangul. On a mixed-language page, these rules govern the Korean runs; the rest of the skill governs the rest.

Latin-script defaults do not transfer to Hangul. Its syllables are full-width, square, and dense; it has no case and no true italic; its fonts run to thousands of glyphs; and its copy has speech levels English does not. Most "AI-made Korean page" tells come from applying English habits to it.

## The Korean slop test

Would a Korean designer at a good product company ship this, or recognize a translated English template? The tells: Pretendard with no decision behind it, English eyebrow labels ("FEATURES", "WHY US") decorating a Korean page, a faux-italic accent word in a Hangul headline, mid-word line breaks, and copy that reads like it was translated: "~를 통해", "당신", "새로운 차원의 경험".

## Document setup

- **Declare the language.** `<html lang="ko">`, or `lang="ko"` on the Korean container of a mixed page. It drives line breaking, screen-reader pronunciation, and which glyph shapes the browser picks for Hanja; without it, Han characters can render with Chinese or Japanese forms. <!-- rule:ko-lang-attribute -->

## Typography

- **Measure in em or ic, not ch.** `ch` is the width of the Latin "0" and varies with the fallback chain; one Hangul syllable is roughly 1em. Body copy: about 30–40 syllables per line, so `max-width` around 30–40em (or `ic`, which resolves to the CJK ideograph advance and falls back to 1em). <!-- rule:ko-measure -->
- **More leading than Latin.** Hangul's dense, square syllables need air: body line-height 1.6–1.8, headings 1.25–1.4. A 1.4–1.5 body copied from a Latin system reads cramped. <!-- rule:ko-line-height -->
- **Break at spaces, not inside words.** Set `word-break: keep-all` on Korean prose and headings so lines break at word spaces (띄어쓰기), paired with `overflow-wrap: anywhere` so URLs and long tokens still wrap. Add `text-wrap: balance` to headings. Check headings at every breakpoint; keep-all moves the break, it does not fix a bad one. <!-- rule:ko-word-break -->
- **No italic for emphasis.** Hangul faces ship no italic, so `font-style: italic` produces a synthesized oblique that looks broken. Emphasize with weight, color, or a size step. The Latin habit of an italic serif accent word in a headline has no Korean equivalent; don't fake one. <!-- rule:ko-no-italic -->
- **No wide tracking on Hangul.** Without case there is no all-caps label to open up; positively tracked Hangul reads as spaced-out syllables, not as a label. Korean product typography commonly runs slightly negative tracking (about -0.01 to -0.03em) on sans body and headings; treat that as convention, not a defect, and tune it to the face. <!-- rule:ko-tracking -->
- **Respect the size floor.** Stacked syllables lose legibility faster than Latin as size drops. Body 15–17px; captions and meta no smaller than 12px. Light weights (300 and below) belong to large display sizes only. <!-- rule:ko-size-floor -->
- **Pair scripts deliberately.** When a Latin face leads the stack and a Korean face carries Hangul, compare x-height, weight, and baseline across a mixed line; use `size-adjust` or a `unicode-range`-scoped `@font-face` to correct a mismatch. A Korean face's own Latin glyphs are often the safer choice for UI text. <!-- rule:ko-script-pairing -->

## Fonts

- **Pretendard is the Korean Inter.** It is the right default for Operate surfaces (app UI, dashboards, settings): neutral, complete, variable, with good Latin. On Persuade and Experience surfaces it is the default an agent reaches for without deciding; choose it only when the brief points there, and say why. The same applies to Noto Sans KR, the Google Fonts default. <!-- rule:ko-font-default -->
- **Know the field.** Sans: Pretendard, SUIT, Wanted Sans, Spoqa Han Sans Neo, IBM Plex Sans KR, Noto Sans KR, Nanum Square Neo. Serif (명조/바탕): Noto Serif KR, MaruBuri, Hahmlet, Gowun Batang, Nanum Myeongjo, RIDIBatang. Display: Black Han Sans, Gmarket Sans, Do Hyeon. Mono: D2Coding. A serif carries editorial and literary Read surfaces far better than another sans. <!-- rule:ko-font-field -->
- **Check the license.** Many Korean faces are OFL; many corporate "free" fonts carry custom terms (no modification, no resale, attribution, embedding limits). Confirm before shipping; noonnu.cc lists terms per face. <!-- rule:ko-font-license -->
- **Never ship a full Korean font file.** Complete Hangul faces run to several megabytes. Use a dynamic-subset build (many `unicode-range` slices, as Pretendard's CDN ships) or a variable font, with `font-display: swap`. Do not subset to the 2,350 KS X 1001 syllables when users can type text: missing syllables fall back to another face mid-word. <!-- rule:ko-font-loading -->
- **Comp font matching does not cover Hangul.** The font index measures Latin samples. When a comp sets Hangul, identify the face by eye, name your best match, and say it was not machine-matched. <!-- rule:ko-font-matching -->

## Copy

Korean copy fails differently from English copy. Judge it in Korean; English readability heuristics (word counts, sentence length in words) do not apply.

- **One speech level per surface.** Pick 해요체 (most product UI) or 합니다체 (finance, public sector, formal notices) and hold it across headings, body, toasts, errors, and empty states. Mixing them, or dropping into 반말, is the most visible Korean copy defect. <!-- rule:ko-speech-level -->
- **One button grammar.** Buttons take a noun or verb stem ("저장", "삭제") or the 하기 form ("저장하기"); pick one convention per product. Never a full sentence ("저장해요"), never mixed within one dialog. <!-- rule:ko-button-grammar -->
- **Don't address the user as 당신.** Korean UI omits the subject. Use 회원님 or 고객님 sparingly where a direct address is unavoidable. <!-- rule:ko-no-dangsin -->
- **Cut translationese.** "~를 통해", "~에 대해", "~에 있어서", "~를 가지고 있다", "~하는 것이 가능합니다" (→ "~할 수 있어요"), double passives ("~되어지다"), and stacked "~의 ~의" chains. Rewrite as a Korean writer would say it, not as English would. <!-- rule:ko-translationese -->
- **Cut imported marketing slop.** "새로운 차원의", "혁신적인", "~의 힘을 경험하세요", "여정", "잠금 해제", "매끄러운", "~를 위한 모든 것", "지금 바로 시작하세요!": these are English AI-copy patterns translated word for word. Say what the product does. <!-- rule:ko-marketing-slop -->
- **Punctuation stays Korean.** Korean copy rarely uses em dashes or colon-split headlines ("제품명: ~"); AI-translated copy is full of both. Exclamation marks in UI copy are almost always noise. <!-- rule:ko-punctuation -->
- **No decorative English.** English eyebrow labels, section kickers, and "Smart한" hybrids on a Korean page are template residue. Use Korean unless the term is a product name or an established loanword the audience actually uses. <!-- rule:ko-decorative-english -->

## Harden

- **Particles after variables.** Never write "{name}을(를)". Choose 은/는, 이/가, 을/를, 과/와 from the final consonant: for a Hangul syllable, `(code - 0xAC00) % 28 === 0` means no final consonant. For 으로/로, a final ㄹ (index 8) also takes 로. When the variable can end in Latin letters or digits, map digit readings or rephrase so no particle follows it. <!-- rule:ko-particles -->
- **IME composition.** Hangul input composes syllables; an Enter `keydown` during composition submits a half-typed syllable or submits twice. Guard Enter handlers with `event.isComposing` (and `keyCode === 229` for older Safari). Character counters and `maxlength` must tolerate in-progress composition. <!-- rule:ko-ime -->
- **Korean formats.** Dates via `Intl.DateTimeFormat('ko-KR')` ("2026. 10. 31.") or "2026년 10월 31일"; times as "오후 3:00". Prices as "12,000원"; large amounts in 만/억 units in prose ("1억 2,000만 원"); "₩" only in dense tables. <!-- rule:ko-formats -->
- **Korean forms.** Names are one field (이름), family name first, usually without a space; never force a first/last split. Addresses start from a 우편번호 search, then a free-text detail line. Phone numbers as 010-1234-5678. <!-- rule:ko-forms -->
- **Test with real Korean strings.** Widths do not follow English: a label can be shorter in characters and wider on screen. Fill every component with real Korean copy at the longest realistic length before calling a layout done. <!-- rule:ko-real-strings -->

## Verifying

- **Look at Korean at shipping sizes.** Check line breaks in headings at each breakpoint, the leading of a full body paragraph, and every mixed Hangul–Latin line. Read the copy aloud in your head for speech-level consistency before finishing. <!-- rule:ko-verify -->
- **Detector findings on Hangul are evidence, not verdicts.** The detector already adjusts several text checks for CJK. Where a finding on a Korean run contradicts this file, weigh both and state which one you followed and why. <!-- rule:ko-detector-findings -->
