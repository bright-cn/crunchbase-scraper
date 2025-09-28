# Crunchbase 爬虫

[![Bright Data Promo](https://github.com/bright-cn/LinkedIn-Scraper/raw/main/Proxies%20and%20scrapers%20GitHub%20bonus%20banner.png)](https://www.bright.cn/products/web-scraper/crunchbase)

本仓库提供两种从 Crunchbase 提取商情数据的方法：

1. 基础爬虫脚本：基于浏览器自动化的轻量级方案，适用于有限数据采集。
2. Bright Data Crunchbase 爬虫 API：面向高并发、可扩展、免维护的企业级稳定数据采集方案。

## 目录
- [1. 基础版 Crunchbase 爬虫](#1-基础版-crunchbase-爬虫)
  - [功能](#功能)
  - [先决条件](#先决条件)
  - [实现](#实现)
  - [示例输出](#示例输出)
  - [重要限制与挑战](#重要限制与挑战)
- [2. Bright Data Crunchbase 爬虫 API](#2-bright-data-crunchbase-爬虫-api)
  - [关键优势](#关键优势)
  - [开始使用](#开始使用)
  - [API 方法](#api-方法)
    - [A. 通过 URL 采集 Crunchbase 数据](#a-通过-url-采集-crunchbase-数据)
    - [B. 按关键词发现 Crunchbase 数据](#b-按关键词发现-crunchbase-数据)
- [API 配置与交付选项](#api-配置与交付选项)
- [零代码爬虫界面](#零代码爬虫界面)
- [备选方案：预采集的 Crunchbase 数据集](#备选方案预采集的-crunchbase-数据集)
- [资源与支持](#资源与支持)


## 1. 基础版 Crunchbase 爬虫

一个 Python 实现示例，用于从 Crunchbase 公司页面提取基础公司数据。

<img width="800" alt="Bright Data Platform Interface" src="https://github.com/bright-cn/crunchbase-scraper/blob/main/images/440236063-03b5a4c6-ba43-4595-bab8-96161740e197.png" />

### 功能

该脚本可采集公开可用的数据点，包括：

- 公司基础信息（简介、官网、成立日期）
- 联系方式（邮箱、电话）
- 运营信息（状态、员工规模、所在地）
- 领导层信息（创始人）
- 行业分类

### 先决条件

- 已安装 Python 3.x
- 安装 SeleniumBase 库：`pip install seleniumbase`

### 实现

1. 获取代码：脚本文件见 [free-crunchbase-scraper/crunchbase-scraper.py](https://github.com/bright-cn/crunchbase-scraper/blob/main/free-crunchbase-scraper/crunchbase-scraper.py)
2. 设置目标 URL：打开脚本并将 `target_url` 修改为你要抓取的 Crunchbase 公司页面。
    
    ```python
    target_url = "https://www.crunchbase.com/organization/your-target-company"
    ```
    
3. 运行脚本：在终端执行 `python crunchbase-scraper.py`

💡 说明：该脚本使用 [SeleniumBase](https://seleniumbase.io/)（先进的 Selenium 封装），内置多种能力以处理验证码与其他浏览器挑战。延伸阅读：[使用 SeleniumBase 进行网页抓取](https://www.bright.cn/blog/web-data/web-scraping-with-seleniumbase) 与 [SeleniumBase 搭配代理](https://www.bright.cn/blog/proxy-101/seleniumbase-with-proxies)。

### 示例输出

脚本会以如下结构化格式提取数据：

```jsonc
{
  "description": "Bright Data offers a platform for ethical web data collection and analysis.",
  "website_url": "[https://www.bright.cn](https://www.bright.cn/)",
  "founding_date": "2018-07-01",
  "email": "[sales@brightdata.com](mailto:sales@brightdata.com)",
  "phone": "(888) 538-9204",
  "company_overview": "Bright Data is a data collection platform that helps businesses gather publicly available web data...",
  "headquarters_location": "New York, United States, North America",
  "operating_status": "active",
  "employee_count": "251-500",
  "founder_names": [
    "Derry Shribman",
    "Ofer Vilenski"
  ],
  "industry_categories": [
    "Business Intelligence",
    "Cloud Data Services", "/* ... */"
  ]
}
```

### 重要限制与挑战

该方式会遇到诸多[网页抓取挑战](https://www.bright.cn/blog/web-data/web-scraping-challenges)，使其不适合生产级数据采集：

- IP 封禁与速率限制：Crunchbase 会监控并限制来自同一 IP 的请求。尝试抓取不久后，你的 IP 很可能被封。
- 复杂的反爬机制：包括验证码（如 [Cloudflare Turnstile](https://www.bright.cn/products/web-unlocker/captcha-solver/cloudflare-turnstile)）与行为分析，专门用于识别并阻断自动化脚本。

  <img width="800" alt="Crunchbase CAPTCHA Challenge" src="https://github.com/bright-cn/crunchbase-scraper/blob/main/images/440239044-44cb5a79-e943-454b-9354-28b78ef67b57.png" />

- 动态站点结构：Crunchbase 经常更新页面布局与代码，任何变化都可能导致脚本失效并需要持续维护。
- 可扩展性问题：难以高效处理多 URL 或大批量数据。
- 维护成本高：需自管基础设施、应对封禁、更新脚本并确保合规。


## 2. Bright Data Crunchbase 爬虫 API
[Bright Data Crunchbase 爬虫 API](https://www.bright.cn/products/web-scraper/crunchbase) 提供稳健、可扩展、低门槛的方式，无需处理抓取复杂性即可从 Crunchbase 提取全面数据。

### 关键优势

- 规避技术难题：基于高级代理轮换与解封技术，自动处理 IP 封禁、验证码与限流
- 企业级扩展性：为大规模数据采集而设计
- 高可靠性：企业级可用性与稳定的数据交付
- 友好易用：简洁 API 集成，免去自研与维护成本
- 结构化输出：提供清洗、规范化的数据，开箱即用
- 合规：遵循包括 GDPR、CCPA 在内的数据隐私法规
- 弹性计费：按成功交付计费
- 专属支持：7×24 专家技术支持
- 接入形态：可通过 API 或 [零代码爬虫](https://www.bright.cn/products/web-scraper/no-code) 使用

### 开始使用

1. 创建账号：注册 [Bright Data 账号](https://www.bright.cn/)（新增支付方式后，新用户获 $5 赠金）
2. 生成 API Token：在控制台获取你的[API 密钥](https://docs.brightdata.com/general/account/api-token)
3. 实施指南：API 与零代码两种方式的详细配置步骤见
[setup-bright-data-crunchbase-scraper.md](https://github.com/bright-cn/crunchbase-scraper/blob/main/setup-bright-data-crunchbase-scraper.md)

### API 方法

该 API 提供两种主要采集方式：

#### A. 通过 URL 采集 Crunchbase 数据

针对指定的 Crunchbase 公司页面，返回完整的档案信息。

输入参数：

| 参数 | 必填 | 描述 |
| --- | --- | --- |
| `url` | 是 | Crunchbase 公司页面完整 URL |

示例请求（Python）：

```python
config = {
    "api_token": "YOUR_API_TOKEN",  # 替换为你的实际 Token
    "organizations": [
        {"url": "https://www.crunchbase.com/organization/apple"},
        {"url": "https://www.crunchbase.com/organization/brightdata"},
    ],
    "output_file": "crunchbase-company-profiles.json", # 可选，自定义输出文件名
}
# ... 脚本后续使用该 config
```

- 将 `"YOUR_API_TOKEN"` 替换为你的 Bright Data API Token
- 修改 `organizations` 列表为你的目标 Crunchbase URL
- 可运行完整脚本见：[crunchbase-scraper-api/crunchbase-profile-fetcher.py](https://github.com/bright-cn/crunchbase-scraper/blob/main/crunchbase-scraper-api/crunchbase-profile-fetcher.py)

示例请求（cURL）：

```bash
curl -X POST \
  "https://api.brightdata.com/datasets/v3/trigger?dataset_id=gd_l1vijqt9jfj7olije&include_errors=true" \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '[{"url":"https://www.crunchbase.com/organization/apple"},{"url":"https://www.crunchbase.com/organization/brightdata"}]'
```

示例输出片段：

API 返回全面且结构化的数据。以下为单个公司的部分字段示例：

```jsonc
{
  "companyName": "Bright Data",
  "legalName": "Bright Data",
  "website": "https://www.bright.cn",
  "description": "Offers a platform for ethical web data collection and analysis...",
  "foundedDate": "2014-01-01",
  "location": {"city": "New York", "state": "New York", "country": "United States"},
  "companyType": "For-Profit",
  "operatingStatus": "Active",
  "ipoStatus": "Private (Acquired)",
  "employeeSizeRange": "251-500",
  "industries": ["Business Intelligence", "Cloud Data Services", "..."],
  "keyPersonnel": {
    "ceo": {"name": "Or Lenchner", "...": "..."},
    "founders": [{"name": "Derry Shribman", "...": "..."}, {"name": "Ofer Vilenski", "...": "..."}]
  },
  "webTraffic": {"monthlyVisits": 865525, "source": "Semrush", "...": "..."},
  "technology": {"activeTechCount": 19, "exampleTechUsed": ["Cloudflare Hosting", "..."]},
  "products": {"totalActive": 23, "exampleProductNames": ["Residential Proxies", "..."]},
  "acquisitionDetails": {"acquiredBy": "EMK Capital", "priceUSD": 200000000, "...": "..."},
  "intellectualProperty": {"patentsGranted": 199, "trademarksRegistered": 18}
  // Additional data fields available
}
```

完整示例响应见：[crunchbase-data/crunchbase-company-profiles.json](https://github.com/bright-cn/crunchbase-scraper/blob/main/crunchbase-data/crunchbase-company-profiles.json)

#### B. 按关键词发现 Crunchbase 数据

根据关键词或行业（如 “AI”“Venture Capital”“SaaS”）发现相关公司。

<img width="800" alt="Discover by Keyword Interface Example" src="https://github.com/bright-cn/crunchbase-scraper/blob/main/images/440271152-56e59e94-19fa-4977-84a0-4b70c794cb20.png" />

输入参数：

| 参数 | 必填 | 描述 |
| --- | --- | --- |
| `keyword` | 是 | 用于搜索相关公司的关键词 |

示例请求（Python）：

```python
config = {
    "api_token": "YOUR_API_TOKEN",  # 替换为你的实际 Token
    "keywords": [
        {"keyword": "AI"},
        {"keyword": "Venture Capital"},
        {"keyword": "SaaS"}
        # 可按需添加更多关键词
    ],
    "output_file": "crunchbase-keyword-results.json", # 可选：自定义输出文件名
}
# ... （脚本将使用该 config 调用 API）
```

- 替换 `"YOUR_API_TOKEN"`
- 修改 `keywords` 列表
- 可运行完整脚本见：[crunchbase-scraper-api/crunchbase-keyword-search.py](https://github.com/bright-cn/crunchbase-scraper/blob/main/crunchbase-scraper-api/crunchbase-keyword-search.py)

示例请求（cURL）：

```bash
curl -X POST \
  "https://api.brightdata.com/datasets/v3/trigger?dataset_id=gd_l1vijqt9jfj7olije&include_errors=true&type=discover_new&discover_by=keyword" \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '[{"keyword":"AI"},{"keyword":"Venture Capital"}]'

```

示例输出片段：

响应将包含与关键词匹配的多家公司数据。以下展示其中一个结果的结构：

```jsonc
{
  "companyName": "Airbus", // 例如：匹配关键字 "AI" 的结果
  "legalName": "Airbus Defense and Space Holdings, Inc.",
  "website": "https://us.airbus.com",
  "description": "Airbus designs, manufactures, and delivers aerospace products...",
  "foundedDate": "2014-01-01",
  "location": {
    "city": "Herndon",
    "state": "Virginia",
    "country": "United States"
  },
  "companyType": "For-Profit",
  "operatingStatus": "Active",
  "ipoStatus": "Private",
  "employeeSizeRange": "10001+",
  "industries": [
    "Aerospace",
    "Commercial",
    "Manufacturing"
  ],
  // ... 还包含与“按 URL 采集”方法类似的丰富字段
}
```

完整示例响应见：[crunchbase-data/crunchbase-keyword-results.json](https://github.com/bright-cn/crunchbase-scraper/blob/main/crunchbase-data/crunchbase-keyword-results.json)

## API 配置与交付选项

你可以在 API 请求中通过以下参数自定义任务：

| 参数 | 类型 | 描述 | 示例 |
| --- | --- | --- | --- |
| `limit` | `integer` | 限制每个输入（URL 或关键词）的最大返回条数 | `limit=50` |
| `include_errors` | `boolean` | 返回结果中包含详细错误信息，便于排查 | `include_errors=true` |
| `format` | `enum` | 输出格式（`json`、`csv`、`ndjson`） | `format=csv` |
| `notify` | `url` | 任务完成后回调通知的 Webhook 地址 | `notify=https://...` |

数据可直接投递至你偏好的[外部存储](https://docs.brightdata.com/scraping-automation/web-scraper-api/overview#via-deliver-to-external-storage%3A)或通过 [Webhook](https://docs.brightdata.com/scraping-automation/web-data-apis/web-scraper-api/overview#via-webhook%3A) 交付。

关于 Web Scraper API 与触发任务的完整文档参见：

- [Bright Data Web Scraper API 文档](https://docs.brightdata.com/scraping-automation/web-scraper-api/overview)
- [触发采集 API 参考](https://docs.brightdata.com/api-reference/web-scraper-api/trigger-a-collection)

## 零代码爬虫界面

若你偏好可视化、点选式的配置方式，Bright Data 还提供 [No-Code Scraper](https://www.bright.cn/products/web-scraper/no-code)。基于同样强大的底层基础设施，你无需写代码即可配置并启动 Crunchbase 采集任务。参见[设置指南](https://github.com/bright-cn/crunchbase-scraper/blob/main/setup-bright-data-crunchbase-scraper.md)。

## 备选方案：预采集的 Crunchbase 数据集

若你需要即时获取大量结构化 Crunchbase 数据、且不希望自行运行采集任务，可考虑 Bright Data 的预采集[Crunchbase 数据集](https://www.bright.cn/products/datasets/crunchbase)。

- 即取即用：即时访问已验证、结构化的数据
- 覆盖全面：单个公司档案包含 100+ 数据点
- 定期更新：可选日更、周更、月更或自定义
- 灵活购买：可购买全量或按需子集，匹配预算与需求
- 易于集成：支持 API 或直接下载
- 支持样本：可申请样本评估数据质量与契合度

## 资源与支持

- Bright Data 文档：
  - [Crunchbase 爬虫 API 产品页](https://www.bright.cn/products/web-scraper/crunchbase)
  - [Web Scraper API 文档](https://docs.brightdata.com/scraping-automation/web-scraper-api/overview)
  - [API 参考：触发采集](https://docs.brightdata.com/api-reference/web-scraper-api/trigger-a-collection)
  - [数据集产品页](https://www.bright.cn/products/datasets)
  - [获取 API Token](https://docs.brightdata.com/general/account/api-token)
- 指南与博文：
  - [如何抓取 Crunchbase（全面指南）](https://www.bright.cn/blog/web-data/how-to-scrape-crunchbase)
  - [不被封的网页抓取方法](https://www.bright.cn/blog/web-data/web-scraping-without-getting-blocked)
  - [本仓库中的 Bright Data Crunchbase 爬虫设置指南](https://github.com/bright-cn/crunchbase-scraper/blob/main/setup-bright-data-crunchbase-scraper.md)
- 技术支持：通过账号控制台 7×24 联系支持，或发送邮件至 [support@brightdata.com](mailto:support@brightdata.com)
