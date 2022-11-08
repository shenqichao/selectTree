<template>
  <div>
    <el-popover :visible-arrow="false" trigger="focus" placement="bottom-start" @show="show" @hide="hide">
      <el-input
        :size="size"
        slot="reference"
        :readonly="categoryShow"
        @input="categoryChange"
        :style="{ lineHeight: '40px' }"
        v-model="text"
        :placeholder="placeholder"
      >
        <span slot="suffix">
          <i
            class="el-icon-circle-close"
            v-show="text"
            style="cursor: pointer;font-weight: 600;"
            @click="clearChange"
          ></i>
          <i class="el-icon-caret-bottom hide" :style="{transform:!rotating?' rotate(-180deg)':''}"></i>
        </span>
      </el-input>
      <div
        :style="{ width: width + 'px', height: 500 + 'px', overflow: 'auto' }"
      >
        <el-tree
          :default-expanded-keys="expandedKeys"
          ref="tree"
          :data="treeList"
          :props="defaultProps"
          accordion
          highlight-current
          :node-key="defaultProps.id"
          :filter-node-method="filterNode"
          :expand-on-click-node="true"
          :check-on-click-node="true"
          @node-click="handleNodeClick"
        >
        </el-tree>
      </div>
    </el-popover>
  </div>
</template>

<script>
export default {
  name: "selectTree",
  props: {
    value:{
        type:[String,Number],
    },
    rangeSeparator:{
        type:String,
        default:'>'
    },
    size: {
      type: String,
      default: "medium",
    },
    placeholder:{
        type:String,
        default:'请选择'
    },
    width: {
      type: Number,
      default: 460,
    },
    height: {
      type: Number,
      default: 600,
    },
    defaultProps: {
      type: Object,
      default: () => ({
        label: "label",
        id: "id",
        children:"children"
      }),
    },
    treeList: {
      type: Array,
      default: () => {
        return [];
      },
    },
  },
  data() {
    return {
      rotating:true,
      //回显展开的tree节点
      expandedKeys: [],
      //定时器名称
      timmer: null,
      //是否只读
      categoryShow: false,
      //输入框
      text: "",
      dataname: [],
    };
  },
  methods: {
    show(){
      this.rotating = false
    },
    hide(){
      this.rotating = true
    },
    categoryChange(val) {
      clearInterval(this.timmer);
      this.timmer = setInterval(() => {
        this.$refs.tree.filter(val);
        clearInterval(this.timmer);
      }, 500);
    },
    clearChange() {
      this.categoryShow = false;
      this.text = "";
      this.$emit('input','')
      this.$refs.tree.setCurrentKey(null);
      this.categoryChange("");
    },
    filterNode(value, data) {
      if (!value) return true;
      return data.label.indexOf(value) !== -1;
    },
    // 递归函数
    platform(node) {
      if (!node.parent) {
        this.text = this.dataname.join(' '+this.rangeSeparator+' ' );
        return;
      }
      this.dataname.unshift(node.data.label);
      this.platform(node.parent);
    },
    handleNodeClick(data, node) {
      this.categoryShow = true;
      this.$emit('input',data[this.defaultProps.id])
      this.dataname = [];
      this.platform(node);
    },
  },
};
</script>

<style>
.hide{
    transition: all .3s;
  }
</style>