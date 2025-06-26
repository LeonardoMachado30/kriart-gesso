<template>
  <header class="top-0 w-full z-50">
    <div
      :class="[
        isScrolled
          ? 'fixed top-0 left-0 right-0 shadow-lg z-50 bg-[#fef102] header-transition header-fixed'
          : 'bg-[#fef102] header-transition',
        'w-full',
      ]"
    >
      <section class="mx-auto max-w-6xl">
        <div
          v-show="!isScrolled"
          class="flex items-center justify-between text-secondary --font-freeman521 text-[#e51924] text-[10px] md:text-md p-2 font-bold transition-all duration-300"
        >
          <p>Atendimento de segundas aos sábados</p>
          <p class="hidden md:block">
            Setor de indústria QI 05 Lote 380 - Gama, Brasília - DF, 72445-050
          </p>
          <a
            href="https://wa.me/5561998810165?text=Ol%C3%A1%20Kriart%20Gesso%2C%20gostaria%20de%20fazer%20um..."
            target="_blank"
            >Whatsapp: (61) 9 9881-0165</a
          >
        </div>
        <div class="flex items-center justify-between px-2 py-4">
          <img src="/logo-mini.svg" alt="Logo mini" width="100" height="30" />

          <!-- Botão burguer visível apenas no mobile -->
          <button
            class="md:hidden flex flex-col justify-center items-center w-10 h-10 rounded focus:outline-none"
            @click="menuAberto ? fecharMenu() : abrirMenu()"
            aria-label="Abrir menu"
          >
            <span
              class="block w-6 h-0.5 bg-[#333075] mb-1 transition-all duration-300"
              :class="{ 'rotate-45 translate-y-2': menuAberto }"
            ></span>
            <span
              class="block w-6 h-0.5 bg-[#333075] mb-1 transition-all duration-300"
              :class="{ 'opacity-0': menuAberto }"
            ></span>
            <span
              class="block w-6 h-0.5 bg-[#333075] transition-all duration-300"
              :class="{ '-rotate-45 -translate-y-2': menuAberto }"
            ></span>
          </button>

          <!-- Nav desktop -->
          <nav class="hidden md:block">
            <ul class="flex gap-4 text-primary text-[#333075]">
              <li
                v-for="section in sections"
                :key="section.id"
                class="hover:scale-110 hover:duration-200 hover:ease-in-out"
                :class="{ 'font-black': activeSection === section.id }"
              >
                <a :href="`#${section.id}`" @click.prevent="scrollToSection(section.id)">
                  {{ section.label }}
                </a>
              </li>
            </ul>
          </nav>

          <!-- Nav mobile com animação de transição -->
          <transition
            name="slide-menu"
            @after-leave="menuFinalizado = true"
            @before-enter="menuFinalizado = false"
          >
            <nav
              v-if="menuAberto"
              :class="[isScrolled ? 'top-22' : 'top-26']"
              class="fixed inset-0 w-full h-[240px] bg-[#fef102] flex flex-col z-[100] md:hidden transition-all duration-300 p-6"
              style="background-color: #fef102"
            >
              <ul class="flex flex-col gap-4 text-md text-[#333075]">
                <li
                  v-for="section in sections"
                  :key="section.id"
                  class="hover:scale-110 hover:duration-200 hover:ease-in-out"
                  :class="{ 'font-black': activeSection === section.id }"
                  @click="scrollToSection(section.id, true)"
                >
                  {{ section.label }}
                </li>
              </ul>
            </nav>
          </transition>
        </div>
      </section>
    </div>
  </header>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted, watch } from 'vue'

const isScrolled = ref(false)
const menuAberto = ref(false)
const menuFinalizado = ref(true) // Para garantir que o menu só some após a animação
const activeSection = ref('inicio')

const sections = [
  { id: 'inicio', label: 'Inicio' },
  { id: 'servicos', label: 'Serviços' },
  { id: 'sobreNos', label: 'Sobre Nós' },
  { id: 'depoimentos', label: 'Depoimentos' },
  { id: 'localizacao', label: 'Localização' },
]
let observer: IntersectionObserver | null = null

const handleScroll = () => {
  isScrolled.value = window.scrollY > 40
  // Fecha o menu ao rolar a página
  if (menuAberto.value && window.innerWidth < 768) {
    fecharMenu()
  }
}

function scrollToSection(sectionId: string, closeMenu = false) {
  const el = document.getElementById(sectionId)
  if (el) {
    const header = document.querySelector('header')
    const headerHeight = header ? (header as HTMLElement).offsetHeight : 0
    const elementTop = el.getBoundingClientRect().top + window.pageYOffset

    const offset = sectionId === 'inicio' ? 0 : 200
    const targetY = elementTop - headerHeight - offset // 200px acima do conteúdo
    animateScrollTo(targetY, 600)
  }
  if (closeMenu) {
    fecharMenu()
  }
}

// Função de animação suave
function animateScrollTo(targetY: number, duration = 600) {
  const startY = window.scrollY
  const change = targetY - startY
  const startTime = performance.now()

  function animate(currentTime: number) {
    const elapsed = currentTime - startTime
    const progress = Math.min(elapsed / duration, 1)
    const ease = easeInOutQuad(progress)
    window.scrollTo(0, startY + change * ease)
    if (progress < 1) {
      requestAnimationFrame(animate)
    }
  }
  requestAnimationFrame(animate)
}

function easeInOutQuad(t: number) {
  return t < 0.5 ? 2 * t * t : -1 + (4 - 2 * t) * t
}

// Função separada para abrir o menu
function abrirMenu() {
  if (!menuAberto.value) {
    menuFinalizado.value = false
    menuAberto.value = true
    document.body.style.overflow = 'hidden'
  }
}

// Função separada para fechar o menu
function fecharMenu() {
  if (menuAberto.value) {
    menuAberto.value = false
    // O overflow será liberado após a animação de saída
  }
}

// Libera o scroll do body quando o menu fecha de fato (após animação)
watch([menuAberto, menuFinalizado], ([aberto, finalizado]) => {
  if (!aberto && finalizado) {
    document.body.style.overflow = ''
  }
})

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  // Garante que o overflow está correto ao montar
  if (!menuAberto.value) {
    document.body.style.overflow = ''
  }

  // Observa as seções para destacar o menu
  observer = new window.IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          activeSection.value = entry.target.id
        }
      })
    },
    {
      root: null,
      rootMargin: '-30% 0px -60% 0px', // Ajusta para ativar quando a seção está mais centralizada
      threshold: 0.1,
    },
  )
  sections.forEach(({ id }) => {
    const el = document.getElementById(id)
    if (el) observer!.observe(el)
  })
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
  document.body.style.overflow = ''
  if (observer) observer.disconnect()
})
</script>

<style scoped lang="scss">
header {
  background-color: #fef102;
}

.header-transition {
  transition:
    box-shadow 0.4s cubic-bezier(0.4, 0, 0.2, 1),
    background-color 0.4s cubic-bezier(0.4, 0, 0.2, 1),
    transform 0.4s cubic-bezier(0.4, 0, 0.2, 1),
    top 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  will-change: box-shadow, background-color, transform, top;
}

.header-fixed {
  /* Exemplo de leve animação de translação para suavizar a entrada */
  transform: translateY(-20px);
  animation: slideDownHeader 0.4s forwards cubic-bezier(0.4, 0, 0.2, 1);
}

@keyframes slideDownHeader {
  from {
    transform: translateY(-20px);
  }
  to {
    transform: translateY(0);
  }
}

/* Transição do menu mobile */
.slide-menu-enter-active {
  animation: slideDownMenu 0.4s cubic-bezier(0.4, 0, 0.2, 1) forwards;
}
.slide-menu-leave-active {
  animation: slideUpMenu 0.4s cubic-bezier(0.4, 0, 0.2, 1) forwards;
}
@keyframes slideDownMenu {
  from {
    transform: translateY(-40px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}
@keyframes slideUpMenu {
  from {
    transform: translateY(0);
    opacity: 1;
  }
  to {
    transform: translateY(-40px);
    opacity: 0;
  }
}

/* Removido o overflow: auto global para evitar conflito com o controle do body pelo JS */
</style>
