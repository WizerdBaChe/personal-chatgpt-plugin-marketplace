---
date: 2026-08-16
source: user-supplied curated write-up (zh-TW); cites web.dev
  (virtualize-long-lists-react-window) and reactnative.dev (virtualizedlist)
verified: windowing math re-derived at intake (start index, visible count,
  spacer height, O(N) -> O(V+O)) — all correct; concept claims match the
  cited official docs; library-status claims checked by web search 2026-08-16
  (see claims audit)
review-when: the React virtualization library landscape shifts again (last
  checked 2026-08-16 — react-virtuoso ascendant); or a framework/browser-native
  virtualization primitive lands
aliases: [列表虛擬化, list virtualization, windowing, virtual scroll, 虛擬捲動,
  react-window, react-virtual, 長列表]
---

# List virtualization（列表虛擬化）

## Claims audit (intake 2026-08-16)

- FACT — windowing math (`startIndex = ⌊scrollTop/itemHeight⌋`, visible count,
  4,000,000px spacer): re-derived at intake, correct.
- FACT — rendered-DOM cost drops O(N) → O(V+O): matches the cited web.dev doc.
- HEURISTIC — overscan sizing (too small → white flash on fast scroll; too
  large → cancels the savings): doc-backed, context-free, sound.
- FACT — virtualization vs infinite scroll are orthogonal (DOM count vs data
  loading) and usually composed: standard.
- **VOLATILE, status note 2026-08** — the body lists `react-window` and
  `@tanstack/react-virtual` as the common picks. Current ecosystem: react-window
  is mature but AGING (fixed-size lean, little active development); TanStack
  Virtual is actively maintained (headless, max flexibility); **react-virtuoso
  overtook react-window in weekly downloads by early 2026** and is the
  feature-rich default pick (dynamic heights, sticky headers, infinite scroll
  built in). Secondary sources (npm-compare / npmtrends / pkgpulse guides,
  checked 2026-08-16). The user body stands as delivered; consult THIS note
  for current picks.
- Conflicts with model knowledge: none.

## Body（user-supplied, zh-TW, as delivered 2026-08-16）

列表虛擬化（List Virtualization，也稱 **windowing**）是長列表的前端渲染最佳化：資料可以有數萬筆，但 DOM／元件只渲染螢幕可見區域附近的少量項目。使用者捲動時，這個「渲染視窗」隨之移動，離開視窗的項目卸載或被重用，新的可見項目才建立。 [web](https://web.dev/articles/virtualize-long-lists-react-window)

### 它解決什麼問題

若直接渲染 10 萬筆資料，即使畫面同時只看得到 20 筆，瀏覽器仍須建立、排版、繪製並維護 10 萬個 DOM 節點。結果通常是：

- 初始載入與 React commit 很慢。
- 捲動發生 layout、paint 與 GC 壓力，造成掉幀。
- 記憶體占用隨資料筆數線性增加。
- 有互動元件、圖片、複雜列內容時問題更明顯。

虛擬化將「已渲染節點數」從 \(O(N)\) 降到約 \(O(V + O)\)：\(N\) 是總資料筆數、\(V\) 是可視列數、\(O\) 是 overscan 緩衝列數。因此 100 筆和 100 萬筆資料，在視窗高度相同時，DOM 負擔可以接近。 [web](https://web.dev/articles/virtualize-long-lists-react-window)

### 運作原理

假設：

- 容器高 600 px。
- 每列固定高 40 px。
- 總共有 100,000 列。
- 使用者目前的 `scrollTop = 4,000 px`。

可見範圍為：

\[
startIndex = \lfloor 4000 / 40 \rfloor = 100
\]

\[
visibleCount = \lceil 600 / 40 \rceil = 15
\]

若上下各多渲染 5 列做 overscan，實際只要 render index `95` 到 `119`，共 25 個 row，而不是 100,000 個。

但外層仍要模擬完整內容高度：

\[
totalHeight = 100000 \times 40 = 4,000,000\text{ px}
\]

實作上通常建立一個有完整高度的 spacer，並將實際 render 的 row 以 `position: absolute` 或 `translateY` 放到正確的垂直位置。這確保捲軸比例、可捲動距離與定位都正確；未渲染區域以空白空間代表。 [reactnative](https://reactnative.dev/docs/next/virtualizedlist)

```text
scroll container（高 600 px，可捲動）
└── total spacer（高 4,000,000 px）
    └── rendered window（僅 index 95–119）
        ├── row 95  → translateY(3800px)
        ├── row 96  → translateY(3840px)
        └── ...
```

### Overscan 與資料載入

**Overscan** 是在可見區上下多保留少量項目，例如看到 `100–114`，實際 render `95–119`。這能避免快速捲動時短暫出現白畫面，但設太大會抵消虛擬化節省的 DOM 成本。 [web](https://web.dev/articles/virtualize-long-lists-react-window)

要區分兩個常被混用的概念：

| 概念 | 管理什麼 | 例子 |
|---|---|---|
| 虛擬列表 | DOM／元件的渲染數量 | 10 萬筆已在 client 記憶體，僅畫出可視 25 筆 |
| Infinite scroll | 資料的載入時機與分頁 | 捲到底才向 API 取下一頁 50 筆 |
| 兩者組合 | 資料量與 DOM 量 | 分頁取資料，同時只 render 可視範圍 |

大資料產品通常兩者都用：infinite loading 限制前端持有的資料，virtualization 限制 DOM 節點數。

### 實作考量

#### 固定高度列

最好做。只需由 `scrollTop / itemHeight` 算出索引範圍，定位也可直接計算。適用於 log viewer、資料表、選項選單、設定頁清單。

React 常用選擇：

- `react-window`：輕量，適合固定高度或可預估尺寸的 list/grid；其設計就是只保留視窗內的 DOM，捲動時回收或替換節點。 [web](https://web.dev/articles/virtualize-long-lists-react-window)
- `@tanstack/react-virtual`：較底層、彈性高，適合複雜 React 應用。
- React Native：`FlatList`／`VirtualizedList`；後者透過有限的 render window 與空白占位降低記憶體與大型清單效能成本。 [reactnative](https://reactnative.dev/docs/next/virtualizedlist)

（intake note: 現況補充見上方 claims audit 的 VOLATILE 條 — react-virtuoso 已成 2026 的 feature-rich 預設選項。）

#### 可變高度列

例如聊天訊息、Markdown 卡片、動態圖片、高度不定的表格列。這是虛擬化最常見的難點：你不能只用 `index × height` 推導位置。

常見策略：

- 先提供 `estimateSize` 作為預估高度。
- 實際 render 後用 `ResizeObserver` 量測 row 高度。
- 快取每列高度與累積 offset。
- 量測結果改變後，重新計算後續項目的位置。
- 聊天室 prepend 歷史訊息時，補償 `scrollTop`，避免使用者閱讀位置跳動。

在 React 中概念上會像：

```tsx
const rowVirtualizer = useVirtualizer({
  count: messages.length,
  getScrollElement: () => parentRef.current,
  estimateSize: () => 72,
  overscan: 8,
})
```

然後以 `rowVirtualizer.getVirtualItems()` 回傳的虛擬 row，僅 render 它們，並用其計算出的 `start` 放到正確位置。

### 何時該用

建議使用：

- 數百至數十萬筆的 table、activity feed、log、聊天紀錄或檔案清單。
- 每列有複雜 React component、圖表、圖片或昂貴計算。
- 已經觀察到長列表初始 render 慢或捲動掉幀。

不一定要用：

- 幾十筆、結構很簡單的列表。
- 每列高度和互動狀態非常複雜，但資料量小。
- SEO 需要讓所有列表內容都出現在初始 HTML 的場景；虛擬化可能讓視窗外內容不在 DOM。

核心直覺是：**資料不必刪掉，但不可見的資料不必變成 DOM。**
