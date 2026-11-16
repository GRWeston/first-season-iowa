# A/B Test Analysis: Home Page Headline

**Data:** `ab-test-results.csv`, 100 trials run Nov 16, 2026, 1:30–1:34 pm (Central), all on `claude-sonnet-4-6`, in the pre-assigned order from `ab-test-assignments.csv` (every trial's version matched its assignment). No trials failed, were rerun, or were dropped; the error log is empty. No responses were truncated.

| | Version A (control) | Version B (variant) |
|---|---|---|
| Headline | Iowa Deer Hunting for Beginners: How to Start | Never Hunted Before? Plan Your First Iowa Deer Hunt in Five Steps |
| Visitors | 50 | 50 |
| Yes | 50 | 50 |
| Yes share | 100% | 100% |

**Difference (B − A):** 0 percentage points.

**Two-proportion z test (planned):** both shares are 100%, so the standard error is 0 and z cannot be computed; there is no difference to test. As a check, Fisher's exact test on the same 2×2 table gives p = 1.00.

**Decision rule:** support required B's yes share to be higher than A's with p < .05. B was not higher, so **the hypothesis is not supported. The result is flat.**

**Why:** every AI visitor said yes to both versions, a ceiling effect. The plan named this risk in advance: the page content is identical in both versions and strongly fits the persona, so the visitor judged mostly on the content and the headline had no room to change the answer. A yes/no outcome cannot register a "more convinced" visitor once everyone is already convinced.

**What it can and cannot tell us:** it shows the headline change did not hurt and that the page as a whole reads as useful to the target persona. It cannot show how real beginners react to a headline in search results or at first glance; the AI visitor reads the full page text carefully and has no time pressure or competing tabs.

**Roll out B?** Not on this evidence. There is no measured gain, and A matches search keywords better.
