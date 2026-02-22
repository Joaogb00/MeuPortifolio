<template>
  <Header @mudarModo="atualizarModo" />

  <section class="hero-section">
    <div class="overlay"></div>

    <div class="apresentacao anima-entrada">
      <p class="tagline">Desenvolvedor Full-Stack</p>
      <h1 class="titulo-cores">João Gabriel Pinto Matozinhos</h1>

      <div class="box-icones">
        <a href="https://github.com/Joaogb00" class="icones" target="_blank">
          <i class="bi bi-github"></i>
        </a>
        <a href="https://www.linkedin.com/in/joão-gabriel-506031260/" class="icones" target="_blank">
          <i class="bi bi-linkedin"></i>
        </a>
        <a href="https://wa.me/55319XXXXXXXX" class="icones" target="_blank">
          <i class="bi bi-whatsapp"></i>
        </a>
      </div>
    </div>
  </section>

  <div id="sobre" class="container">
    <div class="conteudo-sobre-grid anima-entrada-atrasada">
      
      <div class="coluna-foto revelar">
        <div class="foto-moldura">
          <img src="../../assets/img/diversos/eu.jpg" alt="João Gabriel" class="minha-foto">
          <div class="detalhe-moldura"></div>
        </div>
      </div>

      <div class="coluna-texto">
        <h2 class="subtitulo-apresentacao revelar">Quem sou eu</h2>
        <h1 class="titulo-sobre revelar">SOBRE MIM</h1>
        <div class="linha-decorativa revelar"></div>
        
        <transition name="fade-texto" mode="out-in">
          <div :key="modoLeigo">
            <div v-if="!modoLeigo">
              <p class="descricao-longa">
                Olá! Sou o <strong>João Gabriel</strong>, um desenvolvedor focado em construir soluções digitais 
                modernas e eficientes. Unindo lógica de back-end com um olhar apurado para o design no front-end, 
                entrego interfaces que priorizam a experiência do usuário.
              </p>
              <p class="descricao-longa">
                Atualmente, dedico-me ao ecossistema Full-Stack, explorando tecnologias que permitem criar 
                sistemas escaláveis, performáticos e visualmente impactantes.
              </p>
            </div>
            
            <div v-else>
              <p class="descricao-longa">
                Olá! Eu sou o <strong>João Gabriel</strong>. Em termos simples: eu construo sites e sistemas que 
                ajudam empresas a crescerem na internet de forma rápida, segura e bonita.
              </p>
              <p class="descricao-longa">
                Meu foco é transformar suas necessidades em uma ferramenta digital que seja fácil de usar 
                e que realmente traga resultados para o seu dia a dia.
              </p>
            </div>
          </div>
        </transition>
        
        <div class="tags-habilidades revelar">
          <span>{{ modoLeigo ? 'Sites Modernos' : 'Vue.js' }}</span>
          <span>{{ modoLeigo ? 'Sistemas Rápidos' : 'Node.js' }}</span>
          <span>{{ modoLeigo ? 'Design Intuitivo' : 'UI/UX Design' }}</span>
          <span>{{ modoLeigo ? 'Soluções Completas' : 'Full-Stack' }}</span>
        </div>
      </div>
    </div>
  </div>

  <button class="btn-topo" :class="{ 'show': mostrarBotao }" @click="voltarAoTopo">
    <i class="bi bi-arrow-up"></i>
  </button>
</template>

<script>
import Header from '../Header.vue';

export default {
  name: 'Inicio',
  components: { Header },
  data() {
    return {
      mostrarBotao: false,
      modoLeigo: false,
      observer: null
    }
  },
  methods: {
    atualizarModo(valor) {
      this.modoLeigo = valor;
    },
    handleScroll() {
      this.mostrarBotao = window.scrollY > 400;
    },
    voltarAoTopo() {
      window.scrollTo({ top: 0, behavior: 'smooth' });
    },
    initScrollReveal() {
      this.observer = new IntersectionObserver((entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            entry.target.classList.add('ativo');
          }
        });
      }, { threshold: 0.1 });

      document.querySelectorAll('.revelar').forEach((el) => this.observer.observe(el));
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll);
    this.initScrollReveal();
  },
  unmounted() {
    window.removeEventListener('scroll', this.handleScroll);
    if (this.observer) this.observer.disconnect();
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;700;900&display=swap');

:global(html) { scroll-behavior: smooth; }
:global(body) { background-color: rgb(15, 15, 15); }

/* --- NOVAS ANIMAÇÕES DE FADE-IN (Baseadas no seu modelo) --- */
.anima-entrada {
    animation: fadeInSurgir 1.5s ease-out forwards;
}

.anima-entrada-atrasada {
    animation: fadeInSurgir 2s ease-out forwards;
}

@keyframes fadeInSurgir {
    from {
        opacity: 0;
        transform: translateY(30px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

/* --- REVELAÇÃO NO SCROLL --- */
.revelar {
  opacity: 0;
  transform: translateY(40px);
  transition: opacity 1.2s ease-out, transform 1.2s ease-out;
}
.revelar.ativo {
  opacity: 1;
  transform: translateY(0);
}

/* --- HERO SECTION --- */
.hero-section {
  position: relative;
  background-color: rgb(15, 15, 15); 
  background-image: url("../../assets/img/fundos/F7.jpg");
  height: 100vh;
  background-size: cover;
  background-position: center;
  display: flex; justify-content: center; align-items: center;
}

.overlay {
  position: absolute; top: 0; left: 0; width: 100%; height: 100%;
  background: linear-gradient(to bottom, rgba(0,0,0,0.2), rgba(0,0,0,0.9));
}

.apresentacao { z-index: 2; text-align: center; }

.tagline {
  color: #00cdfb;
  text-transform: uppercase;
  letter-spacing: 5px;
  font-size: 0.9rem;
  margin-bottom: 10px;
  font-weight: bold;
}

.titulo-cores {
  font-size: clamp(2.5rem, 10vw, 5rem);
  font-weight: 900;
  background: linear-gradient(to right, #4a86c2, #00cdfb, #4d6ff9, #ffffff, #4a86c2);
  background-size: 200% auto;
  -webkit-background-clip: text; background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: brilho-suave 5s linear infinite;
}

@keyframes brilho-suave { to { background-position: 200% center; } }

.box-icones { margin-top: 35px; display: flex; justify-content: center; gap: 30px; }
.icones {
  font-size: 2.5rem; text-decoration: none;
  background: linear-gradient(to right, #4a86c2, #00cdfb);
  -webkit-background-clip: text; background-clip: text;
  -webkit-text-fill-color: transparent;
  transition: 0.4s;
}
.icones:hover { transform: translateY(-8px) scale(1.1); }

/* --- SEÇÃO SOBRE MIM --- */
.container {
  background-color: rgb(15, 15, 15);
  min-height: 100vh;
  display: flex; justify-content: center; align-items: center;
  padding: 100px 20px;
}

.conteudo-sobre-grid {
  display: grid; grid-template-columns: 1fr 1.2fr;
  gap: 80px; max-width: 1100px; width: 100%; align-items: center;
}

/* Moldura e Foto interativas */
.foto-moldura { position: relative; width: 100%; max-width: 350px; height: 450px; margin: 0 auto; }
.minha-foto { 
  width: 100%; height: 100%; object-fit: cover; border-radius: 20px; z-index: 2; 
  position: relative; border: 1px solid rgba(255,255,255,0.1);
  transition: transform 0.5s ease, box-shadow 0.5s ease;
}
.detalhe-moldura {
  position: absolute; top: 20px; left: 20px; right: -20px; bottom: -20px;
  border: 2px solid #00cdfb; border-radius: 20px; z-index: 1; transition: all 0.5s ease;
}

.foto-moldura:hover .minha-foto { transform: translate(-10px, -10px); box-shadow: 15px 15px 30px rgba(0, 0, 0, 0.5); }
.foto-moldura:hover .detalhe-moldura { transform: translate(10px, 10px); background: rgba(0, 205, 251, 0.05); }

.coluna-texto { color: white; text-align: left; }
.titulo-sobre { font-size: 3rem; font-weight: 900; margin-bottom: 15px; }
.subtitulo-apresentacao { color: #00cdfb; letter-spacing: 4px; font-size: 0.9rem; text-transform: uppercase; }
.linha-decorativa { width: 80px; height: 4px; background: #00cdfb; margin-bottom: 30px; }
.descricao-longa { color: #b0b0b0; line-height: 1.8; font-size: 1.1rem; margin-bottom: 20px; }
.descricao-longa strong { color: #00cdfb; }

.tags-habilidades { display: flex; flex-wrap: wrap; gap: 12px; margin-top: 30px; }
.tags-habilidades span { border: 1px solid #00cdfb; color: #00cdfb; padding: 6px 18px; border-radius: 50px; font-size: 0.85rem; }

/* Botão Topo */
.btn-topo {
  position: fixed; bottom: 30px; right: 30px; width: 50px; height: 50px; border-radius: 50%;
  background: linear-gradient(45deg, #4a86c2, #00cdfb); color: white; border: none; cursor: pointer; z-index: 2000;
  display: flex; align-items: center; justify-content: center; opacity: 0; visibility: hidden; transform: translateY(20px); transition: all 0.4s;
}
.btn-topo.show { opacity: 1; visibility: visible; transform: translateY(0); }

@media (max-width: 900px) {
  .conteudo-sobre-grid { grid-template-columns: 1fr; text-align: center; }
  .coluna-texto { text-align: center; }
  .linha-decorativa { margin: 0 auto 30px auto; }
  .tags-habilidades { justify-content: center; }
}

/* Transição de texto modo leigo */
.fade-texto-enter-active, .fade-texto-leave-active { transition: all 0.5s ease; }
.fade-texto-enter-from { opacity: 0; transform: translateX(20px); }
.fade-texto-leave-to { opacity: 0; transform: translateX(-20px); }
</style>