# fnb-monthly-recon

> 面向小型餐饮门店的月结三线对账 Agent Skill：把 POS、支付通道/银行流水、团购平台核销数据放在同一口径下核对，并输出可审阅的月结报告。

[![Skill](https://img.shields.io/badge/Agent%20Skill-fnb--monthly--recon-2ea44f)](skills/fnb-monthly-recon/SKILL.md)
[![Language](https://img.shields.io/badge/language-Chinese-blue)](README.md)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

## 功能概览

- 统一对账期间、交易口径和到账口径
- 汇总 POS、支付通道/银行流水、团购核销三方数据
- 支持总额、分项、逐笔和团购核销交叉核对
- 分类记录差异、原因、证据和后续责任人
- 计算固定成本、变动成本、毛利润、净利润和保守分配金额
- 生成可以直接复制到 Markdown、邮件或内部文档的月结报告

## 目录

```text
.
├── README.md
├── LICENSE
├── examples/
│   └── sample-input.md
├── skills/
│   └── fnb-monthly-recon/
│       └── SKILL.md
└── templates/
    ├── monthly-report.md
    └── reconciliation-checklist.md
```

## 安装与使用

### GitHub Copilot / Agent Skills

打开仓库查看 Skill 文件，或使用支持 Agent Skills 的客户端安装：

```bash
gh skill preview oscar45084321-a11y/fnb-monthly-recon-skill fnb-monthly-recon
gh skill install oscar45084321-a11y/fnb-monthly-recon-skill --skill fnb-monthly-recon
```

> `gh skill` 的具体可用性取决于你的 GitHub CLI 版本和客户端支持情况。也可以手动将 `skills/fnb-monthly-recon/SKILL.md` 复制到目标项目的 Skills 目录。

### 手动使用

1. 准备 POS 交易明细、支付通道/银行流水、团购核销明细和成本数据。
2. 阅读 `examples/sample-input.md`，按同样结构向 Agent 提供数据。
3. 使用 `templates/reconciliation-checklist.md` 逐项确认。
4. 要求 Agent 按 `templates/monthly-report.md` 的结构输出报告。
5. 人工复核差异证据、成本凭证和利润分配协议后再归档。

## 推荐提示词

```text
请按 fnb-monthly-recon Skill 对以下资料进行月结三线对账。
对账期间：YYYY-MM-DD 至 YYYY-MM-DD
POS 口径：按支付时间/下单时间（请选择其一）
支付通道口径：按交易发生日/到账日（请选择其一）
团购口径：按核销时间
请先列出缺失资料和口径冲突，不要猜测；然后输出总额对照、逐笔差异、成本利润核算、待办事项和月结报告。
```

## 输入数据要求

| 数据 | 最少字段 | 建议补充字段 |
|---|---|---|
| POS | 交易时间、订单号、实收金额、支付方式、订单状态 | 原价、折扣、退款金额、团购券码 |
| 支付通道/银行 | 交易或到账时间、金额、交易类型、商户单号 | 手续费、净到账、渠道订单号、退款标记 |
| 团购平台 | 核销时间、券码/订单号、套餐、核销金额、状态 | 结算金额、平台费、退款时间 |
| 成本 | 日期、类别、金额 | 凭证号、是否含税、付款状态 |

## 重要口径说明

- POS 营业额、团购核销金额、平台结算到账金额不是同一个指标，必须分列。
- T+1 或更长到账周期要建立“交易发生日—到账日”的跨日映射，不要简单按自然月相减。
- 现金没有银行流水佐证，应单列并结合 POS 现金记录和实际盘点。
- 报告中的利润和分配金额是管理核算结果，不替代会计、税务或法律意见。
- 不要把银行卡号、身份证号、完整手机号、支付密钥或未脱敏客户信息提交给 Agent。

## 示例与模板

- [结构化输入示例](examples/sample-input.md)
- [月结报告模板](templates/monthly-report.md)
- [对账检查清单](templates/reconciliation-checklist.md)

## 隐私与安全

这是一个通用工作流 Skill，不会自动访问你的 POS、银行或团购后台。分享或提交数据前请脱敏；不要在公开 Issue、Pull Request 或仓库中上传真实流水、商户密钥、账号密码和客户个人信息。

## 贡献

欢迎通过 Issue 或 Pull Request 提交：

- 新的渠道字段映射
- 更清晰的差异分类
- 脱敏后的示例
- 适用于不同门店的报告模板

请不要提交真实财务数据。

## License

MIT，详见 [LICENSE](LICENSE)。
