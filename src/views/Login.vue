<template>
  <div>
    <el-container>
      <el-header>
        <div style="font-size: 30px; color: #409EFF">
          <a>AircraftWars 排行榜</a>
        </div>
      </el-header>

      <el-main>
        <el-table
            :data="tableData"
            stripe
            style="width: 60%; margin-left: 320px">
          <el-table-column
              type="index"
              width="180">
          </el-table-column>
          <el-table-column
              prop="playerName"
              label="玩家"
              width="180">
          </el-table-column>
          <el-table-column
              prop="score"
              label="分数">
          </el-table-column>
          <el-table-column
              prop="playTime"
              label="日期">
          </el-table-column>
        </el-table>
      </el-main>

    </el-container>
  </div>
</template>

<script>
import request from "../utils/request";

  export default {

    created() {
      request.get("http://127.0.0.1:1234/api/getTopNRankingInfo", {
        params: {
          n: 10,
        }
      }).then(res => {
        this.tableData = res.data;
      })
    },
    data() {
      return {
        tableData: []
      }
    },

  methods: {


  },
  name: "Login.vue"
}
</script>

<style scoped>


</style>