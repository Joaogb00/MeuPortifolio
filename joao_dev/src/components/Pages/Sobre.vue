<template>
  <section id="sobre" class="sobre-container">
    <div class="conteudo-grid anima-entrada-atrasada">
      
      <div class="coluna-foto revelar">
        <div class="foto-moldura">
          <img src="../../assets/img/diversos/eu.jpg" alt="João Gabriel" class="minha-foto">
          <div class="detalhe-decorativo"></div>
        </div>
      </div>

      <div class="coluna-texto">
        <header class="revelar">
          <span class="subtitulo">{{ modoLeigo ? 'Prazer em conhecer' : 'Quem sou eu' }}</span>
          <h2 class="titulo-secao">SOBRE MIM</h2>
          <div class="linha-accent"></div>
        </header>
        
        <div class="wrapper-transicao">
          <transition name="fade-texto" mode="out-in">
            <div :key="modoLeigo" class="texto-dinamico">
              <template v-if="!modoLeigo">
                <p class="paragrafo">
                  Olá! Sou o <strong>João Gabriel</strong>, um desenvolvedor focado em construir soluções digitais 
                  modernas e eficientes. Unindo lógica de back-end com um olhar apurado para o design no front-end.
                </p>
                <p class="paragrafo">
                  Atualmente, dedico-me ao ecossistema <strong>Full-Stack</strong>, criando sistemas escaláveis 
                  e interfaces que priorizam a experiência do usuário.
                </p>
              </template>
              
              <template v-else>
                <p class="paragrafo">
                  Olá! Eu sou o <strong>João Gabriel</strong>. Em termos simples: eu construo sites e sistemas que 
                  ajudam empresas a crescerem na internet de forma rápida e segura.
                </p>
                <p class="paragrafo">
                  Meu foco é transformar suas ideias em uma ferramenta fácil de usar que realmente traga 
                  resultados para o seu negócio.
                </p>
              </template>
            </div>
          </transition>
        </div>
        
        <div class="tags-skills revelar">
          <span v-for="skill in skillsFiltradas" :key="skill" class="tag">
            {{ skill }}
          </span>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Sobre',
  props: {
    modoLeigo: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    skillsFiltradas() {
      return this.modoLeigo 
        ? ['Sites Modernos', 'Sistemas Rápidos', 'Design Intuitivo', 'Soluções Digitais']
        : ['Vue.js', 'Node.js', 'TypeScript', 'UI/UX Design'];
    }
  },
  mounted() {
    this.initScrollReveal();
  },
  methods: {
    initScrollReveal() {
      const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) entry.target.classList.add('ativo');
        });
      }, { threshold: 0.1 });

      document.querySelectorAll('.revelar').forEach(el => observer.observe(el));
    }
  }
}
</script>

<style scoped>
.sobre-container {
  background-color: #0f0f0f;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 80px 24px;
  overflow: hidden;
}

.conteudo-grid {
  display: grid;
  grid-template-columns: 1fr 1.2fr;
  gap: clamp(40px, 8vw, 100px);
  max-width: 1200px;
  width: 100%;
}

/* Estilização da Foto */
.foto-moldura {
  position: relative;
  max-width: 380px;
  aspect-ratio: 3/4;
  margin: 0 auto;
}

.minha-foto {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 16px;
  position: relative;
  z-index: 2;
  filter: grayscale(20%);
  transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
}

.detalhe-decorativo {
  position: absolute;
  inset: 20px -20px -20px 20px;
  border: 2px solid #00cdfb;
  border-radius: 16px;
  z-index: 1;
  transition: all 0.5s ease;
}

.foto-moldura:hover .minha-foto {
  transform: translate(-10px, -10px);
  filter: grayscale(0%);
}

.foto-moldura:hover .detalhe-decorativo {
  transform: translate(10px, 10px);
}

/* Texto e Tipografia */
.coluna-texto { color: #ffffff; }

.subtitulo {
  color: #00cdfb;
  text-transform: uppercase;
  letter-spacing: 4px;
  font-size: 0.85rem;
  font-weight: 600;
}

.titulo-secao {
  font-size: clamp(2rem, 5vw, 3.5rem);
  font-weight: 900;
  margin: 10px 0;
}

.linha-accent {
  width: 60px;
  height: 4px;
  background: #00cdfb;
  margin-bottom: 2rem;
}

.paragrafo {
  color: #c0c0c0;
  line-height: 1.8;
  font-size: 1.1rem;
  margin-bottom: 1.5rem;
}

.paragrafo strong { color: #00cdfb; }

/* Tags */
.tags-skills {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  margin-top: 2rem;
}

.tag {
  padding: 8px 20px;
  border: 1px solid rgba(0, 205, 251, 0.3);
  color: #00cdfb;
  border-radius: 100px;
  font-size: 0.9rem;
  background: rgba(0, 205, 251, 0.05);
  transition: 0.3s;
}

.tag:hover {
  background: rgba(0, 205, 251, 0.2);
  border-color: #00cdfb;
}

/* Transições e Animações */
.fade-texto-enter-active, .fade-texto-leave-active {
  transition: all 0.4s ease;
}
.fade-texto-enter-from { opacity: 0; transform: translateY(10px); }
.fade-texto-leave-to { opacity: 0; transform: translateY(-10px); }

.revelar {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s ease-out;
}
.revelar.ativo {
  opacity: 1;
  transform: translateY(0);
}

@media (max-width: 900px) {
  .conteudo-grid { grid-template-columns: 1fr; gap: 60px; }
  .coluna-texto { text-align: center; }
  .linha-accent { margin: 0 auto 2rem auto; }
  .tags-skills { justify-content: center; }
}
</style>