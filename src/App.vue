<script setup lang="ts">
import { ref } from 'vue'

const itens = ref([
    {
        id: 1,
        contaOrigem: 25455,
        valorTrans: 1024.02,
        dataTransf: '27/06/2024 15:21:00'
    },
    {
        id: 2,
        contaOrigem: 25455,
        valorTrans: 1024.02,
        dataTransf: '28/06/2024 18:12:00'
    }
])
const loading = ref(false)
</script>

<template>
    <main>
        <div class="container">
            <div class="main-item">
                <div class="main-title">
                    <h1>Bem vindo ao agendamento de transferência</h1>
                </div>
            </div>
            <div class="side-item">
                <div class="side-button">
                    <button class="button-plus">Adicionar Transferência</button>
                </div>
                <div class="itens">
                    <div v-if="loading">Carregando...</div>
                    <div v-else>
                        <div v-for="item in itens" :key="item.id" class="item-detail">
                            <p style="color: black">{{ item.valorTrans }}</p>
                            <p style="color: black">{{ item.dataTransf }}</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </main>
</template>

<style scoped>
.container {
    background-color: #000;
    display: flex;
    padding: 15px;
    height: 100vh;
}
.main-item {
    flex-grow: 4;
    padding: 5px;
    background-color: rgb(176, 176, 176);
    height: 100%;
    border-radius: 15px;
    display: flex;
    justify-content: center;
}
.main-item .main-title {
    padding: 10px;
    color: #000;
    text-align: center;
    align-self: center;
}
.side-item {
    flex-grow: 1;
    padding: 15px;
    background-color: rgb(176, 176, 176);
    height: 100%;
    border-radius: 15px;
    margin-left: 1rem;
}
.side-item .side-button .button-plus {
    background-color: #1743d8;
    width: 100%;
    height: 60px;
    border-radius: 5px;
}
.side-item .item-detail {
    margin-top: 10px;
    background-color: white;
    flex-direction: row;
    display: flex;
    padding: 10px;
    justify-content: space-evenly;
    border-radius: 5px;
}
</style>
