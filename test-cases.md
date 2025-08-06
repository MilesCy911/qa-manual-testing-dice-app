# ✅ Test Cases for Dice Roller App

| TC ID | Test Description                 | Steps | Expected Result                  | Priority | Status |
|-------|----------------------------------|-------|----------------------------------|----------|--------|
| TC001 | Roll Dice                        | Click "Roll" once | A number 1–6 appears after text | High     | Pass   |
| TC002 | Check Range Validity             | Click 50 times | No number outside 1–6 should show | High | Pass |
| TC003 | Check Text Format                | Click "Roll" | Format: "You rolled: X" | Medium | Pass |
| TC004 | Refresh Page Behavior            | Click roll > Refresh | Should reset to “You rolled:” | Low | Fail |
| TC005 | Rapid Clicking Behavior          | Click 5x rapidly | All clicks respond without freezing | Medium | Pass |
| TC006 | Visual Update Test               | Roll dice | No duplication or flickering | Medium | Pass |
