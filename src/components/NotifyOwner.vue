<template>
    <div class="container">
        <h1>
            通知车主挪车
        </h1>
        <p>
            如需通知车主，请点击以下按钮
        </p>
        <button class="notify-btn" @click="notifyOwner">通知车主挪车</button>
        <button class="cll-btn" @click="callOwner">打电话</button>
    </div>
    </template>
    <script lang="ts" setup>
        const phone = '1xxxxxxxxxx'; // 车主的手机号
        const wxpusherAppToken = 'AT_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // Wxpusher APP Token
        const wxpusherUIDs = ['UID_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx']; // 车主的UIDs
         
        
        const notifyOwner = async() => {
            try {
                const data = await (await fetch("https://wxpusher.zjiecode.com/api/send/message", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({
                appToken: wxpusherAppToken,
                content: "您好，有人需要您挪车，请及时处理。",
                contentType: 1,
                uids: wxpusherUIDs
                    })
                })).json();
                if (data.code === 1000) {
                alert("通知已发送！");
                    } else {
                alert("通知发送失败，请稍后重试。");
                    }
                } catch (error) {
                 console.error("Error sending notification:", error);
                 alert("通知发送出错，请检查网络连接。");
                 }
                                    };
                const callOwner = () => {
                window.location.href = `tel:${phone}`;
                    };
    </script>
    <style scoped>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }
    body {
      font-family: Arial, sans-serif;
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
      background: #f0f2f5;
      color: #333;
    }
    .container {
      text-align: center;
      padding: 20px;
      width: 100%;
      max-width: 400px;
      border-radius: 8px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
      background: #fff;
    }
    h1 {
      font-size: 24px;
      margin-bottom: 20px;
      color: #007bff;
    }
    p {
      margin-bottom: 20px;
      font-size: 16px;
      color: #555;
    }
    button {
      width: 100%;
      padding: 15px;
      margin: 10px 0;
      font-size: 18px;
      font-weight: bold;
      color: #fff;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      transition: background 0.3s;
    }
    .notify-btn {
      background: #28a745;
    }
    .notify-btn:hover {
      background: #218838;
    }
    .cll-btn {
      background: #17a2b8;
    }
    .cll-btn:hover {
      background: #138496;
    }
    </style>