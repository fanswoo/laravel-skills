---
name: puppeteer-automation
description: 使用 Puppeteer 進行網頁自動化。當用戶說「截圖」、「screenshot」、「測試頁面」、「自動化瀏覽器」或需要操作網頁時使用
---

# Puppeteer 網頁自動化

## 任務
$ARGUMENTS

## 設定要求
- 使用 headless 模式
- 忽略 SSL 證書錯誤

## 網站位址
- 首頁: https://ligo.local
- Nova 後台: https://ligo.local/panel
- Admin 後台: https://ligo.local/admin
- UserCenter: https://ligo.local/user-center

## 登入方式
如需登入，使用 `php artisan auth:login 6` 生成登入 URL，然後讓 Puppeteer 訪問該 URL 完成登入

## 截圖儲存
所有截圖儲存於 `storage/temporary` 目錄下
