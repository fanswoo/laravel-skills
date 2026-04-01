---
name: filament-notes
description: Filament 開發注意事項。當撰寫或修改 Filament 相關程式碼時自動套用，確保遵循專案特定的 Filament 慣例
---

# Filament 開發注意事項

## 元件使用規範

1. **禁止使用 `Placeholder`** — 應使用 `TextEntry` 取代。當需要顯示唯讀資訊時，使用 `TextEntry` 而非 `Placeholder`。

## Resource 放置規範

2. **禁止建立巢狀 Resources 資料夾** — 所有繼承 `Filament\Resources\Resource` 的類別只能放在 `App\Admin\Resources` 或 `App\UserCenter\Resources` 目錄下，不可在子資料夾中再建立 `Resources/` 目錄。例如 `App\Admin\Resources\Quotations\Resources\QuotationItems\Resources\` 這樣的巢狀結構是禁止的。

## Action 鉤子規範

3. **禁止在 Action 上掛載鉤子** — `EditAction`、`DeleteAction`、`CreateAction` 等按鈕上不可撰寫 `before()`、`after()`、`successRedirectUrl()` 等鉤子。如果需要鉤子邏輯，應寫在對應的 Page 類別中（如 `EditPage`、`CreatePage`），使用 Page 提供的 `afterSave()`、`afterCreate()`、`afterDelete()` 等方法。

## Activity Log 規範

4. **Activity Log 使用 pxlrbt 套件** — 需要實作 activity log 時，應使用 `\pxlrbt\FilamentActivityLog\Pages\ListActivities` 類別，不可自行實作 activity log 頁面。

## Filament v5 Namespace 規範

5. **Actions 必須使用 `Filament\Actions` namespace** — Filament v5 中所有 Action 類別（`EditAction`、`DeleteAction`、`CreateAction`、`ViewAction`、`BulkAction` 等）統一位於 `Filament\Actions\` 下。**禁止使用** `Filament\Tables\Actions\`、`Filament\Forms\Actions\` 等舊版 namespace，這些在 v5 中已不存在。
