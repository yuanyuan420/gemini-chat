# 如何使用 GitHub 同步與管理您的 Gemini 對話紀錄

這是一份標準作業流程 (SOP)，教您如何將 Gemini CLI 的對話紀錄，透過 Git 和 GitHub 進行版本控制，以實現在不同電腦間同步與存取。

## (一) 首次設定 (只需操作一次)

在開始前，請先完成以下三個設定步驟。

### 步驟 1：建立 GitHub 儲存庫 (Repository)

在您的 GitHub 網站上，建立一個**新的、空的、私有的 (Private)** 儲存庫。例如，您可以將其命名為 `gemini-chats`。

### 步驟 2：將儲存庫複製 (Clone) 到您的電腦

在您的電腦上，執行 `git clone` 指令，將您剛剛建立的儲存庫下載到本機。

**請告訴 Gemini** 執行以下指令，並將 `[您的儲存庫網址]` 換成您自己的網址：

```bash
git clone [您的儲存庫網址] GeminiChats
```

這會在您的**使用者主目錄**下 (例如 `C:\Users\[您的使用者名稱]\`) 建立一個名為 `GeminiChats` 的資料夾，此資料夾將會與您的 GitHub 儲存庫連結。

### 步驟 3：設定 GitHub 權限 (如果需要)

如果您在本機電腦上使用的 Git 帳號，與 GitHub 儲存庫的擁有者不同，您就需要設定「協作者 (Collaborator)」權限。

1.  **儲存庫擁有者** 前往 GitHub 儲存庫的 `Settings` > `Collaborators and teams`。
2.  點擊 `Add people`，搜尋您在本機使用的 Git 帳號 (例如 `[本機的Git使用者名稱]`)。
3.  給予 **Write** (寫入) 權限。
4.  被邀請的 GitHub 帳號會收到一封 Email，**務必點擊信中連結接受邀請**。

## (二) 日常操作：儲存與同步單次對話

完成首次設定後，每次您想儲存對話時，請遵循以下流程。

### 步驟 1：在 Gemini CLI 中儲存對話

在 Gemini CLI 的互動介面中 (`>`)，使用 `/chat save` 指令儲存目前的對話。**請使用一個簡單的英文或數字名稱，不要包含路徑或特殊字元。**

```
/chat save [您的對話名稱]
```

### 步驟 2：找出並移動對話檔案

`chat save` 指令會將檔案存放在一個暫存資料夾中。您需要告訴 Gemini，幫您找到它並移動到 `GeminiChats` 資料夾。

**您可以這樣對 Gemini 說：**

> 「幫我找到 `[您的對話名稱]` 這個對話紀錄，然後把它移動到 `GeminiChats` 資料夾。」

Gemini 會使用工具找到檔案 (通常位於您**使用者主目錄**下的 `.gemini\tmp\...` 資料夾中)，並將其安全地複製到 `GeminiChats` 資料夾內，並命名為 `[您的對話名稱].json`。

### 步驟 3：將對話同步到 GitHub

當檔案成功移動到 `GeminiChats` 資料夾後，請告訴 Gemini 將它推送到 GitHub。

**您可以這樣對 Gemini 說：**

> 「幫我把 `GeminiChats` 資料夾的變更推送到 GitHub。」

Gemini 會依序為您執行以下三個 `git` 指令：

1.  `git add .`
2.  `git commit -m "Add_new_chat_log"` (訊息可自訂)
3.  `git push`

完成後，您的對話紀錄就安全地儲存在 GitHub 上了。

## (三) 在另一台電腦上繼續對話

當您換到另一台已經完成「首次設定」的電腦時，請依照以下步驟操作。

### 步驟 1：從 GitHub 下載最新紀錄

告訴 Gemini 在 `GeminiChats` 資料夾中，執行 `git pull` 指令，將雲端的紀錄同步到您的電腦。

### 步驟 2：在 Gemini CLI 中載入對話

在 Gemini CLI 的互動介面中 (`>`)，使用 `/chat restore` 指令，並提供您想載入的對話檔案的**完整路徑**。

例如：
```
/chat restore "C:\Users\[您的使用者名稱]\GeminiChats\[對話檔案名稱].json"
```

載入成功後，您就可以從上次中斷的地方繼續對話了。
