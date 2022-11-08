<template>
  <div id="app">
    <el-button @click="view">查看</el-button>
    <selectTree size="mini" v-model="treeId" :rangeSeparator="rangeSeparator" :placeholder="placeholder" :width="width" :height="height" :defaultProps="defaultProps" :treeList="treeList" />
  </div>
</template>


<script>
import selectTree from './components/selectTree.vue';
export default {
  name: 'App',
  data(){
    return{
      treeId:'',
      rangeSeparator:'-',
      placeholder:'dh选择',
      width:460,
      height:600,
      defaultProps:{
        label:'label',
        children:'children',
        id:'id'
      },
      treeList:[{
          id: 1,
          label: '一级 2',
          children: [{
            id: 3,
            label: '二级 2-1',
            children: [{
              id: 4,
              label: '三级 3-1-1'
            }, {
              id: 5,
              label: '三级 3-1-2',
              disabled: true
            }]
          }, {
            id: 2,
            label: '二级 2-2',
            disabled: true,
            children: [{
              id: 6,
              label: '三级 3-2-1'
            }, {
              id: 7,
              label: '三级 3-2-2',
              disabled: true
            }]
          }]
      }],
    }
  },  
  components:{
    selectTree
  },
  methods:{
    view(){
      console.log(this.treeId);
    }
  }
}
</script>

<style>
</style>
