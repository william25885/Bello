# Bello

一個基於 Vue.js 和 Flask 開發的聚會管理系統，提供用戶認證、聚會創建與管理、即時聊天、個人資料管理以及管理員後台等功能。

## 專案簡介

Bello 是一個全端 Web 應用程式，採用前後端分離架構。系統允許用戶創建和管理聚會活動，參與者可以透過即時聊天功能進行交流，管理員則可以透過後台管理系統監控和管理整個平台。

## 主要功能

### 用戶功能
- 🔐 用戶註冊與登入
- 👤 個人資料管理與更新
- 📅 創建聚會活動
- 🔍 瀏覽與搜尋聚會列表
- ✅ 加入/離開聚會
- 💬 即時聊天功能（私聊與聚會群聊）
- 📋 查看我的聚會列表

### 管理員功能
- 👥 用戶管理（查看、移除用戶）
- 📊 聚會管理（查看、取消、結束聚會）
- 💬 聊天記錄查詢（私聊與聚會聊天記錄）
- 🔍 用戶聊天對象查詢

## 技術棧

### 前端
- **框架**: Vue.js 3.5.13
- **路由**: Vue Router 4.4.5
- **狀態管理**: Pinia 2.2.6
- **UI 框架**: Bootstrap 5.3.3, Bootstrap Vue Next 0.26.10
- **HTTP 客戶端**: Axios 1.7.9
- **建置工具**: Vite 6.0.1

### 後端
- **框架**: Flask 3.1.0
- **資料庫**: PostgreSQL 16.6
- **資料庫驅動**: psycopg2-binary 2.9.10
- **CORS**: Flask-CORS 5.0.0
- **環境變數**: python-dotenv 1.0.1

### 開發環境
- **作業系統**: Windows 11
- **Python**: 3.10.9
- **Node.js**: 21.5.0
- **PostgreSQL**: 16.6

## 專案結構

```
資料庫管理期末專案/
├── backend/                 # 後端 Flask 應用
│   ├── actions/            # API 端點實現
│   │   ├── auth/          # 認證相關（登入、註冊、登出）
│   │   ├── meeting/       # 聚會管理
│   │   ├── profile/       # 個人資料
│   │   ├── admin/         # 管理員功能
│   │   └── chat/          # 聊天功能
│   ├── app.py             # Flask 應用主程式
│   ├── main.py            # 應用入口
│   ├── config.py          # 配置檔案
│   ├── DB_utils.py        # 資料庫工具函數
│   ├── init_bello_db.sql  # 資料庫初始化 SQL
│   ├── requirements.txt   # Python 依賴
│   └── env.example        # 環境變數範例
│
└── frontend/              # 前端 Vue.js 應用
    ├── src/
    │   ├── views/         # 頁面元件
    │   ├── components/    # 可重用元件
    │   ├── router/        # 路由配置
    │   └── stores/        # Pinia 狀態管理
    ├── package.json       # Node.js 依賴
    └── vite.config.js     # Vite 配置
```

## 安裝與設置

### 前置需求

確保已安裝以下軟體：
- Python 3.10.9 或更高版本
- Node.js 21.5.0 或更高版本
- PostgreSQL 16.6 或更高版本

### 後端設置 (127.0.0.1:8800)

1. **配置環境變數**
   
   將 `backend/env.example` 複製為 `backend/.env` 並填入資料庫連線資訊：
   ```bash
   cd backend
   cp env.example .env
   ```
   
   編輯 `.env` 檔案：
   ```env
   DB_NAME=bello
   DB_USER=postgres
   DB_PASSWORD=0000
   DB_HOST=localhost
   DB_PORT=5432
   ```
   
   > ⚠️ **注意**: 預設資料庫密碼為 `0000`，如需更改請同步修改以下檔案：
   > - `backend/DB_utils.py` 第 14 行
   > - `backend/config.py` 第 10 行
   > - `backend/.env` 檔案

2. **安裝 Python 依賴**
   ```bash
   pip install -r requirements.txt
   ```

3. **初始化資料庫**
   
   > ⚠️ **重要**: 如果資料庫已存在且包含舊資料，建議先刪除舊資料庫：
   ```bash
   psql -U postgres
   DROP DATABASE bello;
   \q
   ```
   
   然後執行初始化腳本：
   ```bash
   psql -U postgres -f init_bello_db.sql
   ```
   
   > 📝 **說明**: 
   > - 預設 PostgreSQL port 為 5432
   > - `init_bello_db.sql` 會創建資料庫並插入 10,000 筆測試用戶資料
   > - 如需重新初始化，請先刪除舊資料庫

4. **啟動後端服務**
   ```bash
   python main.py
   ```
   
   後端服務將運行在 `http://127.0.0.1:8800`

### 前端設置 (127.0.0.1:5173)

1. **安裝 Node.js 依賴**
   ```bash
   cd frontend
   npm install
   ```

2. **啟動開發伺服器**
   ```bash
   npm run dev
   ```
   
   前端應用將運行在 `http://127.0.0.1:5173`

### 預設端口配置

- **前端**: 5173 (已預設在程式碼中)
- **後端**: 8800 (已預設在 `.env`、`app.py`、`config.py`、`DB_utils.py`、`main.py` 中)
- **PostgreSQL**: 5432 (已預設在相關配置檔案中)

## 程式架構說明

### 前端 (Vue.js)

1. **Views（頁面元件）**
   - `LoginView` / `RegisterView`: 用戶認證頁面
   - `LobbyView`: 大廳頁面
   - `CreateMeetingView`: 創建聚會頁面
   - `MeetingListView`: 聚會列表頁面
   - `MyMeetingsView`: 我的聚會頁面
   - `ChatView`: 私聊頁面
   - `MeetingChatView`: 聚會聊天頁面
   - `ProfileView`: 個人資料頁面
   - `AdminLobbyView`: 管理員大廳
   - `AdminMeetingsView`: 管理員聚會管理
   - `AdminUsersView`: 管理員用戶管理
   - `AdminUserChatRecordsView`: 用戶聊天記錄查詢
   - `AdminMeetingChatRecordsView`: 聚會聊天記錄查詢

2. **Router（路由系統）**
   - 基於 Vue Router 實現的路由系統
   - 包含 Navigation Guards，控制頁面訪問權限
   - 實現前端頁面導航與狀態管理
   - 支援用戶認證和管理員權限驗證

3. **Components（元件）**
   - `MeetingCard`: 聚會卡片元件
   - `UserMeetingCard`: 用戶聚會卡片元件

### 後端 (Flask)

1. **Actions（API 端點）**
   - `auth/`: 用戶認證相關
     - `login.py`: 用戶登入
     - `signup.py`: 用戶註冊
     - `exit.py`: 用戶登出
   - `meeting/`: 聚會管理功能
     - `create_meeting.py`: 創建聚會
     - `list_meeting.py`: 列出所有聚會
     - `join_meeting.py`: 加入聚會
     - `leave_meeting.py`: 離開聚會
     - `cancel_meeting.py`: 取消聚會
     - `finish_meeting.py`: 結束聚會
     - `my_meetings.py`: 查詢我的聚會
   - `profile/`: 個人資料操作
     - `get_profile.py`: 取得個人資料
     - `update_profile.py`: 更新個人資料
     - `sns_management.py`: 社群媒體管理
   - `admin/`: 管理員功能
     - `users.py`: 用戶管理
     - `meetings.py`: 聚會管理
     - `remove_user.py`: 移除用戶
     - `cancel_meeting.py`: 取消聚會
     - `finish_meeting.py`: 結束聚會
     - `chat_partners.py`: 查詢用戶聊天對象
     - `chat_history.py`: 查詢聊天記錄
     - `meeting_chat.py`: 查詢聚會聊天記錄
   - `chat/`: 即時通訊功能
     - `private_chat.py`: 私聊功能
     - `meeting_chat.py`: 聚會聊天功能
     - `search_user.py`: 搜尋用戶

2. **DB_utils**
   - 封裝與資料庫相關的功能
   - 包含資料庫連線管理與查詢操作
   - 提供統一的資料庫存取介面

3. **CORS 配置**
   - 允許來自 `http://localhost:5173` 的前端請求
   - 支援 GET、POST、PUT、DELETE、OPTIONS 方法

## 測試注意事項

### 多用戶測試

⚠️ **重要**: 在測試多用戶聊天情境時，**不能在同一個瀏覽器開兩個分頁登入不同帳號**，這會導致 session 衝突。

**建議做法**:
- 使用兩個不同的瀏覽器（例如：Safari 和 Chrome）
- 或使用多個無痕視窗登入不同帳號
- 統一在 `http://127.0.0.1:5173` 登入

### 理想 Demo 情境

建議同時開啟三個視窗進行測試：
- 2 個用戶視窗（不同瀏覽器或無痕視窗）
- 1 個管理員視窗

## 常見問題 (FAQ)

### Q: 資料庫連線失敗怎麼辦？
A: 請確認：
1. PostgreSQL 服務是否正在運行
2. `.env` 檔案中的資料庫連線資訊是否正確
3. 資料庫密碼是否在所有相關檔案中一致

### Q: 如何重新初始化資料庫？
A: 
1. 先刪除舊資料庫：`DROP DATABASE bello;`
2. 重新執行初始化腳本：`psql -U postgres -f init_bello_db.sql`

### Q: 前端無法連接到後端 API？
A: 請確認：
1. 後端服務是否運行在 `http://127.0.0.1:8800`
2. 前端是否運行在 `http://127.0.0.1:5173`
3. CORS 配置是否正確

### Q: 如何更改預設端口？
A: 
- 前端端口：修改 `vite.config.js`
- 後端端口：修改 `main.py` 和相關配置檔案
- 資料庫端口：修改 `.env` 和相關配置檔案

## 開發說明

- 本專案採用前後端分離架構，前後端可獨立開發和部署
- 前端使用 Vue 3 Composition API
- 後端使用 Flask Blueprint 組織路由
- 資料庫使用 PostgreSQL，支援複雜查詢和事務處理

## 授權

本專案為資料庫管理課程期末專案。
