<template>
  <div id="">
    <groupTemplate :root="root" :parent="null"></groupTemplate>
    <el-button class="mainBtn" type="success" @click.prevent="submitQuery()">提交查询</el-button>
    <el-button type="info" @click.prevent="resetRules()">重置</el-button>
  </div>
</template>

<script>
import ruleTemplate from './components/ruleTemplate';
import groupTemplate from './components/groupTemplate';
import axios from 'axios';
import qs from 'qs';
export default {
  name: 'App',
  components: { ruleTemplate, groupTemplate },
  data() {
    return {
      root: {
        essential: 'true',
        condition: 'and',
        rules: [
          {
            field: '',
            operation: '',
            string: '',
            value1: '',
            value2: '',
          },
        ],
      },
    };
  },
  methods: {
    resetRules() {
      this.root = {
        essential: 'true',
        condition: 'and',
        rules: [
          {
            field: '',
            operation: '',
            String: '',
            value1: '',
            value2: '',
          },
        ],
      };
    },
    submitQuery() {
      axios
        .post(
          'http://localhost:8081/product/submitQueryRules',
          qs.stringify({
            queryRules: JSON.stringify(this.root),
          })
        )
        .then((response) => {
          alert(response.data);
        })
        .catch((err) => {});
    },
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.mainBtn {
  margin-left: 50px;
}
</style>
