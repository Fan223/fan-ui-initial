<template>
  <Header />

  <div>
    <ElDrawer
      v-model="topMenu.dialog"
      style="--el-drawer-padding-primary: 0; transition: none"
      size="100%"
      :modal="false"
      :show-close="false"
      direction="ttb"
      :lock-scroll="false"
    >
      <template #header>
        <Header style="color: var(--text-bright)" />
      </template>

      <ElMenu :default-active="topMenu.active" style="width: 80%; margin: 0 auto">
        <HeaderChild :menus="topMenu.data" />
      </ElMenu>
    </ElDrawer>
  </div>

  <Login />
  <RouterView />
</template>

<script setup lang="ts">
import Header from './header/Header.vue';
import HeaderChild from './header/HeaderChild.vue';
import Login from '@/views/Login.vue';
import { useGlobalStore, useNavMenuStore } from '@/pinia';

const { scrollPercent, screenWidth } = storeToRefs(useGlobalStore());
function calcScrollPercent() {
  let scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
  let windowHeight = window.innerHeight;
  let scrollHeight = document.documentElement.scrollHeight;

  let scrolled = Math.min((scrollTop / (scrollHeight - windowHeight)) * 100, 100);
  scrollPercent.value = Math.ceil(scrolled);
}
function handleScroll() {
  requestAnimationFrame(() => {
    calcScrollPercent();
  });
}

const { topMenu, asideMenu } = storeToRefs(useNavMenuStore());
function handleScreenResize() {
  screenWidth.value = window.innerWidth;

  if (screenWidth.value >= 768 && topMenu.value.dialog) {
    topMenu.value.dialog = false;
  }
  if (screenWidth.value >= 992 && asideMenu.value.drawer) {
    asideMenu.value.drawer = false;
  }
}

topMenu.value.data = [
  {
    id: '81973921257693184',
    parentId: '',
    position: 'top',
    name: '个人博客',
    path: '/blog',
    authority: 'blog',
    component: '/blog',
    type: 2,
    icon: 'i-ic-round-menu-book',
    orderNum: 100,
    flag: 'Y',
    createTime: '2023-10-18 15:04:36',
    updateTime: '2023-10-18 15:04:36',
    children: [],
  },
  {
    id: '81977524441653248',
    parentId: '',
    position: 'top',
    name: '在线工具',
    path: '/tool',
    authority: 'tool',
    component: '/tool',
    type: 2,
    icon: 'i-mdi-tools',
    orderNum: 200,
    flag: 'Y',
    createTime: '2023-10-18 15:18:55',
    updateTime: '2023-10-18 15:18:55',
    children: [],
  },
  {
    id: '81977748383932416',
    parentId: '',
    position: 'top',
    name: '网站后台',
    path: '/website',
    authority: 'website',
    component: '/website',
    type: 2,
    icon: 'i-mdi-web',
    orderNum: 300,
    flag: 'Y',
    createTime: '2023-10-18 15:19:49',
    updateTime: '2023-10-18 15:19:49',
    children: [],
  },
  {
    id: '81979760127320064',
    parentId: '',
    position: 'top',
    name: '关于',
    path: '/link',
    authority: 'link',
    component: '',
    type: 1,
    icon: 'i-mdi-about',
    orderNum: 400,
    flag: 'Y',
    createTime: '2023-10-18 15:27:48',
    updateTime: '2023-10-18 15:27:48',
    children: [
      {
        id: '81980159001436160',
        parentId: '81979760127320064',
        position: 'top',
        name: 'GitHub 仓库',
        path: 'https://github.com/Fan223',
        authority: '',
        component: '',
        type: 4,
        icon: 'i-line-md-github',
        orderNum: 410,
        flag: 'Y',
        createTime: '2023-10-18 15:29:23',
        updateTime: '2023-10-18 15:29:23',
        children: [],
      },
      {
        id: '81985658707054592',
        parentId: '81979760127320064',
        position: 'top',
        name: 'Blog',
        path: 'https://blog.fan223.cn/',
        authority: '',
        component: '',
        type: 2,
        icon: 'i-ic-round-menu-book',
        orderNum: 420,
        flag: 'Y',
        createTime: '2023-10-18 15:51:15',
        updateTime: '2023-10-18 15:51:15',
        children: [],
      },
    ],
  },
];

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
  window.addEventListener('resize', handleScroll);
  window.addEventListener('resize', handleScreenResize);
});
onBeforeUnmount(() => {
  window.removeEventListener('scroll', handleScroll);
  window.removeEventListener('resize', handleScroll);
  window.removeEventListener('resize', handleScreenResize);
});
</script>

<style scoped lang="scss"></style>
