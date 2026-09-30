# 盘叔搜书 v1.5 · 全网电子书一键搜 & 下载 🔍📚

> 一个开箱即用、无需账号配置、聚合多源、纯 Python 标准库的**电子书搜索引擎**。
> 从免费源一路搜到付费可买入口：LibGen 免费直下 → bookfetch 公版古籍 → PanSou 网盘/TG → 付费论坛兜底。想找书，给关键词就够；免费下不到，也告诉你哪家付费站有货、多少钱、怎么买。

| 赞赏码 | 盘叔微信 |
|:---:|:---:|
| ![赞赏码](https://cdn.jsdelivr.net/gh/x3747991-ship-it/sanmingtonghui-bazi-skillpack@main/appreciation.jpg) | ![盘叔微信](https://cdn.jsdelivr.net/gh/x3747991-ship-it/weili-qianli-bazi-skillpack@main/wechat_qr.jpg) |

**觉得好用？欢迎赞赏请盘叔喝杯茶；想交流命理，扫码添加盘叔微信。** 更多命理玄学 AI 技能与干货，关注公众号 **【野生你盘叔】**。

---

## 版本

- **v1.5**（当前）—— 四阶段全覆盖 + LibGen 镜像轮换 + 国内无代理适配 + 补充源层。完整更新明细见 [`CHANGELOG.md`](./CHANGELOG.md)。

## 它解决什么问题

网上找电子书最折磨人的三件事：

- **要配环境**——要么装 pip 包，要么装 node 依赖，要么下载几十 MB 的二进制；
- **要登账号**——各大资源站都要 cookie、要登录、要每日额度；
- **要好几个站轮流试**——LibGen、Z-Library、网盘、古籍库……一个搜不到就再换一个，手点得酸；
- **免费没有就抓瞎**——不知道这书哪里付费能买到。

**盘叔搜书**把这些全干掉：免费源按阶段自动推进，**每阶段的源"可用则用、失败自动跳过"**；免费下不到就进入付费兜底，给你**具体站点、价格、付费方式、入口**，不再大海捞针。

## 四阶段流水线

| 阶段 | 能力 | 源 | 国内无代理直连 |
|---|---|---:|---|
| 0 | LibGen 免费直下（镜像轮换） | libgen.* / Z-Library | ❌ 需代理 |
| 1 | bookfetch 公版古籍（可转 EPUB） | GitHub 公版库 / ctext / 维基文库 | ✅ 部分（ctext 可用） |
| 2 | PanSou 网盘/TG | 百度/夸克/阿里网盘、磁力 | ✅ |
| 3 | 付费论坛兜底 | 国学资源网/古籍屋/道客巴巴/淘宝等（见 `paid_sources.md`） | ✅ |
| 补充 | LibGen 平替 + 古籍 | 九久日记 / 书格 / Anna's Archive / 古登堡 | ✅（Anna's 需代理） |

> 国内无代理用户 = 阶段0 失效但**优雅降级**，阶段1（ctext 古籍）、2、3 与补充源照常可用。

## 两步上手

```
# 搜书——直接给书名/作者，别管格式
python scripts/ebook_hunter.py search 三体

# 下载——看上第几本，给个序号
python scripts/ebook_hunter.py download 3 -o ./books
```

搜索完还顺手帮你处理好：真实文件名还原（含中文文件名乱码修复）、同名自动编号不覆盖、输出目录自动创建。

## 核心特性

- ✅ **开箱即用**：零配置、免认证、零第三方依赖，纯标准库 >=3.8
- ✅ **四阶段全覆盖**：LibGen → bookfetch 古籍 → PanSou 网盘 → 付费兜底
- ✅ **LibGen 镜像轮换**：某镜像被墙/失效自动换下一个，不被单源拖死
- ✅ **付费兜底**：免费下不到时，报"哪家站有货 / 价格 / 付费方式 / 入口"
- ✅ **补充源**：九久日记（LibGen 平替）、书格（古籍）、Anna's Archive（海外）、古登堡（外文公版）
- ✅ **中文完美**：中文书名/作者正常解析、中文文件名正确落盘（修复 Windows Content-Disposition 乱码）
- ✅ **cookie 完全按需**：默认一条 cookie 都不需要；仅明确用 Z-Library 且无凭据时才提示
- ✅ **鲁棒解析**：自研 HTML 解析器，脏 HTML 也能正确抽出书名/作者/年份/格式
- ✅ **省心下载**：防覆盖、目录自动建、Content-Disposition 还原真实文件名
- ✅ **代理友好 + 国内适配**：自动读 `HTTPS_PROXY`；不可达源自动跳过，可加分直连
- ✅ **可分享**：整个 `盘叔搜书/` 文件夹拷走即用，换机零配置

## 快速上手

```bash
# 搜索（默认走免认证源）
python scripts/ebook_hunter.py search <关键词...>

# 限定条数
python scripts/ebook_hunter.py search <关键词...> --limit 30

# 追加 Z-Library（需已配置凭据，否则静默跳过并提示）
python scripts/ebook_hunter.py search <关键词...> --zlib

# 下载：序号对应上次搜索结果的编号
python scripts/ebook_hunter.py download <序号> [-o 下载目录]
```

各阶段的完整调用与国内对策见 [`盘叔搜书/SKILL.md`](./盘叔搜书/SKILL.md)。

**搜索完成后，脚本自动打印「关于盘叔」结尾推送（赞赏码 + 微信 + 公众号 + 苍盘命书）——一次搜索推一次，二维码必带不遗漏。**

## 目录结构

```
panshu-soushu-skillpack/
├── README.md                 # 本文件（介绍 + 赞赏码 + 苍盘广告）
├── CHANGELOG.md              # 更新日志
└── 盘叔搜书/                 # 完整技能包，可直接拷贝分享
    ├── SKILL.md              # 技能定义（四阶段编排 + 结尾广告铁律 + 固定推送模板）
    ├── README.md             # 安装说明
    ├── paid_sources.md       # 阶段3 付费兜底来源目录
    ├── assets/README.md      # 赞赏码/微信二维码图片说明（分享时勿删）
    ├── scripts/ebook_hunter.py  # 阶段0 实现，纯标准库
    └── credentials/README.md    # Z-Library cookie 配置模板（不含真实凭据）
```

## 关于「苍盘命书」

如果你也想看看，自己的八字背后到底隐藏着怎样的人生轨迹——

欢迎报名成为**【苍盘命书免费体验官】**。

**直通链接：** https://mp.weixin.qq.com/s/9NFaItizyhEpjDzmTyEcPQ

---

## License

MIT