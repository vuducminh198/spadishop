<style scoped>
    .mstransparentButton{
        background:transparent;
        color:black;
        font-size: 10px;
        border:0;
        padding:0;
    }
</style>
<template>
    <aside class="main-sidebar">

        <!-- sidebar: style can be found in sidebar.less -->
        <section class="sidebar">

            <!-- Sidebar user panel (optional) -->
            <div class="user-panel">
                <div class="pull-left image">
                    <img :src="pictureUrl"/>
                </div>
                <div class="pull-left info">
                    <div>
                        <p class="white">{{ $store.state.adminInfo.name }}</p>
                    </div>
                    <button class="mstransparentButton"  @click="m_logoutAdmin">
                        <i class="fa fa-circle text-success"></i> Online
                        (<span>Đăng xuất</span>)
                    </button>
                </div>
            </div>

            <!-- search form (Optional) -->
            <form v-on:submit.prevent class="sidebar-form">
                <div class="input-group">
                    <input type="text"
                           style="border:0!important"
                           name="search"
                           id="search"
                           class="search form-control"
                           data-toggle="hideseek" placeholder="Search Menus"
                           data-list=".sidebar-menu">
                    <span class="input-group-btn">
            <button type="submit" name="search" id="search-btn" class="btn btn-flat">
              <i class="fa fa-search"></i>
            </button>
          </span>
                </div>
            </form>
            <!-- /.search form -->

            <!-- Sidebar Menu -->
            <sidebar-menu/>
            <!-- /.sidebar-menu -->
        </section>
        <!-- /.sidebar -->
    </aside>
</template>
<script>
    import SidebarMenu from './SidebarMenu'


    export default {
        name: 'Sidebar',
        props: ['displayName', 'pictureUrl'],
        components: {SidebarMenu},
        beforeMount() {

        },
        mounted: function () {
            //window.jQuery('[data-toggle="hideseek"]').off().hideseek()
        },
        methods: {
            m_logoutAdmin() {
                this.setCookie('token','');
                this.$store.commit('updateToken','');
                this.$router.push('/quan-tri/dang-nhap');
            }
        }
    }
</script>
<style>
    .user-panel .image img {
        border-radius: 50%;
    }
</style>
