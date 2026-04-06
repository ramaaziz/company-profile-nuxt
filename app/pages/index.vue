<script setup>
import { steps } from "#build/ui/prose";

const { data: page } = await useAsyncData("index", () =>
  queryCollection("content").first(),
);
const isOpen = ref(false);
const selectedItem = ref({});
const openModal = (features) => {
  selectedItem.value = features;
  isOpen.value = true;
};
const isOpen2 = ref(false);
const selectedItem2 = ref({});
const openModal2 = (step) => {
  selectedItem2.value = step;
  isOpen2.value = true;
  console.log(selectedItem2.value);
};
if (!page.value) {
  throw createError({
    statusCode: 404,
    statusMessage: "Page not found",
    fatal: true,
  });
}

useSeoMeta({
  title: page.value.seo?.title || page.value.title,
  ogTitle: page.value.seo?.title || page.value.title,
  description: page.value.seo?.description || page.value.description,
  ogDescription: page.value.seo?.description || page.value.description,
});
</script>

<template>
  <div v-if="page" class="relative">
    <div>
      <UColorModeImage
        light="/logos/logo-pjt.png"
        dark="/logos/logo-pjt.png"
        class="absolute left-1/2 -translate-x-1/2 top-15 pointer-events-none object-cover h-[250px] sm:h-[560px] opacity-50"
      />
    </div>

    <UPageHero
      :description="page.description"
      :ui="{
        container: 'md:pt-18 lg:pt-20',
        title: 'max-w-3xl mx-auto',
      }"
    >
      <template #top>
        <StarsBg />
      </template>

      <template #title>
        <MDC :value="page.title" unwrap="p" />
      </template>
    </UPageHero>

    <UPageSection
      :description="page.section.description"
      :features="page.section.features"
      orientation="horizontal"
      :ui="{
        container: 'lg:px-0 2xl:px-20 mx-0 max-w-none md:mr-10',
        features: 'gap-0',
      }"
      reverse
    >
      <template #title>
        <MDC :value="page.section.title" class="sm:*:leading-11" />
      </template>
      <img
        :src="page.section.images.desktop"
        :alt="page.section.title"
        class="hidden lg:block 2xl:hidden left-0 w-full max-w-2xl rounded-2xl"
      />
      <img
        :src="page.section.images.mobile"
        :alt="page.section.title"
        class="block lg:hidden 2xl:block 2xl:w-full 2xl:max-w-2xl"
      />
    </UPageSection>

    <USeparator :ui="{ border: 'border-primary/30' }" />

    <UPageSection
      id="features"
      :description="page.features.description"
      :ui="{
        title: 'text-left @container relative flex',
        description: 'text-left',
        features: 'grid grid-cols-2 sm:grid-cols-3 gap-8',
      }"
      class="relative overflow-hidden"
    >
      <template #top>
        <StarsBg />
      </template>
      <template #headline>
        <UColorModeImage
          light="/images/light/line-3.svg"
          dark="/images/dark/line-3.svg"
          class="absolute -top-10 sm:top-0 right-1/2 h-24"
        />
      </template>
      <template #title>
        <MDC :value="page.features.title" />
      </template>

      <template #features>
        <UPageCard
          v-for="(features, index) in page.features.items"
          :key="index"
          class="group cursor-pointer"
          :ui="{
            container: 'p-4 sm:p-4',
            title: 'flex items-center gap-1',
          }"
          spotlight
          spotlight-color="primary"
          @click="openModal(features)"
        >
          <UColorModeImage
            v-if="features.image"
            :light="features.image?.light"
            :dark="features.image?.dark"
            :alt="features.title"
            class="size-full rounded-lg transition-transform group-hover:scale-105 duration-300"
          />
          <div class="flex flex-col gap-2">
            <span class="text-lg font-semibold">
              {{ features.title }}
            </span>
            <span class="text-sm text-muted hidden sm:block">
              {{ features.description }}
            </span>
          </div>
        </UPageCard>

        <UModal v-model:open="isOpen">
          <template #content>
            <UCard>
              <template #header>
                <div class="flex items-center justify-between">
                  <h3 class="font-bold text-xl">{{ selectedItem.title }}</h3>
                  <UButton
                    color="gray"
                    variant="ghost"
                    icon="i-heroicons-x-mark-20-solid"
                    class="-my-1"
                    @click="isOpen = false"
                  />
                </div>
              </template>

              <UCarousel
                v-slot="{ item }"
                loop
                dots
                :autoplay="{ delay: 2000 }"
                :items="selectedItem.projectImages"
              >
                <div class="flex items-center justify-center h-96 w-full">
                  <img
                    :src="item"
                    class="rounded-lg max-w-xs max-h-full object-cover"
                    loading="lazy"
                  />
                </div>
              </UCarousel>

              <div class="pt-16">
                <p
                  class="text-gray-600 dark:text-gray-400 items-center justify-center text-center"
                >
                  {{ selectedItem.description }}
                </p>
              </div>
            </UCard>
          </template>
        </UModal>
      </template>
    </UPageSection>

    <USeparator :ui="{ border: 'border-primary/30' }" />

    <UPageSection
      id="steps"
      :description="page.steps.description"
      :features="page.steps.sertifikasi"
      orientation="horizontal"
      :ui="{
        container: 'lg:px-8 2xl:px-20 mx-0 max-w-none md:mr-10',
        features: 'gap-0',
      }"
    >
      <template #headline>
        <UColorModeImage
          light="/images/light/line-3.svg"
          dark="/images/dark/line-3.svg"
          class="absolute -top-10 sm:top-0 right-1/2 h-24"
        />
      </template>
      <template #title>
        <MDC :value="page.steps.title" class="sm:*:leading-11" />
      </template>
      <div class="grid grid-cols-2 sm:grid-cols-2 gap-4">
        <UPageCard
          v-for="(step, index) in page.steps.items"
          :key="index"
          class="group cursor-pointer"
          :ui="{ container: 'p-4 sm:p-4', title: 'flex items-center gap-1' }"
          spotlight
          spotlight-color="primary"
          @click="openModal2(step)"
        >
          <UColorModeImage
            v-if="step.image"
            :light="step.image?.light"
            :dark="step.image?.dark"
            :alt="step.title"
            class="w-full object-cover aspect-square transition-transform group-hover:scale-105 duration-300"
          />

          <div class="text-center gap-2">
            <span class="text-lg font-semibold">
              {{ step.title }}
            </span>
            <span class="text-sm text-muted">
              {{ step.description }}
            </span>
          </div>
        </UPageCard>
        <UModal v-model:open="isOpen2">
          <template #content>
            <UCard>
              <template #header>
                <div class="flex items-center justify-between">
                  <h3 class="font-bold text-xl">{{ selectedItem2.title }}</h3>
                  <UButton
                    color="gray"
                    variant="ghost"
                    icon="i-heroicons-x-mark-20-solid"
                    class="-my-1"
                    @click="isOpen2 = false"
                  />
                </div>
              </template>

              <div class="flex items-center justify-center h-96 w-full">
                <img
                  :src="selectedItem2.sertificate"
                  class="rounded-lg max-w-xs max-h-full object-cover"
                  loading="lazy"
                />
              </div>

              <div class="pt-16">
                <p
                  class="text-gray-600 dark:text-gray-400 items-center justify-center text-center"
                >
                  {{ selectedItem2.description }}
                </p>
              </div>
            </UCard>
          </template>
        </UModal>
      </div>
    </UPageSection>

    <UPageSection
      id="pricing"
      class="mb-32 overflow-hidden"
      :title="page.pricing.title"
      :description="page.pricing.description"
      :ui="{ title: 'text-left @container relative', description: 'text-left' }"
    >
      <template #headline>
        <UColorModeImage
          light="/images/light/line-5.svg"
          dark="/images/dark/line-5.svg"
          class="absolute -top-10 sm:top-0 right-1/2 h-24"
        />
      </template>
      <template #title>
        <MDC :value="page.testimonials.title" />
      </template>

      <UContainer>
        <UPageColumns class="xl:columns-3">
          <UPageCard
            v-for="(testimonial, index) in page.testimonials.items"
            :key="index"
            variant="subtle"
            :description="testimonial.quote"
            :ui="{
              description:
                'before:content-[open-quote] after:content-[close-quote]',
            }"
          >
            <template #footer>
              <UUser v-bind="testimonial.user" size="xl" />
            </template>
          </UPageCard>
        </UPageColumns>
      </UContainer>
    </UPageSection>

    <UPageSection
      id="testimonials"
      :title="page.testimonials.title"
      :description="page.testimonials.description"
      :items="page.testimonials.items"
    >
      <template #headline>
        <UColorModeImage
          light="/images/light/line-5.svg"
          dark="/images/dark/line-5.svg"
          class="absolute -top-10 sm:top-0 right-1/2 h-24"
        />
      </template>
      <template #title>
        <MDC :value="page.testimonials.title" />
      </template>

      <UContainer>
        <UPageColumns class="xl:columns-3">
          <UPageCard
            v-for="(testimonial, index) in page.testimonials.items"
            :key="index"
            variant="subtle"
            :description="testimonial.quote"
            :ui="{
              description:
                'before:content-[open-quote] after:content-[close-quote]',
            }"
          >
            <template #footer>
              <UUser v-bind="testimonial.user" size="xl" />
            </template>
          </UPageCard>
        </UPageColumns>
      </UContainer>
    </UPageSection>

    <USeparator />

    <UPageCTA
      v-bind="page.cta"
      variant="naked"
      class="overflow-hidden @container"
    >
      <template #title>
        <MDC :value="page.cta.title" />

        <div class="@max-[1280px]:hidden">
          <UColorModeImage
            light="/images/light/line-6.svg"
            dark="/images/dark/line-6.svg"
            class="absolute left-10 -top-10 sm:top-0 h-full"
          />
          <UColorModeImage
            light="/images/light/line-7.svg"
            dark="/images/dark/line-7.svg"
            class="absolute right-0 bottom-0 h-full"
          />
        </div>
      </template>

      <LazyStarsBg />
    </UPageCTA>
  </div>
</template>
