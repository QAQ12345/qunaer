<template>
    <div class='recommen'>
        <div class='back'>
            <p class='recommen-title'><span>相关推荐</span></p>
            <ul>
                <li class='recommon-li border-bottom' v-for='item in items'>
                    <p class='title'>{{item.title}}</p>
                    <p class='price border-bottom'><span class='money'>￥</span><span class='price-num'>{{item.price}}</span>起/张</p>
                    <router-link class='address border-bottom iconfont' :to='{path:"/weekend/detail/map?title="+item.title+"&price="+item.price+"&x="+item.x+"&y="+item.y}'><p><span class='address-icon '>&#xe665;</span>{{item.address}}<span class='address-arrow'>&#xe649;</span></p></router-link>
                </li>
            </ul>
        </div>
        <div class='list-product'>
            <span class='list-line'></span>
            <p class='list-provide'><span class='list-content'>本产品由爱陌客自营提供</span></p>
        </div>
        <ul class='list iconfont' ref='list'>
             <li class='list-li' v-for='item in lists' ref='listLi'>
                 <span class='list-icon' v-html='item.icon'></span>
                 <span class='list-content'>{{item.content}}</span>
             </li>
             <li ref='moreLi' @click='handleMoreClick' class='more border-left'><span v-html='arrow'></span><span ref='more'>更多</span></li>
         </ul>
        <ul class='link'>
            <li><a class='link-a' href='#'>登录</a></li>
            <li><a class='link-a' href='#'>我的订单</a></li>
            <li><a class='link-a' href='#'>最近浏览</a></li>
            <li><a class='link-a' href='#'>关于我们</a></li>
        </ul>
        <div class='version'>
            <a class='touchscreen-version'>触屏版</a>
            <a class='computer-version'>电脑版</a>
        </div>
        <p class='copyright'>Daozheer 京ICP备05021087<a class='feedback'>意见反馈</a></p>
    </div>
</template>

<script>
	export default {
	    data () {
            return {
                message:false,
                arrow:'&#xe64b;',
                items:[],
                lists:[]
            }
	    },
        created() {
            this.$http.get('/static/recommen.json').then(response => {
                this.data  = response.body.data;
                this.items = this.data.items;
                this.lists = this.data.lists;
            }, response => {
                console.log('ajax error')
            });
        },
	    methods: {
            handleMoreClick(e) {
                this.message=!this.message;
                if(this.message) {
                    for(var i=0;i<this.$refs.listLi.length;i++){
                        this.$refs.listLi[i].style.width='25%';
                    }
                    this.$refs.list.style.height='2.6rem';
                    this.$refs.more.innerText='收起';
                    this.$refs.moreLi.style.top='80%';
                    this.arrow='&#xe601;';
                }else {
                    for(var i=0;i<this.$refs.listLi.length;i++){
                        this.$refs.listLi[i].style.width='26%';
                    }
                    this.$refs.list.style.height='.6rem';
                    this.$refs.more.innerText='更多';
                    this.$refs.moreLi.style.top='15%';
                    this.arrow='&#xe64b;';
                }
            }
        }
	}
</script>


<style scoped>
    @import "../../../assets/font/iconfont.css";
    .recommen{
        color:#9e9e9e;
    }
    .back{
        border-top:1px solid #c8cccd;
        background:#fff;
        padding:.2rem .2rem 0;
        margin-top:.2rem;
        border-bottom:1px solid #c8cccd;
    }
    .back::after{
        border-bottom:1px solid #c8cccd;
    }
    .recommen-title{
        position:relative;
        font-size:.3rem;
        color:#000;  
    }
    .recommen-title span{
        margin-left:.1rem;
    }
    .recommon-li{
        margin-top:.3rem;
    }
    .recommon-li::after{
        border-bottom:1px solid #e0e0e0;
    }
    .recommen-title::before{
        position:absolute;
        left:0;
        top:.03rem;
        content:'';
        width:.06rem;
        height:.25rem;
        background:#00bcd4;
    }
    .title{
        line-height:.32rem;
        font-size:.32rem;
        color:#000;
    }
    .price{
        font-size:.24rem;
        margin:.3rem 0 0;
        padding-bottom:.1rem;
    }
    .price::before{
        border-bottom:.02rem dashed #ccc;
    }
    .money{
        color:#ff8300;
    }
    .price-num{
        font-size:.36rem;
        color:#ff8300;
        margin-right:.1rem;
    }
    .address{
        color:#9e9e9e;
        line-height:.9rem;
        font-size:.28rem;
    }
    .address-icon{
        margin-right:.1rem;
    }
    .address-arrow{
        float:right;
    }
    .list-product{
        position:relative;
        width:100%;
        height:.4rem;
        padding:.3rem 0 .1rem;
        line-height:.4rem;
        text-align:center;
        margin-top:.1rem;
    }
    .list-content{
        padding:0 .2rem;
        background:#f3f3f3;
    }
    .list-line{
        width:100%;
        position:absolute;
        top:.4rem;
        left:0;
        border-bottom:1px solid #ddd;
    }
    .list-icon{
        width:.44rem;
        height:.44rem;
        line-height:.24rem;
        font-size:.24rem;
        border:1px solid #9e9e9e;
        border-radius:50%;
        padding:.07rem;
        font-size:.24rem;
    }
    .list-provide{
        width:100%;
        position:absolute;
        top:.2rem;
        left:0;
        font-size:.24rem;
        text-align:center;
    }
    .list{
        position:relative;
        width:100%;
        height:.6rem;
        padding: .2rem 0 0;
        overflow:hidden;
    }
    .list-li{
        height:.7rem;
        width:26%;
        float:left;
        font-size:.28rem;
        text-align:center;
    }
    .more{
        position:absolute;
        right:5%;
        top:15%;
        padding-left:.15rem;
    }
    .more::before{
        border-left:1px solid #9e9e9e;
    }
    .link{
        width:100%;
        height:.78rem;
        line-height:.78rem;
        margin-bottom:.2rem;
        border-bottom:1px solid #cacaca;
    }
    .link-a{
        float:left;
        width:25%;
        text-align:center;
    }
    .version{
        width:100%;
        display:flex;
        justify-content:space-between;
    }
    .touchscreen-version{
        width:50%;
        color:#000;
        box-sizing:border-box;
        padding-right:.2rem;
        text-align:right;
    }
    .computer-version{
        width:50%;
        box-sizing:border-box;
        padding-left:.2rem;
        text-align:left;
    }
    .copyright{
        height:.68rem;
        padding:.2rem;
        text-align:center;
        margin-bottom:1rem;
    }
    .feedback{
        color:#9e9e9e;
    }
</style>