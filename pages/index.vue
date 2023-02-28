<template>
  <div class="page-index">
    <el-container>
      <el-header>
        <el-row>
          <el-col :span="6">
            <el-image style="width: 60px; height: 60px" :src="logo" :fit="'contain'" />
          </el-col>
          <el-col :span="18">
            <el-menu
              :default-active="activeIndex"
              class="el-menu-demo"
              mode="horizontal"
              :ellipsis="false"
            >
              <el-menu-item v-for="menu in menuList" :index="menu.value"
                :key="menu.value" @click="turnToPage(menu)">
                {{menu.label}}会员
              </el-menu-item>
            </el-menu>
          </el-col>
        </el-row>
      </el-header>
      <el-container>
        <el-main>
          <router-view v-slot="{ Component, route }">
            <component
              :is="Component"
              :key="route.name"
            />
          </router-view>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>
<script lang="ts" setup>
import { ref,watch } from 'vue';
import { useRouter,route } from 'vue-router';
import logo from '../assets/images/logo.jpg';
import About from './about.vue';


const router = useRouter();
const route = useRoute();

const activeIndex = ref();
const menuList = ref([
  {label:'爱奇艺',value:'aiqiyi'},
  {label:'腾讯',value:'tencent'},
  {label:'优酷',value:'youku'},
  {label:'芒果TV',value:'mango'},
  {label:'b站',value:'bilibili'},
  {label:'百度网盘',value:'baidu'},
])

const turnToPage = (menu)=>{
  router.push({
    path: `/${menu.value}`, 
    params:{
      name:menu.label
    }
  })
}

watch(() => route, (newVal) => {
  debugger
}, { deep: true });
</script>
