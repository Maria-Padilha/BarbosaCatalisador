<template>
  <v-app>
    <div class="min-h-screen bg-slate-950 text-slate-100 flex flex-col">
      <!-- NAVBAR -->
      <header
          class="sticky top-0 z-30 border-b border-white/10 bg-slate-950/80 backdrop-blur"
      >
        <v-container class="flex items-center justify-between py-3">
          <!-- Logo -->
         <v-sheet class="bg-transparent w-[180px]">
           <v-img alt="logo barbosa" :src="require('@/assets/img/logo.png')" cover width="100%" height="100%" />
         </v-sheet>

          <!-- Menu Desktop -->
          <nav class="hidden md:flex items-center gap-6 text-sm font-medium">
            <button class="hover:text-amber-400" @click="scrollToSection('como-funciona')">
              Como funciona
            </button>
            <button class="hover:text-amber-400" @click="scrollToSection('vender')">
              Vender
            </button>
            <button class="hover:text-amber-400" @click="scrollToSection('comprar')">
              Comprar
            </button>
            <button class="hover:text-amber-400" @click="scrollToSection('porque-nos')">
              Por que nós
            </button>
            <button class="hover:text-amber-400" @click="scrollToSection('faq')">
              Dúvidas
            </button>

            <v-btn
                class="ml-4 text-none"
                color="#00C94F"
                variant="flat"
                rounded="xl"
                @click="scrollToSection('contato')"
            >
              Falar no WhatsApp
            </v-btn>
          </nav>

          <!-- Botão mobile -->
          <div class="md:hidden">
            <v-btn
                icon
                variant="text"
                @click="menuAberto = !menuAberto"
                class="text-slate-100"
            >
              <v-icon>{{ menuAberto ? 'mdi-close' : 'mdi-menu' }}</v-icon>
            </v-btn>
          </div>
        </v-container>

        <!-- Menu Mobile -->
        <transition name="fade">
          <div
              v-if="menuAberto"
              class="md:hidden border-t border-white/10 bg-slate-950"
          >
            <v-container class="py-3 flex flex-col gap-2 text-sm">
              <button class="py-1 text-left" @click="goAndClose('como-funciona')">
                Como funciona
              </button>
              <button class="py-1 text-left" @click="goAndClose('vender')">
                Vender catalisador
              </button>
              <button class="py-1 text-left" @click="goAndClose('comprar')">
                Comprar catalisador
              </button>
              <button class="py-1 text-left" @click="goAndClose('porque-nos')">
                Por que nós
              </button>
              <button class="py-1 text-left" @click="goAndClose('faq')">
                Dúvidas frequentes
              </button>

              <v-btn
                  class="mt-2"
                  block
                  color="amber"
                  variant="flat"
                  rounded="xl"
                  @click="goAndClose('contato')"
              >
                Falar no WhatsApp
              </v-btn>
            </v-container>
          </div>
        </transition>
      </header>

      <!-- CONTEÚDO -->
      <v-main>
        <!-- HERO -->
        <section
            id="hero"
            class="min-h-[90vh] flex items-center"
        >
          <v-container>
            <div class="grid md:grid-cols-2 gap-10 items-center py-10">
              <!-- Texto -->
              <div>
                <p class="text-amber-400 font-semibold mb-3 uppercase tracking-[0.2em] text-xs">
                  Compra &amp; venda de catalisadores
                </p>
                <h1
                    class="text-4xl md:text-5xl lg:text-6xl font-extrabold leading-tight mb-4"
                >
                  Transforme seu
                  <span class="text-transparent bg-clip-text bg-gradient-to-r to-amber-400 from-green-500">
                    catalisador usado
                  </span>
                  em dinheiro na hora.
                </h1>
                <p class="text-slate-300 text-base md:text-lg max-w-xl mb-6">
                  Fazemos avaliação rápida e justa, com base na cotação atual dos
                  metais preciosos. Pagamento imediato via PIX e logística
                  facilitada para Cuiabá e Varzêa Grande.
                </p>

                <div class="flex flex-col sm:flex-row gap-3 mb-6">
                  <v-btn
                      color="#00C94F"
                      variant="flat"
                      rounded="xl"
                      size="large"
                      class="text-none"
                      @click="scrollToSection('contato')"
                  >
                    Solicitar cotação agora
                    <v-icon end>mdi-whatsapp</v-icon>
                  </v-btn>

                  <v-btn
                      variant="outlined"
                      rounded="xl"
                      size="large"
                      class="border-amber-300 text-amber-300 text-none"
                      @click="scrollToSection('como-funciona')"
                  >
                    Ver como funciona
                  </v-btn>
                </div>

                <div class="flex flex-wrap gap-4 text-xs text-slate-400">
                  <div class="flex items-center gap-2">
                    <span class="w-2 h-2 rounded-full bg-emerald-400"></span>
                    Pagamento no mesmo dia
                  </div>
                  <div class="flex items-center gap-2">
                    <span class="w-2 h-2 rounded-full bg-amber-400"></span>
                    Avaliação transparente
                  </div>
                  <div class="flex items-center gap-2">
                    <span class="w-2 h-2 rounded-full bg-sky-400"></span>
                    Atendemos Cuiabá e VG
                  </div>
                </div>
              </div>

              <!-- Card lateral / destaque — AGORA COM SLIDER -->
              <div>
                <div
                    class="rounded-3xl pa-5 border border-white/10 bg-gradient-to-b from-white/5 to-white/0 p-6 shadow-2xl shadow-amber-500/10"
                >
                  <h2 class="font-semibold text-lg mb-1">
                    Exemplos de Catalisadores
                  </h2>
                  <p class="text-sm text-slate-300 mb-4">
                    Veja alguns modelos reais que compramos e avaliamos diariamente.
                  </p>

                  <!-- SLIDER -->
                  <v-carousel
                      height="260"
                      hide-delimiter-background
                      :show-arrows="false"
                      cycle
                      interval="2500"
                      class="rounded-xl overflow-hidden border border-white/10"
                  >
                    <v-carousel-item
                        v-for="(item, i) in sliderCatalisadores"
                        :key="i"
                    >
                      <div class="relative w-full h-full">
                        <img
                            :src="item.img"
                            class="w-full h-full object-cover"
                            alt="Catalisador"
                        />
                        <div
                            class="absolute bottom-0 left-0 right-0 bg-black/60 px-3 py-2 text-xs text-slate-200"
                        >
                          {{ item.texto }}
                        </div>
                      </div>
                    </v-carousel-item>
                  </v-carousel>

                  <!-- Call to action -->
                  <v-btn
                      block
                      color="amber"
                      variant="flat"
                      rounded="xl"
                      size="large"
                      class="mt-5 text-none"
                      @click="scrollToSection('contato')"
                  >
                    Solicitar Cotação
                  </v-btn>

                  <p class="mt-3 text-[11px] text-slate-400">
                    Envie seu modelo e receba avaliação em poucos minutos.
                  </p>
                </div>
              </div>
            </div>
          </v-container>
        </section>

        <!-- COMO FUNCIONA -->
        <section
            id="como-funciona"
            class="py-14 border-t border-white/5 bg-slate-900/40"
        >
          <v-container>
            <div class="flex flex-col md:flex-row md:items-end md:justify-between gap-4 mb-8">
              <div data-aos="fade-down" data-aos-duration="1000">
                <h2 class="text-3xl md:text-4xl font-bold mb-2">
                  Como funciona
                </h2>
                <p class="text-slate-300 max-w-2xl">
                  Nosso processo é simples, transparente e pensado para que você
                  tenha segurança em cada etapa, seja para vender ou comprar
                  catalisadores.
                </p>
              </div>
            </div>

            <div class="grid md:grid-cols-3 gap-6">
              <div
                  v-for="(passo, i) in passos"
                  :key="i"
                  data-aos="fade-down" data-aos-duration="1200" :data-aos-delay="200 * i"
                  class="rounded-2xl border border-white/10 bg-slate-900/70 pa-5 card"
              >
                <div class="flex items-center gap-3 mb-3">
                  <div
                      class="w-9 h-9 flex items-center justify-center rounded-full bg-amber-500/10 border border-amber-500/40 text-amber-300 text-sm font-semibold"
                  >
                    {{ i + 1 }}
                  </div>
                  <h3 class="font-semibold text-base">
                    {{ passo.titulo }}
                  </h3>
                </div>
                <p class="text-sm text-slate-300">
                  {{ passo.descricao }}
                </p>
              </div>
            </div>
          </v-container>
        </section>

        <!-- VENDER -->
        <section
            id="vender"
            class="py-14"
        >
          <v-container>
            <div class="grid lg:grid-cols-2 gap-10 items-center">
              <div data-aos="fade-down" data-aos-duration="1200">
                <p class="text-amber-400 text-xs font-semibold uppercase tracking-[0.2em] mb-2">
                  Vender catalisador
                </p>
                <h2 class="text-3xl md:text-4xl font-bold mb-3">
                  Venda seu catalisador usado com preço justo
                </h2>
                <p class="text-slate-300 mb-6">
                  Catalisadores automotivos contêm metais valiosos como
                  <span class="font-semibold">platina, paládio e ródio</span>.
                  Compramos esses componentes com base na cotação atual dos
                  metais, garantindo o melhor retorno possível.
                </p>

                <ul class="space-y-2 text-sm text-slate-200 mb-6">
                  <li class="flex gap-2">
                    <span class="mt-1 text-green-400">●</span>
                    Pagamento rápido via PIX, TED ou dinheiro.
                  </li>
                  <li class="flex gap-2">
                    <span class="mt-1 text-green-400">●</span>
                    Avaliação técnica e transparente, sem promessas irreais.
                  </li>
                  <li class="flex gap-2">
                    <span class="mt-1 text-green-400">●</span>
                    Aceitamos catalisadores inteiros, sucata e lotes.
                  </li>
                  <li class="flex gap-2">
                    <span class="mt-1 text-green-400">●</span>
                    Coleta ou envio via transportadora em diversas regiões.
                  </li>
                </ul>

                <v-btn
                    color="amber"
                    variant="flat"
                    rounded="xl"
                    size="large"
                    class="text-none"
                    @click="scrollToSection('contato')"
                >
                  Quero vender agora
                </v-btn>
              </div>

              <div class="space-y-4 text-sm text-slate-300">
                <div
                    data-aos="fade-down" data-aos-duration="1200" data-aos-delay="200"
                    class="rounded-2xl border border-emerald-400/40 bg-emerald-500/5 pa-5 card"
                >
                  <v-img alt="catalisador" :src="require('@/assets/img/catalisador-carro.jpg')" class="rounded-lg" />
                </div>
              </div>
            </div>
          </v-container>
        </section>

        <!-- COMPRAR -->
        <section
            id="comprar"
            class="py-14 border-t border-white/5 bg-slate-900/40"
        >
          <v-container>
            <div class="grid lg:grid-cols-2 gap-10 items-center">
              <div data-aos="fade-down" data-aos-duration="1200" class="order-2 lg:order-1">
                <p class="text-amber-400 text-xs font-semibold uppercase tracking-[0.2em] mb-2">
                  Comprar catalisador
                </p>
                <h2 class="text-3xl md:text-4xl font-bold mb-3">
                  Catalisadores com procedência e qualidade garantida
                </h2>
                <p class="text-slate-300 mb-6">
                  Trabalhamos com peças selecionadas, revisadas e com procedência
                  comprovada. Ideal para oficinas, revendedores e clientes que
                  precisam repor o catalisador com segurança.
                </p>

                <ul class="space-y-2 text-sm text-slate-200 mb-6">
                  <li class="flex gap-2">
                    <span class="mt-1 text-sky-400">●</span>
                    Variedade de modelos para diferentes marcas e anos.
                  </li>
                  <li class="flex gap-2">
                    <span class="mt-1 text-sky-400">●</span>
                    Testes de funcionamento e análise visual.
                  </li>
                  <li class="flex gap-2">
                    <span class="mt-1 text-sky-400">●</span>
                    Opção de envio para todo o Brasil.
                  </li>
                  <li class="flex gap-2">
                    <span class="mt-1 text-sky-400">●</span>
                    Suporte para ajudar a encontrar o modelo correto.
                  </li>
                </ul>

                <v-btn
                    variant="outlined"
                    rounded="xl"
                    size="large"
                    class="border-amber-300 text-amber-300 text-none"
                    @click="scrollToSection('contato')"
                >
                  Consultar estoque
                </v-btn>
              </div>

              <div class="order-1 lg:order-2">
                <div
                    data-aos="fade-down" data-aos-duration="1200"
                    class="rounded-3xl card border border-white/10 bg-gradient-to-br from-slate-900 via-slate-900/80 to-slate-950 pa-5 shadow-lg"
                >
                  <v-img alt="catalisador" :src="require('@/assets/img/catalisador-pessoa.jpg')" class="rounded-lg" />
                </div>
              </div>
            </div>
          </v-container>
        </section>

        <!-- POR QUE NÓS -->
        <section
            id="porque-nos"
            class="py-14"
        >
          <v-container>
            <div data-aos="fade-down" data-aos-duration="1200" class="text-center max-w-2xl mx-auto mb-10">
              <h2 class="text-3xl md:text-4xl font-bold mb-3">
                Por que escolher nossa empresa?
              </h2>
              <p class="text-slate-300">
                Atuamos com foco em transparência, segurança e relacionamento
                de longo prazo. Nosso objetivo é que você sempre queira fazer
                negócio de novo.
              </p>
            </div>

            <div class="grid md:grid-cols-4 gap-6">
              <div
                  v-for="(beneficio, i) in beneficios"
                  :key="i"
                  data-aos="fade-down" data-aos-duration="1200" :data-aos-delay="200 * i"
                  class="rounded-2xl border border-white/10 bg-slate-900/70 pa-5 card text-sm"
              >
                <p class="text-2xl mb-3">
                  {{ beneficio.icone }}
                </p>
                <h3 class="font-semibold mb-2 text-base">
                  {{ beneficio.titulo }}
                </h3>
                <p class="text-slate-300">
                  {{ beneficio.descricao }}
                </p>
              </div>
            </div>
          </v-container>
        </section>

        <!-- TRABALHO COM CATALISADORES -->
        <section class="py-16 bg-gradient-to-b from-slate-950 via-slate-900 to-slate-950">
          <v-container>
            <div data-aos="fade-down" data-aos-duration="1200" class="text-center max-w-2xl mx-auto mb-10">
              <h2 class="text-3xl md:text-4xl font-bold mb-3">
                Nossos catalisadores em destaque
              </h2>
              <p class="text-slate-300">
                Veja alguns dos modelos de catalisadores que trabalhamos
                frequentemente, seja na compra ou venda.
              </p>
            </div>

            <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-8">
              <div
                  v-for="(item, i) in cardsCatalisadores"
                  :key="i"
                  data-aos="fade-down" data-aos-duration="1200" :data-aos-delay="50 * i"
                  class="group relative rounded-2xl overflow-hidden card pa-5 border border-white/10 bg-slate-900/70"
              >
                <img
                    :src="item.img"
                    class="w-full h-64 rounded-lg"
                    alt="Catalisador"
                />

                <div class="p-5 text-sm text-slate-300">
                  {{ item.texto }}
                </div>
              </div>
            </div>
          </v-container>
        </section>

        <!-- DEPOIMENTOS -->
        <section
            id="depoimentos"
            class="py-14 border-t border-white/5 bg-slate-900/40"
        >
          <v-container>
            <div data-aos="fade-down" data-aos-duration="1200" class="flex flex-col md:flex-row md:items-end md:justify-between gap-4 mb-8">
              <div>
                <h2 class="text-3xl md:text-4xl font-bold mb-2">
                  Quem já fez negócio com a gente
                </h2>
                <p class="text-slate-300 max-w-xl">
                  Veja a experiência de alguns clientes que venderam ou compraram
                  catalisadores conosco.
                </p>
              </div>
            </div>

            <div class="grid md:grid-cols-3 gap-6">
              <div
                  v-for="(dep, i) in depoimentos"
                  :key="i"
                  data-aos="fade-down" data-aos-duration="1200" :data-aos-delay="200 * i"
                  class="rounded-2xl border border-white/10 bg-slate-950/70 pa-5 card text-sm"
              >
                <v-icon icon="mdi-format-quote-open" size="40px" color="amber" />
                <p class="text-slate-200 mb-4 mt-2">
                  {{ dep.texto }}
                </p>
                <div class="flex flex-col">
                  <span class="font-semibold text-slate-100">
                    {{ dep.nome }}
                  </span>
                  <span class="text-xs text-slate-400">
                    {{ dep.tipo }}
                  </span>
                </div>
              </div>
            </div>
          </v-container>
        </section>

        <!-- FAQ -->
        <section
            id="faq"
            class="py-14"
        >
          <v-container>
            <div data-aos="fade-down" data-aos-duration="1200" class="text-center max-w-2xl mx-auto mb-10">
              <h2 class="text-3xl md:text-4xl font-bold mb-3">
                Dúvidas frequentes
              </h2>
              <p class="text-slate-300">
                Algumas das perguntas mais comuns sobre a compra e venda de
                catalisadores.
              </p>
            </div>

            <div data-aos="fade-down" data-aos-duration="1200" data-aos-delay="200" class="max-w-3xl mx-auto space-y-3">
              <v-expansion-panels variant="accordion" theme="dark" bg-color="#0C1529">
                <v-expansion-panel
                    v-for="(item, i) in faq"
                    :key="i"
                >
                  <v-expansion-panel-title>
                    {{ item.pergunta }}
                  </v-expansion-panel-title>
                  <v-expansion-panel-text>
                    {{ item.resposta }}
                  </v-expansion-panel-text>
                </v-expansion-panel>
              </v-expansion-panels>
            </div>
          </v-container>
        </section>

        <!-- CONTATO / WHATSAPP -->
        <section
            id="contato"
            class="py-16 border-t border-white/10 bg-gradient-to-b from-slate-900 via-slate-950 to-slate-950"
        >
          <v-container>
            <div class="grid lg:grid-cols-2 gap-10 items-center">
              <div data-aos="fade-down" data-aos-duration="1200">
                <p class="text-amber-400 text-xs font-semibold uppercase tracking-[0.2em] mb-2">
                  Cotação rápida
                </p>
                <h2 class="text-3xl md:text-4xl font-bold mb-3">
                  Envie agora os dados do seu catalisador
                </h2>
                <p class="text-slate-300 mb-6">
                  Você pode mandar fotos, código do catalisador ou modelo do
                  veículo. Retornamos com o valor estimado e explicamos todo o
                  processo de forma simples.
                </p>

                <ul class="space-y-2 text-sm text-slate-200 mb-6">
                  <li class="flex gap-2">
                    <span class="mt-1 text-green-400">●</span>
                    Atendimento via WhatsApp
                  </li>
                  <li class="flex gap-2">
                    <span class="mt-1 text-green-400">●</span>
                    Resposta em horário comercial
                  </li>
                  <li class="flex gap-2">
                    <span class="mt-1 text-green-400">●</span>
                    Negociação segura e transparente
                  </li>
                </ul>

                <div class="flex flex-col sm:flex-row gap-3">
                  <a
                      :href="whatsLink"
                      target="_blank"
                      rel="noopener noreferrer"
                      class="w-full sm:w-auto"
                  >
                    <v-btn
                        block
                        color="amber"
                        variant="flat"
                        rounded="xl"
                        size="large"
                        class="text-none"
                    >
                      Chamar no WhatsApp
                      <v-icon end>mdi-whatsapp</v-icon>
                    </v-btn>
                  </a>
                </div>
              </div>

              <div class="order-1 lg:order-2">
                <div
                    data-aos="fade-down" data-aos-duration="1200"
                    class="rounded-3xl card border border-white/10 bg-gradient-to-br from-slate-900 via-slate-900/80 to-slate-950 pa-5 shadow-lg"
                >
                  <v-img alt="catalisador" :src="require('@/assets/img/catalisador-carro-2.jpg')" class="rounded-lg" />
                </div>
              </div>
            </div>
          </v-container>
        </section>
      </v-main>

      <!-- FOOTER -->
      <footer class="border-t border-white/10 bg-slate-950">
        <v-container class="py-5 text-xs text-slate-400 flex flex-col md:flex-row gap-3 md:items-center md:justify-between">
          <div>
            © {{ new Date().getFullYear() }} Catalisador Trade. Todos os direitos
            reservados.
          </div>
          <div class="flex flex-wrap gap-3">
            <span>Compra e venda de catalisadores automotivos.</span>
            <span class="hidden md:inline-block">•</span>
            <span>Atendimento via WhatsApp.</span>
          </div>
        </v-container>
      </footer>
    </div>
  </v-app>
</template>

<script setup>
import { ref, computed } from 'vue'

const menuAberto = ref(false)

// Troque pelo número da empresa
const whatsappNumero = '5565999999999' // ex: 55 + DDD + número

const whatsMensagem = encodeURIComponent(
    'Olá! Gostaria de uma cotação para catalisador.'
)

const whatsLink = computed(
    () => `https://wa.me/${whatsappNumero}?text=${whatsMensagem}`
)

const scrollToSection = (id) => {
  const el = document.getElementById(id)
  if (!el) return
  const y = el.getBoundingClientRect().top + window.scrollY - 80
  window.scrollTo({ top: y, behavior: 'smooth' })
}

const goAndClose = (id) => {
  menuAberto.value = false
  scrollToSection(id)
}

const passos = [
  {
    titulo: 'Envie fotos ou código',
    descricao:
        'Você manda fotos do catalisador, o código gravado nele ou os dados do veículo (modelo, ano e motor).'
  },
  {
    titulo: 'Receba a cotação',
    descricao:
        'Avaliamos o catalisador com base na cotação dos metais preciosos e enviamos uma proposta de compra.'
  },
  {
    titulo: 'Pagamento imediato',
    descricao:
        'Se você aprovar o valor, combinamos a coleta ou envio e efetuamos o pagamento na hora combinada.'
  }
]

const beneficios = [
  {
    icone: '💸',
    titulo: 'Preço atualizado',
    descricao:
        'Usamos como base a cotação dos metais nobres, garantindo valores condizentes com o mercado.'
  },
  {
    icone: '⚖️',
    titulo: 'Transparência total',
    descricao:
        'Explicamos como chegamos ao valor de compra e tiramos todas as dúvidas durante a negociação.'
  },
  {
    icone: '⚡',
    titulo: 'Agilidade no atendimento',
    descricao:
        'Respostas rápidas e fechamento simples, sem burocracia desnecessária.'
  },
  {
    icone: '🛡️',
    titulo: 'Segurança no processo',
    descricao:
        'Negócios realizados com seriedade, visando relacionamento de longo prazo.'
  }
]

const depoimentos = [
  {
    nome: 'João Santos',
    tipo: 'Vendeu catalisador de sucata',
    texto:
        'Enviei as fotos pelo WhatsApp, recebi a cotação no mesmo dia e o pagamento caiu certinho no PIX. Processo simples e honesto.'
  },
  {
    nome: 'Auto Center Rodrigues',
    tipo: 'Oficina mecânica',
    texto:
        'Compramos catalisadores para alguns clientes e sempre fomos bem atendidos. Entrega rápida e sem dor de cabeça.'
  },
  {
    nome: 'Marcos Almeida',
    tipo: 'Revendedor',
    texto:
        'Negociamos lotes com frequência. Gosto da transparência na avaliação e do compromisso com prazo.'
  }
]

const faq = [
  {
    pergunta: 'Qual tipo de catalisador vocês compram?',
    resposta:
        'Compramos catalisadores automotivos originais, inteiros ou em forma de sucata, de diversos modelos e marcas. Em caso de dúvida, envie fotos para avaliarmos.'
  },
  {
    pergunta: 'Preciso levar o catalisador até vocês?',
    resposta:
        'Dependendo da região e do volume, podemos combinar coleta, ponto de entrega ou envio via transportadora. Tudo é combinado durante a negociação.'
  },
  {
    pergunta: 'Como é definido o valor de compra?',
    resposta:
        'O preço leva em conta o tipo de catalisador, o conteúdo de metais nobres e a cotação do mercado internacional no dia da negociação.'
  },
  {
    pergunta: 'O pagamento é feito na hora?',
    resposta:
        'Sim, após confirmar o catalisador e finalizar a negociação, realizamos o pagamento conforme combinado (PIX, TED ou dinheiro).'
  },
]

const sliderCatalisadores = [
  {
    img: require('@/assets/img/catalisador-1.jpg'),
    texto: 'Conjunto de catalisadores completos e bem preservados — ideal para avaliação de alto valor.'
  },
  {
    img: require('@/assets/img/catalisador-2.jpeg'),
    texto: 'Lote variado com dezenas de catalisadores usados, modelos nacionais e importados.'
  },
  {
    img: require('@/assets/img/catalisador-3.jpeg'),
    texto: 'Cerâmica interna de catalisadores triturada, usada para extração de metais preciosos.'
  },
  {
    img: require('@/assets/img/catalisador-4.jpeg'),
    texto: 'Catalisadores em diferentes estados, perfeitos para reciclagem e desmontagem.'
  }
]

const cardsCatalisadores = [
  {img: require('@/assets/img/cat1.png')},
  {img: require('@/assets/img/cat2.png')},
  {img: require('@/assets/img/cat3.png')},
  {img: require('@/assets/img/cat4.png')},
  {img: require('@/assets/img/cat5.png')},
  {img: require('@/assets/img/cat6.png')},
  {img: require('@/assets/img/cat7.png')},
  {img: require('@/assets/img/cat8.png')},
  {img: require('@/assets/img/cat9.png')},
  {img: require('@/assets/img/cat10.png')},
]

</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.18s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.card {
  transition: all 0.3s ease-in-out;
  cursor: pointer;
}

.card:hover {
  transform: scale(1.1);
  box-shadow: 0 0 10px #F2C72F;
  transition: all 0.3s ease-in-out;
}
</style>