---
name: change-eloquent-to-default-rule
description: 將 FF\ORM\ORM 類別轉換為 Laravel Eloquent 標準。當用戶說「轉換到 Eloquent」、「migrate to Eloquent」、「改用 Laravel ORM」或需要將自訂 ORM 遷移到標準 Eloquent 時使用
---

# 轉換至 Eloquent

## 需求
- 讀取 $ARGUMENTS 類別，將其轉換成 laravel 標準使用規則
- 調整所有對 $ARGUMENTS 類別的引用，以符合新的命名規則

## 功能說明

### 修改 $ARGUMENTS 類別的繼承類別:
 - `FF\ORM\ORM` 應改為 `Illuminate\Database\Eloquent\Model`
 - 如有使用 `SoftDeletes` 功能，請改為使用 `Illuminate\Database\Eloquent\SoftDeletes` trait，並確保 `deleted_at` 欄位的變更
 - 如有使用 `Timestamps` 功能，請確保 `created_at` 和 `updated_at` 欄位存在，並移除任何自訂的時間戳記邏輯
 - 注意 Attributes，原 FF\ORM\ORM 中的 Mutators 命名為 xxxGet() xxxSet()，Eloquent 中則為 "xxx(): Attribute"

### 檢查所有檔案中對 $ARGUMENTS 類別的引用
應使用 laravel 標準的 Eloquent方法，切記檢查並不限於以下資料夾:
- app/
- resources/
- tests/

## 注意事項
- 撰寫程式碼時，特別注意其可測試性、高閱讀性、低耦合性
- 若適合的話，盡量使用 PHP Attribute 和 Laravel Attribute 取代舊的寫法
- `FF\ORM\ORM` 類別的路徑位於 '\ligo\vendor\fanswoo\framework-core\src\ORM\ORM.php'
- 應使用 mcp 查詢 laravel v11，確保符合標準
