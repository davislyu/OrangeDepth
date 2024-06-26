<template>
  <div class="homepage-container">
    <HeaderComp title="OrangeDepth°" :videoSource="orangeVideo"  >
      <template v-slot:extra-content>
        <AboutChart :AboutText="AboutText"  />
      </template>
    </HeaderComp>
    <div class="content">
      <About_siteComp :about_text="aboutSiteText"  />
      <div class="facts-container">
        <FactCard
          v-for="fact in paginatedFacts"
          :key="fact.fact_id"
          :fact_text="fact.fact_text"
          v-motion-slide-visible-left
        />
      </div>

      <Button
        label="Refresh"
        @click="nextPage"
        severity="warning"
        outlined
        class="button-refresh"
      />
      <div class="merch-container">
        <div class="merch-text">
          <h1>Our exclusive AI generated merch</h1>

          <p>
            Discover our exclusive AI-generated merchandise collection, where
            the zest of oranges meets the precision of data charts! Dive into a
            wardrobe where every Doughnutce is a splash of citrus sunshine,
            meticulously blended with the analytical prowess of data
            visualization. Our clothing line is not just apparel; it's a
            statement for those who revel in the tangy touch of oranges and the
            sharp insights of charts.
          </p>
        </div>
        <div class="caruselle-container">
          <CaruselleComp :images="caruselleImagesArray" />
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import Button from "primevue/button";
import orangeVideo from "../../assets/orangeVideo.mp4";
import { Ifact } from "../../interfaces/FactInterface";
import FactCard from "../../components/FactCard.vue";
import CaruselleComp from "../CaruselleComp.vue";
import About_siteComp from "../About_siteComp.vue";
import * as clothingImages from "../../assets/clothing";

import {
  HeaderComp,
  ref,
  computed,
  AboutChart,
  onMounted,
  reactive,
} from "../../index.ts";
const videoElement = ref<HTMLVideoElement | null>(null);

const currentPage = ref(0);
const pageSize = 3;
const aboutSiteText = ref(
  "Welcome to OrangeDepth°, where citrus meets data mastery! Dive into juicy datasets and charts with us. Whether you're a data ninja or just love vitamin C, grab a glass of orange juice and let's squeeze some insights together! 🍊💻 #DataCitrusMastery. Join us on a flavorful journey of discovery, where every chart is a slice of citrus sunshine and every dataset is a refreshing splash of insight. Let's zest up your data skills and embark on an orange-infused adventure together! 🚀🍊"
);
const facts = reactive<Ifact[]>([
  {
    fact_id: 1,
    fact_text:
      "Oranges are a rich source of vitamin C, which is essential for the immune system.",
  },
  {
    fact_id: 2,
    fact_text: "The orange is a hybrid between pomelo and mandarin.",
  },
  {
    fact_id: 3,
    fact_text: "Oranges originated around 4000 B.C. in Southeast Asia.",
  },
  {
    fact_id: 4,
    fact_text: "The fruit  used to describe the color.",
  },
  {
    fact_id: 5,
    fact_text: "There are over 600 varieties of oranges worldwide.",
  },
  {
    fact_id: 6,
    fact_text: "Brazil is the largest producer of oranges in the world.",
  },
  {
    fact_id: 7,
    fact_text: "Oranges are the largest citrus fruit in the world.",
  },
  {
    fact_id: 8,
    fact_text:
      "An orange tree can grow to reach 30 feet and live for over a hundred years.",
  },
  {
    fact_id: 9,
    fact_text:
      "Almost one-third of the world’s orange supply comes from Brazil.",
  },
  {
    fact_id: 10,
    fact_text:
      "Orange peels are rich in nutrients, including fiber, vitamin C, and plant compounds like polyphenols.",
  },
  {
    fact_id: 11,
    fact_text:
      "Oranges grow on evergreen flowering trees. These trees have a lifespan of over 50 years! Hence, an orange tree can provide its fruits to multiple generations.",
  },
  {
    fact_id: 12,
    fact_text:
      "Orange is just a modified berry! And just like other berries, oranges also have three fleshy layers with two or more seeds. They also develop from just one flower with one ovary.",
  },
]);
const paginatedFacts = computed(() => {
  const start = currentPage.value * pageSize;
  return facts.slice(start, start + pageSize);
});
const caruselleImagesArray = reactive([
  clothingImages.shirt,
  clothingImages.shirt2,
  clothingImages.shirt3,
  clothingImages.shirt4,
  clothingImages.shoes,
  clothingImages.shoes2,
  clothingImages.shoes3,
  clothingImages.socks,
  clothingImages.hat,
  clothingImages.umbrella,
  clothingImages.pants,
]);
onMounted(() => {
  if (videoElement.value) {
    videoElement.value.playbackRate = 0.8;
  }
});

function nextPage() {
  if ((currentPage.value + 1) * pageSize < facts.length) {
    currentPage.value++;
  } else {
    currentPage.value = 0;
  }
}
const AboutText = ref<string>(
  "        Welcome to a zestful realm where data crunching meets citrus punch!Here, numbers are juicier, and insights come with a twist of orange. Weserve up fresh, tangy data in a fun, flavorful way, making analytics anadventure in taste and knowledge. Get ready to peel back the layers ofinformation and discover the sweet core of citrus-powered data!"
);
</script>

<style lang="scss" scoped>
@import "../../styles/specificPages/_homePageMixins.scss";
@include homePageStyling;
</style>
