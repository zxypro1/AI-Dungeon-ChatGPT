<template>
  <div class="chat-container">
    <div class="chat-messages">
      <div v-for="(message, index) in messages" :key="index">
        <el-card :class="message.type === 'received' ? 'message-received' : 'message-sent'">
          {{ message.content }}
        </el-card>
      </div>
    </div>
    <div class="chat-input">
      <el-input
        v-model="inputMessage"
        type="textarea"
        :rows="1"
        placeholder="输入消息"
        @keyup.enter.native="sendMessage"
        style="background-color: black;"
      />
      <el-button type="primary" @click="sendMessage" style="color: white; background-color: black; border-color: gray;">发送</el-button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputMessage: '',
      messages: [{type: 'received', content: 'test'}],
    };
  },
  methods: {
    sendMessage() {
      if (this.inputMessage.trim()) {
        this.messages.push({ type: 'sent', content: this.inputMessage });
        this.inputMessage = '';
      }
    },
  },
};
</script>

<style scoped>
.chat-container {
  display: flex;
  flex-direction: column;
  height: 90vh;
  border: 1px solid #ccc; /* 添加边框 */
  border-radius: 4px; /* 添加圆角 */
  background-color: #333333;
  color: #ffffff;
}

.chat-messages {
  flex: 1;
  overflow-y: auto;
  padding: 16px;
  display: flex;
  flex-direction: column;
}

.message-received {
  max-width: 100%;
  margin-bottom: 16px;
  border-radius: 20px;
}
.message-sent {
  max-width: 60%;
  margin-bottom: 16px;
  border-radius: 10px;
}

.message-received {
  align-self: flex-end;
  background-color: #333333;
  color: #ffffff;
}

.message-sent {
  align-self: flex-start;
  background-color: #0a0e12;
  color: #ffffff;
  margin-left: auto;
}

.chat-input {
  display: flex;
  align-items: center;
  padding: 8px;
  border-top: 1px solid #ccc; /* 添加顶部边框 */
}

.chat-input > * {
  margin: 4px;
}
</style>
