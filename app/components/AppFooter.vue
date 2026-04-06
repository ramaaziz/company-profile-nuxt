<script setup lang="ts"></script>

<template>
  <USeparator />

  <UFooter :ui="{ top: 'border-b border-default' }">
    <template #top>
      <UContainer
        class="flex flex-col items-center gap-2 py-12 sm:flex-row sm:justify-between"
      >
        <div class="text-center sm:text-left">
          <p class="text-sm leading-relaxed text-gray-600 dark:text-gray-400">
            <span class="font-bold text-gray-900 dark:text-white text-lg"
              >PT Permata Jaya Tehnik</span
            >
            <br />
            Jl. Terusan Jakarta, Ruko Puri Dago <br />
            Kav B No. 6 RT007 RW015 Sukamiskin <br />
            Arcamanik, Kota Bandung - 40291 <br />
            <span class="font-medium">022 - 63196046</span>
          </p>
        </div>
        <iframe
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d669.154127078746!2d107.66899595119986!3d-6.917652982295999!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x2e68e78b66eecc11%3A0x6d195f5f0829301c!2sPT%20PERMATA%20JAYA%20TEHNIK%2FDAFFA%20TOURS!5e1!3m2!1sen!2sid!4v1773024067406!5m2!1sen!2sid"
          width="100%"
          style="border: 0"
          loading="lazy"
          class="rounded-xl shadow-lg w-1/3"
        ></iframe>
      </UContainer>
    </template>

    <template #left>
      <p class="text-sm text-muted">
        PT Permata Jaya Tehnik • © {{ new Date().getFullYear() }}
      </p>
    </template>

    <template #right>
      <UAvatar
        src="/images/logo/logoISO9001.png"
        alt="PT Permata Jaya Tehnik"
        size="sm"
        class="mr-2"
      />
      <UAvatar
        src="/images/logo/logoISO14001.png"
        alt="PT Permata Jaya Tehnik"
        size="sm"
        class="mr-2"
      />
      <UAvatar
        src="/images/logo/logoISO45001.png"
        alt="PT Permata Jaya Tehnik"
        size="sm"
        class="mr-2"
      />
      <UAvatar
        src="/images/logo/smk3.png"
        alt="PT Permata Jaya Tehnik"
        size="sm"
        class="mr-2"
      />
    </template>
  </UFooter>
</template>
