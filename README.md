# Anytime Mailbox residential, non-CMRA US addresses

As of 2026-11-06, 96 of the 2,121 Anytime Mailbox US locations (4.5%) are residential and not a CMRA in USPS data.

- Page: https://tools.upthos.com/en/address/data (中文: https://tools.upthos.com/address/data)
- Files: [`residential-addresses.csv`](residential-addresses.csv), [`residential-addresses.json`](residential-addresses.json) (96 rows, UTF-8, same content)
- Raw URLs: `https://raw.githubusercontent.com/imraywang/anytime-mailbox-residential-addresses/main/residential-addresses.csv`, `https://raw.githubusercontent.com/imraywang/anytime-mailbox-residential-addresses/main/residential-addresses.json` (the same files are also served with CORS at `https://tools.upthos.com/address/data/residential-addresses.csv` and `.json`)
- Verified on: 2026-11-06
- License: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)
- Publisher: UPTHOS (https://upthos.com)

## By state

24 states and DC. Lowest starting monthly price among the listed locations, on the scrape date.

| State | Locations | From |
|---|---|---|
| CA | 16 | $7.99 |
| FL | 14 | $7.99 |
| NY | 14 | $9.99 |
| TX | 10 | $9.49 |
| IL | 6 | $9.99 |
| GA | 5 | $9.99 |
| NC | 4 | $9.99 |
| NJ | 4 | $13.99 |
| WA | 3 | $9.99 |
| AZ | 2 | $9.99 |
| DC | 2 | $14.95 |
| MD | 2 | $9.99 |
| MT | 2 | $14.99 |
| AL | 1 | $39.00 |
| DE | 1 | $8.99 |
| LA | 1 | $39.00 |
| MA | 1 | $49.99 |
| MO | 1 | $14.99 |
| NH | 1 | $39.00 |
| OH | 1 | $19.99 |
| OR | 1 | $9.99 |
| PA | 1 | $11.99 |
| TN | 1 | $9.99 |
| VA | 1 | $19.99 |
| WI | 1 | $9.99 |

## Method

1. **Scrape.** On 2026-11-06 we scraped all 2,121 US locations on the Anytime Mailbox site: address, starting monthly price and location page.
2. **Geocodio pre-filter.** A first pass with Geocodio’s RDI (Residential Delivery Indicator) flagged 323 as residential. The 146 locations Geocodio returned no result for were not checked further.
3. **Smarty, one by one.** Each of the 323 candidates was looked up in Smarty (CASS-certified, USPS data) for RDI, DPV delivery confirmation and the CMRA flag.
4. **Filter.** We kept only addresses that pass all three: DPV-confirmed (Y/S/D), RDI residential, and not flagged as a CMRA. Of 109 confirmed residential, 96 are not CMRAs.

Every address listed was verified, but an address missing from the list is not proven non-residential: the Geocodio pre-filter misses some, so locations that never reached Smarty may include residential ones. Address types change over time; you can re-check one with the address type checker.

## Fields

| Field | Meaning | 含义 |
|---|---|---|
| `address` | Street address (from the location page) | 街道地址（来自网点页） |
| `city` | City | 城市 |
| `state` | Two-letter state code | 州的两字母代码 |
| `zip` | 5-digit ZIP (string, keeps leading zeros) | 5 位邮编（字符串，保留前导 0） |
| `monthly_price_usd` | Cheapest plan’s monthly price on the location page on the scrape date (USD) | 抓取当天网点页上最便宜套餐的月费（美元） |
| `anytime_mailbox_url` | Anytime Mailbox location page (not a referral link) | Anytime Mailbox 网点页（不是推荐链接） |
| `verified_on` | Smarty verification date | Smarty 验证日期 |
| `verification` | Verification standard (constant) | 验证标准，固定值 |

The JSON file is an object with metadata (`name`, `verified_on`, `license`, `source`, `count`, `fields`) and a `records` array; each record has the fields above.

## Updates

Refreshed together with the residential address list: we re-scrape the locations, re-verify only new or changed ones and drop delisted ones, at least once a quarter. verified_on and the date on this page change with each refresh.

## Citation

> UPTHOS Tools, 2026-11-06. Anytime Mailbox residential, non-CMRA US addresses. https://tools.upthos.com/en/address/data

## 中文说明

截至 2026-11-06，Anytime Mailbox 的 2,121 个美国网点中，96 个（4.5%）在 USPS 数据里是住宅且不是 CMRA 代收点。

1. **抓取**：2026-11-06 抓取 Anytime Mailbox 网站上全部 2,121 个美国网点的地址、起步月费和网点页链接。
2. **Geocodio 预筛**：用 Geocodio 的 RDI（住宅投递标识）粗筛，323 个标为住宅，进入下一步。Geocodio 没返回结果的 146 个没有继续检查。
3. **Smarty 逐条验证**：把这 323 个候选逐条交给 Smarty（CASS 认证，数据来自 USPS）查询 RDI、DPV 投递确认和 CMRA 标记。
4. **过滤**：只保留三项都满足的：DPV 确认可投递（Y/S/D）、RDI 为住宅、未被标为 CMRA。109 个确认住宅里去掉 CMRA 后剩 96 个。

这份名单只保证「列出的都验证过」，不保证「没列出的都不是住宅」：Geocodio 预筛会漏判，没进入 Smarty 这一步的网点里可能还有住宅地址。地址类型会随时间变化，使用前可以用地址类型检测再查一次。

许可：CC BY 4.0，可复制、修改、商用，注明来源即可。引用格式：

> UPTHOS Tools, 2026-11-06. Anytime Mailbox 住宅且非 CMRA 美国地址数据集. https://tools.upthos.com/address/data
