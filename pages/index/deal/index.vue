<template>
    <div class="container" style="margin-top:20px;">
        <div class="col-sm-4" >
            <div style="background-color:white; padding: 26px;">
                <h6 class="headText">Danh mục</h6>
                <ul v-if="!mainData.isErrorGetCategory"
                    style="margin:0; padding:0; list-style-type: none; margin-top:30px;">
                    <li v-for="item in mainData.listCategory" style="font-family: 'Open Sans'; font-size:15px;">
                        <el-checkbox></el-checkbox>
                        {{item.name}}
                    </li>
                </ul>
            </div>
            <div style="background-color:white; padding: 26px; margin-top:30px;">
                <h6 class="headText">Tỉnh thành</h6>
                <ul v-if="!mainData.isErrorGetCity"
                    style="margin:0; padding:0; list-style-type: none; margin-top:20px;">
                    <li style="font-family: 'Open Sans'; font-size:15px;" v-for="item,index in mainData.listCity"
                        v-show="index<5 || index>=5 && v.showMoreListCity">
                        <el-checkbox></el-checkbox>
                        {{item.name}}
                    </li>
                    <li><a href="javascript:;" style="margin-top:10px;" v-if="!v.showMoreListCity"
                           @click="v.showMoreListCity=true">Tất cả</a>
                        <a href="javascript:;" style="margin-top:10px;" v-else @click="v.showMoreListCity=false">Ẩn
                            bớt</a>
                    </li>
                </ul>

            </div>
            <div style="background-color:white; padding: 26px; margin-top:30px;">
                <h6 class="headText">Trạng thái</h6>
                <ul style="margin:0; padding:0; list-style-type: none; margin-top:20px; font-family: 'Open Sans'; font-size:15px;">
                    <li>
                        <el-checkbox></el-checkbox>
                        Có coupon
                    </li>
                    <li>
                        <el-checkbox></el-checkbox>
                        Có giảm giá
                    </li>
                    <li>
                        <el-checkbox></el-checkbox>
                        Sản phẩm mới
                    </li>
                </ul>
            </div>
        </div>
        <div class="col-sm-8">
            <template v-if="!mainData.isErrorDeal">
            <div v-for="item in mainData.listDeal" class="col-sm-6" style="margin-bottom:20px;">
                <div style="background-color:white;">

                </div>

            </div>
            </template>

        </div>

    </div>
</template>
<script>
    import axios from 'axios'

    export default {
        name: 'PUBLIC_listShop',
        async asyncData() {
            let mainData = {};
            await axios.get(process.env.API.Deal_PublicGetByType)
                .then(data => {
                    mainData.listDeal = data.data;
                })
                .catch(error => {
                    mainData.isErrorDeal = true;
                })
            await  axios.get(process.env.API.Category_Get)
                .then(data => {
                    mainData.listCategory = data.data;
                })
                .catch(error => {
                    mainData.isErrorGetCategory = false;
                })
            await  axios.get(process.env.API.City_List)
                .then(res => {
                    mainData.listCity = res.data;
                })
                .catch(error => mainData.isErrorGetCity = true)
            return {
                mainData
            }
        },
        data() {
            return {
                v: {
                    showMoreListCity: false
                }
            }
        }
    }
</script>
<style>
    .text-head {
        font-family: 'Open Sans', Helvetica, Arial, sans-serif;
        font-size: 18px;
        font-weight: bold;

    }

    .headText {
        font-family: "Open Sans";
        position: relative;
        margin-top: 0;
        font-weight: 600;
        line-height: 1.2;
        color: #4a4a4a;
    }

    .headText:before {
        position: absolute;
        content: "";
        bottom: -0.9rem;
        left: -1.7rem;
        width: 50px;
        height: 1px;
        background-color: #dadada;
    }

    .shopSmall {
        border: 3px solid white;
        width: 80px;
        height: 80px;
        background-size: cover;
        margin:20px;
        position: absolute;
    }
    .shopSmallName{
        color:white;
        font-family: "Open Sans";
        margin-left:20px;
        margin-top:110px;
        font-size:24px;
        position: absolute;
    }
    .rateStar .fa-star {
        color: #FCEB12;
        font-size: 18px;
    }

    .buttonFlat {
        color: rgba(45, 45, 48, .4);
        cursor: pointer;
        text-align: center;
        font-size:18px;
    }

    .buttonFlat:hover {

        color: rgba(45, 45, 48, 1);
    }
</style>