<template>
  <div class="container">
    <h1>通知车主挪车</h1>
    <p>如需通知车主，请点击以下按钮</p>
    <input
      type="text"
      placeholder="请输入您的电话号码"
      v-model="notifierPhone"
    />
    <button class="notify-btn" @click="notifyOwner">通知车主挪车</button>
    <!-- 只有在通知成功后才显示拨打电话按钮 -->
    <button
      v-if="isNotifySuccessful"
      class="call-btn"
      @click="callOwner"
      :disabled="!isNotifySuccessful"
    >
      拨打车主电话
    </button>
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue";

// 响应式变量
const notifierPhone = ref(""); // 通知人电话号码
const isNotifySuccessful = ref(false); // 是否成功通知车主
const phone = "18976607056"; // 车主的手机号
const wxpusherAppToken = "AT_Ph2M9MV2OvN4sp7dlMm2cFiP9q5EqqEc"; // Wxpusher APP Token
const wxpusherUIDs = [
  "UID_YzpdJt3OaEhwYAe9RUJzi5ZjHmkw",
  "UID_nCZ0QvCNigVjJsbKSukzHgbEzC1d",
]; // 车主的UIDs

// 验证手机号格式
function validatePhoneNumber(phoneNumber: string): boolean {
  const phoneRegex = /^1[34578]\d{9}$/; // 匹配中国大陆手机号
  if (phoneRegex.test(phoneNumber)) {
    return true;
  } else {
    alert("手机号格式错误，请重新输入！");
    return false;
  }
}

// 通知车主
const notifyOwner = async () => {
  if (!notifierPhone.value.trim()) {
    alert("请填写您的电话号码！");
    return;
  }

  // 在通知车主之前验证手机号
  if (!validatePhoneNumber(notifierPhone.value)) {
    return;
  }

  try {
    const data = await (
      await fetch("https://wxpusher.zjiecode.com/api/send/message", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          appToken: wxpusherAppToken,
          content: `您好，有人需要您挪车。通知人电话：${notifierPhone.value}`,
          contentType: 2,
          verifyPayType: 0,
          uids: wxpusherUIDs,
        }),
      })
    ).json();

    if (data.code === 1000) {
      alert("通知已发送！");
      isNotifySuccessful.value = true; // 通知成功，显示拨打电话按钮
    } else {
      alert("通知发送失败，请稍后重试。");
    }
  } catch (error) {
    console.error("Error sending notification:", error);
    alert("通知发送出错，请检查网络连接。");
  }
};

// 拨打车主电话
const callOwner = () => {
  window.location.href = `tel:${phone}`;
};
</script>

<style scoped>
  /* 你的样式 */
</style>


<style scoped>
  /* 你的样式 */
</style>

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
    .call-btn {
      background: #17a2b8;
    }
    .cll-btn:hover {
      background: #138496;
    }
    </style>