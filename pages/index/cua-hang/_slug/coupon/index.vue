<template>
    <div class="container-fluid" style="padding:0;">
        <div style="background-color:white; padding:10px; position: relative;  margin:7.5px; margin-bottom:5px; margin-top:0;"
             class="">
            <el-select v-model="v.category" placeholder="Chọn danh mục">
                <el-option label="Danh mục" key="Danh mục" value="all"></el-option>
            </el-select>
        </div>
        <div class="col-sm-4 col-xs-6 mxColumn" v-for="item in mainData.listDeal">
            <div style=" border-top:0px; text-overflow: ellipsis; border-radius: 0; background-color:white">
                <div :style="`width:100%; height:200px; background-size:cover; background-image:url(${img_base+item.images[0]}); position:relative`">
                    <span style="font-family: 'Open Sans'; font-size:13px; background-color:orangered; color:white; padding:3px 5px;" class="msLabel">HOT</span>
                </div>
                <div style="padding:10px;">
                    <span style="font-family: 'Open Sans'; font-size:18px; text-overflow: ellipsis;">{{item.title}}</span>

                    <table class="table" style="padding:0; margin:0;">
                        <tbody style="margin:0;padding:0;">
                        <tr style="margin:0; padding:0">
                            <td style="border:0; border-right:1px dashed rgba(45,45,48,.2); margin:0; padding:0">
                                <div class="pull-left rateStar">
                                    <span class="fa fa-star"></span>
                                    <span class="fa fa-star"></span>
                                    <span class="fa fa-star"></span>
                                    <span class="fa fa-star"></span>
                                    <span class="fa fa-star"></span><br/>
                                    <span style="font-size:11px; font-family: 'Open Sans'">  (1502 đánh giá)</span>
                                </div>
                            </td>
                            <td style="border:0;   margin:0; padding:0; text-align: center;">
                                <span class="el-icon-goods buttonFlat"></span>
                            </td>
                            <td style="border:0; border-left:1px dashed rgba(45,45,48,.2);  margin:0; padding:0; text-align: center;">
                                <span class="el-icon-star-off buttonFlat"></span>
                            </td>
                            <td style="border:0; border-left:1px dashed rgba(45,45,48,.2); margin:0; padding:0; text-align:center">
                                <span class="el-icon-view buttonFlat"
                                      @click="$router.push(`/cua-hang/${$route.params.slug}/coupon/${item.slug}`)"></span>
                            </td>
                        </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>


    </div>
</template>
<script>
    import axios from 'axios'


    export default {

        head: {
            title: 'Spadi.vn | Coupon dành cho bạn tại Spadi.vn'
        },
        async asyncData({app, route}) {
            let mainData = {};
            await axios.get(process.env.API.Coupon_PublicGet + '?chain=' + route.params.slug)
                .then(res => {
                    mainData.listDeal = res.data;
                })
                .catch(error => {
                    mainData.isError = true;
                })
            return {mainData}
        },
        data() {
            return {
                v: {
                    category: 'all'
                }
            }
        }
    }
</script>
<style>
    @media (min-width: 769px) {
        .mxColumn {
            padding: 7.5px !important;
        }
    }

    .buttonFlat {
        color: rgba(45, 45, 48, .4);
        cursor: pointer;
        text-align: center;
        font-size: 18px;
    }

    .rateStar .fa-star {
        font-size: 14px;
    }

    .buttonFlat:hover {

        color: rgba(45, 45, 48, 1);
    }
    /*.msLabel{*/
        /*width:40px;*/
        /*text-align: center;*/
    /*}*/
    /*.msLabel:after{*/
        /*content: "";*/
        /*width: 0;*/
        /*height: 0;*/
        /*left: 0;*/
        /*margin-top:22px;*/
        /*border-style: solid;*/
        /*position: absolute;*/
        /*border-width: 0 18.5px 10px;*/
        /*border-color: transparent orangered;*/
        /*position: absolute;*/
    /*}*/
</style>
