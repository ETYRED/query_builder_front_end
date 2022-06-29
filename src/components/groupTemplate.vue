<template>
  <div class="groupDiv" v-if="root.condition">
    <div>
      <!-- <el-button-group>
        <el-button type="primary" size="small">AND</el-button>
        <el-button type="primary" size="small">OR</el-button>
      </el-button-group> -->
      <el-radio class="radio" v-model="root.condition" label="and">and</el-radio>
      <el-radio class="radio" v-model="root.condition" label="or">or</el-radio>
      <el-button class="groupBtn" type="primary" size="small" @click.prevent="addRule(root)">
        添加条件
      </el-button>
      <el-button class="groupBtn" type="primary" size="small" @click.prevent="addGroup(root)">
        添加条件组
      </el-button>
      <el-button
        v-if="!root.essential"
        type="danger"
        size="small"
        @click.prevent="deleteGroup(root, parent)"
      >
        删除
      </el-button>
    </div>
    <groupTemplate
      v-for="(item, index) in root.rules"
      :key="index"
      :root="item"
      :parent="root.rules"
    ></groupTemplate>
  </div>

  <div v-else>
    <ruleTemplate :root="root" :parent="parent"></ruleTemplate>
  </div>
</template>

<script>
import ruleTemplate from './ruleTemplate';
export default {
  name: 'groupTemplate',
  data() {
    return {
      msg: 'hello vue',
    };
  },
  components: { ruleTemplate },
  props: {
    root: Object,
    parent: Array,
  },
  methods: {
    addRule(root) {
      root.rules.push({
        field: '',
        operation: '',
        string: '',
        value1: '',
        value2: '',
      });
    },
    addGroup(root) {
      root.rules.push({
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
      });
    },
    deleteGroup(root, parent) {
      var index = parent.indexOf(root);
      if (index > -1) {
        parent.splice(index, 1);
      }
    },
  },
};
</script>

<style>
.groupDiv {
  margin-left: 50px;
  margin-bottom: 5px;
  padding: 5px;
  border: 1px solid black;
  border-radius: 10px;
}
.radio {
  margin-bottom: 5px;
}
.groupBtn {
  margin-bottom: 5px;
}
</style>
