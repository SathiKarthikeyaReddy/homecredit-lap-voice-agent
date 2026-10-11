# Home Credit LAP Qualification Voice Agent

An AI voice agent for Home Credit that calls existing customers about a pre-approved Loan Against Property offer (up to 75 lakh), collects 7 eligibility data points, disqualifies ineligible customers immediately, routes existing-loan and EMI-reduction cases to a loan-transfer specialist, and hands qualified customers to a senior loan expert.

Built and tested on Retell AI (single-prompt agent, GPT 4.1, voice Monika, English-India). All test callers are fictional.

## Files

| File | What it is |
|---|---|
| `system_prompt_v1.4.txt` | The final system prompt (paste the text below the BEGIN PROMPT line into the agent) |
| `evidence_links.csv` | Public recording and log link for every test call |
| `transcripts.md` | Full transcript of every test call |
| `edge_case_register.md` | About 100 edge cases, each marked as tested live, written in the prompt, added in v1.4, or deliberately excluded |

## Test calls

Recording and log links are public. Browsers download them as files.

| ID | Scenario | Prompt | Audio | Log |
|---|---|---|---|---|
| E1 | Happy path to senior-expert handoff | v1.1 | [audio](https://dxc03zgurdly9.cloudfront.net/93bd1c594225a967a009c8f302ae91d6b724701a068b36fb7cf81c8ac3b9d3df/recording.wav) | [log](https://dxc03zgurdly9.cloudfront.net/93bd1c594225a967a009c8f302ae91d6b724701a068b36fb7cf81c8ac3b9d3df/public.log) |
| E2 | Agricultural property: disqualified | v1.2 | [audio](https://dxc03zgurdly9.cloudfront.net/2edfc38076558326fc6fda1397f96021bb84d879021a39cebfcb1a87e60d45f0/recording.wav) | [log](https://dxc03zgurdly9.cloudfront.net/2edfc38076558326fc6fda1397f96021bb84d879021a39cebfcb1a87e60d45f0/public.log) |
| E3 | Cash income, self-employed: disqualified | v1.2 | [audio](https://dxc03zgurdly9.cloudfront.net/9f8f7e0626c21c46a6295f934282e0d119f6e843107b8c28ad7d910eba758ab5/recording.wav) | [log](https://dxc03zgurdly9.cloudfront.net/9f8f7e0626c21c46a6295f934282e0d119f6e843107b8c28ad7d910eba758ab5/public.log) |
| E4 | Cash income, salaried; exactly 75 lakh accepted | v1.1 | [audio](https://dxc03zgurdly9.cloudfront.net/9a3ea5e961de3051a8afcd6310e75b772307da8edf54f1436b88baf83003678f/recording.wav) | [log](https://dxc03zgurdly9.cloudfront.net/9a3ea5e961de3051a8afcd6310e75b772307da8edf54f1436b88baf83003678f/public.log) |
| E5 | No original documents, with presence check | v1.2 | [audio](https://dxc03zgurdly9.cloudfront.net/893178a5e83bf23ed824ee737b743a2a3b454a8f50259b8a1c4e3f2635ce339e/recording.wav) | [log](https://dxc03zgurdly9.cloudfront.net/893178a5e83bf23ed824ee737b743a2a3b454a8f50259b8a1c4e3f2635ce339e/public.log) |
| E6 | Tenure 2 years; several facts in one sentence | v1.2 | [audio](https://dxc03zgurdly9.cloudfront.net/591a049354364a5b71a6a0454703bc4ae45f50b0cdc7406408d9419a0f7902af/recording.wav) | [log](https://dxc03zgurdly9.cloudfront.net/591a049354364a5b71a6a0454703bc4ae45f50b0cdc7406408d9419a0f7902af/public.log) |
| E7 | Tenure 20 years; joint ownership; industrial | v1.3 | [audio](https://dxc03zgurdly9.cloudfront.net/9c18210b8a0e46cb71d3a007c94255de0ac963a9082cac61b66eebce7bc7999b/recording.wav) | [log](https://dxc03zgurdly9.cloudfront.net/9c18210b8a0e46cb71d3a007c94255de0ac963a9082cac61b66eebce7bc7999b/public.log) |
| E8 | Existing loan: transfer specialist message | v1.3 | [audio](https://dxc03zgurdly9.cloudfront.net/db3dd9230b6885857bb766a8e26d06a6773ee4adc7cd478b28686840923f419c/recording.wav) | [log](https://dxc03zgurdly9.cloudfront.net/db3dd9230b6885857bb766a8e26d06a6773ee4adc7cd478b28686840923f419c/public.log) |
| E9 | Several facts in one sentence (partial call) | v1.3 | [audio](https://dxc03zgurdly9.cloudfront.net/4d9d20906090d69a2b02adc0eaff31497aa3863c7e3aed875dd7a061cbf27c55/recording.wav) | [log](https://dxc03zgurdly9.cloudfront.net/4d9d20906090d69a2b02adc0eaff31497aa3863c7e3aed875dd7a061cbf27c55/public.log) |
| E10 | Tenure 2 years on the final prompt | v1.4 | [audio](https://dxc03zgurdly9.cloudfront.net/a401f64bda7580c33f28c58c22967d804ba0973c58718adbac13cbb167f1a6a8/recording.wav) | [log](https://dxc03zgurdly9.cloudfront.net/a401f64bda7580c33f28c58c22967d804ba0973c58718adbac13cbb167f1a6a8/public.log) |
| E11 | First version: two defects found | v1.0 | [audio](https://dxc03zgurdly9.cloudfront.net/38a7e7b1b03229069104492ceebba845da166b511d296d619b1f13bffbc4b853/recording.wav) | [log](https://dxc03zgurdly9.cloudfront.net/38a7e7b1b03229069104492ceebba845da166b511d296d619b1f13bffbc4b853/public.log) |

## Version history

- **v1.0:** first version. E11 exposed two defects: a "yes" to "are you still there?" was taken as the documents answer, and "I've got one" (no unit) was accepted as the market value.
- **v1.1:** fixed both; answers must contain a usable value; shorter first question; name and "Thank you" repetition limited.
- **v1.2:** disqualification message goes straight to the closing line.
- **v1.3:** "my own flat" now counts as sole ownership and is never re-asked.
- **v1.4:** adds an append-only edge-case section (hold on, "I already told you", hedged amounts and tenures, complaints, not-a-customer, language requests, input normalisation). No earlier text changed.

## Honest limits

- Not recorded live: busy/callback, loan above 75 lakh, EMI-reduction transfer, ambiguous documents, contradictions, prompt-injection handling, and Hindi.
- The handoff was recorded on v1.1; v1.4 only adds a new section.
- Speech-recognition slips in the transcripts come from the browser microphone, not the agent's logic.
