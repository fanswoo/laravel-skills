---
name: tailwindcss-development
description: "使用 Tailwind CSS v4 utilities 為應用程式設定樣式。當新增樣式、重新調整元件樣式、處理漸層、間距、版面配置、flex、grid、響應式設計、深色模式、顏色、排版或邊框時啟用；或當使用者提到 CSS、樣式、classes、Tailwind、restyle、hero section、卡片、按鈕或任何視覺/UI 變更時也會啟用。"
license: MIT
metadata:
  author: laravel
---

# Tailwind CSS 開發

## 何時啟用

在以下情境啟用此技能：

- 為元件或頁面新增樣式
- 處理響應式設計
- 實作深色模式
- 將重複的樣式抽取為元件
- 除錯間距或版面配置問題

## 文件查詢

使用 `search-docs` 取得 Tailwind CSS v4 的詳細模式與文件。

## 基本使用

- 使用 Tailwind CSS classes 為 HTML 設定樣式。在引入新的樣式模式前，先檢查並遵循專案既有的 Tailwind 慣例。
- 主動建議將重複的樣式模式抽取為符合專案慣例的元件（例如 Blade、JSX、Vue）。
- 留意 class 的擺放位置、順序、優先順序與預設值。移除多餘的 classes，謹慎地將 classes 放到父層或子層元素以減少重複，並將元素做合理的群組。

## 嚴格規範

- **禁止任何自定義名稱的 CSS**：不得撰寫自定義 class 名稱或自訂 CSS 樣式（例如 `.my-card`、`.custom-button`）。一律只能使用 Tailwind 提供的 utility classes。若需要複用樣式，請抽成元件（Blade/Vue/JSX）而不是自訂 CSS。
- **禁止使用 arbitrary values**：不得使用方括號的任意值語法，例如 `w-[12px]`、`text-[20px]`、`bg-[#123456]`、`mt-[13px]`。一律使用 Tailwind 預設的 spacing / size / color scale。若預設 scale 不足，請透過 `@theme` 擴充設計 token，而非使用 arbitrary values。

## Tailwind CSS v4 特定事項

- 一律使用 Tailwind CSS v4，並避免使用已棄用的 utilities。
- Tailwind v4 不支援 `corePlugins`。

### CSS-First 設定

在 Tailwind v4 中，設定改為 CSS-first，透過 `@theme` 指令來完成——不再需要獨立的 `tailwind.config.js` 檔案：

<!-- CSS-First Config -->
```css
@theme {
  --color-brand: oklch(0.72 0.11 178);
}
```

### Import 語法

在 Tailwind v4 中，使用標準的 CSS `@import` 語法引入 Tailwind，取代 v3 使用的 `@tailwind` 指令：

<!-- v4 Import Syntax -->
```diff
- @tailwind base;
- @tailwind components;
- @tailwind utilities;
+ @import "tailwindcss";
```

### 被取代的 Utilities

Tailwind v4 移除了已棄用的 utilities。請使用下表所列的替代方案。不透明度的數值仍維持數字格式。

| 已棄用 | 替代方案 |
|------------|-------------|
| bg-opacity-* | bg-black/* |
| text-opacity-* | text-black/* |
| border-opacity-* | border-black/* |
| divide-opacity-* | divide-black/* |
| ring-opacity-* | ring-black/* |
| placeholder-opacity-* | placeholder-black/* |
| flex-shrink-* | shrink-* |
| flex-grow-* | grow-* |
| overflow-ellipsis | text-ellipsis |
| decoration-slice | box-decoration-slice |
| decoration-clone | box-decoration-clone |

## 間距

在同層元素之間使用 `gap` utilities 來設定間距，而不是使用 margin：

<!-- Gap Utilities -->
```html
<div class="flex gap-8">
    <div>Item 1</div>
    <div>Item 2</div>
</div>
```

## 深色模式

若既有的頁面與元件支援深色模式，新增的頁面與元件也必須以相同方式支援，通常是透過 `dark:` variant：

<!-- Dark Mode -->
```html
<div class="bg-white dark:bg-gray-900 text-gray-900 dark:text-white">
    Content adapts to color scheme
</div>
```

## 常見模式

### Flexbox 版面配置

<!-- Flexbox Layout -->
```html
<div class="flex items-center justify-between gap-4">
    <div>Left content</div>
    <div>Right content</div>
</div>
```

### Grid 版面配置

<!-- Grid Layout -->
```html
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
    <div>Card 1</div>
    <div>Card 2</div>
    <div>Card 3</div>
</div>
```

## 常見陷阱

- 使用已棄用的 v3 utilities（bg-opacity-*、flex-shrink-* 等）
- 使用 `@tailwind` 指令而非 `@import "tailwindcss"`
- 嘗試使用 `tailwind.config.js` 而非 CSS `@theme` 指令
- 在同層元素之間使用 margin 而非 gap utilities 來設定間距
- 專案使用深色模式時忘記加上深色模式 variants
- 撰寫自定義 class 名稱或自訂 CSS 樣式
- 使用 arbitrary values（例如 `w-[12px]`、`text-[#abcdef]`）
