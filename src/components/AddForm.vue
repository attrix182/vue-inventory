<script setup>

import { addDoc, collection } from 'firebase/firestore';
import { ref } from 'vue'

import { useFirestore } from 'vuefire'

const db = useFirestore()

const name = ref();
const desc = ref();



async function addItem() {
    await addDoc(collection(db, 'items'), {
        name: name.value,
        desc: desc.value
    }).then(() => {
        console.log('added')
        clearInputs();
    })
}

function clearInputs() {
    name.value = '';
    desc.value = '';
}


</script>

<template>

<v-card color="indigo-darken-3"  class="mx-auto mt-10" max-width="400">
    <v-card-title>Fill form to add item</v-card-title>
    <v-form>
        <v-container>
            <v-row>
                <v-col cols="12" md="4">
                    <v-text-field v-model="name" label="Name"></v-text-field>
                </v-col>

                <v-col cols="12" md="4">
                    <v-text-field v-model="desc" label="Desc"></v-text-field>
                </v-col>

                <v-col cols="12" md="4">
                    <v-btn  v-bind:disabled="!name || !desc"  class="add-btn" @click="addItem">
                        Add
                    </v-btn>
                </v-col>
            </v-row>
        </v-container>

    </v-form>
</v-card>
</template>

<style>
.add-btn{
    min-height: 56px;
    width: 93px;
}

</style>