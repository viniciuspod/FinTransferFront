<script setup lang="ts">
import axios, { type AxiosRequestConfig } from 'axios'
import { onMounted, ref } from 'vue'

const itens = ref()

const getAllTransf = async () => {
    const response = await axios.get(
        'http://localhost:8080/FinTransferApi/api/transferencia/get/all'
    )
    return response.data
}

const startComponent = async () => {
    itens.value = await getAllTransf()
    console.log(itens.value)
}

const alterStatusScreen = () => {
    showItem.value = !showItem.value
}

onMounted(() => {
    startComponent()
})

const loading = ref(false)
const showItem = ref(false)
</script>

<template>
    <main>
        <div class="container">
            <div class="main-item">
                <div v-if="!showItem" class="main-title">
                    <h1>Bem vindo ao agendamento de transferência</h1>
                </div>
                <div v-else>
                    <div style="width: 20px; height: 20px; background-color: blueviolet"></div>
                </div>
            </div>
            <div class="side-item">
                <div class="side-button">
                    <button @click="alterStatusScreen()" class="button-plus">
                        Adicionar Transferência
                    </button>
                </div>
                <div class="itens">
                    <div v-for="item in itens" :key="item.id" class="item-detail">
                        <div class="contaOri">
                            <p style="color: black; font-weight: bold">Conta Origem</p>
                            <p style="color: black">{{ item.contaOrigem }}</p>
                        </div>
                        <div class="contaDest">
                            <p style="color: black; font-weight: bold">Conta Destino</p>
                            <p style="color: black">{{ item.contaDestino }}</p>
                        </div>
                        <div class="dtAgenda">
                            <p style="color: black; font-weight: bold">Data Agendamento</p>
                            <p style="color: black">{{ item.dtAgendamento }}</p>
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
    font-size: 10px;
    text-align: center;
}
.itens {
    overflow-y: auto;
    max-height: 90%;
    margin-top: 10px;
}
</style>
