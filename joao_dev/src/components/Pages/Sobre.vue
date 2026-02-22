<template>
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
                                <strong>João Gabriel</strong>
                                Este e a linguagem Profissional
                            </p>
                            <p class="descricao-longa">
                                Descrição
                            </p>
                        </div>

                        <div v-else>
                            <p class="descricao-longa">
                                 Eu sou o <strong>João Gabriel</strong>. Em termos simples: eu construo sites teste1 Teste1
                            </p>
                            <p class="descricao-longa">
                                descrição
                            </p>
                        </div>
                    </div>
                </transition>

                <div class="tags-habilidades revelar">
                    <span class="rotulo">{{ modoLeigo ? 'Sites Modernos' : 'Vue.js' }}</span>
                    <span class="rotulo">{{ modoLeigo ? 'Sistemas Rápidos' : 'Node.js' }}</span>
                    <span class="rotulo">{{ modoLeigo ? 'Design Intuitivo' : 'UI/UX Design' }}</span>
                    <span class="rotulo">{{ modoLeigo ? 'Soluções Completas' : 'Full-Stack' }}</span>
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
    data() {
        return {
            observer: null
        }
    },
    methods: {
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
        this.initScrollReveal();
    },
    beforeUnmount() {
        if (this.observer) this.observer.disconnect();
    }
}
</script>

<style scoped>
/* --- CONTAINER PRINCIPAL --- */
.container {
  background-color: rgb(15, 15, 15);
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 100px 20px;
  overflow: hidden;
}

.conteudo-sobre-grid {
  display: grid;
  grid-template-columns: 1fr 1.2fr;
  gap: 80px;
  max-width: 1100px;
  width: 100%;
  align-items: center;
}

/* --- LOGICA DE REVELAÇÃO (FADE-IN NO SCROLL) --- */
.revelar {
  opacity: 0;
  transform: translateY(40px);
  transition: opacity 1.2s ease-out, transform 1.2s ease-out;
  will-change: opacity, transform;
}

.revelar.ativo {
  opacity: 1;
  transform: translateY(0);
}

/* --- FOTO E MOLDURA --- */
.foto-moldura {
  position: relative;
  width: 100%;
  max-width: 350px;
  height: 450px;
  margin: 0 auto;
}

.minha-foto {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 20px;
  z-index: 2;
  position: relative;
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: transform 0.5s ease;
}

.detalhe-moldura {
  position: absolute;
  top: 20px; left: 20px; right: -20px; bottom: -20px;
  border: 2px solid #00cdfb;
  border-radius: 20px;
  z-index: 1;
  transition: all 0.5s ease;
}

.foto-moldura:hover .minha-foto {
  transform: translate(-10px, -10px);
  box-shadow: 15px 15px 30px rgba(0, 0, 0, 0.5);
}

.foto-moldura:hover .detalhe-moldura {
  transform: translate(10px, 10px);
  background: rgba(0, 205, 251, 0.05);
}

/* --- TEXTOS --- */
.coluna-texto {
  color: white;
  text-align: left;
}

.titulo-sobre {
  font-size: 3rem;
  font-weight: 900;
  margin-bottom: 15px;
}

.subtitulo-apresentacao {
  color: #00cdfb;
  letter-spacing: 4px;
  font-size: 0.9rem;
  text-transform: uppercase;
}

.linha-decorativa {
  width: 80px;
  height: 4px;
  background: #00cdfb;
  margin-bottom: 30px;
}

.descricao-longa {
  color: #b0b0b0;
  line-height: 1.8;
  font-size: 1.1rem;
  margin-bottom: 20px;
}

.descricao-longa strong {
  color: #00cdfb;
}

/* --- TAGS / HABILIDADES --- */
.tags-habilidades {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  margin-top: 30px;
}

.rotulo {
  border: 1px solid #00cdfb;
  color: #00cdfb;
  padding: 6px 18px;
  border-radius: 50px;
  font-size: 0.85rem;
  transition: all 0.4s ease;
  cursor: default;
}

.rotulo:hover {
  background-color: #00cdfb;
  color: black;
  transform: scale(1.05);
}

/* --- TRANSIÇÃO DE TROCA DE MODO (FADE LATERAL) --- */
.fade-texto-enter-active,
.fade-texto-leave-active {
  transition: all 0.5s ease;
}

.fade-texto-enter-from {
  opacity: 0;
  transform: translateX(20px);
}

.fade-texto-leave-to {
  opacity: 0;
  transform: translateX(-20px);
}

/* --- RESPONSIVIDADE --- */
@media (max-width: 900px) {
  .conteudo-sobre-grid {
    grid-template-columns: 1fr;
    text-align: center;
    gap: 50px;
  }

  .coluna-texto {
    text-align: center;
  }

  .linha-decorativa {
    margin: 0 auto 30px auto;
  }

  .tags-habilidades {
    justify-content: center;
  }
  
  .foto-moldura {
    max-width: 280px;
    height: 380px;
  }
}
</style>