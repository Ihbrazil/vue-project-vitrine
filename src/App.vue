<script setup>
  import VitrinePage from './pages/VitrinePage.vue'
  import SacolaPage from './pages/SacolaPage.vue'

  import { provide, ref } from 'vue'

  const pagina = ref(0)
  const sacola = ref([])

  provide('sacola', sacola)

  const paginas = [
    { label: 'Vitrine', comp: VitrinePage },
    { label: 'Sacola', comp: SacolaPage }
  ]
</script>

<template>
  <div class="main menu">
    <a
      v-for="(aba, idx) in paginas"
      :key="'aba' + idx"
      @click="pagina = idx"
    >
      {{ aba.label }}
      <span v-if="idx == 1">({{ sacola.length }})</span>
    </a>
  </div>

  <div>
    <KeepAlive>
      <component :is="paginas[pagina].comp" />
    </KeepAlive>
  </div>
</template>

<style scoped>
/* ===== MENU SUPERIOR ===== */
.main.menu {
  display: flex;
  gap: 1rem;
  padding: 1rem;
  background: #ffffff;
  border-bottom: 2px solid #eee;
  box-shadow: 0 2px 8px rgba(0,0,0,0.05);
}

.main.menu a {
  cursor: pointer;
  font-weight: 600;
  padding: 0.5rem 1rem;
  border-radius: 8px;
  transition: 0.3s;
  color: #333;
}

.main.menu a:hover {
  background: #f0f0f0;
}

.main.menu span {
  font-size: 0.9rem;
  color: #007bff;
  font-weight: bold;
}


/* ===== VITRINE ===== */
.card {
  background: #fff;
  padding: 1.5rem;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.08);
  margin-bottom: 1.5rem;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 6px 18px rgba(0,0,0,0.12);
}

.card h2 {
  margin: 0;
  font-size: 1.4rem;
  color: #222;
}

.card_desc {
  margin: 0.5rem 0 1rem;
  color: #555;
  line-height: 1.4;
}

.card_footer {
  font-size: 1.2rem;
  font-weight: bold;
  color: #007bff;
  margin-bottom: 1rem;
}

.card button {
  background: #007bff;
  color: white;
  border: none;
  padding: 0.6rem 1.2rem;
  border-radius: 8px;
  font-size: 1rem;
  cursor: pointer;
  transition: 0.3s;
}

.card button:hover {
  background: #005fcc;
}


/* ===== MENSAGEM DE ALERTA ===== */
.msg_vitrine {
  background: #ffecec;
  color: #d60000;
  padding: 0.8rem 1rem;
  border-radius: 8px;
  margin-bottom: 1rem;
  border-left: 4px solid #ff4d4d;
  font-weight: 600;
}


/* ===== RESPONSIVIDADE ===== */
@media (min-width: 1024px) {
  .card {
    max-width: 600px;
  }

  .main.menu {
    justify-content: center;
  }
}
</style>
