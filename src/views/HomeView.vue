<template>
  <v-app>
    <div class="site-page min-h-screen text-slate-900">
      <!-- NAVBAR -->
      <header class="navbar">
        <v-container class="nav-wrap">
          <button class="brand" @click="scrollToSection('hero')" aria-label="Ir para o início">
            <v-sheet class="brand-logo" color="transparent">
              <v-img
                  :src="require('@/assets/img/logo.png')"
                  alt="Logo Barbosa Catalisadores"
                  contain
                  height="54"
              />
            </v-sheet>
          </button>

          <nav class="desktop-menu">
            <button @click="scrollToSection('como-funciona')">Como funciona</button>
            <button @click="scrollToSection('vender')">Vender</button>
            <button @click="scrollToSection('comprar')">Comprar</button>
            <button @click="scrollToSection('galeria')">Galeria</button>
            <button @click="scrollToSection('faq')">Dúvidas</button>
          </nav>

          <div class="desktop-actions">
            <a :href="whatsLink" target="_blank" rel="noopener noreferrer">
              <v-btn rounded="xl" size="large" class="btn-primary text-none" elevation="0">
                Falar no WhatsApp
                <v-icon end>mdi-whatsapp</v-icon>
              </v-btn>
            </a>
          </div>

          <v-btn
              class="mobile-menu-button"
              icon
              variant="text"
              @click="menuAberto = !menuAberto"
          >
            <v-icon>{{ menuAberto ? 'mdi-close' : 'mdi-menu' }}</v-icon>
          </v-btn>
        </v-container>

        <transition name="fade">
          <div v-if="menuAberto" class="mobile-menu">
            <v-container class="mobile-menu-inner">
              <button @click="goAndClose('como-funciona')">Como funciona</button>
              <button @click="goAndClose('vender')">Vender catalisador</button>
              <button @click="goAndClose('comprar')">Comprar catalisador</button>
              <button @click="goAndClose('galeria')">Galeria</button>
              <button @click="goAndClose('faq')">Dúvidas frequentes</button>

              <a :href="whatsLink" target="_blank" rel="noopener noreferrer">
                <v-btn block rounded="xl" size="large" class="btn-primary text-none mt-3" elevation="0">
                  Chamar no WhatsApp
                  <v-icon end>mdi-whatsapp</v-icon>
                </v-btn>
              </a>
            </v-container>
          </div>
        </transition>
      </header>

      <v-main>
        <!-- HERO -->
        <section id="hero" class="hero-section">
          <div class="hero-bg-glow hero-bg-glow-one" />
          <div class="hero-bg-glow hero-bg-glow-two" />

          <v-container>
            <div class="hero-grid">
              <div class="hero-copy" data-aos="fade-right" data-aos-duration="900">
                <div class="hero-badge">
                  <v-icon size="18">mdi-recycle</v-icon>
                  Compra e venda de catalisadores
                </div>

                <h1>
                  Seu catalisador usado pode virar
                  <span>dinheiro rápido</span>
                </h1>

                <p class="hero-subtitle">
                  Cotação simples, pagamento via PIX e atendimento direto pelo WhatsApp.
                </p>

                <div class="hero-actions">
                  <a :href="whatsLink" target="_blank" rel="noopener noreferrer">
                    <v-btn rounded="xl" size="x-large" class="btn-primary text-none" elevation="0">
                      Solicitar cotação
                      <v-icon end>mdi-whatsapp</v-icon>
                    </v-btn>
                  </a>

                  <v-btn
                      rounded="xl"
                      size="x-large"
                      variant="outlined"
                      class="btn-secondary text-none"
                      @click="scrollToSection('galeria')"
                  >
                    Ver catalisadores
                  </v-btn>
                </div>

                <div class="hero-stats">
                  <div v-for="item in stats" :key="item.label" class="stat-card">
                    <strong>{{ item.value }}</strong>
                    <span>{{ item.label }}</span>
                  </div>
                </div>
              </div>

              <div class="hero-visual" data-aos="fade-left" data-aos-duration="900">
                <div class="main-photo-card">
                  <v-carousel
                      height="520"
                      cycle
                      interval="2800"
                      hide-delimiter-background
                      :show-arrows="false"
                      class="hero-carousel"
                  >
                    <v-carousel-item v-for="(item, i) in sliderCatalisadores" :key="i">
                      <img :src="item.img" :alt="item.alt" class="carousel-image" />
                    </v-carousel-item>
                  </v-carousel>

                  <div class="floating-card floating-card-top">
                    <v-icon color="#16a34a">mdi-cash</v-icon>
                    <span>Pagamento rápido</span>
                  </div>

                  <div class="floating-card floating-card-bottom">
                    <v-icon color="#0284c7">mdi-camera</v-icon>
                    <span>Envie fotos para cotar</span>
                  </div>
                </div>
              </div>
            </div>
          </v-container>
        </section>

        <!-- COMO FUNCIONA -->
        <section id="como-funciona" class="section-padding section-white">
          <v-container>
            <div class="section-heading center" data-aos="fade-up">
              <span class="eyebrow">Processo simples</span>
              <h2>Como funciona</h2>
              <p>Você envia, nós avaliamos, combinamos a retirada ou entrega e o pagamento é feito com segurança.</p>
            </div>

            <div class="steps-grid">
              <article
                  v-for="(passo, i) in passos"
                  :key="passo.titulo"
                  class="step-card"
                  data-aos="fade-up"
                  :data-aos-delay="120 * i"
              >
                <div class="step-number">{{ String(i + 1).padStart(2, '0') }}</div>
                <v-icon :icon="passo.icon" size="34" />
                <h3>{{ passo.titulo }}</h3>
                <p>{{ passo.descricao }}</p>
              </article>
            </div>
          </v-container>
        </section>

        <!-- VENDER -->
        <section id="vender" class="section-padding section-soft">
          <v-container>
            <div class="split-grid">
              <div class="image-mosaic" data-aos="fade-right">
                <img class="mosaic-large" :src="images.venderPrincipal" alt="Catalisador automotivo" />
                <img class="mosaic-small one" :src="images.venderDetalhe" alt="Detalhe de catalisador" />
                <img class="mosaic-small two" :src="images.oficina" alt="Oficina mecânica" />
              </div>

              <div class="section-copy" data-aos="fade-left">
                <span class="eyebrow">Para vender</span>
                <h2>Venda seu catalisador usado sem complicação</h2>
                <p>
                  Atendimento direto para peças inteiras, sucata e lotes. Envie fotos pelo WhatsApp e receba uma avaliação.
                </p>

                <div class="feature-list">
                  <div v-for="item in venderFeatures" :key="item" class="feature-item">
                    <v-icon size="22" color="#16a34a">mdi-check-circle</v-icon>
                    <span>{{ item }}</span>
                  </div>
                </div>

                <a :href="whatsVenderLink" target="_blank" rel="noopener noreferrer">
                  <v-btn rounded="xl" size="large" class="btn-primary text-none" elevation="0">
                    Quero vender agora
                    <v-icon end>mdi-arrow-right</v-icon>
                  </v-btn>
                </a>
              </div>
            </div>
          </v-container>
        </section>

        <!-- COMPRAR -->
        <section id="comprar" class="section-padding section-white">
          <v-container>
            <div class="split-grid reverse-mobile">
              <div class="section-copy" data-aos="fade-right">
                <span class="eyebrow">Para comprar</span>
                <h2>Catalisadores com procedência e suporte na escolha</h2>
                <p>
                  Consulte disponibilidade, modelos compatíveis e opções de envio. Ideal para oficinas, revendedores e clientes finais.
                </p>

                <div class="feature-list two-columns">
                  <div v-for="item in comprarFeatures" :key="item" class="feature-item">
                    <v-icon size="22" color="#0284c7">mdi-check-circle</v-icon>
                    <span>{{ item }}</span>
                  </div>
                </div>

                <a :href="whatsComprarLink" target="_blank" rel="noopener noreferrer">
                  <v-btn rounded="xl" size="large" variant="outlined" class="btn-outline text-none">
                    Consultar estoque
                    <v-icon end>mdi-whatsapp</v-icon>
                  </v-btn>
                </a>
              </div>

              <div class="product-showcase" data-aos="fade-left">
                <div class="product-main-card">
                  <img :src="images.comprarPrincipal" alt="Catalisador em bancada" />
                </div>
                <div class="mini-product-row">
                  <div v-for="item in miniProdutos" :key="item.alt" class="mini-product-card">
                    <img :src="item.img" :alt="item.alt" />
                  </div>
                </div>
              </div>
            </div>
          </v-container>
        </section>

        <!-- BENEFÍCIOS -->
        <section id="porque-nos" class="section-padding section-soft">
          <v-container>
            <div class="section-heading" data-aos="fade-up">
              <span class="eyebrow">Por que escolher</span>
              <h2>Negociação clara do início ao fim</h2>
            </div>

            <div class="benefits-grid">
              <article
                  v-for="(beneficio, i) in beneficios"
                  :key="beneficio.titulo"
                  class="benefit-card"
                  data-aos="fade-up"
                  :data-aos-delay="100 * i"
              >
                <div class="benefit-icon">
                  <v-icon :icon="beneficio.icon" size="30" />
                </div>
                <h3>{{ beneficio.titulo }}</h3>
                <p>{{ beneficio.descricao }}</p>
              </article>
            </div>
          </v-container>
        </section>

        <!-- GALERIA -->
        <section id="galeria" class="section-padding gallery-section">
          <v-container>
            <div class="section-heading center" data-aos="fade-up">
              <span class="eyebrow">Catálogo visual</span>
              <h2>Catalisadores em destaque</h2>
              <p>Uma vitrine mais limpa para mostrar os modelos sem poluir a tela.</p>
            </div>

            <div class="gallery-featured" data-aos="fade-up">
              <div class="featured-copy">
                <span>Compra • Venda • Avaliação</span>
                <h3>Envie a foto do catalisador e receba uma cotação</h3>
              </div>

              <div class="featured-images">
                <img
                    v-for="item in cardsCatalisadores.slice(0, 3)"
                    :key="item.alt"
                    :src="item.img"
                    :alt="item.alt"
                />
              </div>
            </div>

            <div class="catalog-grid">
              <article
                  v-for="(item, i) in cardsCatalisadores"
                  :key="i"
                  class="catalog-card"
                  data-aos="fade-up"
                  :data-aos-delay="35 * i"
              >
                <div class="catalog-image-wrap">
                  <img :src="item.img" :alt="item.alt" />
                </div>

                <div class="catalog-info">
                  <span>{{ item.label }}</span>
                  <v-icon size="18" color="#16a34a">mdi-arrow-top-right</v-icon>
                </div>
              </article>
            </div>
          </v-container>
        </section>

        <!-- DEPOIMENTOS -->
        <section class="section-padding testimonials-section">
          <v-container>
            <div class="section-heading center light" data-aos="fade-up">
              <span class="eyebrow">Clientes</span>
              <h2>Atendimento direto e confiável</h2>
            </div>

            <div class="testimonials-grid">
              <article
                  v-for="(dep, i) in depoimentos"
                  :key="dep.nome"
                  class="testimonial-card"
                  data-aos="fade-up"
                  :data-aos-delay="120 * i"
              >
                <v-icon icon="mdi-format-quote-open" size="34" />
                <p>“{{ dep.texto }}”</p>
                <strong>{{ dep.nome }}</strong>
                <span>{{ dep.tipo }}</span>
              </article>
            </div>
          </v-container>
        </section>

        <!-- FAQ -->
        <section id="faq" class="section-padding section-soft">
          <v-container>
            <div class="faq-grid">
              <div class="section-copy" data-aos="fade-right">
                <span class="eyebrow">Dúvidas</span>
                <h2>Perguntas frequentes</h2>
                <p>Respostas curtas para facilitar a decisão do cliente.</p>

                <a :href="whatsLink" target="_blank" rel="noopener noreferrer">
                  <v-btn rounded="xl" size="large" class="btn-primary text-none mt-4" elevation="0">
                    Tirar dúvida no WhatsApp
                  </v-btn>
                </a>
              </div>

              <div data-aos="fade-left">
                <v-expansion-panels class="faq-panels" variant="accordion">
                  <v-expansion-panel v-for="item in faq" :key="item.pergunta" elevation="0">
                    <v-expansion-panel-title>{{ item.pergunta }}</v-expansion-panel-title>
                    <v-expansion-panel-text>{{ item.resposta }}</v-expansion-panel-text>
                  </v-expansion-panel>
                </v-expansion-panels>
              </div>
            </div>
          </v-container>
        </section>

        <!-- CTA FINAL -->
        <section id="contato" class="final-cta">
          <v-container>
            <div class="final-cta-card" data-aos="fade-up">
              <div>
                <span class="eyebrow">Cotação rápida</span>
                <h2>Envie a foto do catalisador e receba uma avaliação</h2>
                <p>Atendimento pelo WhatsApp para venda, compra ou consulta de modelos.</p>
              </div>

              <a :href="whatsLink" target="_blank" rel="noopener noreferrer">
                <v-btn rounded="xl" size="x-large" class="btn-primary text-none" elevation="0">
                  Chamar agora
                  <v-icon end>mdi-whatsapp</v-icon>
                </v-btn>
              </a>
            </div>
          </v-container>
        </section>
      </v-main>

      <!-- FOOTER -->
      <footer class="footer">
        <v-container class="footer-wrap">
          <div>
            <strong>Barbosa Catalisador</strong>
            <span>© {{ new Date().getFullYear() }}. Todos os direitos reservados.</span>
          </div>

          <div>
            <span>Compra e venda de catalisadores automotivos.</span>
            <span>Atendimento via WhatsApp</span>
          </div>
        </v-container>
      </footer>
    </div>
  </v-app>
</template>

<script setup>
import { computed, ref } from 'vue'

const menuAberto = ref(false)

const whatsappNumero = '5565996478524'

const mensagemBase = 'Olá! Gostaria de uma cotação para catalisador.'
const mensagemVender = 'Olá! Tenho um catalisador e gostaria de vender. Posso enviar fotos para cotação?'
const mensagemComprar = 'Olá! Gostaria de consultar catalisadores disponíveis para compra.'

const createWhatsLink = (mensagem) => `https://wa.me/${whatsappNumero}?text=${encodeURIComponent(mensagem)}`

const whatsLink = computed(() => createWhatsLink(mensagemBase))
const whatsVenderLink = computed(() => createWhatsLink(mensagemVender))
const whatsComprarLink = computed(() => createWhatsLink(mensagemComprar))

const scrollToSection = (id) => {
  const el = document.getElementById(id)
  if (!el) return
  const y = el.getBoundingClientRect().top + window.scrollY - 82
  window.scrollTo({ top: y, behavior: 'smooth' })
}

const goAndClose = (id) => {
  menuAberto.value = false
  scrollToSection(id)
}

const internetImages = {
  catMetal: 'https://images.unsplash.com/photo-1621905251918-48416bd8575a?auto=format&fit=crop&w=1400&q=85',
  oficina: 'https://img.magnific.com/fotos-gratis/trabalhador-de-servico-de-carro-muscular-reparando-o-veiculo_146671-19605.jpg?semt=ais_hybrid&w=740&q=80',
  mecanico: 'https://images.unsplash.com/photo-1625047509168-a7026f36de04?auto=format&fit=crop&w=1200&q=85',
  metalPecas: 'https://images.unsplash.com/photo-1581092160562-40aa08e78837?auto=format&fit=crop&w=1200&q=85',
  carroOficina: 'https://images.unsplash.com/photo-1487754180451-c456f719a1fc?auto=format&fit=crop&w=1200&q=85'
}

const images = {
  venderPrincipal: require('@/assets/img/catalisador-carro.jpg'),
  venderDetalhe: require('@/assets/img/catalisador-1.jpg'),
  oficina: internetImages.oficina,
  comprarPrincipal: require('@/assets/img/catalisador-pessoa.jpg')
}

const sliderCatalisadores = [
  { img: require('@/assets/img/catalisador-1.jpg'), alt: 'Catalisador automotivo usado' },
  { img: require('@/assets/img/catalisador-2.jpeg'), alt: 'Catalisador em detalhe' },
  { img: require('@/assets/img/catalisador-3.jpeg'), alt: 'Peças de catalisador' },
  { img: require('@/assets/img/catalisador-4.jpeg'), alt: 'Catalisador automotivo' },
  { img: internetImages.catMetal, alt: 'Peças metálicas automotivas' }
]

const stats = [
  { value: 'PIX', label: 'pagamento rápido' },
  { value: 'Fotos', label: 'cotação pelo WhatsApp' },
  { value: 'Lotes', label: 'peças e sucatas' }
]

const passos = [
  {
    icon: 'mdi-camera-outline',
    titulo: 'Envie fotos',
    descricao: 'Mande imagens, código da peça ou dados do veículo.'
  },
  {
    icon: 'mdi-chart-line',
    titulo: 'Receba a cotação',
    descricao: 'Avaliamos e enviamos uma proposta clara.'
  },
  {
    icon: 'mdi-cash-check',
    titulo: 'Feche com segurança',
    descricao: 'Combinamos retirada, entrega e pagamento.'
  }
]

const venderFeatures = [
  'Cotação por foto ou código',
  'Compra de peças inteiras e sucata',
  'Pagamento via PIX',
  'Atendimento para lotes e oficinas'
]

const comprarFeatures = [
  'Modelos variados',
  'Peças selecionadas',
  'Envio combinado',
  'Suporte na escolha'
]

const beneficios = [
  {
    icon: 'mdi-cash-multiple',
    titulo: 'Preço justo',
    descricao: 'Avaliação conforme tipo de peça e mercado.'
  },
  {
    icon: 'mdi-shield-check-outline',
    titulo: 'Negociação segura',
    descricao: 'Processo direto, claro e sem enrolação.'
  },
  {
    icon: 'mdi-whatsapp',
    titulo: 'Atendimento rápido',
    descricao: 'Contato fácil para cotar, comprar ou tirar dúvidas.'
  },
  {
    icon: 'mdi-truck-fast-outline',
    titulo: 'Logística facilitada',
    descricao: 'Coleta, entrega ou envio combinados caso a caso.'
  }
]

const miniProdutos = [
  { img: require('@/assets/img/cat1.png'), alt: 'Catalisador modelo 1' },
  { img: require('@/assets/img/cat2.png'), alt: 'Catalisador modelo 2' },
  { img: require('@/assets/img/cat3.png'), alt: 'Catalisador modelo 3' }
]

const cardsCatalisadores = [
  { img: require('@/assets/img/cat1.png'), label: 'Modelo automotivo', alt: 'Catalisador modelo automotivo' },
  { img: require('@/assets/img/cat2.png'), label: 'Peça usada', alt: 'Catalisador usado' },
  { img: require('@/assets/img/cat3.png'), label: 'Linha oficina', alt: 'Catalisador para oficina' },
  { img: require('@/assets/img/cat4.png'), label: 'Sucata', alt: 'Sucata de catalisador' },
  { img: require('@/assets/img/cat5.png'), label: 'Compra por lote', alt: 'Catalisador em lote' },
  { img: require('@/assets/img/cat6.png'), label: 'Modelo selecionado', alt: 'Catalisador selecionado' },
  { img: require('@/assets/img/cat7.png'), label: 'Reposição', alt: 'Catalisador para reposição' },
  { img: require('@/assets/img/cat8.png'), label: 'Avaliação', alt: 'Catalisador para avaliação' },
  { img: require('@/assets/img/cat9.png'), label: 'Estoque', alt: 'Catalisador em estoque' },
  { img: require('@/assets/img/cat10.png'), label: 'Procedência', alt: 'Catalisador com procedência' },
  { img: internetImages.metalPecas, label: 'Peças metálicas', alt: 'Peças metálicas automotivas' },
  { img: internetImages.carroOficina, label: 'Oficina', alt: 'Carro em oficina' }
]

const depoimentos = [
  {
    nome: 'João Santos',
    tipo: 'Cliente vendedor',
    texto: 'Enviei as fotos e recebi a cotação no mesmo dia. Fechamos tudo pelo WhatsApp.'
  },
  {
    nome: 'Auto Center Rodrigues',
    tipo: 'Oficina mecânica',
    texto: 'Atendimento rápido e peças com boa procedência. Facilitou muito para a oficina.'
  },
  {
    nome: 'Marcos Almeida',
    tipo: 'Revendedor',
    texto: 'Negociação clara, pagamento combinado certinho e contato direto.'
  }
]

const faq = [
  {
    pergunta: 'Vocês compram catalisador usado?',
    resposta: 'Sim. Compramos catalisadores inteiros, sucata e lotes.'
  },
  {
    pergunta: 'Como faço para cotar?',
    resposta: 'Envie fotos, código da peça ou dados do veículo pelo WhatsApp.'
  },
  {
    pergunta: 'O pagamento é via PIX?',
    resposta: 'Sim. A forma de pagamento é combinada antes do fechamento.'
  },
  {
    pergunta: 'Vocês vendem para oficinas?',
    resposta: 'Sim. Atendemos oficinas, revendedores e clientes finais.'
  }
]
</script>

<style scoped>
.site-page {
  background:
      radial-gradient(circle at top left, rgba(34, 197, 94, 0.14), transparent 32rem),
      radial-gradient(circle at top right, rgba(14, 165, 233, 0.13), transparent 30rem),
      #f8fafc;
  overflow-x: hidden;
}

.navbar {
  position: sticky;
  top: 0;
  z-index: 40;
  border-bottom: 1px solid rgba(15, 23, 42, 0.08);
  background: rgba(255, 255, 255, 0.82);
  backdrop-filter: blur(18px);
}

.nav-wrap {
  min-height: 82px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 24px;
}

.brand {
  display: flex;
  align-items: center;
}

.brand-logo {
  width: 178px;
}

.desktop-menu {
  display: flex;
  align-items: center;
  gap: 26px;
  font-size: 14px;
  font-weight: 700;
  color: #334155;
}

.desktop-menu button {
  transition: 0.22s ease;
}

.desktop-menu button:hover {
  color: #16a34a;
  transform: translateY(-1px);
}

.desktop-actions {
  display: flex;
  align-items: center;
}

.mobile-menu-button {
  display: none;
}

.mobile-menu {
  border-top: 1px solid rgba(15, 23, 42, 0.08);
  background: rgba(255, 255, 255, 0.96);
}

.mobile-menu-inner {
  display: flex;
  flex-direction: column;
  gap: 12px;
  padding-top: 18px;
  padding-bottom: 18px;
  font-weight: 700;
  color: #334155;
}

.btn-primary {
  background: linear-gradient(135deg, #16a34a, #22c55e) !important;
  color: white !important;
  box-shadow: 0 14px 34px rgba(22, 163, 74, 0.24) !important;
}

.btn-secondary {
  border-color: rgba(15, 23, 42, 0.16) !important;
  color: #0f172a !important;
  background: rgba(255, 255, 255, 0.72) !important;
}

.btn-outline {
  border-color: rgba(2, 132, 199, 0.42) !important;
  color: #0369a1 !important;
  background: rgba(255, 255, 255, 0.78) !important;
}

.hero-section {
  position: relative;
  min-height: calc(100vh - 82px);
  display: flex;
  align-items: center;
  padding: 64px 0;
}

.hero-bg-glow {
  position: absolute;
  border-radius: 999px;
  filter: blur(40px);
  pointer-events: none;
}

.hero-bg-glow-one {
  width: 340px;
  height: 340px;
  left: -120px;
  top: 140px;
  background: rgba(34, 197, 94, 0.17);
}

.hero-bg-glow-two {
  width: 360px;
  height: 360px;
  right: -130px;
  bottom: 40px;
  background: rgba(14, 165, 233, 0.15);
}

.hero-grid {
  position: relative;
  z-index: 2;
  display: grid;
  grid-template-columns: minmax(0, 0.95fr) minmax(0, 1.05fr);
  align-items: center;
  gap: 56px;
}

.hero-badge,
.eyebrow {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  width: fit-content;
  padding: 8px 14px;
  border: 1px solid rgba(22, 163, 74, 0.18);
  border-radius: 999px;
  background: rgba(240, 253, 244, 0.86);
  color: #15803d;
  font-size: 12px;
  font-weight: 900;
  letter-spacing: 0.12em;
  text-transform: uppercase;
}

.hero-copy h1 {
  margin-top: 22px;
  max-width: 680px;
  font-size: clamp(42px, 6vw, 76px);
  line-height: 0.96;
  font-weight: 950;
  letter-spacing: -0.06em;
  color: #0f172a;
}

.hero-copy h1 span {
  display: block;
  color: transparent;
  background: linear-gradient(135deg, #16a34a, #0284c7);
  background-clip: text;
  -webkit-background-clip: text;
}

.hero-subtitle {
  max-width: 560px;
  margin: 24px 0 0;
  color: #475569;
  font-size: 20px;
  line-height: 1.55;
}

.hero-actions {
  display: flex;
  flex-wrap: wrap;
  gap: 14px;
  margin-top: 34px;
}

.hero-stats {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 14px;
  margin-top: 34px;
  max-width: 590px;
}

.stat-card {
  padding: 18px;
  border: 1px solid rgba(15, 23, 42, 0.08);
  border-radius: 24px;
  background: rgba(255, 255, 255, 0.72);
  box-shadow: 0 18px 44px rgba(15, 23, 42, 0.06);
}

.stat-card strong {
  display: block;
  font-size: 24px;
  color: #0f172a;
}

.stat-card span {
  display: block;
  margin-top: 4px;
  color: #64748b;
  font-size: 13px;
  font-weight: 700;
}

.main-photo-card {
  position: relative;
  padding: 14px;
  border-radius: 38px;
  background: rgba(255, 255, 255, 0.72);
  border: 1px solid rgba(15, 23, 42, 0.08);
  box-shadow: 0 30px 90px rgba(15, 23, 42, 0.16);
}

.hero-carousel {
  border-radius: 28px;
  overflow: hidden;
}

.carousel-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.floating-card {
  position: absolute;
  display: flex;
  align-items: center;
  gap: 9px;
  padding: 12px 16px;
  border-radius: 18px;
  background: rgba(255, 255, 255, 0.9);
  border: 1px solid rgba(15, 23, 42, 0.08);
  box-shadow: 0 18px 36px rgba(15, 23, 42, 0.13);
  color: #0f172a;
  font-weight: 900;
  font-size: 13px;
}

.floating-card-top {
  top: 34px;
  left: -22px;
}

.floating-card-bottom {
  right: -20px;
  bottom: 44px;
}

.section-padding {
  padding: 92px 0;
}

.section-white {
  background: #ffffff;
}

.section-soft {
  background: linear-gradient(180deg, #f8fafc, #eef6f3);
}

.section-heading {
  max-width: 760px;
  margin-bottom: 42px;
}

.section-heading.center {
  margin-left: auto;
  margin-right: auto;
  text-align: center;
}

.section-heading h2,
.section-copy h2,
.final-cta-card h2 {
  margin-top: 14px;
  color: #0f172a;
  font-size: clamp(32px, 4vw, 52px);
  line-height: 1.05;
  font-weight: 950;
  letter-spacing: -0.045em;
}

.section-heading p,
.section-copy p,
.final-cta-card p {
  margin-top: 16px;
  color: #64748b;
  font-size: 17px;
  line-height: 1.65;
}

.steps-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 22px;
}

.step-card,
.benefit-card,
.testimonial-card {
  position: relative;
  min-height: 240px;
  padding: 28px;
  border-radius: 30px;
  background: rgba(255, 255, 255, 0.9);
  border: 1px solid rgba(15, 23, 42, 0.08);
  box-shadow: 0 20px 60px rgba(15, 23, 42, 0.06);
  transition: 0.28s ease;
}

.step-card:hover,
.benefit-card:hover,
.gallery-card:hover,
.testimonial-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 28px 70px rgba(15, 23, 42, 0.12);
}

.step-number {
  position: absolute;
  top: 22px;
  right: 24px;
  color: rgba(15, 23, 42, 0.08);
  font-size: 48px;
  font-weight: 950;
  letter-spacing: -0.06em;
}

.step-card .v-icon,
.benefit-icon {
  color: #16a34a;
}

.step-card h3,
.benefit-card h3 {
  margin-top: 22px;
  color: #0f172a;
  font-size: 21px;
  font-weight: 900;
}

.step-card p,
.benefit-card p {
  margin-top: 10px;
  color: #64748b;
  line-height: 1.6;
}

.split-grid {
  display: grid;
  grid-template-columns: minmax(0, 1fr) minmax(0, 1fr);
  gap: 64px;
  align-items: center;
}

.image-mosaic {
  position: relative;
  min-height: 570px;
}

.image-mosaic img,
.product-main-card img,
.mini-product-card img,
.gallery-card img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.mosaic-large {
  position: absolute;
  inset: 0 auto auto 0;
  width: 78%;
  height: 470px;
  border-radius: 34px;
  box-shadow: 0 28px 70px rgba(15, 23, 42, 0.18);
}

.mosaic-small {
  position: absolute;
  border: 10px solid #ffffff;
  border-radius: 28px;
  box-shadow: 0 22px 60px rgba(15, 23, 42, 0.14);
}

.mosaic-small.one {
  right: 0;
  top: 48px;
  width: 43%;
  height: 230px;
}

.mosaic-small.two {
  right: 38px;
  bottom: 0;
  width: 50%;
  height: 230px;
}

.feature-list {
  display: grid;
  gap: 14px;
  margin: 28px 0 34px;
}

.feature-list.two-columns {
  grid-template-columns: repeat(2, minmax(0, 1fr));
}

.feature-item {
  display: flex;
  align-items: center;
  gap: 11px;
  color: #334155;
  font-weight: 800;
}

.product-showcase {
  display: grid;
  gap: 16px;
}

.product-main-card {
  height: 440px;
  overflow: hidden;
  border-radius: 36px;
  background: white;
  padding: 12px;
  box-shadow: 0 26px 70px rgba(15, 23, 42, 0.14);
}

.product-main-card img {
  border-radius: 26px;
}

.mini-product-row {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 16px;
}

.mini-product-card {
  height: 138px;
  padding: 10px;
  border-radius: 24px;
  background: white;
  border: 1px solid rgba(15, 23, 42, 0.08);
  box-shadow: 0 18px 44px rgba(15, 23, 42, 0.08);
}

.mini-product-card img {
  border-radius: 16px;
}

.benefits-grid {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 22px;
}

.benefit-icon {
  width: 58px;
  height: 58px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 20px;
  background: #ecfdf5;
}

.gallery-section {
  background:
      radial-gradient(circle at top left, rgba(34, 197, 94, 0.08), transparent 28rem),
      #ffffff;
}

.gallery-featured {
  display: grid;
  grid-template-columns: 0.85fr 1.15fr;
  gap: 28px;
  align-items: center;
  margin-bottom: 28px;
  padding: clamp(24px, 4vw, 42px);
  border-radius: 36px;
  background: linear-gradient(135deg, #f0fdf4, #eff6ff);
  border: 1px solid rgba(15, 23, 42, 0.07);
  box-shadow: 0 22px 70px rgba(15, 23, 42, 0.07);
}

.featured-copy span {
  color: #16a34a;
  font-size: 12px;
  font-weight: 950;
  letter-spacing: 0.13em;
  text-transform: uppercase;
}

.featured-copy h3 {
  max-width: 520px;
  margin-top: 12px;
  color: #0f172a;
  font-size: clamp(28px, 3vw, 42px);
  line-height: 1.05;
  font-weight: 950;
  letter-spacing: -0.04em;
}

.featured-images {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 14px;
}

.featured-images img {
  width: 100%;
  height: 190px;
  object-fit: contain;
  padding: 18px;
  border-radius: 26px;
  background: rgba(255, 255, 255, 0.72);
  border: 1px solid rgba(15, 23, 42, 0.06);
}

.catalog-grid {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 18px;
}

.catalog-card {
  overflow: hidden;
  border-radius: 28px;
  background: #ffffff;
  border: 1px solid rgba(15, 23, 42, 0.08);
  box-shadow: 0 16px 46px rgba(15, 23, 42, 0.06);
  transition: 0.25s ease;
}

.catalog-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 24px 62px rgba(15, 23, 42, 0.12);
}

.catalog-image-wrap {
  height: 210px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  background: linear-gradient(180deg, #f8fafc, #eef2f7);
}

.catalog-image-wrap img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  mix-blend-mode: multiply;
}

.catalog-info {
  min-height: 62px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  padding: 16px 18px;
  color: #0f172a;
  font-size: 14px;
  font-weight: 900;
}

.testimonials-section {
  background: linear-gradient(135deg, #0f172a, #123126 55%, #0f172a);
  color: white;
}

.section-heading.light h2,
.section-heading.light p {
  color: white;
}

.testimonials-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 22px;
}

.testimonial-card {
  background: rgba(255, 255, 255, 0.1);
  border-color: rgba(255, 255, 255, 0.14);
  color: white;
  backdrop-filter: blur(16px);
}

.testimonial-card p {
  margin: 20px 0;
  color: rgba(255, 255, 255, 0.82);
  line-height: 1.7;
}

.testimonial-card strong,
.testimonial-card span {
  display: block;
}

.testimonial-card span {
  margin-top: 4px;
  color: rgba(255, 255, 255, 0.58);
  font-size: 13px;
}

.faq-grid {
  display: grid;
  grid-template-columns: 0.8fr 1.2fr;
  gap: 54px;
  align-items: start;
}

.faq-panels :deep(.v-expansion-panel) {
  margin-bottom: 12px;
  border: 1px solid rgba(15, 23, 42, 0.08);
  border-radius: 22px !important;
  overflow: hidden;
  background: #ffffff !important;
  box-shadow: 0 16px 44px rgba(15, 23, 42, 0.05);
}

.faq-panels :deep(.v-expansion-panel-title) {
  color: #0f172a;
  font-weight: 900;
  padding: 20px 22px;
}

.faq-panels :deep(.v-expansion-panel-text__wrapper) {
  color: #64748b;
  line-height: 1.65;
}

.final-cta {
  padding: 74px 0;
  background: #ffffff;
}

.final-cta-card {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 32px;
  padding: clamp(30px, 5vw, 58px);
  border-radius: 42px;
  background:
      linear-gradient(135deg, rgba(240, 253, 244, 0.96), rgba(224, 242, 254, 0.92)),
      #f8fafc;
  border: 1px solid rgba(15, 23, 42, 0.08);
  box-shadow: 0 26px 80px rgba(15, 23, 42, 0.08);
}

.final-cta-card h2 {
  max-width: 780px;
}

.footer {
  padding: 26px 0;
  border-top: 1px solid rgba(15, 23, 42, 0.08);
  background: #ffffff;
}

.footer-wrap {
  display: flex;
  justify-content: space-between;
  gap: 24px;
  color: #64748b;
  font-size: 13px;
}

.footer-wrap div {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
}

.footer-wrap strong {
  color: #0f172a;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

@media (max-width: 1100px) {
  .desktop-menu,
  .desktop-actions {
    display: none;
  }

  .mobile-menu-button {
    display: inline-flex;
  }

  .hero-grid,
  .split-grid,
  .faq-grid {
    grid-template-columns: 1fr;
  }

  .hero-section {
    padding-top: 42px;
  }

  .hero-copy h1,
  .hero-subtitle {
    max-width: 100%;
  }

  .floating-card-top {
    left: 18px;
  }

  .floating-card-bottom {
    right: 18px;
  }

  .reverse-mobile .section-copy {
    order: 2;
  }

  .reverse-mobile .product-showcase {
    order: 1;
  }

  .benefits-grid,
  .catalog-grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }

  .gallery-featured {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 760px) {
  .nav-wrap {
    min-height: 72px;
  }

  .brand-logo {
    width: 142px;
  }

  .hero-section {
    min-height: auto;
    padding: 34px 0 60px;
  }

  .hero-grid {
    gap: 38px;
  }

  .hero-actions {
    flex-direction: column;
  }

  .hero-actions a,
  .hero-actions .v-btn {
    width: 100%;
  }

  .hero-stats,
  .steps-grid,
  .testimonials-grid,
  .benefits-grid,
  .catalog-grid,
  .feature-list.two-columns {
    grid-template-columns: 1fr;
  }

  .featured-images {
    grid-template-columns: 1fr;
  }

  .featured-images img {
    height: 170px;
  }

  .main-photo-card {
    padding: 10px;
    border-radius: 28px;
  }

  .hero-carousel {
    border-radius: 20px;
  }

  .hero-carousel :deep(.v-window),
  .hero-carousel :deep(.v-carousel__item) {
    height: 390px !important;
  }

  .floating-card {
    display: none;
  }

  .section-padding {
    padding: 68px 0;
  }

  .image-mosaic {
    min-height: auto;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 14px;
  }

  .mosaic-large,
  .mosaic-small,
  .mosaic-small.one,
  .mosaic-small.two {
    position: static;
    width: 100%;
    height: 210px;
    border: 0;
    border-radius: 24px;
  }

  .mosaic-large {
    grid-column: span 2;
  }

  .product-main-card {
    height: 330px;
    border-radius: 28px;
  }

  .mini-product-row {
    gap: 10px;
  }

  .mini-product-card {
    height: 108px;
    border-radius: 18px;
    padding: 7px;
  }

  .catalog-image-wrap {
    height: 220px;
  }

  .final-cta-card,
  .footer-wrap {
    flex-direction: column;
    align-items: flex-start;
  }

  .final-cta-card a,
  .final-cta-card .v-btn {
    width: 100%;
  }
}
</style>