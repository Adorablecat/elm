<template>
    <div class="popup">
        <h2>{{seller.name}}</h2>
        <div class="promote">
            <h3>优惠信息</h3>
            <ul>
                <li v-for="item in seller.supports">{{item.description}}</li>
            </ul>
        </div>
        <div class="bulletin">
            <h3>商家公告</h3>
            <p>{{seller.bulletin}}</p>
        </div>
        <span class="close" @click="close">&times;</span>
    </div>
</template>

<script>
export default {
    props : {
        seller : {
            type : Object,
            required : true
        }
    },
    methods : {
        close(){
            this.$emit('closePopup');
        }
    }
}
</script>

<style lang="less" scoped>
    .popup{
        position: fixed;
        top:0;
        left : 0;
        z-index: 1000;
        width: 100%;
        height : 100%;
        background: rgba(7,17,27,.8);
        color: #fff;
        font-size: 12px;
        h2 {
            margin: 64px auto 20px;
            text-align: center;
            font-size:16px;
            font-weight: 700;
        }
        .promote {
            padding: 0 36px;
            li {
                line-height: 26px;
            }
        }
        h3 {
            margin : 20px auto;
            text-align: center;
            font-size: 14px;
        }
        .bulletin {
            padding: 0 36px;
            p {
                line-height: 26px;
            }
        }
        .close {
            position: absolute;
            font-size: 32px;
            bottom: 32px;
            color :rgba(255,255,255,.5);
            left : 50%;
            transform: translateX(-50%);
        }
    }
</style>
