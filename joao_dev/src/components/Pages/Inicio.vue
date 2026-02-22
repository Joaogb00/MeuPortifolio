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

<Sobre :modoLeigo="modoLeigo" />
  
  <Projetos/>

  <button class="btn-topo" :class="{ 'show': mostrarBotao }" @click="voltarAoTopo">
    <i class="bi bi-arrow-up"></i>
  </button>
</template>

<script>
import Header from '../Header.vue';
import Projetos from './Projetos.vue';
import Sobre from './Sobre.vue'; 

export default {
  name: 'Inicio',
  components: { Header, Sobre, Projetos },
  data() {
    return {
      mostrarBotao: false,
      modoLeigo: false
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
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll);
  },
  unmounted() {
    window.removeEventListener('scroll', this.handleScroll);
  }
}
</script>

<style scoped>

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

.anima-entrada {
    animation: fadeInSurgir 1.5s ease-out forwards;
}

@keyframes fadeInSurgir {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
}




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
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: brilho-suave 5s linear infinite;
}

@keyframes brilho-suave {
  to {
    background-position: 200% center;
  }
}

.box-icones {
  margin-top: 35px;
  display: flex;
  justify-content: center;
  gap: 30px;
}

.icones {
  font-size: 2.5rem;
  text-decoration: none;
  background: linear-gradient(to right, #4a86c2, #00cdfb);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  transition: 0.4s;
}

.icones:hover {
  transform: translateY(-8px) scale(1.1);
}




/* Botão Topo */
.btn-topo {
  position: fixed;
  bottom: 30px;
  right: 30px;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background: linear-gradient(45deg, #4a86c2, #00cdfb);
  color: white;
  border: none;
  cursor: pointer;
  z-index: 2000;
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  visibility: hidden;
  transform: translateY(20px);
  transition: all 0.4s;
}

.btn-topo.show {
  opacity: 1;
  visibility: visible;
  transform: translateY(0);
}

@media (max-width: 900px) {
  .conteudo-sobre-grid {
    grid-template-columns: 1fr;
    text-align: center;
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
}

/* Transição de texto modo leigo */
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
.projetos{
  background-color: rgba(23, 23, 23, 0.886);
  height: 100vh;
}
</style>