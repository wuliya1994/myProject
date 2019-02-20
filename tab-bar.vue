<!--tab选择-->
<template>
    <div class="tab-box-list">
      <div v-for="(item, index) in tabList" :key="index" class="tab nav_item">
        <input type="radio" :id="index" :value="item.value"  name="group" v-model="bindData" />
        <label :for="index">{{item.label}}</label>
      </div>
    </div>
</template>

<script>
  export default {
    name: 'tab-bar',
    props: {
      tabList: {
        type: Array,
        default: function () {
          return [
            {label: '全部', value: 1},
            {label: '文学', value: 2},
            {label: '历史', value: 3},
            {label: '政治', value: 4},
            {label: '地理', value: 5},
            {label: '体育', value: 6},
            {label: '科学', value: 7},
            {label: '语文', value: 8},
            {label: '其他', value: 9}
          ]
        }
      }
    },
    data () {
      return {
        bindData: ''
      }
    },
    watch: {
      bindData () {
        const data = {bindData: this.bindData}
        this.$emit('bindDataChanged', data)
      },
      tabList () {
        this._initDefaultData()
      }
    },
    methods: {
      _initDefaultData () {
        this.bindData = this.tabList[0].value // 初始化bindData的值,默认选中第一个
        this.$emit('tabListChanged', this.tabList)
      }
    },
    created () {
      this._initDefaultData()
    }
  }
</script>

<style scoped>
  .tab-box-list{
    height: 2rem;
    border-bottom: 1px solid #e5e5e5;
    color: #666;
    display: flex;
    align-items: center;
    flex-flow: row nowrap;
    line-height: 1.75rem;
    overflow-y: hidden;
    overflow-x: auto;
    background-color: white;
    position: relative;
    z-index: 2;
    margin-bottom: 0.5rem;
  }
  .tab-box-list::-webkit-scrollbar {/*隐藏滚轮*/
    display: none;
    width: 0;
    background: transparent;
  }
  .tab {
    height: 84%;
    position: relative;
  }
  .tab label{
    -webkit-box-flex: 1;
    -moz-box-flex: 1;
    box-flex: 1;
    text-align: center;
    cursor: pointer;
    font-size: 15px;
    display: inline-block;
    height: 100%;
  }
  input[type="radio"] {
    position: absolute;
    clip: rect(0, 0, 0, 0);
  }
  input[type="radio"]:checked+label {
    border-bottom: 3px solid #0096eb;
    color: #0096eb;
  }
  .nav_item {
    padding: 0 18px;
    list-style: none;
    white-space: nowrap;
  }
</style>
