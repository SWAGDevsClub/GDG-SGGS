<template>
  <NuxtLayout name="default">
    <v-container fluid class="mt-5">
      <v-row>
        <v-col md="12">
          <h1>Past Events</h1>
          <p>
            Explore our past events, where innovation, learning, and collaboration came together. From workshops to
            hackathons, each event has left a lasting impact, fostering a vibrant community of creators and innovators.
          </p>
        </v-col>
      </v-row>
      <ClientOnly>
        <v-row class="mb-7">
          <v-col>
            <v-toolbar flat class="px-0" style="border-radius: 15px">
              <v-tabs v-model="model" color="primary" slider-color="primary" centered class="px-2">
                <v-tab
                  v-for="(item, index) in scheduleData"
                  :key="index"
                  @click="handleTabClick(item.year, index)"
                >
                  {{ item.year }}
                  <!-- Conditionally render the red dot animation based on year and active tab -->
                  <template v-if="item.year === '2025' && showAnimation">
                    <iframe
                      style="margin-bottom: 30% !important; border: none;"
                      width="25px"
                      height="30px"
                      src="https://lottie.host/embed/ca16656a-68c5-4658-b4ac-a0e5805c7154/BfeO7czldI.lottie"
                    ></iframe>
                  </template>
                </v-tab>
              </v-tabs>
            </v-toolbar>

            <v-tabs-window v-model="model" class="mt-5 py-0" style="background-color: white; border-radius: 15px">
              <v-tabs-window-item v-for="(item, index) in scheduleData" :key="index" class="pa-0 ma-0">
                <CommonScheduleDetails :data="item" />
              </v-tabs-window-item>
            </v-tabs-window>
          </v-col>
        </v-row>
      </ClientOnly>
    </v-container>
  </NuxtLayout>
</template>

<script setup>
const model = ref(null); // Track the active tab index
const showAnimation = ref(true); // Flag to control the visibility of the animation

const { mainData, scheduleData } = useJSONData();

definePageMeta({
  layout: false,
});

useSeoMeta({
  contentType: "text/html; charset=utf-8",
  title: "Agenda - " + mainData.eventInfo.name + " | " + mainData.communityName,
  description: mainData.eventInfo.description.short,
  keywords: mainData.seo.keywords,
  ogLocale: 'en_US',
  author: "OSS Labs",
  creator: "OSS Labs",
  viewport: "width=device-width, initial-scale=1.0",
  ogTitle:
    "Agenda - " + mainData.eventInfo.name + " | " + mainData.communityName,
  ogDescription: mainData.eventInfo.description.short,
  ogImage: `${mainData.seo.hostUrl}/thumbnail.png?auto=format&fit=crop&frame=1&h=512&w=1024`,
  ogUrl: mainData.seo.hostUrl,
  ogType: "website",
  twitterTitle:
    "Agenda - " + mainData.eventInfo.name + " | " + mainData.communityName,
  twitterDescription: mainData.eventInfo.description.short,
  twitterImage: `${mainData.seo.hostUrl}thumbnail.png?auto=format&fit=crop&frame=1&h=512&w=1024`,
  twitterCard: "summary_large_image",
});

const handleTabClick = (year, index) => {
  
  if (year === '2025') {
    showAnimation.value = false; 
  } else {
    showAnimation.value = true; 
  }
};
</script>

<style scoped>
/* Custom styles for the red dot animation */
</style>
