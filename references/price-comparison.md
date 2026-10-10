# Price comparison

## Same product, different channels
| Channel | Search URL pattern (checked 2026-10-10) | Notes |
|---|---|---|
| Official site | brand site | Most reliable reference price; US Shopify stores often expose `/products/<handle>.js` (JSON with variants and prices) |
| 京东 | `https://search.jd.com/Search?keyword=<kw>` ✅ (page loads; prices need JS/login) | Prefer 自营 / 官方旗舰店 / 京东国际 自营 |
| 天猫 / 淘宝 | `https://s.taobao.com/search?q=<kw>` ✅ (login wall for results) | Prefer 官方旗舰店 / 天猫国际 海外旗舰店 |
| 拼多多 | `https://mobile.yangkeduo.com/search_result.html?search_key=<kw>` ✅ (app/login needed for results) | High authenticity risk outside 官方旗舰店 / 百亿补贴 |
| 抖音商城 | In-app search only | Check the shop name and 跨境 label |
| iHerb | `https://www.iherb.com/search?kw=<kw>` (home ✅; search may return 403 to scripts) | Ships to China; prices vary with promos |
| Amazon | `https://www.amazon.com/s?k=<kw>` | Often returns pages without prices to scripts |

If you can't read a price, write "未能获取实时价格" and give the search link. **Never estimate.**

## Same ingredient, other brands
Normalize to the **effective daily dose** you assessed in Section 1:

```
price per day = pack price ÷ (units per pack ÷ units per day)
price per unit of active = pack price ÷ (units per pack × amount per unit)   # e.g. per 1000 IU, per 100 mg
```

- Compare the same form where it matters (D3 vs D2; fish oil EPA+DHA content, not "1000 mg fish oil").
- A cheaper per-mg price at a dose above the UL is not a saving. Say so.
- Include shipping/tax if it is a consistent part of the price (跨境 comprehensive tax is usually included in the shown price).

## Authenticity risk (flag, don't accuse)
- Price well below the official/flagship price (e.g. < 60–70%)
- 个人代购, no business licence shown, no 跨境 or 进口 declaration
- No Chinese label on a general-trade import; mismatched batch/expiry
- Brand anti-counterfeit page available? Link it (e.g. "真伪鉴别" on the China site)

## Record keeping
Every price row gets: channel · listing title · pack size · price · currency · **checked at YYYY-MM-DD HH:MM (TZ)** · URL.
