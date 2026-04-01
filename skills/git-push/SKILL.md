---
name: git-push
description: Git 提交並推送。當用戶說「提交」、「commit」、「push」、「推上去」、「git push」或需要將變更提交並推送到遠端時使用
---

# Git 提交並推送

## 流程

1. 執行 `git status` 檢視目前變更
2. 執行 `git diff --staged` 和 `git diff` 檢視變更內容
3. 執行 `git log --oneline -5` 檢視最近的 commit 風格
4. 根據變更內容，產生簡潔的 commit message（以本專案既有的 commit 風格為準）
5. 如果用戶有提供 `$ARGUMENTS`，則以用戶提供的內容作為 commit message
6. 直接執行，不需要向用戶確認：
   - `git add -A`（加入所有變更，包含未暫存的修改和未追蹤的新檔案）
   - `git commit -m "message"`
   - `git push`

## 注意事項
- 必須提交所有變更（staged + unstaged + untracked），不可只挑選部分檔案
- 如果沒有任何變更，告知用戶「沒有需要提交的變更」並停止
- 不要提交含有敏感資訊的檔案（.env、credentials 等）
- commit message 使用英文，簡潔描述變更內容
