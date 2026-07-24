<script setup>
    import { ref, watch } from 'vue'
    import CardProduto from '../components/CardProduto.vue'

    let produtos = ref([])
    const msg = ref(null)

    fetch('/dados.json')
    .then(resp => resp.json())
    .then(data => produtos.value = data)
    .catch(err => msg.value = err)

    const sendMsg = () => {
    msg.value = "Produto já adicionado."
    }

    watch(msg, (newMsg) => {
    if (newMsg) setTimeout(() => msg.value = null, 2000)
    })
</script>

<template>
  <h1>Vitrine ({{ produtos.length }})</h1>

  <p class="msg_vitrine" v-if="msg">{{ msg }}</p>

  <CardProduto
    v-for="(prod, idx) in produtos"
    :key="'prod_vitrine_' + idx"
    :produto="prod"
    @send-msg="sendMsg"
  />
</template>
