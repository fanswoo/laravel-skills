---
name: change-database-to-default-rule
description: 將資料表和欄位名稱轉換為 snake_case。當用戶說「轉換 snake case」、「改成 snake_case」、「資料庫命名規則」或需要將資料表欄位改為 Laravel 標準命名時使用
---

# 轉換資料表至 snake case

## 需求
 - 讀取 $ARGUMENTS 類別，並將其 database 欄位改為 snake_case 命名規則
 - 調整所有對 $ARGUMENTS 類別的引用，以符合新的命名規則

## 功能說明

### 建立 migration
- 資料庫名稱應改為 snake_case，且為複數形式
- 欄位名稱應改為 snake_case

### 修改 $ARGUMENTS 類別的 $table 屬性:
- 資料庫名稱應改為 snake_case，且為複數形式

### 修改 $ARGUMENTS 類別的欄位名稱:
- 欄位名稱應改為 snake_case

### 檢查所有檔案中對 $ARGUMENTS 類別的引用
- 應更新所有該 Eloquent 欄位名稱被其它類別使用的狀況，並注意該欄位在其它 Eloquent 關聯中也可能被引用
- 切記檢查並不限於以下資料夾:
 - app/
 - resources/
 - tests/

## 注意事項
- 撰寫程式碼時，特別注意其可測試性、高閱讀性、低耦合性
- 若適合的話，盡量使用 PHP Attribute 和 Laravel Attribute 取代舊的寫法
