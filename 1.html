<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>狗狗樂園：每日毛孩萌照</title>
  <style>
    /* 全局設定 */
    body {
      font-family: "Noto Sans CJK TC", "Microsoft YaHei", "微軟正黑體", sans-serif;
      margin: 0;
      padding: 20px;
      background-color: #f0f8ff; /* 淡藍色背景 */
      color: #333;
      display: flex;
      flex-direction: column;
      align-items: center;
      min-height: 100vh;
      box-sizing: border-box;
    }

    /* 容器樣式 */
    .container {
      background-color: #ffffff;
      padding: 30px;
      border-radius: 12px;
      box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
      text-align: center;
      max-width: 600px;
      width: 100%;
      box-sizing: border-box;
      margin-bottom: 20px;
      position: relative; /* 為了載入動畫定位 */
    }

    h1 {
      color: #4682b4;
      margin-bottom: 25px;
      font-size: 2.2em;
    }

    /* 圖片容器與圖片本身樣式 */
    .image-wrapper {
      position: relative; /* 為加載動畫定位 */
      margin-top: 20px;
      margin-bottom: 30px;
      overflow: hidden;
      border-radius: 8px;
      border: 3px solid #add8e6;
      display: inline-block;
      max-width: 100%;
      aspect-ratio: 1 / 1; /* 保持正方形比例，避免載入時高度跳動 */
      min-height: 200px; /* 最小高度 */
      background-color: #e0f2f7; /* 加載時的背景色 */
      display: flex;
      align-items: center;
      justify-content: center;
    }

    #dogImage {
      max-width: 100%;
      height: auto;
      display: block;
      opacity: 0; /* 預設隱藏，用於淡入效果 */
      transition: opacity 0.5s ease-in-out; /* 淡入動畫 */
    }

    /* 載入動畫 */
    .loader {
      border: 6px solid #f3f3f3; /* Light grey */
      border-top: 6px solid #4682b4; /* Blue */
      border-radius: 50%;
      width: 50px;
      height: 50px;
      animation: spin 1s linear infinite;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      z-index: 1; /* 確保在圖片上方 */
    }

    @keyframes spin {
      0% { transform: translate(-50%, -50%) rotate(0deg); }
      100% { transform: translate(-50%, -50%) rotate(360deg); }
    }

    /* 載入狀態與提示訊息 */
    .message-text {
        color: #888;
        font-style: italic;
        margin-top: 15px;
        min-height: 20px;
    }

    /* 錯誤圖片樣式 */
    .error-image {
      max-width: 80%;
      height: auto;
      opacity: 0.5; /* 讓它看起來像個佔位符 */
    }

    /* 按鈕樣式 */
    .button-group {
      margin-top: 20px;
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 15px;
    }

    .action-button {
      background-color: #5cb85c;
      color: white;
      padding: 12px 25px;
      border: none;
      border-radius: 6px;
      font-size: 1.1em;
      cursor: pointer;
      transition: background-color 0.3s ease, transform 0.2s ease, box-shadow 0.2s ease;
      flex-grow: 1;
      max-width: 250px;
      box-shadow: 0 3px 6px rgba(0,0,0,0.1); /* 輕微陰影 */
    }

    .action-button:hover {
      background-color: #4cae4c;
      transform: translateY(-2px);
      box-shadow: 0 5px 10px rgba(0,0,0,0.2);
    }

    .action-button:active {
      background-color: #449d44;
      transform: translateY(0);
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    }

    /* 冷知識區塊樣式 */
    .fun-fact-section {
      background-color: #e6f7ff;
      padding: 20px;
      border-radius: 10px;
      margin-top: 25px;
      border: 1px dashed #a0d9f0;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .fun-fact-section h2 {
      color: #4682b4;
      margin-bottom: 15px;
      font-size: 1.6em;
    }

    .fun-fact-section p {
      font-size: 1.1em;
      line-height: 1.6;
      color: #555;
      margin-bottom: 15px; /* 與按鈕間距 */
      text-align: center;
    }
    
    .fun-fact-section button {
        background-color: #ff9800; /* 橘色按鈕 */
        color: white;
        padding: 8px 15px;
        border: none;
        border-radius: 5px;
        font-size: 0.9em;
        cursor: pointer;
        transition: background-color 0.3s ease;
    }
    .fun-fact-section button:hover {
        background-color: #fb8c00;
    }

    /* 留言區塊樣式 */
    .comment-section {
      background-color: #ffffff;
      padding: 25px;
      border-radius: 12px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.08);
      text-align: left;
      max-width: 600px;
      width: 100%;
      box-sizing: border-box;
      margin-top: 20px;
    }

    .comment-section h2 {
      color: #4682b4;
      margin-bottom: 20px;
      font-size: 1.8em;
      border-bottom: 2px solid #add8e6;
      padding-bottom: 10px;
    }

    .comment-form label {
      display: block;
      margin-bottom: 8px;
      font-weight: bold;
      color: #555;
    }

    .comment-form textarea {
      width: calc(100% - 22px); /* 考慮內邊距和邊框 */
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 5px;
      min-height: 80px;
      resize: vertical;
      font-family: "Noto Sans CJK TC", "Microsoft YaHei", "微軟正黑體", sans-serif;
      box-sizing: border-box; /* 確保寬度計算包含 padding */
    }

    .comment-form button {
      background-color: #007bff;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 5px;
      font-size: 1em;
      cursor: pointer;
      transition: background-color 0.3s ease, transform 0.2s ease;
      margin-top: 15px;
    }

    .comment-form button:hover {
      background-color: #0056b3;
      transform: translateY(-1px);
    }
    .comment-form button:active {
        background-color: #004085;
        transform: translateY(0);
    }

    /* 留言列表樣式 */
    .comment-entry {
        border-top: 1px dashed #eee;
        padding-top: 10px;
        margin-top: 10px;
        word-wrap: break-word; /* 防止長文字溢出 */
    }

    .comment-entry strong {
        color: #444;
    }

    .comment-entry small {
        display: block;
        color: #999;
        font-size: 0.85em;
        margin-top: 5px;
    }

    /* 機械回覆樣式 */
    .bot-response {
        background-color: #e6f7ff; /* 淺藍色背景 */
        border-left: 4px solid #4682b4; /* 左側藍色邊框 */
        padding: 10px;
        margin-top: 10px;
        font-style: italic;
        color: #555;
        border-radius: 5px;
        word-wrap: break-word;
    }

    .bot-response strong {
        color: #4682b4;
    }

    /* 響應式調整 */
    @media (max-width: 768px) {
      body {
        padding: 15px;
      }
      .container, .comment-section, .fun-fact-section {
        padding: 20px;
      }
      h1 {
        font-size: 1.8em;
      }
      .action-button {
        padding: 10px 20px;
        font-size: 1em;
        max-width: none;
      }
      .button-group {
        flex-direction: column;
      }
      .fun-fact-section h2 {
        font-size: 1.4em;
      }
    }

    @media (max-width: 480px) {
      body {
        padding: 10px;
      }
      .container, .comment-section, .fun-fact-section {
        padding: 15px;
      }
      h1 {
        font-size: 1.5em;
      }
      .action-button {
        font-size: 0.95em;
      }
      .fun-fact-section h2 {
        font-size: 1.2em;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>狗狗樂園：每日毛孩萌照</h1>
    <div class="image-wrapper">
      <div class="loader" id="loader"></div> <img id="dogImage" src="" alt="隨機狗狗圖片">
      <img id="errorDogImage" src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxMDAiIGhlaWdodD0iMTAwIiB2aWV3Qm94PSIwIDAgMTAwIDEwMCI+CiAgPHJlY3QgeD0iMCIgeT0iMCIgd2lkdGg9IjEwMCIgaGVpZ2h0PSIxMDAiIGZpbGw9IiNDQ0MiLz4KICA8cGF0aCBkPSJNNTAgMTBjLTUuNSAwLTEwIDQuNS0xMCAxMHYyNi43MThjMC0uNzY0LS43NjItMS4yNDctMS44MjQtMS42MTYtMi44MjYtLjk3OS02LjMyMi0uOTUyLTkuMTgyLS43MDctMi43ODYuMjQ1LTMuODQ0IDEuMTUtNS40MTQgMi43NjYtMi44NjIgMi44NjItMi41MTEgNy43NDctMi41NjkgOC41MTItLjAyNC4zMTEtLjAyNi42NzUtLjAyNiAxLjAxN3Y4Ljg1YzAgLjgyNS4xNzQgMS41NjkuMzU4IDIuMTIyLjE4NC41NTMuNDIxLjk4Ny42ODkgMS4zNjMuMjY4LjM3LjU0NC41OTYuODEuNjk3LjI2Ny4xMDEuNDY1LjE1LjYwMy4xNXYxOS44NzZjMCAxLjEwNS44OTUgMiAxIDJoMjBjMS4xMDUgMCAyLS44OTUgMi0yVjU3LjcxNGMwLS44MjUuMTc0LTEuNTY5LjM1OC0yLjEyMi4xODQtLjU1My40MjEtLjk4Ny42ODktMS4zNjMuMjY4LS4zNy41NDQtLjU5Ni44MS0uNjk3LjI2Ny0uMTAxLjQ2NS0uMTUtLjYwMy0uMTUtMi43ODYtLjI0NS0zLjg0NC0xLjE1LTUuNDE0LTIuNzY2LTIuODYyLTIuODYyLTIuNTExLTcuNzQ3LTIuNTY5LTguNTEyLS4wMjQtLjMxMS0uMDI2LS42NzUtLjAyNi0xLjAxN3YtOC44NWMwLS44MjUuMTc0LTEuNTY5LjM1OC0yLjEyMi4xODQtLjU1My40MjEtLjk4Ny42ODktMS4zNjMuMjY4LS4zNy41NDQtLjU5Ni44MS0uNjk3LjI2Ny0uMTAxLjQ2NS0uMTUgLjYwMy0uMTVsLjE1MiAxMC43MjVjMCAuMTMxLS4wMTUuMTczLS4wMTUuNDUtLjk5MSAxMi43NzUtMS40MTkgMTkuODg3LS40MTEgMjMuNDMyIDEuMDI1IDQuNjc0IDIuOTQ3IDYuNzc3IDcuOTAzIDYuOTkyIDIuMTg5LjA5OCAzLjMzMS4wNDkgMy45MjYtLjEzLS43NDctLjkxNC0xLjE5NS0yLjA0Ni0xLjQyOC0zLjI5My0uMjMyLTEuMjQ3LS4yMTgtMi42NTMtLjAxMi00LjI5Mi4xNDUtMS4yMi42ODItMi4wNjUgMS41NTYtMi41ODcuODc0LS41MjIgMS45OTQtLjcyNyAzLjMxNS0uODczIDEuMzIxLS4xNDYgMi43OTctLjIxOSAzLjgyNy0uMjI2IDEuNDMyLS4wMTEgMy4wMzYtLjAzIDQuODQ0LS4wMDQuOTA0LjAxNSAxLjcxNy4wNDggMi4zMzcuMDg5LS43NDcuOTE0LTEuMTk1IDIuMDQ2LTEuNDI4IDMuMjkzLS4yMzIgMS4yNDctLjIxOCAyLjY1My0uMDEyIDQuMjkyLjE0NSAxLjIyLjY4MiAyLjA2NSAxLjU1NiAyLjU4Ny44NzQuNTIyIDEuOTk0LjcyNyAzLjMxNS44NzMgMS4zMjEuMTQ2IDIuNzk3LjIxOSAzLjgyNy4yMjYgMS40MzIuMDExIDMuMDM2LjAzIDQuODQ0LjAwNC45MDQtLjAxNSAxLjcxNy0uMDQ4IDIuMzM3LS4wODlWMTEuMjE4YzAtLjI1My0uMDI3LS40OTYtLjA4LS43MDctLjA1NC0uMjExLS4xNDUtLjQzMi0uMjY3LS42NTMtLjEyMy0uMjIyLS4yNzctLjQwMS0uNDU5LS41MzgtLjE4My0uMTM2LS4zOTctLjIxOC0uNjI3LS4yNTItLjQzNS0uMDYxLS42ODMtLjA4Ny0xLjM2My0uMTIyLTIuMjEzLS4xMTktMi44MjYtLjIzMi0zLjQ4Ni0uMzMxTDUwIDEwWiIvPgogIDxwYXRoIGQ9Ik01OC4yNjQgNzQuODg4YzAuMTY0LS43NjQuNjYtMS42NzIgMS40OTQtMi42ODMuNTE2LS42MjguNjktMS4xMzYuNzQ3LTEuNDQ5LjA1Ny0uMzE0LjAzNi0uNjQzLS4wNi0uOTc0LS4wOTYtLjMzMi0uMjM4LS41NTYtLjQxMi0uNjQyLS4xNzQtLjA4Ny0uMzc5LS4wOTctLjY1OC0uMDk3aC0zLjU2NmwtLjIyNi0yLNDcuMTctLjExYzIuMTg5LS40OTcgMi45MTktMS4xNjUgMi45MTktMi45MTl2LTMuNjY4YzAtLjE3LS4wMjMtLjMyNC0uMDY5LS40NTgtLjA0NS0uMTM0LS4xMTYtLjI1Mi0uMjExLS4zNTEtLjA5NS0uMDk5LS4yMDgtLjE3Mi0uMzQxLS4yMTctLjEzMy0uMDQ1LS4yOTYtLjA2OC0uNDc4LS4wNjgtLjE1MSAwLS4yODQuMDEzLS40MDUuMDM5VjE4LjM0NmMwLS43NDctLjA3NC0xLjE5NS0uMjIyLTEuNDI5LS4yMzItLjIzMi0uMjE4LS42NDQtLjAxMi0xLjIyLjE0NS0uODcuNjgyLTEuNDYyIDEuNTU2LTEuNzM0LjA4OC0uMDI4LjE3OS0uMDU1LjI2Mi0uMDc5LjI4My0uMDgyLjY1MS0uMTUxIDEuMDQ1LS4yMDQuMzgxLS4wNTIgLjgxMi0uMDkzIDEuMzA1LS4xMjIuNDI3LS4wMjYuODg3LS4wNDMgMS4zMTktLjA0MyAxLjMyMSAwIDIuNzk3LjAxNSAzLjgyNy4wNDUuNzg5LjAyMyAxLjU0Ny4wNTUgMi4zODkuMDg2LjgwNC4wMzEgMS41ODguMDYzIDIuMzkyLjA5MVM2MS45NTUgMTUuNzU4IDYyLjY0IDE2YzIuOTkgLjU1NiA0LjQ2IDEuNjk0IDQuNDYgMy40ODZWMjIuNjEzYzAgLjYxNy4yMDQgMS4xMjguNDA3IDEuNTE3LjIwNC4zOS40NjIuNjUyLjY3OC43ODkuMjE2LjEzNi40MTQuMjA0LjU5NC4yMDQuMTk5IDAgLjQwMi0uMDE0LjYyLS4wNDMtLjY3OC0uNzgxLTEuNTMyLTEuMzk2LTIuNjA3LTEuODUxLS44NTYtLjM1NS0xLjU1Ni0uNTkzLTIuMjg2LS43MTMtLjczLS4xMi0xLjQxMS0uMTQ0LTIuMDQzLS4wOTMtLjYzMi4wNTItMS4xNzcuMTc0LTEuNjMzLjM2M0w1OC4yNjQgNzQuODg4WiIvPgogIDxwYXRoIGQ9Ik0zOS42NzIgNzQuODg4Yy0uMTY0LS43NjQtLjY2LTEuNjcyLTEuNDk0LTIuNjgzLS41MTYtLjYyOC0uNjktMS4xMzYtLjc0Ny0xLjQ0OS0uMDU3LS4zMTQtLjAzNi0uNjQzLjA2LS45NzQuMDk2LS4zMzIuMjM4LS41NTYuNDEyLS42NDIuMTc0LS4wODcuMzc5LS4wOTcuNjU4LS4wOTdoMy41NjZsLjIyNi0yLjI0Ny0uMTctLjExYy0yLjE4OS0uNDk3LTIuOTE5LTEuMTY1LTIuOTE5LTIuOTE5di0zLjY2OGMwLS4xNy4wMjMtLjMyNC4wNjktLjQ1OC4wNDUtLjEzNC4xMTYtLjI1Mi4yMTEtLjM1MS4wOTUtLjA5OS4yMDgtLjE3Mi4zNDEtLjIxNy4xMzMtLjA0NS4yOTYtLjA2OC40NzgtLjA2OC4xNTEgMCAuMjg0LjAxMy40MDUuMDM5VjE4LjM0NmMwLS43NDcuMDc0LTEuMTk1LjIyMi0xLjQyOS4yMzItLjIzMi4yMTgtLjY0NC4wMTItMS4yMi0uMTQ1LS44Ny0uNjgyLTEuNDYyLTEuNTU2LTEuNzM0LS4wODgtLjAyOC0uMTc5LS4wNTUtLjI2Mi0uMDc5LS4yODMtLjA4Mi0uNjUxLS4xNTEtMS4wNDUtLjIwNC0uMzgxLS4wNTItLjgxMi0uMDkzLTEuMzA1LS4xMjItLjQyNy0uMDI2LS44ODctLjA0My0xLjMxOS0uMDQzLTEuMzIxIDAtMi43OTcuMDE1LTMuODI3LjA0NS0uNzg5LjAyMy0xLjU0Ny4wNTUtMi4zODkuMDg2LS44MDQuMDMxLTEuNTg4LjA2My0yLjM5Mi4wOTNTMzYuMDIzIDE1Ljc1OCAzNS4zMzggMTZjLTIuOTkgLjU1Ni00LjQ2IDEuNjk0LTQuNDYgMy40ODZWMTYuMjU2Yy0xLjMxNS0uMTQ1LTIuNzk3LS4yMTktMy44MjctLjIyNi0xLjQzMi0uMDExLTMuMDM2LS4wMy00Ljg0NC0uMDA0LS45MDQuMDE1LTEuNzE3LjA0OC0yLjMzNy4wODlWMTEuMjE4YzAtLjI1My4wMjctLjQ5Ni4wOC0uNzA3LjA1NC0uMjExLjE0NS0uNDMyLjI2Ny0uNjUzLjEyMy0uMjIyLjI3Ny0uNDAxLjQ1OS0uNTM4LjE4My0uMTM2LjM5Ny0uMjE4LjYyNy0uMjUyLjQzNS0uMDYxLjY4My0uMDg3IDEuMzYzLS4xMjJjMi4yMTMtLjExOSAyLjgyNi0uMjMyIDMuNDg2LS4zMzFWMjIuNjEzYzAgLjYxNy0uMjA0IDEuMTI4LS40MDcgMS41MTctLjIwNC4zOS0uNDYyLjY1Mi0uNjc4Ljc4OS0uMjE2LjEzNi0uNDE0LjIwNC0uNTk0LjIwNC0uMTk5IDAtLjQwMi0uMDE0LS42Mi0uMDQzLjY3OC0uNzgxIDEuNTMyLTEuMzk2IDIuNjA3LTEuODUxLjg1Ni0uMzU1IDEuNTU2LS41OTMgMi4yODYtLjcxMy43My0uMTIgMS40MTEtLjE0NCAyLjA0My0uMDkzLjYzMi4wNTIgMS4xNzcuMTc0IDEuNjMzLjM2M0wzOS42NzIgNzQuODg4WiIvPgogIDxjaXJjbGUgY3g9IjI1IiBjeT0iMjUiIHI9IjUiIGZpbGw9IiMzMzMiLz4KICA8Y2lyY2xlIGN4PSI3NSIgY3k9IjI1IiByPSI1IiBmaWxsPSIjMzMzIi8+Cjwvc3ZnPgo=" alt="狗狗走失中" class="error-image">
    </div>
    <p class="message-text" id="statusMessage">正在載入可愛狗狗中...</p>

    <div class="fun-fact-section">
      <h2>狗狗冷知識</h2>
      <p id="dogFunFact">載入中...</p>
      <button id="refreshFactButton">換個冷知識</button>
    </div>

    <div class="button-group">
      <button class="action-button" id="nextDogButton">想再看一張！</button>
      <button class="action-button" id="shareButton">分享到社群</button>
    </div>
  </div>

  <div class="comment-section">
    <h2>留言區</h2>
    <div class="comment-form">
      <label for="commentText">留下你的愛心與評論：</label>
      <textarea id="commentText" placeholder="說說你對這隻狗狗的看法..."></textarea>
      <button id="submitComment">送出留言</button>
    </div>
    <div id="commentsList" style="margin-top: 20px;">
        <p style="color: #666; text-align: center;" id="noCommentMessage">目前沒有留言。</p>
    </div>
  </div>

  <script>
    const dogImageElement = document.getElementById('dogImage');
    const errorDogImageElement = document.getElementById('errorDogImage');
    const loaderElement = document.getElementById('loader');
    const statusMessage = document.getElementById('statusMessage');
    const nextDogButton = document.getElementById('nextDogButton');
    const shareButton = document.getElementById('shareButton');
    const submitCommentButton = document.getElementById('submitComment');
    const commentTextarea = document.getElementById('commentText');
    const commentsList = document.getElementById('commentsList');
    const noCommentMessage = document.getElementById('noCommentMessage');
    const dogFunFactElement = document.getElementById('dogFunFact');
    const refreshFactButton = document.getElementById('refreshFactButton');

    // 狗狗冷知識庫
    const dogFacts = [
      "狗狗的嗅覺比人類靈敏約10萬倍！",
      "狗狗的濕鼻子有助於吸收氣味化學物質，讓牠們的嗅覺更靈敏。",
      "狗狗能透過人類的語氣和肢體語言，理解人類的情緒。",
      "世界上最小的狗狗品種是吉娃娃，最大的則是愛爾蘭獵狼犬。",
      "狗狗平均每分鐘呼吸約10到30次，而興奮時會更快。",
      "狗狗可以用耳朵表達情緒，例如警覺時會豎起。",
      "狗狗的汗腺主要分佈在牠們的腳掌上。",
      "研究表明，與狗狗互動可以降低血壓和心率。",
      "狗狗的平均壽命約為10到14年，但有些品種壽命更長。",
      "狗狗能夢到人類，並在夢中模仿牠們的行為。",
      "狗狗在睡覺時可能會抽動或發出聲音，這表示牠們正在做夢。",
      "成年狗狗有42顆牙齒，比人類多出10顆。",
      "狗狗的瞳孔會放大，以捕捉更多的光線，讓牠們在昏暗環境下看得更清楚。",
      "有些狗狗經過訓練，能偵測出人類的疾病，如癌症或低血糖。",
      "狗狗的指紋（或說是鼻紋）是獨一無二的，就像人類的指紋一樣。",
      "世界上有超過340個被認可的狗狗品種。",
      "狗狗的聽力範圍比人類更廣，能聽到更高頻率的聲音。",
      "當狗狗的尾巴向右搖擺時，通常表示牠們很開心；向左搖擺則可能表示恐懼或緊張。",
      "狗狗會用舔來表達感情，這是一種模仿幼犬時期舔媽媽的行為。",
      "狗狗其實是狼的近親，經過人類馴化而來。"
    ];

    // 機械回覆語句庫
    const botResponses = [
      "汪！感謝您的可愛留言！",
      "您的留言已收到，狗狗很開心喔！",
      "這隻狗狗替您點讚了！謝謝留言！",
      "真是一隻好狗狗，很高興您也喜歡！",
      "您的愛心我們都收到了！"
    ];

    // 顯示冷知識的函數
    function displayRandomFact() {
      const randomIndex = Math.floor(Math.random() * dogFacts.length);
      dogFunFactElement.textContent = dogFacts[randomIndex];
    }

    // 載入狗狗圖片的函數
    function fetchDogImage() {
      // 重置圖片顯示狀態
      dogImageElement.style.opacity = '0'; // 設置為透明，用於淡入
      dogImageElement.style.display = 'none';
      errorDogImageElement.style.display = 'none';

      loaderElement.style.display = 'block'; // 顯示載入動畫
      statusMessage.textContent = '正在載入可愛狗狗中...';
      statusMessage.style.color = '#888';

      fetch('https://dog.ceo/api/breeds/image/random')
        .then(response => {
          if (!response.ok) {
            throw new Error(`HTTP 錯誤！狀態：${response.status}`);
          }
          return response.json();
        })
        .then(data => {
          const imageUrl = data.message;
          dogImageElement.src = imageUrl;
          dogImageElement.alt = "一隻可愛的狗狗圖片"; // 更新圖片替代文字

          dogImageElement.onload = () => {
            loaderElement.style.display = 'none'; // 隱藏載入動畫
            dogImageElement.style.display = 'block';
            dogImageElement.style.opacity = '1'; // 淡入顯示圖片

            statusMessage.textContent = '狗狗圖片載入成功！';
            statusMessage.style.color = '#5cb85c';
            
            // 隨機顯示狗狗冷知識
            displayRandomFact();

            setTimeout(() => {
              statusMessage.textContent = '';
            }, 3000);
          };
          // 處理圖片載入失敗的情況 (如果圖片本身有問題)
          dogImageElement.onerror = () => {
              loaderElement.style.display = 'none';
              dogImageElement.style.display = 'none';
              errorDogImageElement.style.display = 'block'; // 顯示錯誤圖片
              statusMessage.textContent = '圖片載入失敗，狗狗走失中...';
              statusMessage.style.color = 'red';
          };
        })
        .catch(error => {
          console.error('載入狗狗圖片時發生錯誤：', error);
          loaderElement.style.display = 'none';
          dogImageElement.style.display = 'none';
          errorDogImageElement.style.display = 'block'; // 顯示錯誤圖片
          statusMessage.textContent = '載入圖片失敗，請稍後再試。';
          statusMessage.style.color = 'red';
          dogFunFactElement.textContent = '無法載入冷知識。';
        });
    }

    // 首次載入圖片和冷知識
    fetchDogImage();

    // 綁定按鈕事件
    nextDogButton.addEventListener('click', fetchDogImage);
    refreshFactButton.addEventListener('click', displayRandomFact); // 綁定冷知識刷新按鈕

    // 分享按鈕點擊事件 (示意功能)
    shareButton.addEventListener('click', () => {
      // 嘗試使用 Web Share API
      if (navigator.share) {
        navigator.share({
          title: '狗狗樂園：每日毛孩萌照',
          text: '快來看看這些可愛的狗狗！',
          url: window.location.href // 分享當前頁面連結
        }).then(() => {
          console.log('分享成功！');
        }).catch((error) => {
          console.error('分享失敗：', error);
          alert('您的裝置不支援分享功能，或分享被取消了。');
        });
      } else {
        // 如果不支援 Web Share API，提供替代方案
        const currentImageUrl = dogImageElement.src;
        if (currentImageUrl && currentImageUrl.startsWith('http')) {
            prompt('您可以使用以下連結分享這張狗狗圖片：', currentImageUrl);
        } else {
            alert('您的瀏覽器不支援分享功能，或暫時沒有圖片可供分享。');
        }
      }
    });

    // 提交留言按鈕點擊事件 (示意功能)
    submitCommentButton.addEventListener('click', () => {
      const commentText = commentTextarea.value.trim();
      if (commentText) {
        const timestamp = new Date().toLocaleString('zh-TW', {
            year: 'numeric', month: '2-digit', day: '2-digit',
            hour: '2-digit', minute: '2-digit', second: '2-digit',
            hour12: false
        });

        // 訪客留言
        const commentEntryDiv = document.createElement('div');
        commentEntryDiv.className = 'comment-entry';
        commentEntryDiv.innerHTML = `
          <strong>訪客：</strong> ${commentText}
          <br>
          <small>${timestamp}</small>
        `;

        // 機械回覆
        const randomResponseIndex = Math.floor(Math.random() * botResponses.length);
        const botResponse = botResponses[randomResponseIndex];
        const botResponseDiv = document.createElement('div');
        botResponseDiv.className = 'bot-response';
        botResponseDiv.innerHTML = `
          <strong>小助手回覆：</strong> ${botResponse}
        `;

        if (noCommentMessage) {
            noCommentMessage.style.display = 'none'; // 隱藏「目前沒有留言」提示
        }
        commentsList.prepend(botResponseDiv); // 機械回覆放前面
        commentsList.prepend(commentEntryDiv); // 訪客留言放最前面 (最新留言在頂部)
        
        commentTextarea.value = ''; // 清空輸入框
        // 輕微提示，不影響流暢度
        statusMessage.textContent = '留言已送出，感謝您的分享！';
        statusMessage.style.color = '#007bff';
        setTimeout(() => { statusMessage.textContent = ''; }, 3000);
      } else {
        alert('請輸入您的留言！');
      }
    });
  </script>
</body>
</html>
