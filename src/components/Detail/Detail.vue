<template>
    <div class="detail">
        <div class="detail-hd">
            <span @click="closeDetail">&lt;</span>
            <img :src="food.image" alt="">
        </div>
        <div class="detail-base">
            <h2>{{food.name}}</h2>
            <p class="sale">月售{{food.sellCount}}份，好评率{{food.rating}}</p>
            <p class="price"><strong>￥{{food.price}}</strong> <del v-if="food.oldPrice">{{food.oldPrice}}</del> </p>
        </div>
        <div class="detail-info">
            <h2>商品信息</h2>
            <p>{{food.info}}</p>
        </div>
        <div class="comments">
            <h2>商品评价</h2>
        </div>
    </div>
</template>

<script>
export default {
    props : {
        food : {
            type : Object,
            required : true
        }
    },
    methods : {
        closeDetail(){
            this.$emit('close');
        }
    }
}
</script>

<style lang="less" scoped>
    .detail {
        width: 100%;
        position: fixed;
        left :0;
        top :0;
        bottom: 48px;
        background: #eee;
        .detail-hd {
            height: 375px;
            position: relative;
            img {
                width: 100%;
                height: 100%;
            }
            span {
                position: absolute;
                top:10px;
                left:10px;
                font-size: 32px;
                color: #fff;
            }
        }
        .detail-base {
            margin: 18px;
            h2 {
                font-size: 14px;
                line-height: 14px;
                color: rgb(7,17,27);
                font-weight: 700;
            }
            .sale {
                font-size:10px;
                line-height: 10px;
                color: rgb(147,153,159);
                margin: 8px 0 18px 0;
            }
            .price {
                font-size: 14px;
                color: rgb(240,20,20);
                font-weight: 700;
            }
        }
        .detail-info {
            margin: 18px;
        }
        .comments {
            margin: 18px;
        }
    }
</style>
