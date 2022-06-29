<template>
  <div class="ruleDiv">
    <el-select
      class="fieldSelector"
      v-model="root.field"
      placeholder="请选择字段"
      @change="changeField(root)"
    >
      <el-option
        v-for="(item, index) in fields"
        :key="index"
        :label="item.name"
        :value="item.name"
      ></el-option>
    </el-select>
    <div>
      <el-select
        class="operationSelector"
        v-if="root.field === ''"
        placeholder="请先选择字段"
      ></el-select>
      <div v-for="(item, index) in operators" :key="index">
        <el-select
          class="operationSelector"
          v-if="item.type === root.field"
          v-model="root.operation"
          placeholder="请选择操作"
          @change="changeOperation(root)"
        >
          <el-option
            v-for="(item, index) in item.validOperations"
            :key="index"
            :label="item"
            :value="item"
          ></el-option>
        </el-select>
      </div>
    </div>

    <div
      style="display:flex"
      v-if="root.operation === 'between' || root.operation === 'not between'"
    >
      <el-input v-model="root.value1" placeholder="请输入值"></el-input>
      ~
      <el-input v-model="root.value2" placeholder="请输入值"></el-input>
    </div>
    <div v-else-if="root.field === 'category'">
      <el-select v-model="root.string" placeholder="请选择">
        <el-option
          v-for="(item, index) in categorys"
          :key="index"
          :label="item"
          :value="item"
        ></el-option>
      </el-select>
    </div>
    <div v-else>
      <el-input v-model="root.string" placeholder="请输入内容"></el-input>
    </div>

    <el-button
      class="ruleDeleteBtn"
      type="danger"
      size="small"
      @click.prevent="deleteRule(root, parent)"
    >
      删除
    </el-button>
  </div>
</template>

<script>
export default {
  props: {
    root: Object,
    parent: Object,
  },
  data() {
    return {
      fields: [
        {
          name: 'name',
          type: 'string',
        },
        {
          name: 'category',
          type: 'select',
        },
        {
          name: 'price',
          type: 'number',
        },
      ],
      operators: [
        {
          type: 'name',
          validOperations: ['equal', 'not equal'],
        },
        {
          type: 'category',
          validOperations: ['equal', 'not equal'],
        },
        {
          type: 'price',
          validOperations: [
            'less',
            'equal',
            'not equal',
            'greater',
            'less or equal',
            'equal or greater',
            'between',
            'not between',
          ],
        },
      ],
      categorys: ['Books', 'Movies', 'Music', 'Tools', 'Goodies', 'Clothes'],
    };
  },
  components: {},
  methods: {
    deleteRule(root, parent) {
      var index = parent.indexOf(root);
      if (index > -1) {
        parent.splice(index, 1);
      }
    },
    changeField(root) {
      (root.operation = ''), (root.String = ''), (root.value1 = ''), (root.value2 = '');
    },
    changeOperation(root) {
      (root.String = ''), (root.value1 = ''), (root.value2 = '');
    },
  },
};
</script>

<style>
.ruleDiv {
  margin-left: 50px;
  margin-bottom: 5px;
  display: flex;
}
.fieldSelector {
  margin-right: 5px;
}
.operationSelector {
  margin-right: 5px;
}
.ruleDeleteBtn {
  margin-left: 5px;
}
</style>
