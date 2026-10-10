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
- Search: ARTG https://www.tga.gov.au/resources/artg ✅ (needs a browser user-agent; plain curl may time out) and the eBS search https://www.ebs.tga.gov.au/ ✅
- An AUST L number means it's listed, not that efficacy was evaluated by TGA.

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
