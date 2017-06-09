<template>
    <div>
        <div class="goods">
           <div class="menu">
               <ul>
                   <li v-for="(item,index) in goods" :class="{'on' : current==index }" @click="selectCategory(index)">{{item.name}}</li>
               </ul>
           </div>
           <div class="list" id="list" ref="list">
               <div>
                   <dl v-for="item in goods">
                      <dt>{{item.name}}</dt>
                      <dd v-for="food in item.foods" @click="selectFood(food)">
                          <img :src="food.icon" alt="">
                          <div class="food">
                              <h3>{{food.name}}</h3>
                              <p class="description">{{food.description}}</p>
                              <p class="sale">月售份{{food.sellCount}} 好评率{{food.rating}}</p>
                              <p class="price"><span>￥<strong>{{food.price}}</strong></span> <del v-if="food.oldPrice">￥{{food.oldPrice}}</del></p>
                              <ele-buy :food="food"></ele-buy>
                          </div>
                      </dd>
                   </dl>
               </div>
           </div>
        </div>
        <transition name="slide">
            <ele-detail v-show="showDetail" :food="currentFood" @close="showDetail=false"></ele-detail>
        </transition>
        <ele-cart :cartFoods="cartFoods" :minPrice="seller.minPrice"
        :deliveryPrice="seller.deliveryPrice"></ele-cart>
    </div>
</template>
<script>
import data from '../../../data.json'
const IScroll = require("../../../static/js/iscroll.js")
import Detail from '../Detail/Detail'
import Buy from '../Buy/Buy'
import Cart from '../Cart/Cart'

export default {
    data(){
        return {
            goods : [],
            seller : {},
            current : 0,
            showDetail : false,
            currentFood : {},
        }
    },
    computed : {
        cartFoods(){
            let foods = [];
            this.goods.forEach( (item) =>  {
                item.foods.forEach( (item1) => {
                    if (item1.count) {
                        foods.push(item1);
                    }
                });
            });
            return foods;
        }
    },
    methods : {
        selectCategory(index){
            this.current = index;
            let dls = this.$refs.list.getElementsByTagName('dl');
            this.listScroll.scrollToElement(dls[index]);
        },
        selectFood(food){
            this.showDetail = true;
            this.currentFood = food;
        }
    },
    created(){
        this.goods = data.goods;
        this.seller = data.seller;
    },
    mounted(){
        this.listScroll = new IScroll("#list",{click:true});
        this.menuScroll = new IScroll(".menu",{click:true});
        this.listScroll.on('scroll',function(){
        })
        this.listScroll.on('scrollEnd',function(){
        })
    },
    components : {
        'ele-detail' : Detail,
        'ele-buy' : Buy,
        'ele-cart' : Cart
    }
}
</script>

<style lang="less" scoped>
    .slide-enter-active,.slide-leave-active{
        transition: all .5s;
    }
    .slide-enter,.slide-leave-active {
        transform: translateX(100%);
        opacity: 0;
    }
    .goods {
        display: flex;
        position: fixed;
        left : 0;
        right: 0;
        top:174px;
        bottom: 48px;
        overflow: hidden;
        .menu {
            min-width: 80px;
            li {
                height: 54px;
                padding: 0 12px;
                display: flex;
                align-items: center;
                background: #f3f5f7;
                font-size: 12px;
                color: rgb(77,85,93);
                &.on{
                    background: #fff;
                }
            }
        }
        .list {
            flex-grow: 1;
            dt {
                height: 26px;
                line-height: 26px;
                background: #f3f5f7;
                border-left: 3px solid #d9dde1;
                font-size: 12px;
                color: rgb(147,153,159);
                padding-left: 14px;
            }
            dd {
                margin : 18px;
                display: flex;
                img {
                    width: 57px;
                    height: 57px;
                }
                .food {
                    position: relative;
                    flex-grow: 1;
                    margin-left:10px;
                    .buy {
                        position: absolute;
                        right : 0px;
                        bottom: 0px;
                    }
                    h3 {
                        font-size: 14px;
                        line-height: 14px;
                        color: rgb(7,17,27);
                    }
                    .description,.sale {
                        font-size: 10px;
                        line-height: 14px;
                        color: rgb(147,153,159);
                        margin-top: 8px;
                    }
                    .price {
                        margin-top: 8px;
                        span {
                            color: rgb(240,20,20);
                            font-size: 10px;
                            strong {
                                font-size: 14px;
                                font-weight: 700;
                            }
                        }
                        del {
                            font-size: 10px;
                            line-height: 10px;
                            color: rgb(7,17,27);
                            font-weight: 700;
                        }
                    }
                }
            }
        }
    }
</style>
