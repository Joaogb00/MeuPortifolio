<template>
  <div>
    <Header @mudarModo="atualizarModo" />

    <section class="hero-section">
      <div class="overlay"></div>

      <div class="apresentacao anima-entrada">
        <p class="tagline">Desenvolvedor Full-Stack</p>
        <h1 class="titulo-cores">João Gabriel</h1>

        <div class="box-icones">
          <a href="https://github.com/Joaogb00" class="icones" target="_blank">
            <i class="bi bi-github"></i>
          </a>
          <a href="https://www.linkedin.com/in/joão-gabriel-506031260/" class="icones" target="_blank">
            <i class="bi bi-linkedin"></i>
          </a>
          <a href="https://wa.me/5531991890942" class="icones" target="_blank">
            <i class="bi bi-whatsapp"></i>
          </a>
        </div>
      </div>
    </section>

  

 <Sobre :modoLeigo="modoLeigo" /> 
<Projetos/>
    <button 
      class="btn-topo" 
      :class="{ 'show': mostrarBotao }" 
      @click="voltarAoTopo"
      aria-label="Voltar ao topo"
    >
      <i class="bi bi-arrow-up"></i>
    </button>
  </div>
</template>

<script>
import Header from '../Header.vue';
import Projetos from './Projetos.vue';

import Sobre from './Sobre.vue';

export default {
  name: 'Inicio',
  components: { Header,Sobre,Projetos },
  data() {
    return {
      mostrarBotao: false,
      modoLeigo: false
    }
  },
  methods: {
    atualizarModo(valor) { this.modoLeigo = valor; },
    voltarAoTopo() { window.scrollTo({ top: 0, behavior: 'smooth' }); },
    handleScroll() { this.mostrarBotao = window.scrollY > 400; }
  },
  mounted() { window.addEventListener('scroll', this.handleScroll); },
  unmounted() { window.removeEventListener('scroll', this.handleScroll); }
}
</script>

<style scoped>
/* --- CONFIGURAÇÕES GERAIS --- */
:global(html) {
  scroll-behavior: smooth;
}

/* --- ANIMAÇÕES DE ENTRADA --- */
.anima-entrada {
  animation: fadeInSurgir 1.2s ease-out forwards;
}

.anima-entrada-atrasada {
  animation: fadeInSurgir 1.6s ease-out forwards;
}

@keyframes fadeInSurgir {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
}

/* --- REVELAÇÃO NO SCROLL --- */
.revelar {
  opacity: 0;
  transform: translateY(40px);
  transition: opacity 1s ease-out, transform 1s ease-out;
}

.revelar.ativo {
  opacity: 1;
  transform: translateY(0);
}

/* --- HERO SECTION --- */
.hero-section {
  position: relative;
  background-color: #0f0f0f;
  background-image: url("../../assets/img/fundos/F7.jpg");
  height: 100vh;
  background-size: cover;
  background-position: center;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
}

.overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(to bottom, rgba(0,0,0,0.3), rgba(15,15,15,1));
}

.apresentacao {
  z-index: 2;
  text-align: center;
}

.tagline {
  color: #00cdfb;
  text-transform: uppercase;
  letter-spacing: 5px;
  font-size: 0.85rem;
  margin-bottom: 10px;
  font-weight: 700;
}

.titulo-cores {
  font-size: clamp(2.5rem, 8vw, 5rem);
  font-weight: 900;
  background: linear-gradient(to right, #4a86c2, #00cdfb, #ffffff, #00cdfb, #4a86c2);
  background-size: 200% auto;
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: brilho-suave 6s linear infinite;
}

@keyframes brilho-suave {
  to { background-position: 200% center; }
}

.box-icones {
  margin-top: 30px;
  display: flex;
  justify-content: center;
  gap: 25px;
}

.icones {
  font-size: 2.2rem;
  color: #00cdfb;
  transition: 0.3s ease;
}

.icones:hover {
  transform: translateY(-5px) scale(1.1);
  color: #ffffff;
}

/* --- SEÇÃO SOBRE --- */
.container {
  background-color: #0f0f0f;
  min-height: 80vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 80px 24px;
}

.conteudo-sobre-grid {
  display: grid;
  grid-template-columns: 1fr 1.2fr;
  gap: 60px;
  max-width: 1100px;
  width: 100%;
}

.foto-moldura {
  position: relative;
  width: 100%;
  max-width: 320px;
  aspect-ratio: 3/4;
  margin: 0 auto;
}

.minha-foto {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 16px;
  z-index: 2;
  position: relative;
  filter: grayscale(20%);
  transition: 0.5s ease;
}

.detalhe-moldura {
  position: absolute;
  inset: 15px -15px -15px 15px;
  border: 2px solid #00cdfb;
  border-radius: 16px;
  z-index: 1;
  transition: 0.5s ease;
}

.foto-moldura:hover .minha-foto {
  transform: translate(-8px, -8px);
  filter: grayscale(0%);
}

.foto-moldura:hover .detalhe-moldura {
  transform: translate(8px, 8px);
}

.coluna-texto {
  color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.titulo-sobre {
  font-size: clamp(2rem, 5vw, 3rem);
  font-weight: 900;
  margin-bottom: 15px;
}

.subtitulo-apresentacao {
  color: #00cdfb;
  letter-spacing: 3px;
  font-size: 0.8rem;
  text-transform: uppercase;
  margin-bottom: 5px;
}

.linha-decorativa {
  width: 60px;
  height: 4px;
  background: #00cdfb;
  margin-bottom: 25px;
}

.descricao-longa {
  color: #cccccc;
  line-height: 1.7;
  font-size: 1.05rem;
  margin-bottom: 15px;
}

:deep(.descricao-longa strong) {
  color: #00cdfb;
  font-weight: 600;
}

.tags-habilidades {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-top: 20px;
}

.tags-habilidades span {
  border: 1px solid rgba(0, 205, 251, 0.4);
  color: #00cdfb;
  padding: 5px 15px;
  border-radius: 30px;
  font-size: 0.8rem;
  background: rgba(0, 205, 251, 0.05);
  transition: 0.3s;
}

.tags-habilidades span:hover {
  background: #00cdfb;
  color: #000;
}

/* BOTÃO VOLTAR AO TOPO */
.btn-topo {
  position: fixed;
  bottom: 30px;
  right: 30px;
  width: 45px;
  height: 45px;
  border-radius: 50%;
  background: #00cdfb;
  color: #000;
  border: none;
  cursor: pointer;
  z-index: 99;
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  visibility: hidden;
  transition: 0.4s;
  box-shadow: 0 4px 15px rgba(0, 205, 251, 0.3);
}

.btn-topo.show {
  opacity: 1;
  visibility: visible;
}

/* TRANSIÇÕES DE TEXTO */
.fade-texto-enter-active, .fade-texto-leave-active {
  transition: all 0.4s ease;
}
.fade-texto-enter-from { opacity: 0; transform: translateY(10px); }
.fade-texto-leave-to { opacity: 0; transform: translateY(-10px); }

/* RESPONSIVIDADE */
@media (max-width: 900px) {
  .conteudo-sobre-grid {
    grid-template-columns: 1fr;
    text-align: center;
    gap: 40px;
  }
  .coluna-texto { align-items: center; }
  .linha-decorativa { margin: 0 auto 25px auto; }
  .tags-habilidades { justify-content: center; }
}
</style>