<template>
  <div id="app">
    <nav class="navbar navbar-dark sticky-top bg-dark flex-md-nowrap p-0">
          <router-link  to="/" class="navbar-brand col-sm-4 col-md-2 mr-0">{{ $t("app_variamos") }}</router-link>
          <input class="form-control form-control-dark w-100 height-100" name="keyword" type="text" v-bind:placeholder="$t('app_search')" v-bind:aria-label="$t('app_search')">
          <ul class="navbar-nav px-3">
            <li class="nav-item text-nowrap">
              <a class="nav-link">{{ $t("app_sign_out") }}</a>
            </li>
          </ul>
        </nav>
        <div class="container-fluid">
            <div class="row">
              <Menu class="col-md-2 d-none d-md-block bg-light sidebar">
                <div class="sidebar-sticky">
                      <Filetree></Filetree>
                      <Divider />
                  <ul class="nav flex-column" style="display:none;">
                    <li class="nav-item">
                      <router-link class="nav-link" to="/">
                        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-home"><path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"></path><polyline points="9 22 9 12 15 12 15 22"></polyline></svg>
                        {{ $t("app_menu_home") }}
                      </router-link>
                    </li>
                    <li class="nav-item">
                      <router-link class="nav-link" to="/applies">
                        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather">
                        <circle cx="12" cy="12" r="10" />
                        <circle cx="12" cy="12" r="5" />
                        </svg>
                        {{ $t("app_menu_applies") }}
                      </router-link>
                    </li>
                    <li class="nav-item">
                      <router-link class="nav-link" to="/hlvl">
                        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather">
                        <circle cx="12" cy="12" r="10" />
                        <circle cx="12" cy="12" r="5" />
                        </svg>
                        {{ $t("app_menu_hlvl") }}
                      </router-link>
                    </li>
                    <li class="nav-item">
                      <router-link class="nav-link" to="/fragop">
                        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather">
                        <circle cx="12" cy="12" r="10" />
                        <circle cx="12" cy="12" r="5" />
                        </svg>
                        {{ $t("app_menu_fragop") }}
                      </router-link>
                    </li>
                    <li class="nav-item">
                      <router-link class="nav-link" to="/about">
                        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-users"><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"></path><circle cx="9" cy="7" r="4"></circle><path d="M23 21v-2a4 4 0 0 0-3-3.87"></path><path d="M16 3.13a4 4 0 0 1 0 7.75"></path></svg>
                        {{ $t("app_menu_about") }}
                      </router-link>
                    </li>
                    <li class="nav-item">
                      <router-link class="nav-link" to="/reports">
                        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-bar-chart-2"><line x1="18" y1="20" x2="18" y2="10"></line><line x1="12" y1="20" x2="12" y2="4"></line><line x1="6" y1="20" x2="6" y2="14"></line></svg>
                        {{ $t("app_menu_reports") }}
                      </router-link>
                    </li>
                  </ul>
                </div>
              </Menu>

              <main role="main" class="top-main col-md-9 ml-sm-auto col-lg-10 pt-3 px-4">

                <div class="container">
                  <div id="mainview">
                    <keep-alive>
                      <router-view></router-view>
                    </keep-alive>
                  </div>
                </div>

                <!-- begin main modal -->
                <div>                 
                      <div class="modal" id="main_modal">
                      <div class="modal-wrapper">
                        <div class="modal-container">
                          <content select=".modal-header">
                            <div id="main_modal_header" class="modal-header">
                              <h3>
                                
                              </h3>
                            </div>
                          </content>
                          <div id="main_modal_body" class="modal-body">
                            
                          </div>
                          <div class="modal-footer">
                            <div id="main_modal_footer"></div>
                            <div><button @click="hide_modal()">{{ $t("modal_close") }}</button></div>
                          </div>
                        </div>
                      </div>
                    </div>
                </div>
                <!-- end main modal -->

              </main>
          </div>

        </div>
  </div>
</template>

<script>
import Filetree from './views/Filemanagetree.vue'

export default {
  components:{
    Filetree
  },
  data: function(){
    return {
      split: 0.5
    }
  },
  methods: {
    hide_modal(){
      document.getElementById('main_modal').style.display="none";
    }
  }
}
</script>

<style>
@media (min-width: 768px){
  .top-main{
      -ms-flex: 0 0 83%;
      flex: 0 0 83%;
      max-width: 83%;
  }
}

.height-100 {
    height: 100% !important;
}

.dropdown-item.active, .dropdown-item:active {
   background-color: gainsboro !important;
}

.submenu{
  padding-left: 25px !important;
}

#mainview {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 7px;
}

.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
  display: none;
  transition: opacity .3s ease;
}
.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}
.modal-container {
  background: #fff;
  width: 650px;
  border-radius: 5px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all .3s ease;
  margin: 0 auto;
  padding: 20px 30px;
}
.modal-footer {
  margin-top: 15px;
}
.modal-enter, .modal-leave {
  opacity: 0;
}
.modal-enter .modal-container, .modal-leave .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}

</style>
