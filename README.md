# CRM i18n（远程语言包）

面向 CRM2 前端（`crm2-admin`）的 **CDN 远程国际化** 仓库。

- **内置（App 包内）**：`en-US`、`zh-CN`（不放本仓库）
- **远程（本仓库 → jsDelivr）**：其它语言

## CDN

| 项 | 值 |
|---|---|
| 仓库 | `https://github.com/shengrongit/crm-i18n.git` |
| 分支 | `main` |
| CDN 基址 | `https://cdn.jsdelivr.net/gh/shengrongit/crm-i18n@main` |

| 资源 | URL |
|---|---|
| 清单 | `{CDN}/manifest.json` |
| UI 文案 | `{CDN}/i18n/<code>.<version>.json` |
| 长文（可选） | `{CDN}/content/<code>.<version>.json` |

推送后刷新清单缓存：

```bash
curl "https://purge.jsdelivr.net/gh/shengrongit/crm-i18n@main/manifest.json"
```

## 目录

```
crm-i18n/
├── README.md
├── manifest.json
├── _templates/en-US.json   # 英文模板（key 基准，不进 manifest）
├── i18n/
│   └── <code>.<version>.json
└── content/                # 可选
```

## 约定

1. 版本号写在**文件名**里（`vi-VN.2.json`），不要用 `?v=`。
2. 改文案：version +1 → 新文件 → 更新 manifest → push → purge。
3. UI JSON 为扁平结构，配合 `vue-i18n` `flatJson: true`。
4. 以 `_templates/en-US.json` 为唯一 key 模板；其它语言只译值。
5. **不要**把 `zh-CN` / `en-US` 放进 `languages`。
6. **相同译文不要重复写字面量**：只在一处写文本，其余用 `@:canonicalKey` 链接（如 `"wallet.deposit.title": "@:menu.wallet.deposit"`）。同步脚本会自动去重。

完整说明见主仓：`CDN远程国际化模式说明.md`。
