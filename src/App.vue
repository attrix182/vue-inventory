<script setup>
import { useCollection } from 'vuefire'
import { collection } from 'firebase/firestore'
import ItemCard from './components/ItemCard.vue'
import AddForm from './components/AddForm.vue'

import { useFirestore } from 'vuefire'

const db = useFirestore()

const items = useCollection(collection(db, 'items'))


</script>

<template>


  <AddForm />
  
  <div>
    <div class="d-flex justify-center align-center mt-5" v-for="item in items" :key="item.id">
      <ItemCard :item="item" />
    </div>

  </div>

</template>

<style scoped></style>
