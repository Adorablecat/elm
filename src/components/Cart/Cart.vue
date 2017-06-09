<template>
    <div>
        <div class="cart" @click.stop="toggleCart">
            <div class="cart-left">
                <div class="cart-outer">
                    <div class="cart-inner" :class="{'on' : total>0}">
                        <span class="iconfont icon-gouwuche"></span>
                    </div>
                    <div class="count" v-show="total>0">{{total}}</div>
                </div>
            </div>
            <div class="cart-md">
                <h3>￥{{totalPrice}}</h3>
                <p>另需配送费￥{{deliveryPrice}}元</p>
            </div>
            <div class="cart-right" :class="{'on' : totalPrice >= minPrice }">
                {{payDesc}}
            </div>
        </div>
        <transition name="slide">
            <div class="cart-list" v-show="show && cartFoods.length">
                <div class="list-hd">
                    <h2>购物车</h2>
                    <span @click="clear">清空</span>
                </div>
                <ul>
                    <li v-for="food in cartFoods">
                        <h3>{{food.name}}</h3>
                        <div class="buy-btn">
                            <strong>￥{{food.price * food.count}}</strong>
                            <ele-buy :food="food"></ele-buy>
                        </div>
                    </li>
                </ul>
            </div>
        </transition>
        <transition name="fade">
            <div class="mask" v-show="show && cartFoods.length">
            </div>
        </transition>
    </div>
</template>

<script>
import Buy from '../Buy/Buy'
export default {
    data(){
        return {
            show : false
        }
    },
    props : {
        cartFoods : {
            type : Array,
            required : true
        },
        minPrice : Number,
        deliveryPrice: Number
    },
    computed : {
        total(){
            let cnt = 0;
            this.cartFoods.forEach( (item) => {
                cnt += item.count;
            });
            return cnt;
        },
        totalPrice(){
            let sum = 0;
            this.cartFoods.forEach( (item) => {
                sum += item.price * item.count;
            });
            return sum;
        },
        payDesc(){
            if (this.totalPrice == 0 ) {
                return `￥${this.minPrice}元起送`;
            } else if (this.totalPrice < this.minPrice) {
                let dif = this.minPrice - this.totalPrice;
                return `还差￥${dif}元起送`;
            } else {
                return '去结算';
            }
        }
    },
    methods: {
        clear(){
            this.cartFoods.forEach( food => food.count = 0 );
            this.show = false;
        },
        toggleCart(){
            if (this.cartFoods.length) {
                this.show = !this.show;
            }
        }
    },
    components:{
        'ele-buy' : Buy
    }
}
</script>

<style lang="less" scoped>
    .slide-enter-active,.slide-leave-active {
        transition: all .5s;
    }
    .slide-enter,.slide-leave-active {
        transform: translateY(100%);
    }

    .fade-enter-active,.fade-leave-active {
        transition: all .5s;
    }
    .fade-enter,.fade-leave-active {
        opacity: 0;
    }
    .cart {
        position: fixed;
        z-index : 100;
        width: 100%;
        height: 48px;
        left: 0;
        bottom: 0;
        background: #141d27;
        display: flex;
        .cart-left{
            min-width: 80px;width: 80px;
            position: relative;
            .cart-outer {
                width: 56px;
                height: 56px;
                border-radius: 50%;
                background:  #141d27;
                position: absolute;
                left: 12px;
                top:-6px;
                .cart-inner {
                    margin:6px;
                    width: 44px;
                    height: 44px;
                    border-radius: 50%;
                    background: rgba(255,255,255,.2);
                    line-height: 44px;
                    text-align: center;
                    &.on {
                        background: rgb(0,160,220);
                        span {
                            color: #fff;
                        }
                    }
                    span {
                        font-size: 24px;
                        color: rgba(255,255,255,.6);
                        display: inline-block;
                    }
                }
                .count {
                    position: absolute;
                    top: 0;
                    right: 0;
                    width: 20px;
                    height: 20px;
                    border-radius: 50%;
                    background: #f00;
                    color: #fff;
                    font-size:10px;
                    text-align: center;
                    line-height: 20px;
                    font-weight: 700;
                }
            }
        }
        .cart-md{
            flex-grow: 1;
            display: flex;
            align-items: center;
            h3 {
                font-size: 16px;
                color: rgba(255,255,255,0.4);
                font-weight: bold;
                margin-right: 10px;
            }

            p {
                font-size: 14px;
                color: rgba(255,255,255,0.4);
                border-left: 1px solid rgba(255,255,255,.1);
                padding-left: 10px;
            }
        }
        .cart-right{
            width: 105px;
            min-width: 105px;
            text-align: center;
            line-height: 48px;
            color: rgba(255,255,255,0.4);
            font-size: 12px;
            font-weight: 700;
            &.on {
                background: #00b43c;
                color:#fff;
            }
        }
    }
    .cart-list{
        position: fixed;
        z-index : 90;
        width: 100%;
        bottom: 48px;
        background: #fff;
        .list-hd{
            height: 40px;
            line-height: 40px;
            position: relative;
            background: #f3f5f7;
            h2 {
                padding-left: 18px;
                font-size: 14px;
            }
            span {
                position: absolute;
                right: 18px;
                color: rgb(0,160,220);
                top: 0px;
                font-size:12px;
            }
        }
        ul li{
            display: flex;
            justify-content: space-between;
            align-items: center;
            height: 48px;
            padding: 0 18px;
            h3 {

            }
            .buy-btn{
                display: flex;
                align-items: center;
                strong {
                    color : #f00;
                    margin-right: 10px;
                }
            }
        }
    }
    .mask {
        position: fixed;
        z-index : 80;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(7,17,27,0.6);
        // filter: blur(10px);
    }
</style>
