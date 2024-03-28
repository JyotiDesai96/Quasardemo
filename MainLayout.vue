<!-- eslint-disable vue/return-in-computed-property -->
<template>
<div class="q-pa-md padding">
    <q-layout view="hHh Lpr lff" class="shadow-2 rounded-borders">
        <q-header elevated :class="$q.dark.isActive ? 'bg-secondary' : 'bg-white'">
            <q-toolbar style="padding:10px;">
                <q-btn flat @click="drawer = !drawer" round dense icon="menu" />
                <q-item>
                    <q-item-section>
                        <q-img class="absolute-middle" src="../assets/youtube.jpg" style="height: 20px; width: 95px">
                          <q-tooltip class="btn-tooltip bg-accent">Youtube Home</q-tooltip>
                        </q-img>
                    </q-item-section>
                </q-item>
                <q-space />
                <q-input outlined rounded dense label="Search" 
                  v-model="global_search" input-class="text-right" 
                  class="q-ml-md" style="width:500px;margin-right:10px;">
                  <template v-slot:append>
                    <q-icon v-if="global_search === ''" name="search" >
                      <q-tooltip class="btn-tooltip bg-accent">Search</q-tooltip>
                    </q-icon>
                    <q-icon v-else name="clear" class="cursor-pointer" @click="global_search = ''">
                      <q-tooltip class="btn-tooltip bg-accent">Search</q-tooltip>
                    </q-icon>
                  </template>
                </q-input>
                <!-- <q-space /> -->
                <q-btn round   icon="local_florist" size="md" style="margin-right:10px;">
                  <q-tooltip class="btn-tooltip bg-accent">Search with your voice</q-tooltip>
                </q-btn>

                <q-space />
                <q-btn round   icon="notifications" size="md" style="margin-right: 10px;">
                  <q-tooltip class="btn-tooltip bg-accent">Notifications</q-tooltip>
                </q-btn>
                <q-avatar>
                  <img src="https://cdn.quasar.dev/img/avatar.png">
                </q-avatar>
            </q-toolbar>
        </q-header>

        <q-drawer 
          v-model="drawer" 
          :mini="miniState"
          @mouseover="miniState = false"
          @mouseout="miniState = true"
          show-if-above 
          :width="200" 
          :breakpoint="500" 
          bordered 
          :class="$q.dark.isActive ? 'bg-grey-9' : 'bg-grey-3'"
        >
            <q-scroll-area class="fit">
                <q-list>
                    <template v-for="(menuItem, index) in menuList">
                        <span :key="index">
                            <q-item clickable :active="menuItem.label === 'Outbox'" v-ripple>
                                <q-item-section avatar>
                                    <q-icon :name="menuItem.icon" />
                                    <!-- <span class="material-icons">{00258{menuItem.icon}}</span> -->
                                </q-item-section>
                                <q-item-section>
                                    {{ menuItem.label }}
                                </q-item-section>
                            </q-item>
                        </span>
                        <q-separator :key="'sep' + index" v-if="menuItem.separator" />
                    </template>

                </q-list>
            </q-scroll-area>
        </q-drawer>

        <q-page-container>
            <q-page padding>
              <div class="q-pa-md q-gutter-sm row" style="display:inline-flex;">
                <q-btn class="btn-menu q-mt-md bg-grey-4 text-black"  size="sm" v-for="menu in subMenuList" :key="menu.menu" color="primary"  :label="menu.menu" >
                  <q-tooltip class="btn-tooltip bg-accent">{{menu.tooltip}}</q-tooltip>
                </q-btn>
              </div>
              <div class="row" style="display:inline-flex;">
                  <q-card class="my-card col-lg-4 col-md-4 col-sm-2 col-xs-2" v-for="user in playListData" :key="user.title" style="margin:10px;">
                      <q-video :src="user.video" v-if="user.video" />
                      <img :src="require('../assets/' + user.image)" class="card-img" v-else>

                      <q-card-section style="display:flex;padding:16px 4px 16px 4px!important;">
                          <div style="margin-right: 8px;">
                              <q-avatar size="30px">
                                  <img src="https://cdn.quasar.dev/img/avatar.png">
                              </q-avatar>
                          </div>
                          <div>
                              <div class="box-title text-grey-9">
                                  <span>{{user.title}}</span>
                              </div>
                              <div class="box-subtitle">{{user.channelname}}</div>
                              <div>
                                  <span class="box-subtitle">{{user.views}}</span>
                                  <span class="box-subtitle">•</span>
                                  <span class="box-subtitle">{{user.createdBy}}</span>
                              </div>
                          </div>
                      </q-card-section>

                      <!-- <q-card-section ></q-card-section> -->
                  </q-card>
              </div>
            </q-page>
        </q-page-container>
    </q-layout>
</div>
</template>

<script>
import {
    ref
} from 'vue'
// import Home from '../components/Home.vue'
const menuList = [{
        icon: 'home',
        label: 'Home',
        path: '/Home',
        separator: true
    },
    {
        icon: 'send',
        label: 'Shorts',
        path: '/Shorts',
        separator: false
    },
    {
        icon: 'subscriptions',
        label: 'Subscriptions',
        path: '/Subscriptions',
        separator: false
    },
    {
        icon: 'style',
        label: 'you',
        path: '/You',
        separator: true
    }
]
const playList = [
  {
      title: 'Mind blowing music instrumental song by AR Rehman',
      icon: '',
      type:'nature',
      image: 'mountains (2).jpg',
      video: '',
      views: '3.4M views',
      channelname: 'Music Meditation',
      createdBy: '4 years ago'
  },
  {
      title: 'Mind blowing music instrumental song by AR Rehman',
      icon: '',
      image: 'parallax1.jpg',
      video: '',
      views: '3.4M views',
      channelname: 'Music Meditation',
      createdBy: '4 years ago'
  },
  {
      title: 'Mind blowing music instrumental song by AR Rehman',
      icon: '',
      image: 'mountains (2).jpg',
      type:'nature',
      video: '',
      views: '3.4M views',
      channelname: 'Music Meditation',
      createdBy: '4 years ago'
  },
  {
      title: 'Prank On Auto Rickshaw Drivers | Part 10 | Prakash Peswani Prank |',
      icon: '',
      image: 'quasar.jpg',
      video: '',
      views: '3.4M views',
      channelname: 'Music Meditation',
      createdBy: '4 years ago'
  },
  {
      title: 'Camila Cabello - I LUV IT Feat. Playboi Carti',
      icon: '',
      image: 'parallax1.jpg',
      video: '',
      views: '3.4M views',
      channelname: 'Music Meditation',
      createdBy: '4 years ago'
  },
  {
      title: 'Nightly News Full Broadcast - March 26',
      icon: '',
      image: 'quasar.jpg',
      type:'music',
      video: '',
      views: '112k views',
      channelname: 'NBC News',
      createdBy: '1 years ago'
  },
  {
      title: 'Video Jukebox Hindi Songs',
      type:'music',
      icon: '',
      image: '',
      video: 'https://www.youtube.com/embed/k3_tw44QsZQ?rel=0',
      views: '12l views',
      channelname: 'Tips Official',
      createdBy: '1 day ago'
  },

]
const subMenus = [
  {
    menu:'All',
    tooltip:'All',
    type:'all',
  },
  {
    menu:'Music',
    tooltip:'Music',
    type:'music',
  },
  {
    menu:'Nature',
    tooltip:'News',
    type:'nature',
  },
  {
    menu:'Live',
    tooltip:'Live',
    type:'live',
  },
  {
    menu:'T-Series',
    tooltip:'T-Series',
    type:'music',
  },
  {
    menu:'Comedy',
    tooltip:'Comedy'
  },
   {
    menu:'new to you',
    tooltip:'new to you'
  },
  {
    menu:'Bollywood music',
    tooltip:'Bollywood music',
    type:'music',
  },
  {
    menu:'recently uploaded',
    tooltip:'recently uploaded'
  },
  {
    menu:'watched',
    tooltip:'watched'
  },
  {
    menu:'shorts',
    tooltip:'shorts'
  },
  {
    menu:'subscriptions',
    tooltip:'subscriptions'
  },
]
export default {
    components: {

    },
    data() {
        return {
          drawer: ref(false),
          menuList,
          playListData: playList,
          miniState: ref(true),
          global_search:ref(''),
          subMenuList:subMenus,
        }
    },
    computed: {
      // filterData(menu){
      //    let filteredUsers = this.playListData.filter((data) => {
      //       return data.type === menu;
      //   });
      //   this.playListData = filteredUsers;
      //   console.log(filteredUsers);
      // }
    },
    methods:{
      
    }
}
</script>

<style scoped>
.padding {
    padding: 0px 0px !important;
}

.q-layout__section--marginal {
    color: black;
}

.my-card {
    width: 100%;
    max-width: 295px;
}

.box-title {
    font-size: 1.rem;
    line-height: 1.2rem;
    font-family: "Roboto", "Arial", sans-serif;
    /* color: black; */
    max-height: 4.4rem;
    text-overflow: ellipsis;
    white-space: normal;
    font-weight: 500;
    letter-spacing: -.2px;
    margin-bottom: 10px;
    text-transform: capitalize !important;
}

.box-subtitle {
    margin-right: -.1em;
    padding-right: 0.1em;
    text-align: left;
    flex-direction: row;
    font-family: "Roboto", "Arial", sans-serif;
    font-size: 0.8rem;
    line-height: 0.8rem;
    font-weight: 400;
    color: #606060;
    letter-spacing: -.2px;
    margin: 0px 5px;
    text-transform: capitalize !important;
}

.card-img {
    height: fit-content;
    width: -webkit-fill-available;
}
.btn-menu{
  font-family: "Roboto", "Arial", sans-serif !important;
  font-size:small !important;
  text-transform: capitalize !important;
  margin:5px 8px;
}
.btn-tooltip{
  text-transform: capitalize !important;
}
</style>
