# 校園設備報修系統 - 報修地點優化與 Agent 開發文件範例｜Campus Equipment Repair System - Location Field Optimization & Agent Development Example

這個資料夾示範如何將「維修 master（第 D 組）」的「校園設備報修系統（Repair Demo）」專案規格，整理成一組 AI 開發 Agent 可以閱讀、理解並依循的文件結構。

This repository demonstrates how to structure the specification for the "Campus Equipment Repair System (Repair Demo)" (Master Repair / Group D) into a set of standardized context files that AI development agents can read, understand, and follow.

---

## 為什麼需要這些文件？｜Why do we need these files?

如果只對 AI 說「請幫我把地點改成下拉選單」，AI 可能會隨機產生代碼，卻忽略了前後端資料流（如 `app.py` 的 API 相容性）、預設選項防呆機制（`value=""`），或是管理後台 (`admin.html`) 的顯示影響。

If we only instruct the AI to "change the location field into a dropdown select," it might write isolated code without considering the end-to-end data flow (such as `app.py` API compatibility), empty value validation (`value=""`), or proper display on the administrative console (`admin.html`).

這三個文件把不同維度的資訊清晰解耦：
These three files separate different dimensions of project context:

- **規格書 (software-spec.md)**：說明系統要完成什麼需求（將文字框改為下拉選單）與驗收條件。／Explains what the system must accomplish and its acceptance criteria.
- **工作規則 (AGENTS.md)**：說明 Agent 修改程式碼時需遵守的規範與步驟。／Defines the rules and guidelines the Agent must adhere to during development.
- **Skill 模組 (skills/location-select-review/SKILL.md)**：說明處理「地點欄位變更」這一類任務時的標準檢查與測試流程。／Provides a structured evaluation and testing workflow specifically for location input modifications.

---

## 文件結構｜File Structure

```text
repair-demo-agent/
├─ README.md
├─ software-spec.md
├─ AGENTS.md
└─ skills/
   └─ location-select-review/
      └─ SKILL.md
```

---

## 三個核心文件｜The Three Core Files

### software-spec.md
說明校園設備報修系統的地點欄位優化需求 (FR-01 ~ FR-04)、前後端資料傳遞機制以及驗收條件 (AC-01 ~ AC-04)。它回答的是：「這個功能要解決什麼問題？地點選單機制如何運作才算完成？」

Describes the location field optimization requirements (FR-01 ~ FR-04), frontend-backend data flow, and acceptance criteria (AC-01 ~ AC-04). It answers: "What problem does this feature solve, and what defines a completed location dropdown mechanism?"

### AGENTS.md
說明 Agent 在本專案中的角色、修改 `index.html`、`app.py` 與 `admin.html` 前後的規範，確保修改過程不會破壞現有的報修案件邏輯或資料格式。

Specifies the Agent's responsibilities and workflows when modifying `index.html`, `app.py`, and `admin.html`, ensuring changes do not break existing ticket logic or data formats.

### skills/location-select-review/SKILL.md
提供針對「地點欄位變更」任務可重複使用的驗證作業流程，包含防呆選項檢查、後台整合確認與測試案例驗證。

Provides a reusable checklist and testing procedure tailored for location input modifications, including validation check for default empty options, admin dashboard display integration, and test case evaluation.

---

## 如何使用這個範例？｜How to Use This Example

1. **閱讀需求規格**：閱讀 `software-spec.md` 了解地點欄位改為 `<select>` 下拉選單的細節與限制。／Read `software-spec.md` to understand the location field dropdown conversion requirements and boundaries.
2. **遵守開發規則**：閱讀 `AGENTS.md` 了解 Agent 在進行前後端修改時應遵守的原則。／Read `AGENTS.md` to understand the engineering rules for frontend and backend modifications.
3. **執行專用檢查**：當任務涉及地點選單或報修欄位修改時，引導 Agent 載入 `skills/location-select-review/SKILL.md` 進行逐項檢查。／When working on location inputs or repair form fields, prompt the Agent to follow `skills/location-select-review/SKILL.md`.
4. **適應團隊需求**：將此架構推廣並套用到其他模組或小組專案中。／Adapt and scale this framework to other modules or group projects.

---

## 如何比較有沒有這些文件的差異？｜How to Compare the Difference

請將本專案目錄當作獨立工作區開啟，並建立一個新的 AI 開發對話。

1. **無文件對比**：在未載入此結構的對話中，嘗試發問：「請幫我把地點改成下拉選單」，觀察 AI 是否會遺漏預設防呆選項 (`value=""`) 或忽略後台列表與 API 影響。
2. **有文件對比**：在本工作區發問相同的問題，觀察 AI 是否會根據 `AGENTS.md` 與 `software-spec.md` 自動考量 `index.html`、`app.py` 及 `admin.html` 的完整相容性，並依據 `SKILL.md` 輸出完整的測試與確認報告。

To observe the impact, compare asking "Please change the location input to a dropdown menu" in a clean environment versus within this configured workspace. Observe how the Agent automatically incorporates validation constraints (`value=""`), backend API requirements (`app.py`), and admin list displays (`admin.html`) when guided by these structured agent files.