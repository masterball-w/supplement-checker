# Regulators and registries by region

Link status was checked from a Linux box on 2026-10-10 (UTC+8).
- ✅ = page fetched OK (HTTP 200, or content retrieved via a browser-like fetch).
- ⚠️ = reachable only intermittently or only via a browser; search-indexed but not fetched.
- ❌ = could not be verified from the box.

Government URLs change often. If one fails, search the site for the database name.

## United States

Key facts:
- FDA does **not** approve dietary supplements for safety or effectiveness before sale. Manufacturers are responsible for safety and labeling (DSHEA 1994). Source: FDA Q&A ✅ https://www.fda.gov/food/information-consumers-using-dietary-supplements/questions-and-answers-dietary-supplements
- Facilities must register with FDA, but the **food facility registration database is not public**. Don't claim "FDA registered" status can be looked up. A label saying "FDA approved" or "FDA certified" is a red flag.
- Structure/function claims ("supports bone health") must carry the FDA disclaimer. Disease claims ("treats / prevents osteoporosis") are not allowed on supplements.

| What to check | Where | Status |
|---|---|---|
| Label record (ingredients, claims, on/off market) | DSLD https://dsld.od.nih.gov/ (API: https://api.ods.od.nih.gov/dsld/v9/) | ✅ |
| FDA supplements hub | https://www.fda.gov/food/dietary-supplements | ✅ |
| New dietary ingredient (NDI) notifications | https://www.fda.gov/food/dietary-supplements/new-dietary-ingredient-ndi-notification-process and the submitted list https://www.fda.gov/food/new-dietary-ingredients-ndi-notification-process/submitted-75-day-premarket-notifications-new-dietary-ingredients | ✅ |
| Warning letters (search by firm) | https://www.fda.gov/inspections-compliance-enforcement-and-criminal-investigations/compliance-actions-and-activities/warning-letters | ✅ |
| Recalls / safety alerts | https://www.fda.gov/safety/recalls-market-withdrawals-safety-alerts | ✅ |
| Inspection outcomes (cGMP, public) | FDA Data Dashboard https://datadashboard.fda.gov/oii/cd/inspections.htm | ✅ |
| Ingredient-specific FDA notes | https://www.fda.gov/food/dietary-supplements/information-select-dietary-supplement-ingredients-and-other-substances | ✅ |
| Registration & listing overview | https://www.fda.gov/industry/fda-basics-industry/registration-and-listing | ✅ |
| Dockets (citizen petitions, NDI files) | https://www.regulations.gov/ | ✅ |

## Australia
- Complementary medicines must be on the ARTG as **AUST L** (listed, low risk, self-assessed permitted indications) or **AUST R** (registered, evaluated).
- Search: ARTG https://www.tga.gov.au/resources/artg (needs a browser user-agent; plain curl may time out; check it with a control query, see below) and the eBS search https://www.ebs.tga.gov.au/ ✅
- An AUST L number means it's listed, not that efficacy was evaluated by TGA.
- **Run a control query first.** In October 2026 the tga.gov.au ARTG search page returned "There were no matching results" for every keyword, even the control `paracetamol`. If a known product returns nothing, the page is broken and its "no results" is not evidence.
- **Working route (primary source):** the TGA-linked ARTG Search Visualisation Tool https://compliance.health.gov.au/artg/ (Power BI; shows the total ARTG count, about 97k entries). It needs a browser. Search by brand, by sponsor name and by ingredient, and record the result counts.
- **Public Summary PDF for one entry:** `https://www.ebs.tga.gov.au/servlet/xmlmillr6?dbid=ebs/PublicHTML/pdfStore.nsf&docid=<ARTG_ID>&agid=(PrintDetailsPublic)&actionid=1`. It shows the "ARTG entry for" line (e.g. "Medicine Listed (Export Only)"), Approval Area, start date, sponsor and address, and conditions such as "must not be supplied for sale in Australia". Save the PDF as evidence.
- **Export Only** entries (Approval Area "Export only Medicines", often category LIE) cannot be sold in Australia. An export-only listing is not a sale-permitted registration for the 假洋牌 rubric (S1).
- Fallbacks, in order: the browser tool on the two pages above; the Wayback snapshot of `https://www.tga.gov.au/resources/artg/<ID>`; search-index snippets (二手).

## Canada
- Natural health products need an 8-digit **NPN** (or DIN-HM).
- Search: LNHPD https://health-products.canada.ca/lnhpd-bdpsnh/index-eng.jsp ✅
- Database info: https://www.canada.ca/en/health-canada/services/drugs-health-products/natural-non-prescription/applications-submissions/product-licensing/licensed-natural-health-products-database.html ✅

## Japan (消費者庁)
- 機能性表示食品 (notification, company responsibility): overview https://www.caa.go.jp/policies/policy/food_labeling/foods_with_function_claims/ ✅. Search portal https://www.caa.go.jp/policies/policy/food_labeling/foods_with_function_claims/search/ ✅. Database https://www.fld.caa.go.jp/caaks/cssc01/ ✅
- 特定保健用食品 (トクホ, approved): https://www.caa.go.jp/policies/policy/food_labeling/foods_for_specified_health_uses/ ✅
- 栄養機能食品: self-declared within fixed nutrient ranges; there is no database.

## EU / UK
- No pre-market authorisation for food supplements. They are notified nationally. Health claims must be authorised.
- EU health claims register: https://ec.europa.eu/food/food-feed-portal/screen/health-claims/eu-register ✅
- EU food supplements policy: https://food.ec.europa.eu/food-safety/labelling-and-nutrition/food-supplements_en ✅
- Novel food status (new ingredients): https://www.efsa.europa.eu/en/topics/topic/novel-food ✅
- GB NHC register: https://www.gov.uk/government/publications/great-britain-nutrition-and-health-claims-nhc-register ✅
- FSA guidance: https://www.food.gov.uk/business-guidance/food-supplements ✅
- MHRA (products that are medicines by function): https://www.mhra.gov.uk/ ✅

## China (中国)

### Channel decides the requirement
| 渠道 | 是否需要蓝帽子 | 怎么看 |
|---|---|---|
| 跨境电商零售进口（天猫国际 / 京东国际 / 抖音全球购 等"海外旗舰店"） | 不按国内保健食品注册/备案管理，可无蓝帽子；按个人自用物品监管，有年度限额 | 商品页标注"跨境/海外直邮/保税"，中文标签可为贴签 |
| 一般贸易进口 | 需要：国食健注J…（注册）或 食健备J…（备案） | 包装印蓝帽子 + 批准文号 |
| 国产 | 需要：国食健注G… / 国食健字G…（旧注册）/ 食健备G…（备案），且生产企业持 SC 许可证（类别 27 保健食品） | 包装印蓝帽子 + 文号 + SC 编号（14 位） |

### Where to query
- 国家市场监督管理总局 特殊食品信息查询平台: https://ypzsx.gsxt.gov.cn/specialfood/ ⚠️ (curl 200 from the box; the page is a JS app and its search can time out; search-indexed as 特殊食品信息查询平台, covering 国产/进口 保健食品 注册 and 备案 searches). Query by 产品名称 or 批准文号.
- SAMR 特殊食品安全监督管理司 portal: https://www.samr.gov.cn/tssps/ ✅ and the 法定主动公开 section https://www.samr.gov.cn/zw/zfxxgk/fdzdgknr/tssps/ ✅
- Registration filing client: https://xbjspzc.gsxt.gov.cn/regist_enter/ ✅. Filing system: https://xbjspba.gsxt.gov.cn/record_pt/ ✅ (both for applicants, not public lookup)
- SC 食品生产许可: 食品生产许可管理办法 https://www.samr.gov.cn/zw/zfxxgk/fdzdgknr/fgs/art/2023/art_b15dbae4c2014671b9463fbe9f513576.html ✅. Lookup https://spaqjg.e-cqs.cn/spscxk/ ⚠️ (title fetched: 食品生产许可获证企业信息查询平台; may show "系统正在建设中"). Local 市场监管局 sites also offer lookups.
- NMPA (if the product might be a drug/OTC instead): https://www.nmpa.gov.cn/ ✅

### Checks
- 文号格式: 国食健注G/J + 4 位年份 + 4 位序号 · 食健备G/J + 年份 + 序号 · 旧 国食健字G/J…（2016 年前注册）. Make sure the number on the pack matches the product name and company on the platform.
- 保健功能是否在核准范围内: the claimed function must appear on that product's registration/filing record. Compare it with 《允许保健食品声称的保健功能目录 非营养素补充剂（2023年版）》 (24 functions, published 2023-08-31) https://www.samr.gov.cn/zw/zfxxgk/fdzdgknr/tssps/art/2023/art_491d5c9de75e425c8cd0203027af1d93.html ✅ Nutrient supplements (维生素/矿物质) filed as 补充 X can only claim 补充 X.
- 普通食品 / 压片糖果 / 固体饮料 / 代用茶 sold with words like 降血糖、降血压、抗癌、增强免疫 is a **red flag** (illegal health claim).

## Claimed-origin check (假洋牌 risk)
Chinese consumer reporting in 2026 described a pattern: a shell company and trademark registered abroad, domestic contract manufacturing, and sales through bonded warehouses and cross-border stores. Sources: 中国经济周刊 2026-04-15 http://paper.people.com.cn/zgjjzk/pc/content/202604/15/content_30154019.html ✅ and 中国网 2026-04-07 http://business.china.com.cn/2026-04/07/content_43392624.shtml ✅.

What the agent checks:
1. **Home-market registry.** Is the product in the official database of the country it claims to come from (ARTG / LNHPD / 消費者庁)? DSLD for the US is a voluntary-coverage reference, not a registry, so absence there is weak evidence.
2. **Home-market presence.** Does the brand have an official site and local retail listings in that country (e.g. Amazon for the US, Chemist Warehouse for AU), or does it appear only on Chinese platforms?
3. **Trademark (optional).** Look the trademark up in:
   - WIPO Global Brand Database https://branddb.wipo.int/ ✅
   - IP Australia https://search.ipaustralia.gov.au/trademarks/search/quick ✅
   - EUIPO eSearch https://euipo.europa.eu/eSearch/ ✅

   A very recent registration date, or an applicant that looks like a Chinese entity, is a signal only. It is not proof.
4. **Wording.** "TGA认证" and "FDA认证" are not how those systems work. TGA lists (AUST L) or registers (AUST R) products, and FDA does not approve supplements.

### Retail absence check with controls (for S2)
To claim a brand is absent from origin-country retail:
1. Search the brand on that country's Amazon and on its two or three biggest pharmacy or health retailers (AU: Amazon.com.au, Chemist Warehouse, Priceline; US: Amazon.com, Walmart, iHerb US, CVS; CA: Amazon.ca, Shoppers Drug Mart; JP: Amazon.co.jp, Rakuten).
2. On the same site and in the same session, search a well-known control product (e.g. "Blackmores Fish Oil" in AU) and record its result count. A nonzero control shows the search works; without it, a "0 results" is weak evidence.
3. Use the site's own search box when URL parameters don't trigger a search (Chemist Warehouse and Priceline ignore `?q=`). Record the final URL, the time with timezone, and a screenshot.
4. Note side effects of geo-location (e.g. Amazon showing "Deliver to United States") and remove any personal data from screenshots before publishing.

### 假洋牌判定 rubric

A 假洋牌 here means a product sold as foreign-made or as a foreign brand whose brand ownership, manufacturing and sales are in fact mainly based in mainland China or Hong Kong, with the foreign identity serving mainly as a marketing label. Score each signal below. Each one needs a source URL and a tag: **一手** (the regulator's or registry's own page, or the company's own website or label) or **二手** (search snippet, mirror site, directory, news report, consumer post).

| # | Signal | Weight |
|---|---|---|
| S1 | The claimed origin has no sale-permitted registration for this product (no AUST L/R, NPN, 届出番号 and so on), or the only entry is export-only (e.g. ARTG "Export Only") | Strong |
| S2 | Absent from mainstream retail in the claimed origin country, including that country's Amazon and main pharmacy chains | Strong |
| S3 | No functioning brand website in the origin country (domain dead, parked, or China-only content) | Medium |
| S4 | The label manufacturer, brand owner, store operator or importer is located in mainland China or HK, or describes itself as an OEM/ODM serving Chinese cross-border sellers | Strong |
| S5 | The trademark was first filed in China/HK, or by an applicant based in China/HK, or the foreign mark changed hands among holding companies shortly before cross-border sales | Medium |
| S6 | Label or listing claims that would not be legal in the origin country (e.g. "TGA认证", "FDA认证", disease claims on a listed medicine) | Medium |
| S7 | Sold mainly through cross-border channels into China (海外旗舰店, 保税仓 / 香港仓发货), with origin fields that contradict each other between listings | Medium |

Verdict scale:

| Verdict | When to use |
|---|---|
| 【假洋牌】 | At least three strong signals, at least two of them verified from 一手 sources, plus no 一手 evidence pointing the other way (e.g. a sale-permitted registration plus real retail presence in the origin country) |
| 【高度疑似假洋牌】 | At least two strong signals, but some of them rest only on 二手 sources, or a live check could not be completed and archived copies were used |
| 【存在假洋牌风险信号】 | One strong signal, or only medium signals |
| 【未发现假洋牌特征】 | Sale-permitted registration in the origin country, real origin-country retail and website, and no China/HK control signal found |

How to write it:
- Put the verdict in the 结论速览 table and open section 2 with it, stated plainly ("综合以下证据，判定为【高度疑似假洋牌】").
- Follow it with the evidence table: 信号 | 事实 | 来源 URL | 一手/二手 | 检索时间.
- Say what would move the verdict up or down (for example "若 TGA 实时查询确认无可售登记，则升级为【假洋牌】").
- The verdict describes origin and brand identity. It is not a finding of counterfeiting or of unsafe contents, so do not say the product is 假货 or harmful unless a regulator or court has said so, and cite that decision.
- For a public video or post that names the brand, show the evidence rows next to the verdict label on screen.

## Third-party certifications (verify in the certifier's own database)
| Program | Database | Status |
|---|---|---|
| USP Dietary Supplement Verified | Product list https://www.quality-supplements.org/usp_verified_products (paginated) and participants https://www.usp.org/verification-services/program-participants | ✅ |
| NSF Contents Tested & Certified | https://info.nsf.org/Certified/Dietary/ and https://www.nsf.org/certified-products-systems | ✅ |
| NSF Certified for Sport | https://www.nsfsport.com/certified-products/ | ✅ |
| Informed Sport / Informed Choice | https://sport.wetestyoutrust.com/ and https://choice.wetestyoutrust.com/ | ✅ |
| BSCG Certified Drug Free | https://www.bscg.org/ | ✅ |
| ConsumerLab (paid, independent testing) | https://www.consumerlab.com/ | ✅ |

"GMP" printed on a label is a claim. In the US, cGMP compliance (21 CFR 111) is mandatory, not a distinction. A third-party GMP registration (NSF/UL) is checkable only in that certifier's list.

## Red-flags checklist
- [ ] "FDA approved / FDA certified" on a supplement
- [ ] Disease treatment or cure claims (cancer, diabetes, 降三高, 根治)
- [ ] 普通食品 / 压片糖果 marketed with health claims; no 蓝帽子 on a general-trade or domestic product that claims health functions
- [ ] Registration number that doesn't match the product or company on the official platform, or can't be found
- [ ] Certification logo not found in the certifier's database
- [ ] Dose above the UL, or proprietary blend hiding amounts
- [ ] Ingredients on FDA warning lists (e.g. DMAA, tianeptine, undeclared sildenafil/sibutramine in "sexual enhancement" or "weight loss" products)
- [ ] Testimonials, "doctors hate this", limited-time pressure, MLM-only sales
- [ ] Price far below the official channel; no flagship store; 个人代购 without 跨境 declaration
- [ ] Recent FDA warning letter or recall for the brand
