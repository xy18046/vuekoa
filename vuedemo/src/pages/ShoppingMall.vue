<template>
    <div>

        <div class="search-bar">
            <van-row>
            <van-col span="3">
                <!-- <img :src="locationIcon" width="100%"/> -->
                <img :src="locationIcon" width="100%" class="location-icon"/>
            </van-col>
            <van-col span="16">
                <input type="text" class="search-input" />
            </van-col>
            <van-col span="5">
                <van-button size="mini">查找</van-button>
            </van-col>
        </van-row>
        </div>
       <!-- swiper area -->
       <div class="swiper-area">
           <van-swipe >
               <van-swipe-item v-for="( banner,index ) in bannerPicArray" :key="index">
                   <img class="swiper-img" v-lazy="banner.image"  />
               </van-swipe-item>
           </van-swipe>
       </div>
        <!-- type bar -->
        <div class="type-bar">
            <div v-for="(cate,index) in category" :key="index" class="imgbox">
                <img v-lazy="cate.image" width="90%" />
                <span>{{cate.mallCategoryName}}</span>
            </div>
        </div>
        <!-- adbanner area -->
        <div>
            <img v-lazy="adBanner" width="100%">
        </div>
        <!-- 商品推荐 -->
        <div class="recommand-area">
            <div class="recommand-title">
                商品推荐
            </div>
            <div class="recommand-body">
                <swiper>
                    <swiper-slide v-for="(item,index) in recommandGoods" :key="index">
                        <div class="recommend-item">
                            <img :src="item.image" width="80%"/>
                            <div>{{item.goodsName}}</div>
                            <div>￥{{item.price}}(￥{{item.mallPrice}})</div>
                        </div>
                    </swiper-slide>
                </swiper>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios'
    import { Swiper, SwiperSlide } from 'vue-awesome-swiper'
    import 'swiper/css/swiper.css'

    export default {
        data (){
            return {
                msg:'Shopping Mall',
                locationIcon:require('../assets/images/location.png'),
                vueIcon:require('../assets/logo.png'),
                bannerPicArray:[],
                    // {imageUrl:'http://7xjyw1.com1.z0glb.clouddn.com/simlevueDemoPic001.jpg'},
                    // {imageUrl:'http://7xjyw1.com1.z0glb.clouddn.com/simlevueDemoPic002.jpg'},
                    // {imageUrl:'http://7xjyw1.com1.z0.glb.clouddn.com/simlevueDemoPic003.jpg'}
                    // {imageUrl: require("../../assets/images/industryScenes/xysscene.png")},
                    // {image:require("../assets/banner/banner1.jpg")},
                    // {image:require("../assets/banner/banner2.jpg")},
                    // {image:require("../assets/banner/banner3.jpg")}
                // ],
                category:[],
                adBanner:'',
                recommandGoods:[]
            }
        },
        components:{
            Swiper,
            SwiperSlide
        },
       
        created(){
            axios({
                url:'https://www.easy-mock.com/mock/5ec3ab411b282023a6f00603/smilevue/index',
                method:'get'
            })
            .then(response=>{
                console.log(response)
                if(response.status == 200){
                    this.category=response.data.data.category
                    this.adBanner = response.data.data.advertesPicture.PICTURE_ADDRESS,
                    this.bannerPicArray = response.data.data.slides,
                    this.recommandGoods = response.data.data.recommend
                }
            })
            .catch(error=>{
                console.log(error)
            })
        }
    }
</script>

<style>
    .search-bar{
        height: 2.2rem;
        background-color: #e5017d;
        line-height: 2.2rem;
        overflow: hidden;
    }
    .search-input{
        width: 100%;
        height: 1.3rem;
        border-top: 0px;
        border-left: 0px;
        border-right: 0px;
        border-bottom: 1px solid #ffffff;
        background-color: #e5017d;
        color: #ffffff;
    }
    .location-icon{
        padding-top: 0.2rem;
        padding-left: 0.5rem;
        margin-top: 0.2rem;
        width: 1rem;
        height: 1.5rem;
    }
    .swiper-area{
        clear: both;
        max-height: 9rem;
        overflow: hidden;

    }
    .swiper-img{
        display: block;
        width: 100%;
        height: 100%;
    }
    .type-bar{
        background-color: #ffffff;
        margin: 0rem 0.2rem 0.2rem 0.2rem;
        border-radius: .3rem;
        font-size: 14px;
        display: flex;
        flex-direction: row;
        flex-wrap: nowrap;
    }
    .type-bar div{
        padding: .3rem;
        font-size: 12px;
        text-align: center;
    }
    .imgbox{
        flex: 1;
    }
    .recommand-area{
        background-color: #ffffff;
        margin-top: .3rem;
    }
    .recommand-title{
        border-bottom: 1px solid #eee;
        font-size: 14px;
        padding: .2rem;
        color:#e5017d
    }
    .recommand-body{
        
    }
</style>