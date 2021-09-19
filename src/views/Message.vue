<template>
  <div>
    <el-form ref="form" :model="myForm" label-width="80px" class="myForm">

      <el-form-item label="输入框">
        <el-input type="textarea" v-model="myForm.sendMsg"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onSubmit">发送</el-button>
      </el-form-item>
      <el-form-item label="收到消息">
        <el-input type="textarea" v-model="myForm.receiveMsg"></el-input>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  name: "Message.vue",
  data() {
    return {
      myForm: {
        sendMsg: '',
        receiveMsg: ''
      }
    }
  },
  methods: {
    onSubmit() {
      let msg = this.myForm.sendMsg;
      const _this = this;
      let webSocket = new WebSocket("ws://localhost:9090/test/one");
      webSocket.onopen = function (){
        console.log('websocket open');
        webSocket.send(_this.myForm.sendMsg);
      }

      webSocket.onclose = function (){
        console.log('websocket close');
      }

      webSocket.onmessage = function(e){
        _this.myForm.receiveMsg = e.data;
        console.log(e.data);

      }
    }
  }
}
</script>

<style scoped>
  .myForm{
    max-width: 500px;
    margin-top: 300px;
    margin-left: 550px;
  }
</style>