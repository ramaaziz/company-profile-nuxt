<script setup lang="ts">
const nuxtApp = useNuxtApp();
const { activeHeadings, updateHeadings } = useScrollspy();

const items = computed(() => [
  {
    label: "Portfolio",
    to: "#features",
    active:
      activeHeadings.value.includes("features") &&
      !activeHeadings.value.includes("steps"),
  },
  {
    label: "Sertifikasi",
    to: "#steps",
    active: activeHeadings.value.includes("steps"),
  },
  {
    label: "Team",
    to: "#testimonials",
    active:
      activeHeadings.value.includes("testimonials") &&
      !activeHeadings.value.includes("pricing"),
  },
]);

nuxtApp.hooks.hookOnce("page:finish", () => {
  updateHeadings(
    [
      document.querySelector("#features"),
      document.querySelector("#steps"),
      document.querySelector("#testimonials"),
    ].filter(Boolean) as Element[],
  );
});
</script>

<template>
  <UHeader>
    <template #left>
      <NuxtLink to="/">
        <img src="/logos/logo-pjt.png" loading="lazy" width="32" />
      </NuxtLink>
      <span>PT Permata Jaya Tehnik</span>
    </template>

    <template #right>
      <UNavigationMenu :items="items" variant="link" class="hidden lg:block" />

      <UColorModeButton />
    </template>

    <template #body>
      <UNavigationMenu :items="items" orientation="vertical" class="-mx-2.5" />
    </template>
  </UHeader>
</template>
