<template>
  <div class="main-panel">
    <div class="header">
      <img class="logo" src="../assets/logo.png" alt="logo"/>
      <div class="title">DevTools</div>
    </div>
    <div class="body">
      <el-card class="box-card">
        <div slot="header" class="clearfix">
          <span>Timestamp Conversion</span>
          <el-button @click="transferTime()" style="float: right; padding: 3px 0" type="text">CONVER</el-button>
        </div>
        <div>
          <el-input
              clearable
              placeholder="Please input timestamp(second)"
              v-model="timestamp">
          </el-input>
          <el-input
              style="margin-top: 10px"
              clearable
              placeholder=""
              v-model="time">
          </el-input>
        </div>
      </el-card>
      <el-card class="box-card">
        <div slot="header" class="clearfix">
          <span>Base64 Decode/Encode</span>
          <el-button @click="base64(1)" style="float: right; padding: 3px 0" type="text">DECODE</el-button>&nbsp;&nbsp;&nbsp;
          <el-button @click="base64()" style="float: right; padding: 3px 0" type="text">ENCODE</el-button>
        </div>
        <div>
          <el-input
              type="textarea"
              :autosize="{ minRows: 2, maxRows: 4}"
              placeholder="Please input content"
              v-model="base64_source">
          </el-input>
          <el-input style="margin-top: 10px" type="textarea" :autosize="{ minRows: 2, maxRows: 4}"
                    v-model="base64_target"></el-input>
        </div>
      </el-card>
      <el-card class="box-card">
        <div slot="header" class="clearfix">
          <span>UUID Gen</span>
          <el-button @click="genUUID" style="float: right; padding: 3px 0" type="text">GEN UUID</el-button>
        </div>
        <div v-for="o in uuids" :key="o" class="text item">
          {{ o }}
        </div>
      </el-card>
    </div>
  </div>
</template>

<script>
import {v4 as uuidv4} from 'uuid';

export default {
  name: "MainPanel",
  components: {},
  created() {
    this.genUUID()
  },
  data() {
    return {
      timestamp: "",
      time: "",
      base64_source: "",
      base64_target: "",
      uuids: []
    }
  },
  methods: {
    base64(type) {
      if (this.base64_source === '' || this.base64_source.trim() === '') {
        return;
      }
      if (type) {
        this.$message.success("base64 decode")
        this.base64_target = Buffer.from(this.base64_source, 'base64').toString('ascii')
      } else {
        this.$message.success("base64 encode")
        this.base64_target = Buffer.from(this.base64_source).toString('base64')
      }
    },
    genUUID() {
      let uuids = []
      for (let i = 0; i < 4; i++) {
        uuids.push(uuidv4())
      }
      this.uuids = uuids
    },
    transferTime() {
      if (this.timestamp === '' || this.timestamp.trim() === '') {
        return;
      }
      this.time = this.timetrans(this.timestamp)
    },
    timetrans(date) {
      var date = new Date(date * 1000);
      var Y = date.getFullYear() + '-';
      var M = (date.getMonth() + 1 < 10 ? '0' + (date.getMonth() + 1) : date.getMonth() + 1) + '-';
      var D = (date.getDate() < 10 ? '0' + (date.getDate()) : date.getDate()) + ' ';
      var h = (date.getHours() < 10 ? '0' + date.getHours() : date.getHours()) + ':';
      var m = (date.getMinutes() < 10 ? '0' + date.getMinutes() : date.getMinutes()) + ':';
      var s = (date.getSeconds() < 10 ? '0' + date.getSeconds() : date.getSeconds());
      return Y + M + D + h + m + s;
    }
  }
}
</script>

<style scoped>
.main-panel {
  width: 100%;
  height: 100%;
  /*margin-left: 10px;*/
}

.main-panel > .header {
  width: 100%;
  height: 40px;
  border-bottom: 1px solid #dddddd;
  box-sizing: border-box;
  padding: 6px 12px;
}

.logo {
  width: 28px;
  height: 28px;
  display: inline-block;
}

.title {
  font-size: 14px;
  margin-left: 18px;
  display: inline-block;
  line-height: 28px;
  vertical-align: top;
}

.text {
  font-size: 15px;
}

.item {
  margin-bottom: 18px;
}

.clearfix:before,
.clearfix:after {
  display: table;
  content: "";
}

.clearfix:after {
  clear: both
}

.box-card {
  margin-top: 20px;
  /*width: 480px;*/
}
</style>
