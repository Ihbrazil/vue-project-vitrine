<script setup>
    import { inject } from 'vue'
    const emit = defineEmits(['send-msg'])

    defineProps(['produto'])
    const sacola = inject('sacola', [])

    const addSacola = (item) => {
    if (!sacola.value.includes(item)) {
        sacola.value.push(item)
    } else {
        emit('send-msg')
    }
}
</script>

<template>
  <section>
    <h2>{{ produto.name }}</h2>
    <p class="card_desc">{{ produto.description }}</p>
    <p class="card_footer">R$ {{ produto.price.toFixed(2) }}</p>
    <button @click="() => addSacola(produto)">Add</button>
  </section>
</template>
