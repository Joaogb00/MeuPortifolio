<template>
  <header class="header">
    <div class="elementos">
      <h3 class="logo"><span></span></h3>

      <nav class="box-links">
  <a href="#sobre" class="nav-link">Sobre</a>
  <a href="#projetos" class="nav-link">Projetos</a>
  <a target="_blank" href="https://wa.me/5531991890942" class="btn-hire">Contrate-me</a>
  
  <button @click="alternarModo" class="btn-tradutor" :class="{ 'ativo': modoLeigo }">
    <i class="bi" :class="modoLeigo ? 'bi-translate' : 'bi-code-slash'"></i>
    <span class="texto-btn">{{ modoLeigo ? 'Modo: Leigo' : 'Modo: Técnico' }}</span>
  </button>
</nav>
    </div>
  </header>
</template>

<script>
export default {
  // Remova o data local "modoLeigo" daqui se quiser que o Header 
  // mostre sempre o estado real que vem do pai, ou use uma prop.
  // Por enquanto, vamos apenas garantir o emit:
  data() {
    return { modoLeigo: false }
  },
  methods: {
    alternarModo() {
      this.modoLeigo = !this.modoLeigo;
      this.$emit('mudarModo', this.modoLeigo);
    }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;900&display=swap');

.header {
  height: 80px;
  position: fixed;
  top: 0;
  z-index: 1000;
  display: flex;
  align-items: center;
  width: 100%;
  background: rgba(0, 0, 0, 0.2);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
}

.elementos {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 30px;
}

.logo {
  font-size: 1.6rem;
  font-weight: 900;
  letter-spacing: -1px;
  background: linear-gradient(to right, #4a86c2, #00cdfb, #4d6ff9);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  color: transparent;
}

.logo span {
  -webkit-text-fill-color: #fff;
}

.box-links {
  display: flex;
  align-items: center;
  gap: 1.5rem;
  /* Reduzi um pouco para caber o novo botão */
}

/* ESTILO DO BOTÃO TRADUTOR */
.btn-tradutor {
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(0, 205, 251, 0.3);
  color: rgba(255, 255, 255, 0.8);
  padding: 8px 15px;
  border-radius: 50px;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 0.8rem;
  font-weight: 600;
  transition: 0.4s;
}

.btn-tradutor i {
  font-size: 1.1rem;
  color: #00cdfb;
}

.btn-tradutor:hover {
  background: rgba(0, 205, 251, 0.1);
  border-color: #00cdfb;
  color: #fff;
}

.btn-tradutor.ativo {
  background: #00cdfb;
  color: #000;
  border-color: #00cdfb;
}

.btn-tradutor.ativo i {
  color: #000;
}

/* LINKS E BOTÃO HIRE */
.nav-link {
  text-decoration: none;
  font-size: 0.95rem;
  font-weight: 500;
  color: rgba(255, 255, 255, 0.8);
  transition: 0.3s;
}

.nav-link:hover {
  color: #00cdfb;
}

.btn-hire {
  padding: 10px 22px;
  border: 1px solid #4a86c2;
  border-radius: 50px;
  text-decoration: none;
  font-size: 0.85rem;
  font-weight: 700;
  color: white;
  text-transform: uppercase;
  transition: 0.4s;
  background: rgba(74, 134, 194, 0.1);
}

.btn-hire:hover {
  background: #4a86c2;
  color: black;
  box-shadow: 0 0 20px rgba(74, 134, 194, 0.4);
}

@media (max-width: 768px) {
  .nav-link {
    display: none;
  }

  .texto-btn {
    display: none;
    /* No celular mostra apenas o ícone do tradutor */
  }

  .btn-tradutor {
    padding: 8px;
  }
}
</style>