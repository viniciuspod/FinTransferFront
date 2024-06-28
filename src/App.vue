<script setup lang="ts">
import axios, { type AxiosRequestConfig } from 'axios'
import { onMounted, ref } from 'vue'

const itens = ref()
const contaOrigem = ref('')
const contaDestino = ref('')
const valor = ref('')
const dtAgendamento = ref('')

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

const postForm = async () => {
    try {
        const formData = {
            contaOrigem: contaOrigem.value,
            contaDestino: contaDestino.value,
            valor: valor.value,
            dataAgendamento: dtAgendamento.value
        }

        console.log(formData)

        const response = await axios.post(
            'http://localhost:8080/FinTransferApi/api/transferencia/save',
            formData
        )
        showItem.value = !showItem.value
        window.location.reload()
    } catch (error: any) {
        alert(error.response.data.message)
        console.error('Erro ao enviar formulário:', error)
    }
}

const alterStatusScreen = () => {
    showItem.value = !showItem.value
}

onMounted(() => {
    startComponent()
})

const showItem = ref(false)
</script>

<template>
    <main>
        <div class="container">
            <div class="main-item">
                <div v-if="!showItem" class="main-title">
                    <h1>Bem vindo ao agendamento de transferência</h1>
                </div>
                <div v-else class="main-form">
                    <div class="form-item">
                        <p style="color: black; font-weight: bold">Conta Origem</p>
                        <input
                            type="text"
                            v-model="contaOrigem"
                            placeholder="Digite a conta origem"
                            class="form-input"
                        />
                    </div>
                    <div class="form-item">
                        <p style="color: black; font-weight: bold">Conta Destino</p>
                        <input
                            type="text"
                            v-model="contaDestino"
                            placeholder="Digite a conta destino"
                            class="form-input"
                        />
                    </div>
                    <div class="form-item">
                        <p style="color: black; font-weight: bold">Valor</p>
                        <input
                            type="number"
                            v-model="valor"
                            placeholder="Digite o valor"
                            class="form-input"
                        />
                    </div>
                    <div class="form-item">
                        <p style="color: black; font-weight: bold">Data Agendamento</p>
                        <input
                            type="datetime-local"
                            v-model="dtAgendamento"
                            placeholder="Digite a data de agendamento"
                            class="form-input"
                        />
                    </div>
                    <div @click="postForm" class="form-button">
                        <button class="button-add">Confirmar</button>
                    </div>
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
    width: 70%;
    height: 100%;
    padding: 5px;
    background-color: rgb(176, 176, 176);
    overflow: hidden;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}
.main-item .main-title {
    color: #000;
    text-align: center;
    align-self: center;
}
.main-item .main-form {
    width: 100%;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-around;
    margin-top: 50px;
}
.main-item .main-form .form-item {
    height: 50px;
    width: 24%;
    background-color: #fff;
    border-radius: 5px;
    padding-left: 5px;
    margin-bottom: 15px;
    flex-basis: 24%;
    flex-grow: 1;
    flex-shrink: 1;
    margin: 5px;
}
@media (max-width: 1200px) {
    .main-item .main-form .form-item {
        width: 48%;
        flex-basis: 48%;
    }
}
@media (max-width: 768px) {
    .main-item .main-form .form-item {
        width: 100%;
        flex-basis: 100%;
    }
}
.main-item .main-form .form-item .form-input {
    border: none;
    outline: none;
    font-size: 16px;
    height: auto;
    width: auto;
    box-sizing: border-box;
}
.main-item .main-form .form-button {
    width: 10%;
    height: 50px;
    margin: 10px;
    flex-basis: 10%;
}
.main-item .main-form .form-button .button-add {
    background-color: #1743d8;
    width: 100%;
    height: 100%;
    border-radius: 5px;
    box-sizing: border-box;
    cursor: pointer;
    color: #cad6fc;
}

.main-item .main-form .form-button .button-add:hover {
    color: #cad6fc;
    background-color: #05289c;
}

@media (max-width: 768px) {
    .main-item .main-form .form-button {
        width: 100%;
        flex-basis: 100%;
    }
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
    cursor: pointer;
    color: #cad6fc;
}

.side-item .side-button .button-plus:hover {
    color: #cad6fc;
    background-color: #05289c;
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
