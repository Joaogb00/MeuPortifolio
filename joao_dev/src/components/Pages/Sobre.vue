<template>
  <div id="sobre" class="container">
    <div class="conteudo-sobre-grid anima-entrada-atrasada">
      
      <div class="coluna-foto revelar">
        <div class="foto-moldura">
          <img src="../assets/img/diversos/eu.jpg" alt="João Gabriel" class="minha-foto">
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
</template>

<script>
export default {
  name: 'Sobre',
  props: {
    modoLeigo: Boolean
  },
  mounted() {
    this.initScrollReveal();
  },
  methods: {
    initScrollReveal() {
      const observer = new IntersectionObserver((entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            entry.target.classList.add('ativo');
          }
        });
      }, { threshold: 0.1 });

      document.querySelectorAll('.revelar').forEach((el) => observer.observe(el));
    }
  }
}
</script>

<style scoped>
/* Estilos específicos da seção Sobre */
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

/* Animações de Scroll */
.revelar {
  opacity: 0;
  transform: translateY(40px);
  transition: opacity 1.2s ease-out, transform 1.2s ease-out;
}
.revelar.ativo {
  opacity: 1;
  transform: translateY(0);
}

/* Animação Inicial Subindo */
.anima-entrada-atrasada {
  animation: fadeInSurgir 2s ease-out forwards;
}

@keyframes fadeInSurgir {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
}

/* Transição de texto modo leigo */
.fade-texto-enter-active, .fade-texto-leave-active { transition: all 0.5s ease; }
.fade-texto-enter-from { opacity: 0; transform: translateX(20px); }
.fade-texto-leave-to { opacity: 0; transform: translateX(-20px); }

@media (max-width: 900px) {
  .conteudo-sobre-grid { grid-template-columns: 1fr; text-align: center; }
  .coluna-texto { text-align: center; }
  .linha-decorativa { margin: 0 auto 30px auto; }
  .tags-habilidades { justify-content: center; }
}
</style>