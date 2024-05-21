<script setup lang="ts">

import { deleteDoc, doc } from 'firebase/firestore';

import { useFirestore } from 'vuefire'
const db = useFirestore()


export interface ItemModel {
  name: string;
  desc: string;
  id:string;
}

const props = defineProps<{ item: ItemModel }>()

async function deleteItem(){
  await deleteDoc(doc(db, 'items', props.item.id))
}



</script>

<template>
  <v-card  color="indigo-darken-3" class="mx-auto" prepend-icon="" subtitle="" width="400">
    <template v-slot:title>
      <span class="font-weight-black">{{ item.name }}</span>
    </template>

    <v-card-text class="bg-surface-light pt-4">
      {{ item.desc }}
    </v-card-text>

    <v-card-actions class="justify-end">
      <v-btn @click="deleteItem" color="error" variant="outlined">Delete</v-btn>
    </v-card-actions>
  </v-card>

</template>

<style scoped></style>
