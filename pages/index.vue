<script setup lang="ts">
const { data: page } = await useAsyncData('index', () => queryContent('/').findOne())
const isOpen = ref(false)
const isOpen1 = ref(false)
const isOpen2 = ref(false)
const isOpen3 = ref(false)
const isOpen4 = ref(false)
const isOpen5 = ref(false)

useSeoMeta({
  title: page.value.title,
  ogTitle: page.value.title,
  description: page.value.description,
  ogDescription: page.value.description
})
const openLinkInNewTab = (link: string) => {
  window.open(link, '_blank');
};

</script>


<template>
  <div>
    <ULandingHero :title="page.hero.title" :description="page.hero.description" :links="page.hero.links">
      <template #headline>
        <UBadge v-if="page.hero.headline" variant="subtle" size="lg" class="relative rounded-full font-semibold">
          <NuxtLink :to="page.hero.headline.to" target="_blank" class="focus:outline-none" tabindex="-1">
          </NuxtLink>

          {{ page.hero.headline.label }}

          <UIcon v-if="page.hero.headline.icon" :name="page.hero.headline.icon"
            class="ml-1 w-4 h-4 pointer-events-none" />
        </UBadge>
      </template>

      <Placeholder />

      <ULandingLogos :title="page.logos.title" align="center">
        <UIcon v-for="icon in page.logos.icons" :key="icon" :name="icon"
          class="w-12 h-12 lg:w-16 lg:h-16 flex-shrink-0 text-gray-900 dark:text-white" />
      </ULandingLogos>
    </ULandingHero>

    <ULandingSection :title="page.features.title" :description="page.features.description"
      :headline="page.features.headline">
      <UPageGrid id="features" class="scroll-mt-[calc(var(--header-height)+140px+128px+96px)]">
        <ULandingCard v-for="(item, index) in page.features.items" :key="index" v-bind="item" />
      </UPageGrid>
    </ULandingSection>

    <ULandingSection :title="page.pricing.title" :description="page.pricing.description"
      :headline="page.pricing.headline">
      <UPricingGrid id="pricing" compact class="scroll-mt-[calc(var(--header-height)+140px+128px+96px)]">
        <UPricingCard v-for="(plan, index) in page.pricing.plans" :key="index" v-bind="plan">
        </UPricingCard>
      </UPricingGrid>
    </ULandingSection>

    <ULandingSection :headline="page.testimonials.headline" :title="page.testimonials.title"
      :description="page.testimonials.description">
      <UPageColumns id="testimonials" class="xl:columns-4 scroll-mt-[calc(var(--header-height)+140px+128px+96px)]">
        <div v-for="(testimonial, index) in page.testimonials.items" :key="index" class="break-inside-avoid">
          <ULandingTestimonial v-bind="testimonial" />
        </div>
      </UPageColumns>
    </ULandingSection>


    <ULandingSection :title="page.cta.title" :description="page.cta.description"
      class="bg-primary-50 dark:bg-primary-400 dark:bg-opacity-10">
      <div class="grid-container">
        <UButton label="Website Klinik PKU" @click="isOpen = true" />
        <UButton label="Website Labelbox" @click="isOpen1 = true" />
        <UButton label="Website Polnep" @click="isOpen2 = true" />
        <UButton label="Website Portofolio" @click="isOpen3 = true" />
        <UButton label="Website Sakew" @click="isOpen4 = true" />
        <UButton label="Website SatuMipa" @click="isOpen5 = true" />
        <UModal v-model="isOpen" :overlay="false">
          <div class="p-1 image-container">
            <img src="public/klinik.jpeg" alt="Panda 1">
          </div>
        </UModal>
        <UModal v-model="isOpen1" :overlay="false">
          <div class="p-4">
            <img src="public/labelbox.jpg" alt="Panda 1">
          </div>
        </UModal>
        <UModal v-model="isOpen2" :overlay="false">
          <div class="p-4">
            <img src="public/polnep.png" alt="Panda 1">
          </div>
        </UModal>
        <UModal v-model="isOpen3" :overlay="false">
          <div class="p-4">
            <img src="public/portofolio.jpg" alt="Panda 1">
          </div>
        </UModal>
        <UModal v-model="isOpen4" :overlay="false">
          <div class="p-4">
            <img src="public/sakew.png" alt="Panda 1">
          </div>
        </UModal>
        <UModal v-model="isOpen5" :overlay="false">
          <div class="p-">
            <img src="public/satumipa.jpg" alt="Panda 1">
          </div>
        </UModal>
      </div>
    </ULandingSection>

    <ULandingSection id="faq" :title="page.faq.title" :description="page.faq.description"
      class="scroll-mt-[var(--header-height)]">
      <ULandingFAQ multiple :items="page.faq.items" :ui="{
      button: {
        label: 'font-semibold',
        trailingIcon: {
          base: 'w-6 h-6'
        }
      }
    }" class="max-w-4xl mx-auto" />
    </ULandingSection>
  </div>
</template>
<style>
/* Styles for the grid */
.grid-container {
  display: grid;
  text-align: center;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}

.image-container {
  text-align: center;
}

.image-container img {
  max-width: 100%;
  height: auto;
}

@media screen and (max-width: 767px) {
  .image-container {
    text-align: center;
  }
}
</style>
