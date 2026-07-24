<script setup>
    import { computed, inject } from 'vue'

    const sacola = inject('sacola')

    const totalSacola = computed(() => {
    return sacola.value.reduce(
        (acc, item) => acc + (item.available * item.price),
        0
    )
    })
</script>

<template>
  <h1>Sacola</h1>

  <table>
    <tr>
      <th>Produto</th>
      <th>Preço</th>
      <th>Quant.</th>
    </tr>

    <tr v-for="(item, idx) in sacola" :key="'item_' + idx">
      <td>{{ item.name }}</td>
      <td>{{ item.price }}</td>
      <td>{{ item.available }}</td>
    </tr>

    <tr>
      <td colspan="3">Total: R$ {{ totalSacola.toFixed(2) }}</td>
    </tr>
  </table>
</template>