<template>
  <section
    class="flex items-center flex-col gap-4 mx-auto max-w-6xl md:my-52 px-4"
    id="depoimentos"
  >
    <h3 class="text-[#333075] md:text-[36px] text-center font-black">
      Nota Máxima em Todas as Avaliações
    </h3>

    <div class="flex flex-col md:flex-row gap-4">
      <div class="flex items-center shadow-2xl p-4">
        <div class="flex flex-col items-center">
          <p class="text-[96px] text-[#4285F4] font-bold">5</p>

          <div class="flex">
            <img
              v-for="(img, index) in Array.from({ length: 5 }, (_, i) => i)"
              :key="index"
              src="/star.svg"
              alt="estrelas"
              width="38"
              height="38"
            />
          </div>
        </div>
        <div class="flex flex-col items-center">
          <p class="text-[36px] font-bold">Google</p>
          <p class="text-lg">classificação máxima</p>
          <img src="/google-logo.svg" alt="Logo do google" />
        </div>
      </div>

      <div
        class="flex flex-col items-center justify-center gap-2 font-black text-sm shadow-2xl p-4"
      >
        <p>Erick Fleury</p>
        <div class="flex">
          <img
            v-for="(img, index) in Array.from({ length: 5 }, (_, i) => i)"
            :key="index"
            src="/star.svg"
            alt="estrelas"
            width="17"
            height="17"
          />
        </div>
        <p class="max-w-[205px]">
          Profissionais excelentes, serviço de ótima qualidade, material excelente. Recomendo.
        </p>
      </div>

      <div
        class="flex flex-col items-center justify-center gap-2 font-black text-sm shadow-2xl p-4"
      >
        <p>Rejane Fleury Santana</p>
        <div class="flex">
          <img
            v-for="(img, index) in Array.from({ length: 5 }, (_, i) => i)"
            :key="index"
            src="/star.svg"
            alt="estrelas"
            width="17"
            height="17"
          />
        </div>
        <p>Excelentíssimos!!!</p>
      </div>

      <div
        class="flex flex-col items-center justify-center gap-2 font-black text-sm shadow-2xl p-4"
      >
        <p>Marcelo Gregorio</p>
        <div class="flex">
          <img
            v-for="(img, index) in Array.from({ length: 5 }, (_, i) => i)"
            :key="index"
            src="/star.svg"
            alt="estrelas"
            width="17"
            height="17"
          />
        </div>
        <p>Bons preços</p>
      </div>
    </div>

    <button class="bg-[#333075] text-white px-4 py-2 shadow-md font-bold">
      Ver mais avaliações
    </button>
  </section>
</template>
