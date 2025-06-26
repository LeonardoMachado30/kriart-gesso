<script setup lang="ts">
import AboutMe from './components/AboutMe.vue'
import FooterKriart from './components/FooterKriart.vue'
import GoogleAvalible from './components/GoogleAvalible.vue'
import HeaderKriart from './components/HeaderKriart.vue'
import LocalizationKriart from './components/LocalizationKriart.vue'
import OurProducts from './components/OurProducts.vue'
</script>

<template>
  <HeaderKriart />

  <main>
    <section
      :style="{ backgroundImage: `url('./background-default.png')` }"
      class="bg-cover min-h-[90vh] p-4 bg-[100%] bg-no-repeat"
      id="inicio"
    >
      <div class="flex flex-col md:mt-[180px] --font-freeman mx-auto max-w-6xl">
        <h1 class="text-2xl md:text-[64px] font-black max-w-[780px] text-[#333075] md:leading-22">
          QUALIDADE INCOMPARÁVEL EM GESSO – O MELHOR DE BRASÍLIA PARA VOCÊ!
        </h1>
        <div class="flex items-center gap-4 text-[#333075] md:text-sm font-black my-8">
          <p>Serviços de Gesso e Drywall * Isolamento e Conforto * Decoração e Detalhes</p>
        </div>
        <div class="flex gap-2">
          <a
            class="bg-[#25D366] px-2 md:px-4 py-2 shadow-md font-bold cursor-pointer hover:scale-110 hover:duration-200 hover:ease-in-out flex items-center gap-2"
            href="https://wa.me/5561998810165?text=Ol%C3%A1%20Kriart%20Gesso%2C%20gostaria%20de%20fazer%20um..."
            target="_blank"
          >
            <img
              src="/whatsapp.svg"
              class="hidden md:block"
              width="16"
              height="16"
              alt="whatsapp icone"
            />
            (61) 99881-0165
          </a>
          <button class="bg-[#333075] text-white px-4 py-2 shadow-md font-bold">
            Nós entramos em contato
          </button>
        </div>

        <div class="bg-white p-4 flex-col flex md:flex-row gap-4 mt-56 mb-4">
          <div class="w-full relative hover:scale-105 hover:duration-400 hover:ease-in-out">
            <img
              src="/forro-gesso.png"
              width="482"
              height="504"
              alt="Forro de gesso moderno e elegante"
              loading="lazy"
            />
            <p
              class="text-center font-bold absolute content-[''] right-0 left-0 bottom-4 text-white text-shadow-2xs"
            >
              Forro de gesso moderno e elegante
            </p>
          </div>
          <div class="w-full relative hover:scale-105 hover:duration-400 hover:ease-in-out">
            <img
              src="/sancas-decorativas.png"
              width="482"
              height="504"
              alt="Sancas decorativas para ambiente"
              loading="lazy"
            />
            <p
              class="text-center font-bold absolute content-[''] right-0 left-0 bottom-4 text-white text-shadow-2xs"
            >
              Sancas decorativas para ambiente
            </p>
          </div>
          <div class="w-full relative hover:scale-105 hover:duration-400 hover:ease-in-out">
            <img
              src="/divisorias-drywall.png"
              width="482"
              height="504"
              alt="Divisórias em drywall práticas"
              loading="lazy"
            />
            <p
              class="text-center font-bold absolute content-[''] right-0 left-0 bottom-4 text-white text-shadow-2xs"
            >
              Divisórias em drywall práticas
            </p>
          </div>
        </div>
      </div>
    </section>

    <section
      class="flex flex-col md:flex-row items-center mx-auto max-w-6xl my-22 gap-20 px-4"
      id="servicos"
    >
      <h3 class="text-[#333075] md:text-[36px] font-black md:leading-12 md:text-start text-center">
        Teto com Rasgos Iluminados: Sofisticação, Conforto Visual e Modernidade para Seu Espaço
      </h3>

      <img src="/gesso-teto.png" width="500" height="" alt="gesso no teto" />
    </section>

    <section
      class="flex flex-col-reverse md:flex-row items-center mx-auto max-w-6xl my-22 gap-20 px-4"
    >
      <img src="/gesso-parede.png" width="500" height="" alt="gesso no teto" />
      <h3 class="text-[#333075] md:text-[36px] font-black md:leading-12 md:text-start text-center">
        Paredes de Gesso 3D: Elegância, Estilo e Sofisticação para Seu Ambiente
      </h3>
    </section>

    <AboutMe />

    <OurProducts />

    <GoogleAvalible />

    <LocalizationKriart />

    <FooterKriart />
  </main>
</template>
