<style scoped>
    .containerItem {
        width: 36px;
        height: 36px;
        background: transparent;
        display: inline-block;
        margin-right: 5px;
        overflow: hidden;
    }

    .google .chi1 {
        background-color: #DB4437;

        color: white
    }

    .facebook .chi1 {
        background-color: #4267B2;
        color: white
    }

    .twitter .chi1 {
        background-color: #1DA1F2;
        color: white;
    }

    .instagram .chi1 {
        background: linear-gradient(to right, #E74A51, #BD3381);
        color: white
    }

    .containerItem button {
        width: 36px;
        height: 36px;
        border: 0;
        transition: all .6s ease-in-out;
        outline: none;
        margin: 0;
        padding: 0;
    }

    .containerItem > button.chi1 {

    }

    .containerItem button.chi2 {
        margin-top: 0;
        background-color: black;
    }

    .containerItem:hover > button.chi1 {
        margin-top: -36px;
    }

    label {
        text-decoration: none;
        font-size: 18px;
        margin-top: 20px;
    }
</style>
<template>
    <div>
        <label>Chia sẻ</label>
        <div>
            <div class="containerItem google">
                <button class="chi1" @click="m_shareOn('google')">
                    <span class="fa fa-google-plus"></span>
                </button>
                <button class="chi2" @click="m_shareOn('google')">
                    <span class="fa fa-google-plus"></span>
                </button>
            </div>
            <div class="containerItem facebook">
                <button class="chi1" @click="m_shareOn('facebook')">
                    <span class="fa fa-facebook"></span>
                </button>
                <button class="chi2" @click="m_shareOn('facebook')">
                    <span class="fa fa-facebook"></span>
                </button>
            </div>
            <div class="containerItem twitter">
                <button class="chi1" @click="m_shareOn('twitter')">
                    <span class="fa fa-twitter"></span>
                </button>
                <button class="chi2" @click="m_shareOn('twitter')">
                    <span class="fa fa-twitter"></span>
                </button>
            </div>
            <div class="containerItem instagram">
                <button class="chi1">
                    <span class="fa fa-instagram" @click="m_shareOn('instagram')"></span>
                </button>
                <button class="chi2">
                    <span class="fa fa-instagram" @click="m_shareOn('instagram')"></span>
                </button>
            </div>
        </div>


    </div>
</template>

<script>
    import $ from 'jquery';

    export default {

        beforeMount() {


        },
        computed: {},
        methods: {
            m_shareOn(type) {
                FB.ui({
                    method: 'feed',
                    link: this.currentHref(),
                    caption: this.data.title,
                }, function(response){

                });
            },

        }
    }
</script>