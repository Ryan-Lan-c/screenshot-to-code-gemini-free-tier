# screenshot-to-code-gemini-free-tier

請選擇語言 / Choose your language:

- 🇹🇼 [中文](./README.md)
- 🇺🇸 [English](./README_en.md)

一個簡單的工具，利用 AI 將截圖、設計稿和 Figma 設計轉換成簡潔、可運行的程式碼。此版本為免費版，使用Gemini 2.5 相關模型，**若需更進階模型，請先取得API KEY後調整程式碼開啟**。~~現已支援 Gemini 3 與 Claude Opus 4.5！~~

原專案請參考來源：https://github.com/abi/screenshot-to-code


https://github.com/user-attachments/assets/85b911c0-efea-4957-badb-daa97ec402ad

支援的技術棧：(最終依然生成html檔)

- HTML + Tailwind
- HTML + CSS
- React + Tailwind
- Vue + Tailwind
- Bootstrap
- Ionic + Tailwind
- SVG

支援的 AI 模型：

- Gemini 2.5 Flash 與 Pro 與 Lite
- ~~Gemini 3 Flash 與 Pro — 最佳模型！（Google）未取得API KEY暫時關閉~~
- Claude Opus 4.5 — 最佳模型！（Anthropic）
- GPT-5.3、GPT-5.2、GPT-4.1（OpenAI）
- 也提供其他模型，但建議優先使用以上模型。
- DALL-E 3 或 Flux Schnell（透過 Replicate）用於圖片生成

更多示範請見下方 [範例](#-範例) 章節。

我們實驗性地支援錄製網站操作影片／螢幕錄影，並將其轉換為可運行的原型。

![google in app quick 3](https://github.com/abi/screenshot-to-code/assets/23818/8758ffa4-9483-4b9b-bb66-abd6d1594c33)

[深入了解影片功能](https://github.com/abi/screenshot-to-code/wiki/Screen-Recording-to-Code)。

[在 Twitter 上追蹤我以獲取最新消息](https://twitter.com/_abi_)。

## 🌍 雲端版本

[在雲端版本試用（付費）](https://screenshottocode.com)。

## 🛠 快速開始

本應用程式的前端使用 React/Vite，後端使用 FastAPI。

所需金鑰：

- [OpenAI API 金鑰](https://github.com/abi/screenshot-to-code/blob/main/Troubleshooting.md)、Anthropic 金鑰，或 Google Gemini 金鑰
- 建議準備多個金鑰，以便比較不同模型的輸出結果

如果想搭配 Ollama 開源模型運行（因品質較差不建議），請參考[此留言](https://github.com/abi/screenshot-to-code/issues/354#issuecomment-2435479853)。

啟動後端（使用 Poetry 管理套件，若尚未安裝請執行 `pip install --upgrade poetry`）：

```bash
cd backend
echo "OPENAI_API_KEY=sk-your-key" > .env
echo "ANTHROPIC_API_KEY=your-key" >> .env
echo "GEMINI_API_KEY=your-key" >> .env
poetry install
poetry env activate
# 執行印出的指令，例如 source /path/to/venv/bin/activate
poetry run uvicorn main:app --reload --port 7001
```

也可以透過前端的設定對話框輸入金鑰（載入前端後點選齒輪圖示）。

啟動前端：

```bash
cd frontend
yarn
yarn dev
```

開啟 http://localhost:1234 即可使用。

若需要讓後端跑在不同的埠號，請修改 `frontend/.env.local` 中的 `VITE_WS_BACKEND_URL`。

## Docker

如果系統已安裝 Docker，在根目錄執行：

```bash
echo "OPENAI_API_KEY=sk-your-key" > .env
docker-compose up -d --build
```

應用程式將在 http://localhost:1234 啟動。請注意，此方式無法進行開發模式，因為檔案變更不會觸發重新建置。

## 🙋‍♂️ 常見問題

- **設定後端時遇到錯誤，該如何解決？** [試試這個方法](https://github.com/abi/screenshot-to-code/issues/3#issuecomment-1814777959)。若仍無法解決，請開一個 Issue。
- **如何取得 OpenAI API 金鑰？** 請參閱 https://github.com/abi/screenshot-to-code/blob/main/Troubleshooting.md
- **如何設定 OpenAI 代理？** 若無法直接存取 OpenAI API（例如受國家限制），可嘗試使用 VPN，或將 OpenAI 的 base URL 設定為代理位址：在 `backend/.env` 或前端設定對話框中設定 `OPENAI_BASE_URL`，請確保 URL 路徑包含「v1」，格式應如：`https://xxx.xxxxx.xxx/v1`
- **如何更改前端連接的後端位址？** 在 `front/.env.local` 中設定 `VITE_HTTP_BACKEND_URL` 和 `VITE_WS_BACKEND_URL`。例如：`VITE_HTTP_BACKEND_URL=http://124.10.20.1:7001`
- **在 Windows 上執行後端時出現 UTF-8 錯誤？** 用 Notepad++ 開啟 `.env` 檔案，前往「編碼」並選擇 UTF-8。
- **如何提供意見回饋？** 歡迎開 Issue 或在 [Twitter](https://twitter.com/_abi_) 上聯繫我。

## 📚 範例

**紐約時報**

| 原始畫面                                                                                                                                                        | 複製結果                                                                                                                                                        |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <img width="1238" alt="Screenshot 2023-11-20 at 12 54 03 PM" src="https://github.com/user-attachments/assets/6b0ae86c-1b0f-4598-a578-c7b62205b3e2"> | <img width="1414" alt="Screenshot 2023-11-20 at 12 59 56 PM" src="https://github.com/user-attachments/assets/981c490e-9be6-407e-8e46-2642f0ca613e"> |


**Instagram**

https://github.com/user-attachments/assets/a335a105-f9cc-40e6-ac6b-64e5390bfc21

**Hacker News**

https://github.com/user-attachments/assets/205cb5c7-9c3c-438d-acd4-26dfe6e077e5
