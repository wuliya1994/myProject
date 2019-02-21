<!--tab选择-->
<template>
    <div class="tab-box-list">
        <div v-for="(item, index) in tabList" :key="index" class="tab nav_item">
            <input type="radio" :id="index" :value="item.value" name="group" v-model="bindData"/>
            <label :for="index">{{item.label}}</label>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'tab-bar',
        props: {
            /**
             * 滚动条的内容集合，形式为[{label:'',value:''}]
             * */
            tabList: {
                type: Array,
                default: function () {
                    return []
                },
            },
            value: {
                type: Object,
                default: function () {
                    return null
                },
            },
        },
        data() {
            return {
                bindData: '',
            }
        },
        watch: {
            bindData() {
                this.$emit('input', this.bindData)
            }
        },
        created() {
            // 初始化bindData的值,默认选中第一个,如果传了初始值则使用初始值
            this.bindData = this.value === null ? this.tabList[0].value : this.value
        }
    }
</script>

<style scoped>
    .tab-box-list {
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

    .tab-box-list::-webkit-scrollbar { /*隐藏滚轮*/
        display: none;
        width: 0;
        background: transparent;
    }

    .tab {
        height: 84%;
        position: relative;
    }

    .tab label {
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

    input[type="radio"]:checked + label {
        border-bottom: 3px solid #0096eb;
        color: #0096eb;
    }

    .nav_item {
        padding: 0 18px;
        list-style: none;
        white-space: nowrap;
    }
</style>
