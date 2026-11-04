# Swell

> 两个关于波的小游戏。纸白、墨黑、朱红，纯静态，双击即玩。

**Swell** is a tiny collection of two wave-themed browser games — one about a sine curve you can bend, one about stacking harmonics into a chord. No framework, no build step, no network: every page is a self-contained HTML file.

---

## 两个游戏

### 波相 · Wavephase

拖动振幅、波长、相位，让一条正弦曲线同时穿过所有圆环。

- 五关递进：初见（只调振幅）→ 相位 → 波长 → 三环 → 细调（小环）
- 自由模式：圆环随机生成，由随机的解反推位置，保证可解
- 曲线穿过圆环即点亮（容差 = 环半径的 65%），全部点亮并保持 0.55 秒通关
- 通关时主曲线向上下扩散出一层层更浅的复制波，随后一起淡出

### 谐律 · Harmonic

把几条正弦叠成一段和声。选卡、转相位、贴合度达标即可施法。

- 六关：单音 → 双音 → 和弦 → 拍音 → 泛音 → 全奏
- 贴合度 ≥ 87% 施法，通关印章碎成红粒子并扩散波纹
- 六种音色全部现场合成：吉他、钢琴、古筝、木琴、钟、弦乐
- 两个彩蛋：按 `7` 进入「潮」，按 `8` 进入「涟」

---

## 在线玩

- 主页：<https://swell-bep.pages.dev/>
- 波相：<https://swell-bep.pages.dev/wavephase/>
- 谐律：<https://swell-bep.pages.dev/harmonic/>

## 本地玩

双击 `index.html` 即可（会跳到 `swell.html`）。也可以直接打开 `wavephase/index.html` 或 `harmonic/index.html`。

无需服务器、无需联网、无外部依赖。

## 技术要点

- **零依赖**：没有框架、没有构建、没有 CDN，CSS 与 JS 全部内联
- **设计坐标 1600×900**：所有绘制按设计坐标写，再按 `min(w/1600, h/900)` 等比缩放；`devicePixelRatio` 单独处理，文字不会糊
- **WebAudio 实时合成**：Karplus-Strong 拨弦（吉他、古筝）、加性合成（钢琴、木琴、钟）、锯齿波 + 滤波包络（弦乐）；混响用程序生成的脉冲响应
- **物理与数学写死**：波相是 `y = A·sin(2π(x−x₀)/λ + φ)`，谐律是 `Σ aᵢ·sin(2πfᵢu + φᵢ)`，判定用解析式而不是采样近似
- **自检**：每个游戏都带一套内置测试，地址后加 `?selftest=1` 即可跑（波相 11 项、谐律 62 项）

## 目录

```
swell/
├─ index.html              入口，自动跳到 swell.html
├─ swell.html              主页：两张大卡片 + 实时预览
├─ wavephase/index.html    波相
├─ harmonic/index.html     谐律
└─ screenshots/
```

`standalone/swell.html` 是把整套东西塞进一个文件的版本（约 120 KB），适合离线分发。

## 兼容性

- 桌面 Chrome / Edge / Firefox 最新版
- 设计为桌面 16:9，未做手机适配
- 音频需要先点击一次页面才会响（浏览器策略）

## 许可

MIT
