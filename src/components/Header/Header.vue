<template>
    <div class="header">
        <div class="seller">
            <img :src="seller.avatar" alt="">
            <div class="info">
                <h2><i></i>{{seller.name}}</h2>
                <p class="delivery">{{seller.description}}/{{seller.deliveryTime}}分钟到达</p>
                <p class="pay">{{seller.supports[0].description}}</p>
            </div>
            <div class="sw" @click="show=true">
                {{seller.supports.length}}个 &gt;
            </div>
        </div>
        <div class="bulletin" @click="show=true">
            <i></i>
            <p>{{seller.bulletin}}</p>
            <span>&gt;</span>
        </div>
        <div class="bg">
            <img :src="seller.avatar" alt="">
        </div>
        <transition name="bounce">
            <ele-popup :seller="seller" v-show="show" @closePopup="show=false"></ele-popup>
        </transition>

    </div>
</template>

<script>
import Popup from "../Popup/Popup"
export default {
    data(){
        return {
            show : false
        }
    },
    props : {
        seller : {
            type : Object,
            required : true
        }
    },
    components : {
        'ele-popup' : Popup
    }
}
</script>

<style lang="less" scoped>
    @keyframes bounceIn {
        0% {transform: scale(0);}
        50%{transform: scale(1.5);}
        100%{transform: scale(1);}
    }
    @keyframes bounceOut {
        0% {transform: scale(1);}
        50%{transform: scale(1.5);}
        100%{transform: scale(0);}
    }

    .bounce-enter-active {animation: bounceIn 0.5s;}
    .bounce-leave-active {animation: bounceOut 0.5s;}

    .header {
        width: 100%;
        height: 134px;
        overflow: hidden;
        position: relative;
        background: rgba(7,17,27,0.5);
        .seller {
            padding: 24px 12px 18px 24px;
            display: flex;
            justify-content: space-between;
            color: #fff;
            img {
                width: 64px;
                height: 64px;
                border-radius: 4px;
            }
            .info {
                flex-grow: 1;
                margin-left: 16px;
                display: flex;
                flex-direction: column;
                justify-content: space-between;
                h2 {
                    font-size: 16px;
                    font-weight: bold;
                    line-height: 18px;
                    i {
                        display: inline-block;
                        width: 30px;
                        height: 18px;
                        background: url(./brand@2x.png) no-repeat 0 0;
                        background-size: contain;
                        margin-right: 5px;
                        vertical-align: top;
                    }
                }
                .delivery {
                    font-size: 12px;
                    line-height: 12px;
                    font-weight: 200;
                }
                .pay {
                    font-size: 10px;
                    line-height: 12px;
                    font-weight: 200;
                }
            }
            .sw {
                align-self: flex-end;
                background: rgba(0,0,0,.2);
                font-size: 10px;
                line-height: 12px;
                font-weight: 200px;
                padding: 7px 8px;
                border-radius: 10px;
            }
        }
        .bulletin{
            padding: 0 10px;
            display: flex;
            height: 28px;
            color: #fff;
            align-items: center;
            i {
                display: inline-block;
                min-width: 22px;
                min-height: 12px;
                background: url('./bulletin@2x.png') no-repeat 0 0;
                background-size: 22px 12px;
            }
            p {
                flex-grow: 1;
                line-height: 28px;
                height: 28px;
                padding: 0 7px;
                font-size: 10px;
                text-overflow: ellipsis;
                white-space: nowrap;
                overflow: hidden;
            }
        }
        .bg {
            position: absolute;
            left:0;
            top:0;
            width: 100%;
            height: 100%;
            z-index:-1;
            filter:blur(10px);
            img {
                width: 100%;
                height: 100%;
            }
        }
    }
</style>
