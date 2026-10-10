# Evidence grading

## Where to search (in this order)
| Source | Use for | URL (checked 2026-10-10) |
|---|---|---|
| PubMed / PMC | RCTs, meta-analyses, animal studies | https://pubmed.ncbi.nlm.nih.gov/ ✅ · https://www.ncbi.nlm.nih.gov/pmc/ ✅ |
| Cochrane Library | High-quality systematic reviews | https://www.cochranelibrary.com/ ❌ (blocks automated fetch: 429/412). Find the review on PubMed and cite its DOI `10.1002/14651858.CDxxxxxx` instead. |
| ClinicalTrials.gov | Registered and ongoing trials, unpublished results | https://clinicaltrials.gov/ ✅ |
| NIH ODS fact sheets | RDA/UL, plain summaries of evidence | https://ods.od.nih.gov/factsheets/list-all/ ✅ |
| EFSA | EU upper limits, dietary reference values, claim opinions | https://www.efsa.europa.eu/en/topics/topic/dietary-reference-values ✅ · https://www.efsa.europa.eu/en/publications ✅ |
| Examine.com | Independent evidence summaries with grades | https://examine.com/ ✅ (via browser-like fetch; plain curl returns 429) |
| CNKI / 万方 | Chinese studies, TCM ingredients | https://www.cnki.net/ ✅ · https://www.wanfangdata.com.cn/ ✅ |

Useful PubMed filters:
- `"<ingredient>"[tiab] AND (meta-analysis[pt] OR systematic review[pt])`
- `"<ingredient>"[tiab] AND randomized controlled trial[pt] AND humans[mh]`

## Verify before citing
1. `esummary` the PMID: `https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esummary.fcgi?db=pubmed&retmode=json&id=<PMID>`. Check that title, journal, year and first author match what you're about to write.
2. `efetch` the abstract (`rettype=abstract&retmode=text`) and take numbers (HR/RR/OR, CI, n, dose, duration) from it, not from memory.
3. DOI: `https://api.crossref.org/works/<DOI>` should return 200 with a matching title.
4. If any check fails, drop the citation.

## Grades
| Grade | Meaning | Typical basis |
|---|---|---|
| **Strong** | Consistent benefit for this outcome in the relevant population | ≥1 good systematic review/meta-analysis of RCTs, or several large RCTs agreeing |
| **Moderate** | Probable benefit, but inconsistent, small effect, or limited populations | Some RCTs or a meta-analysis with heterogeneity / risk of bias |
| **Limited** | Early or mixed human data | Small or short RCTs, observational associations only |
| **Animal / in-vitro only** | No meaningful human outcome data | Cell, rodent or mechanistic studies |
| **Evidence against** | Well-powered RCTs/meta-analyses found no benefit | Large null RCTs |

Rules:
- Grade per **outcome and population**, not per ingredient. ("Vitamin D: corrects deficiency = Strong; prevents fractures in replete adults = Evidence against.")
- Observational associations ("people with high X have less Y") are not evidence that supplementing X helps.
- Animal results show biological plausibility. Never present them as human benefit.
- Note funding/conflicts when a single industry-funded trial carries the claim.

## Dose comparison
For each graded outcome, fill in:

| Item | Product | Studies | Reference |
|---|---|---|---|
| Daily dose | from label × servings/day | dose in cited trials | RDA/AI and UL (ODS / EFSA / 中国营养学会 DRIs) |

- If the product dose is far below the studied dose, the evidence doesn't transfer. Say so.
- If the dose is above the UL, flag it in red flags. Don't recommend it without medical supervision.
- Note the ingredient form (e.g. D3 vs D2, magnesium oxide vs glycinate, standardized extract %). Different forms are not interchangeable.
