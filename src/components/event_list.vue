<template>
    <div class="event-content">
        <div class="event-tab" @click="changeCollapse(0,$event)">未完成
            <span :class="{'close-span': !collapse[0].show}"></span>
        </div>
        <div class="event-box" :style="{'height':'auto','display':'none'}">
            <ul>
                <li class="event-list">
                    <input type="checkbox">
                    <div>{{ pramsMes.content }}</div>
                    <button class="cancel-btn"取消</button>
                </li>
            </ul>
        </div>

        <div class="event-tab" @click="changeCollapse(1,$event)">已完成
            <span :class="{'close-span': !collapse[1].show}"></span>
        </div>
        <div class="event-box" :style="{'height':'auto','display':'none'}">
            <ul>
                <li class="event-list">
                    <input type="checkbox">
                    <div></div>
                    <span class="event-time"></span>
                </li>
            </ul>
        </div>

        <div class="event-tab" @click="changeCollapse(2,$event)">已取消
            <span :class="{'close-span': !collapse[2].show}"></span>
        </div>
        <div class="event-box" :style="{'height':'auto','display':'none'}">
            <ul>
                <li class="event-list">
                    <div class="event-delete"></div>
                    <button class="cancel-btn">恢复</button>
                </li>
            </ul>
        </div>

    </div>
</template>
<script>
    export default {
        data(){
            return {
                collapse:[
                    {
                        show: false,
                    },
                    {
                        show: false,
                    },
                    {
                        show: false
                    }
                ],
            }
        },
        props:["pramsMes"],
        methods: {
            changeCollapse(num, event){
                const show = this.collapse[num].show;
                if(show){
                  this.closeCollapse(event);
                }else{
                  this.openCollapse(event);
                }
                this.collapse[num].show = !show;
            },
            closeCollapse(event){  // 关闭折叠面板
                let ulElement = event.currentTarget.nextElementSibling,
                    children = ulElement.getElementsByTagName('ul')[0];
                ulElement.style.height = children.offsetHeight + 'px';
                setTimeout(function(){
                    ulElement.style.height = '0px';
                    setTimeout(function () {
                        ulElement.style.display = 'none';
                    }, 300)
                },10)
            },
            openCollapse(event){ // 打开折叠面板
                let ulElement = event.currentTarget.nextElementSibling,
                    children = ulElement.getElementsByTagName('ul')[0];
                ulElement.style.display = 'block';
                ulElement.style.height = children.offsetHeight + 'px';
                setTimeout(function () {
                    ulElement.style.height = 'auto';
                }, 300)
            }
        }
    }
</script>
<style lang="scss" rel="stylesheet/scss">
    .event-content {
        .event-tab {
            position: relative;
            height: 44px;
            line-height: 44px;
            padding-left: 20px;
            border-bottom: 1px solid #fff;
            box-sizing: border-box;
            color: #fff;
            cursor: pointer;
            background:#00d1b2;
            span {
                position: absolute;
                right: 20px;
                top: 15px;
                width: 10px;
                height: 10px;
                content: '';
                border: {
                    top: 2px solid #fff;
                    right: 2px solid #fff;
                }
                transform: rotate(135deg);
                transition: transform .3s;
                &.close-span {
                    transform: rotate(45deg);
                }
            }
        }
        .event-box {
            list-style: none;
            overflow: hidden;
            border: {
                left: 1px solid #eee;
                right: 1px solid #eee;
            }
            transition: height .3s;
            .event-list {
                position: relative;
                min-height: 44px;
                line-height: 25px;
                padding: 10px 100px 10px 50px;
                box-sizing: border-box;
                border-bottom: 1px solid #eee;
                color: #373e40;
                input[type=checkbox] {
                    position: absolute;
                    left: 15px;
                    top: 12px;
                    width: 20px;
                    height: 20px;
                }
                .cancel-btn {
                    position: absolute;
                    right: 10px;
                    top: 7px;
                    width: 50px;
                    height: 30px;
                    line-height: 30px;
                    padding: 0;
                    background: #fff;
                    border: 1px solid #c0ccda;
                    color: #666;
                    font-size: 12px;
                }
                .event-time {
                    position: absolute;
                    right: 10px;
                    top: 0;
                    line-height: 44px;
                    font-size: 12px;
                    color: #aaa;
                }
                .event-delete {
                    text-decoration: line-through;
                    color: #999;
                }
            }
        }
    }
</style>
