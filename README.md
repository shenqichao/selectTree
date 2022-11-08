#使用说明
 - 必传字段
 ```
    v-model:{
        tips:'双向绑定的字段',
        type:[Number,String],
    }
    treeList:{
        tips:'tree的列表',
        type:Array
    }
 ```
 - 选传字段
 ```
    size:{
        tips:'输入框的大小',
        type:String|'medium'/'small'/'mini',
        default:'medium'
    }
    placeholder:{
        tips:'输入框没有内容时占位符',
        type:String,
        default:'请选择'
    }
    rangeSeparator:{
        tips:'输入框的父子连接的分隔符',
        type:String,
        default:'>'
    },
    width:{
        tips:'树形图展开的宽度',
        type:Number,
        default:460
    }
    height:{
        tips:'树形图展开的高度',
        type:Number,
        default:600
    }
    defaultProps: {
      tips:'tree的节点名称、值、子树的值',  
      type: Object,
      default: () => ({
        label: "label",
        children:"children",
        id: "id",
      }),
    }
 ```