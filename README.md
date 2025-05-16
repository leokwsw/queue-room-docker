# Queue Room 排隊系統

這是一個簡單易用的排隊管理系統，讓您能夠快速建立和管理排隊服務。無論是餐廳、診所、銀行或其他需要排隊服務的場所，都能輕鬆使用。

## 系統特點

- **即開即用**：只需簡單設置，幾分鐘內即可開始使用
- **無需複雜配置**：只需設置幾個基本參數即可運行
- **穩定可靠**：系統運行穩定，不會出現排隊資料遺失的情況
- **即時更新**：排隊狀態即時更新，讓顧客隨時掌握等待時間
- **靈活運用**：可根據不同場所需求靈活調整

## 快速開始

只需要完成以下簡單步驟，即可開始使用：

1. 安裝必要軟體：
   - Docker（用於運行系統）
   - Git（用於下載系統）

2. 下載系統：
```bash
git clone git@github.com:leokwsw/queue-room-docker.git
cd queue-room-docker
```

3. 設置基本參數：
   - 設置系統運行環境（開發/正式）
   - 設置網站網址
   - 設置安全密碼

4. 啟動系統：
```bash
docker-compose up -d
```

就是這麼簡單！系統啟動後，您就可以立即開始使用排隊管理功能。

## 系統架構

系統由以下服務組成：
- `app`: 主應用程式服務
- `scheduler`: 排程器服務
- `redis`: Redis 快取服務

## 前置需求

- Docker
- Docker Compose
- Git

## 環境設置

1. 克隆主專案：
```bash
git clone <repository-url>
cd queue-room-docker
```

2. 初始化並更新子模組：
```bash
git submodule init
git submodule update
```

3. 環境變數設置：
主應用程式服務（app）需要以下環境變數：
- `NODE_ENV`: 運行環境（development/production）
- `REDIS_HOST`: Redis 主機名稱
- `REDIS_PORT`: Redis 端口
- `REDIS_DB`: Redis 數據庫編號
- `JWT_SECRET`: JWT 密鑰
- `WEB_URL`: Web 應用程式 URL

排程器服務（scheduler）需要以下環境變數：
- `NODE_ENV`: 運行環境（development/production）
- `REDIS_HOST`: Redis 主機名稱
- `REDIS_PORT`: Redis 端口
- `REDIS_DB`: Redis 數據庫編號

> ⚠️ **重要提醒**：`app` 和 `scheduler` 服務的 Redis 相關環境變數（`REDIS_HOST`、`REDIS_PORT` 和 `REDIS_DB`）必須保持完全一致，以確保兩個服務能夠正確地共享和訪問相同的 Redis 數據。

## 運行服務

1. 使用 Docker Compose 啟動所有服務：
```bash
docker-compose up -d
```

2. 查看服務狀態：
```bash
docker-compose ps
```

3. 查看服務日誌：
```bash
docker-compose logs -f [service-name]
```

## 服務說明

### 主應用程式（app）
- 運行在 3000 端口
- 依賴於 Redis 服務
- 使用 JWT 進行身份驗證

### 排程器（scheduler）
- 負責處理排程任務
- 依賴於 Redis 服務

### Redis
- 使用 Redis 7 Alpine 版本
- 啟用 AOF 持久化
- 數據存儲在 Docker volume 中

## 網絡配置

所有服務都在 `app-network` 網絡中運行，使用 bridge 驅動程序。

## 數據持久化

Redis 數據通過 Docker volume `redis-data` 進行持久化存儲。

## 開發說明

1. 修改主應用程式：
```bash
cd queue-room
# 進行修改
```

2. 修改排程器：
```bash
cd queue-room-scheduler
# 進行修改
```

## 注意事項

- 確保所有必要的環境變數都已正確設置
- 在生產環境中，請修改 `JWT_SECRET` 為更安全的值
- 確保 Redis 的持久化設置符合您的需求

## 客製化服務

如果您需要針對特定需求進行系統客製化，例如：
- 新增特定功能
- 修改現有功能
- 整合其他系統
- 調整系統外觀

歡迎直接聯繫我：
- 電子郵件：leokwsw@gmail.com

我們會根據您的需求提供專業的客製化服務。
