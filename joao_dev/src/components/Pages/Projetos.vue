<template>
  <section id="projetos" class="sessao-projetos">
    <div class="container-projetos">

      <div class="cabecalho-projetos revelar">
        <h2 class="subtitulo">Meu Trabalho</h2>
        <h1 class="titulo-sessao">PROJETOS EM DESTAQUE</h1>
        <div class="linha-decorativa"></div>
      </div>

      <div class="grid-projetos">
        <div v-for="(projeto, index) in listaProjetos" :key="index" class="card-projeto revelar"
          :style="{ transitionDelay: (index * 0.1) + 's' }">

          <div class="img-container">
            <img :src="projeto.imagem" :alt="projeto.nome">
            <div class="overlay-card">
              <div class="links-projeto">
                <a :href="projeto.github" target="_blank" title="GitHub"><i class="bi bi-github"></i></a>
                <a :href="projeto.link" target="_blank" title="Ver Site"><i class="bi bi-box-arrow-up-right"></i></a>
              </div>
            </div>
          </div>

          <div class="info-projeto">
            <h3>{{ projeto.nome }}</h3>
            <p>{{ projeto.descricao }}</p>
            <div class="tech-tags">
              <span  v-for="tech in projeto.tecnologias" :key="tech">{{ tech }}</span>
            </div>
          </div>
        </div>
      </div>

    </div>
  </section>
</template>

<script>
import img1 from '@/assets/img/projetos/Porjeto-landing.png'
import img from '@/assets/img/projetos/projeto-mecanica.png'
import img3 from '@/assets/img/projetos/projeto-finance.png'
export default {
  name: 'Projetos',
  data() {
    return {
      listaProjetos: [
        {
          nome: 'Landing-Page Artista',
          descricao: 'Plataforma completa contendo detalhes do artista.',
          imagem: img1, // Substitua pelas suas imagens
          tecnologias: ['Vue.js', 'MongoDB', 'JavaScript', 'HTML', 'CSS'],
          github: 'https://github.com/Joaogb00/Duda-ascensao-Landing-Page-.git',
          link: 'https://dudaascensao.com.br/'
        },
        {
          nome: 'Sistema de Mecanica',
          descricao: 'Dashboard interativo para controle de estoque e fluxo de caixa.',
          imagem: img,
          tecnologias: ['PHP', 'JavaScript', 'HTML', 'CSS', 'MySql'],
          github: '#',
          link: '#'
        },
        {
          nome: 'App de Finanças',
          descricao: 'Aplicativo para controle financeiro pessoal com gráficos em tempo real.',
          imagem: img3,
          tecnologias: ['Vue.js', 'MongoDB', 'JavaScript', 'HTML', 'CSS'],
          github: 'https://github.com/Joaogb00/Cone-finance.git',
          link: '#'
        }
      ]
    }
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
.sessao-projetos {
  background-image:linear-gradient(to bottom, rgba(0, 0, 0, 0.145), rgba(15,15,15,1)), url("../../assets/img/fundos/F10.jpg");
  padding: 100px 20px;
  min-height: 100vh;
  color: white;
  background-size: cover;
  background-position: center;
  
}

.container-projetos {
  max-width: 1200px;
  margin: 0 auto;
}

/* --- Cabeçalho --- */
.cabecalho-projetos {
  text-align: center;
  margin-bottom: 60px;
}

.subtitulo {
  color: #00cdfb;
  letter-spacing: 4px;
  font-size: 0.9rem;
  text-transform: uppercase;
  margin-bottom: 10px;
}

.titulo-sessao {
  font-size: 3rem;
  font-weight: 900;
}

.linha-decorativa {
  width: 80px;
  height: 4px;
  background: #00cdfb;
  margin: 20px auto;
}

/* --- Grid --- */
.grid-projetos {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 30px;
}

/* --- Card do Projeto --- */
.card-projeto {
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  overflow: hidden;
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.card-projeto:hover {
  transform: translateY(-10px);
  border-color: #00cdfb;
  box-shadow: 0 10px 30px rgba(0, 205, 251, 0.1);
}

.img-container {
  position: relative;
  height: 220px;
  overflow: hidden;
}

.img-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s;
}

.card-projeto:hover .img-container img {
  transform: scale(1.1);
}

.overlay-card {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  opacity: 0;
  transition: opacity 0.3s;
}

.card-projeto:hover .overlay-card {
  opacity: 1;
}

.links-projeto {
  display: flex;
  gap: 20px;
}

.links-projeto a {
  color: white;
  font-size: 1.5rem;
  width: 50px;
  height: 50px;
  background: #00cdfb;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: 0.3s;
  text-decoration: none;
}

.links-projeto a:hover {
  transform: scale(1.2);
  background: white;
  color: #00cdfb;
}

.info-projeto {
  padding: 25px;
}

.info-projeto h3 {
  margin-bottom: 10px;
  font-size: 1.4rem;
}

.info-projeto p {
  color: #aaa;
  font-size: 0.95rem;
  line-height: 1.6;
  margin-bottom: 20px;
}

.tech-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.tech-tags span {
  background: rgba(0, 205, 251, 0.1);
  color: #00cdfb;
  padding: 4px 12px;
  border-radius: 50px;
  font-size: 0.75rem;
  font-weight: bold;
  border: 1px solid rgba(0, 205, 251, 0.2);
}

/* --- Animação de Surgimento --- */
.revelar {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s ease-out;
}

.revelar.ativo {
  opacity: 1;
  transform: translateY(0);
}

@media (max-width: 600px) {
  .titulo-sessao {
    font-size: 2rem;
  }
}
</style>