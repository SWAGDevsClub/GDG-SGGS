<template>
  <v-navigation-drawer v-model="sidebar" app floating temporary location="bottom">
    <v-list-item class="py-4" :title="mainData.communityName"></v-list-item>
    <v-divider></v-divider>
    <template v-for="(item, index) in navbarData" :key="index">
      <v-list-item v-if="item.visible" link  :to="item.path" @click="handleClick(item.name)" class="d-flex flex-row">
        <span class="mr-2">{{ item.name }}</span>
        
        <!-- Conditionally show the animation next to the title -->
        <template v-if="item.name === 'Events' && showAnimation">
          <iframe
            style="padding-bottom: 5% !important; border: none;"
            width="20px"
            height="20px"
            src="https://lottie.host/embed/ca16656a-68c5-4658-b4ac-a0e5805c7154/BfeO7czldI.lottie"
          ></iframe>
        </template>
      </v-list-item>
    </template>
  </v-navigation-drawer>
</template>



<script setup>
const { mainData, navbarData } = useJSONData();
const sidebar = useSideBar();
const showAnimation = ref(true);
const handleClick = (name)=>{
  if(name==="Events"){
    showAnimation.value = true;
  }
  else{
    showAnimation.value = false;
  }
}
</script>

<style>
</style>
