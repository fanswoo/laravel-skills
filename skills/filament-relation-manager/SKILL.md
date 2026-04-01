---
name: filament-relation-manager
description: 撰寫 Filament RelationManager。當需要建立或修改 RelationManager 類別時使用，確保使用 $relatedResource 模式且禁止在 RelationManager 中撰寫任何內容
---

# Filament RelationManager 撰寫規範

## 核心原則

**RelationManager 只能包含屬性宣告，絕對禁止撰寫任何方法或邏輯。所有內容（表單、表格、Actions、篩選器等）都必須定義在 `$relatedResource` 指向的 Resource 及其 Schemas/、Tables/ 目錄下。**

## 必要屬性

每個 RelationManager 必須定義以下屬性：

```php
protected static ?string $relatedResource = SomeResource::class; // 必要：指向對應 Resource
protected static string $relationship = 'relationshipName';       // 必要：Eloquent 關聯名稱
protected static ?string $title = '顯示名稱';                      // 選填：UI 顯示標題
```

## 唯一允許的寫法

RelationManager 只允許以下形式，不得有任何額外方法：

```php
<?php

namespace App\Admin\Resources\SomeParent\RelationManagers;

use App\Admin\Resources\SomeChild\SomeChildResource;
use Filament\Resources\RelationManagers\RelationManager;

class SomeChildrenRelationManager extends RelationManager
{
    protected static ?string $relatedResource = SomeChildResource::class;

    protected static string $relationship = 'someChildren';

    protected static ?string $title = '子項目';
}
```

## 嚴格禁止事項

在 RelationManager 中**絕對禁止**以下行為：

1. **禁止定義 `table()` 方法** — 表格設定（欄位、Actions、篩選器）必須在 `$relatedResource` 對應的 Tables/ 目錄下定義
2. **禁止定義 `form()` 方法** — 表單必須在 `$relatedResource` 對應的 Schemas/ 目錄下定義
3. **禁止定義任何 Actions** — headerActions、recordActions 必須在 Resource 的 Table 設定中定義
4. **禁止撰寫業務邏輯** — 所有業務邏輯應放在 Service、Repository 或 Form Schema 的 mutate 方法中
5. **禁止定義查詢修改（modifyQueryUsing）** — 查詢修改應在 Resource 的 Table 設定中處理
6. **禁止沒有 `$relatedResource`** — 每個 RelationManager 都必須有對應的 Resource
7. **禁止定義任何方法** — RelationManager 只能有屬性宣告

## 邏輯應放置的位置

| 邏輯類型 | 正確位置 |
|---------|---------|
| 表單欄位 | `$relatedResource` 的 `Schemas/SomeForm.php` |
| 表格欄位 | `$relatedResource` 的 `Tables/SomeTable.php` |
| headerActions / recordActions | `$relatedResource` 的 `Tables/SomeTable.php` |
| 篩選器 | `$relatedResource` 的 `Filters/` 目錄 |
| 資料變換 | Form Schema 的靜態 `mutateFormDataBeforeCreate()` 方法 |
| 業務邏輯 | Service 或 Repository 類別 |

## 檢查清單

撰寫 RelationManager 前，確認：
- [ ] 對應的 Resource 類別已存在（若不存在，先建立）
- [ ] Resource 的 Form Schema 已定義在 `Schemas/` 目錄
- [ ] Resource 的 Table 已定義在 `Tables/` 目錄（包含所需的 Actions）
- [ ] RelationManager 中**只有**屬性宣告，沒有任何方法
