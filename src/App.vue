<script setup>
import { ref } from 'vue' 
import Footer from './components/Footer.vue';
import HeroSection from './components/HeroSection.vue';
import Header from './components/Header.vue';
import HowItWorks from './components/HowItWorks.vue';
import Guarantee from './components/Guarantee.vue';
import PopUp from './components/PopUp.vue';
import CustomerReviews from './components/CustomerReviews.vue';
import PricingSection from './components/PricingSection.vue';
import FaqSection from './components/FaqSection.vue';
import AnnouncementBubble from './components/AnnouncementBubble.vue';
const bubbleVisible = ref(false)
function onPopupClosed() { setTimeout(() => (bubbleVisible.value = true), 300) }
function goToPlans() { window.location.href = '/plans' }

</script>

<template>
  <Header/>
  <HeroSection/>
  <PopUp @closed="onPopupClosed"/>
  <AnnouncementBubble
    v-model:visible="bubbleVisible"
    shape="circle"
    text="🎉 Get 20% OFF your first PetlyBox!"
    @click="goToPlans"
  />
  <HowItWorks/>
  <PricingSection/>
  <Guarantee/>
  <CustomerReviews/>
  <FaqSection/>
  <Footer/>
</template>

<style scoped>
</style>
