# 跨平台内容转换与分发平台
## Cross-Platform Content Conversion & Distribution Platform

AI 驱动的多平台内容自动转换工具：输入热门视频元数据，自动生成适配 TikTok、YouTube Shorts、Instagram Reels、Twitter/X 与 Reddit 的分发包。

---

## 功能概述

- **输入**：单个热门视频元数据（标题、频道、观看量、时长、URL、描述、热评）
- **输出**：多平台分发包（JSON）+ 自包含演示页面（HTML）
- **支持平台**：YouTube Shorts (9:16)、TikTok (9:16)、Instagram Reels (9:16)、Twitter/X Cards (16:9)、Reddit Thumbnails (1:1)
- **转换策略**：关键帧截取、缩放自适应、平台话题标签生成、视频指纹

---

## 技术栈

- **语言**：Python 3.8+（标准库，零外部依赖）
- **数据来源**：TrendReport.com / YouTube US Trending Top 20
- **包管理**：pip 仅用于测试（必要时），核心模块不依赖第三方库
- **测试**：`unittest`（内置）

---

## 快速开始

```bash
# 1. 从 JSON 运行
echo '{"rank": 1, "title": "Avengers: Doomsday | In Theaters December 18", "channel": "Marvel Entertainment", "views": 16500000, "duration_seconds": 180, "url": "https://www.youtube.com/watch?v=UfNu7pcR0e8", "description": "漫威首支预告片", "top_comment": "观众期待极高"}' | python3 converter.py -

# 2. 跑单元测试
python3 -m unittest test_converter -v
```

---

## 项目结构

```
cross-platform-content-converter/
├── converter.py          # 核心转换引擎
├── test_converter.py     # 单元测试（覆盖 T1-T8）
├── demo/
│   └── index.html        # 演示页面（自包含，零依赖）
├── output/               # 转换输出（JSON + HTML 自动生成）
└── README.md
```

---

## 接口

```python
from converter import ContentConverter, VideoSource

converter = ContentConverter(output_dir="output")
video = VideoSource(
    rank=1,
    title="Avengers: Doomsday",
    channel="Marvel Entertainment",
    views=16_500_000,
    duration_seconds=180,
    url="https://www.youtube.com/watch?v=UfNu7pcR0e8",
    description="...",
    top_comment="...",
)

result = converter.convert(video)  # 全部平台
# 或指定平台
result = converter.convert(video, platforms=["TikTok", "YouTube Shorts"])
```

---

## 数据来源

本工具的演示数据基于 TrendReport.com 发布的 **2026-10-28 YouTube US Trending Top 20**（视频元数据基于公开信息整理）。

---

## 许可

MIT
