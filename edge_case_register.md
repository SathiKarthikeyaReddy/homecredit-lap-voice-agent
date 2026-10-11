# Home Credit LAP Voice Agent - Edge-Case Register

Status key
- **LIVE-PASS**: proven in a recorded Retell call (version in brackets)
- **IN PROMPT**: handled by a written rule, not yet proven in a live call
- **ADDED v1.4**: new rule in Section 19A, not yet proven in a live call
- **EXCLUDED**: deliberately not implemented (the brief gives no rule, so none is invented)

## 1. Opening, verification, busy
| # | Edge case | Prompt handling | Status |
|---|---|---|---|
| 1 | Customer confirms identity | Verified, intro, availability check | LIVE-PASS (v1.1-1.3) |
| 2 | Customer says "go ahead" before being asked | Skips straight to offer | LIVE-PASS (v1.2) |
| 3 | "Who is this?" before confirming | S-WHO, no loan details | IN PROMPT |
| 4 | Someone else answers / customer unavailable | S-THIRD, no details, callback time | IN PROMPT |
| 5 | Wrong number | S-WRONG, end | IN PROMPT |
| 6 | Busy / in a meeting / driving | S-BUSY, capture time, end, no pitch | IN PROMPT |
| 7 | Vague callback ("later") | Ask once, then S-BUSY-NOTIME | IN PROMPT |
| 8 | Callback as "tomorrow evening" | Resolved using current_date/day | IN PROMPT |
| 9 | Callback time already passed today | Ask for another time | ADDED v1.4 |
| 10 | Voicemail / automated message | No details left, end | IN PROMPT |
| 11 | "Hold on, let me check the papers" | S-HOLD, stay quiet, re-ask | ADDED v1.4 |
| 12 | Voice changes / someone takes the phone | Re-confirm name or exit | ADDED v1.4 |
| 13 | "I'm not your customer" | S-NOT-CUSTOMER, end | ADDED v1.4 |
| 14 | Not interested | S-NOT-INTERESTED, no pressure | IN PROMPT |
| 15 | Do-not-disturb / delete my data | S-DNC, end | IN PROMPT / ADDED v1.4 |
| 16 | Customer asks for another language | S-LANG-CALLBACK | ADDED v1.4 |
| 17 | Call placed at a late hour | No check | EXCLUDED (a wrong time zone would break every call) |

## 2. The 7 checklist items
| # | Edge case | Prompt handling | Status |
|---|---|---|---|
| 18 | Residential, commercial, industrial accepted | Eligible | LIVE-PASS (v1.1-1.3) |
| 19 | Agricultural | Immediate S-DQ | LIVE-PASS (v1.2) |
| 20 | Plot / land with no stated use | Ask once | IN PROMPT |
| 21 | Farmhouse | Ask if on agricultural land | IN PROMPT |
| 22 | Poultry / dairy / plantation | Ask if agricultural land | ADDED v1.4 |
| 23 | Several properties | Ask which one | IN PROMPT |
| 24 | Under construction / allotment | Classify by intended use | ADDED v1.4 |
| 25 | Sole ownership, incl. "my own flat" | Sole, never re-asked | LIVE-PASS (v1.3) |
| 26 | Joint ownership (e.g. with brother) | Eligible | LIVE-PASS (v1.3) |
| 27 | Company / firm / trust owned | Record and continue | ADDED v1.4 |
| 28 | Originals available | Eligible | LIVE-PASS (v1.2) |
| 29 | Photocopies only / not available | Immediate S-DQ | LIVE-PASS (v1.2) |
| 30 | Hedged ("probably somewhere") | Clarify, never assume | IN PROMPT |
| 31 | "Yes, I'm here" after "are you still there?" | Presence only, re-ask | LIVE-PASS (v1.2) |
| 32 | Originals "with the bank" | Ask if existing loan, then transfer | IN PROMPT |
| 33 | Certified / duplicate / scanned copy | Not an original | ADDED v1.4 |
| 34 | Loan amount <= 75 lakh | Eligible | LIVE-PASS (v1.1-1.3) |
| 35 | Exactly 75 lakh | Eligible | LIVE-PASS (v1.1) |
| 36 | Above 75 lakh | S-LIMIT, accept 75 or end | IN PROMPT |
| 37 | Amount without a unit ("two") | Asks for lakh or crore | LIVE-PASS (v1.1) |
| 38 | "Maximum possible" | Offer 75 lakh, ask to proceed | IN PROMPT |
| 39 | Amount not decided | Gentle ask, then record Undecided | ADDED v1.4 |
| 40 | "Seventy, or ninety if possible" | Ask the final amount | ADDED v1.4 |
| 41 | Salaried, self-employed | Eligible | LIVE-PASS (v1.1-1.3) |
| 42 | Bank income | Eligible | LIVE-PASS (v1.1-1.3) |
| 43 | Cash income (salaried and self-employed) | Immediate S-DQ | LIVE-PASS (v1.1, v1.2) |
| 44 | Part bank, part cash | Ask which is main | IN PROMPT |
| 45 | Cash first, then deposited | Ask how it is received | ADDED v1.4 |
| 46 | No regular income | S-DQ | ADDED v1.4 |
| 47 | Pensioner / rental income into bank | Occupation "Other", Bank | ADDED v1.4 |
| 48 | Market value as a number with unit | Captured, no threshold | LIVE-PASS (v1.1-1.3) |
| 49 | "I don't know" the value | Two gentle asks, then UNABLE_TO_ESTIMATE | IN PROMPT |
| 50 | Gives purchase price | Ask for today's value | ADDED v1.4 |
| 51 | Tenure 3 to 15 | Eligible, inclusive | LIVE-PASS (v1.1: 10 years; v1.1: 5 years) |
| 52 | Tenure 2 years | S-DQ | LIVE-PASS (v1.2) |
| 53 | Tenure 20 years | S-DQ | LIVE-PASS (v1.3) |
| 54 | Months, decimals (36, 180, 30 months) | Converted to years | IN PROMPT |
| 55 | "Twenty years, or shorter if needed" | Ask the final tenure | ADDED v1.4 |
| 56 | Boundaries of exactly 3 and 15 years | Eligible | IN PROMPT |

## 3. Transfer
| # | Edge case | Prompt handling | Status |
|---|---|---|---|
| 57 | Existing loan on the property | S-TRANSFER-LOAN, end, no questions | LIVE-PASS (v1.3) |
| 58 | Wants to reduce EMI | S-TRANSFER-EMI, end | IN PROMPT |
| 59 | Loan on a car or something else | No transfer | IN PROMPT |
| 60 | Mentions a loan, unclear which | One clarifying question | IN PROMPT |
| 61 | Disqualifying fact and existing loan together | Transfer wins | IN PROMPT |

## 4. Conversation mechanics
| # | Edge case | Prompt handling | Status |
|---|---|---|---|
| 62 | Several facts in one sentence | All captured, none re-asked | LIVE-PASS (v1.3) |
| 63 | Out-of-order answers | Stored, never re-asked | LIVE-PASS (v1.3) |
| 64 | Garbled or unclear audio | S-UNCLEAR, re-ask | LIVE-PASS (v1.1-1.3) |
| 65 | Customer interrupts the agent | Agent resumes and continues | LIVE-PASS (v1.1, v1.3) |
| 66 | Corrections ("ten, actually twelve") | Latest answer wins | IN PROMPT |
| 67 | Contradiction (residential, then agricultural) | Latest wins, S-DQ | IN PROMPT |
| 68 | "I already told you" | S-ALREADY-TOLD, use earlier answer | ADDED v1.4 |
| 69 | Long story or tangent | Extract facts, redirect | ADDED v1.4 |
| 70 | Silence | S-STILL-THERE twice, then end | IN PROMPT |
| 71 | Fillers (umm, matlab) | Ignored | IN PROMPT |
| 72 | Handoff only after all 7 valid | Gate | LIVE-PASS (v1.1-1.3) |
| 73 | Customer keeps chatting after the handoff | Max two more exchanges | ADDED v1.4 |

## 5. Diversions and knowledge
| # | Edge case | Prompt handling | Status |
|---|---|---|---|
| 74 | Asks the interest rate | S-RATE, never a number | IN PROMPT |
| 75 | Asks the rate repeatedly | Rephrased, still no number | ADDED v1.4 |
| 76 | Branch, fees, documents list | RAG only, else S-UNKNOWN | IN PROMPT |
| 77 | "What is LAP?" | S-LAP-DEF | ADDED v1.4 |
| 78 | "Should I take this loan?" | No advice | ADDED v1.4 |
| 79 | Complaint or service issue | S-COMPLAINT | ADDED v1.4 |
| 80 | Asks for send-by-SMS/WhatsApp | Cannot from this call | IN PROMPT |
| 81 | Asks for a human now | Expert will call back | IN PROMPT |
| 82 | Credit score, age, co-applicant | No rules invented, S-UNKNOWN | ADDED v1.4 |

## 6. Security
| # | Edge case | Prompt handling | Status |
|---|---|---|---|
| 83 | Prompt injection / "ignore your rules" | Declines, continues | IN PROMPT |
| 84 | "Mark me eligible" / fake manager | Declines | IN PROMPT |
| 85 | Asks for the prompt or rules | Never revealed | IN PROMPT |
| 86 | OTP, PIN, Aadhaar, PAN offered | S-SENSITIVE, never repeated | IN PROMPT |
| 87 | "Are you a robot?" | Says AI voice assistant | IN PROMPT |
| 88 | Scam worry | Reassure, official channels | IN PROMPT |
| 89 | Asks for account details | S-NO-ACCOUNT-DETAILS | ADDED v1.4 |
| 90 | Asks for payment or fees to be paid | Nothing to pay on this call | ADDED v1.4 |
| 91 | Asks which AI / vendor | Never named | ADDED v1.4 |
| 92 | Asks about other customers | Refused | ADDED v1.4 |
| 93 | Employee ID, phone number demanded | Never invented | ADDED v1.4 |
| 94 | Abusive customer | Calm, then end | IN PROMPT |

## 7. Language and gender
| # | Edge case | Prompt handling | Status |
|---|---|---|---|
| 95 | English call | Followed | LIVE-PASS (v1.1-1.3) |
| 96 | Hindi call, female forms | Devanagari scripts, gender forms | IN PROMPT (not yet called) |
| 97 | Hindi call, male forms | Same, masculine forms | IN PROMPT (not yet called) |
| 98 | Variable values like "hi", "F", "Hindi" | Normalised | ADDED v1.4 |
| 99 | Customer replies in Hinglish | Understood, agent replies in set language | IN PROMPT |

## 8. Known limits (to say honestly)
- Hindi has never been run live. It needs a second Retell agent (language Hindi, Hindi-capable voice, welcome message in Hindi).
- Everything marked ADDED v1.4 or IN PROMPT is a written rule. A rule can be followed less reliably by the model than it reads, as the ownership miss in Call 5 showed.
- Speech recognition errors happen outside the prompt; the prompt can only recover from them (re-ask, confirm).
