<template>
  <section class="mx-auto max-w-6xl md:my-52 px-4">
    <h3 class="text-[#333075] md:text-[36px] text-center font-black mb-6">Nosso Produtos</h3>
    <div class="grid grid-cols-3 gap-2">
      <img
        v-for="(img, index) in Array.from({ length: 6 }, (_, i) => i)"
        :key="index"
        :src="`/material-${index + 1}.png`"
        class="hover:scale-105 hover:duration-400 hover:ease-in-out hover:shadow-lg"
        alt="gesso no teto"
      />
    </div>
  </section>
</template>
