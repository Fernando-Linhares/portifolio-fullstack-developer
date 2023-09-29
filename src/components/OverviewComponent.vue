<script setup>

import image from '@/assets/perfil.png';
import ShieldsComponent from './ShieldsComponent.vue';
import { onMounted, reactive } from 'vue';

let title = 'Desenvolvedor Fullstack | Fernando Linhares';

let description = `Desenvolvedor de software com mais de 5 anos em sistemas e integrações de software.
                Com muita experiência em sistemas de messageria e fila assíncrona de alta carga de dados. `;

const data = reactive({
    shields: {
        visible: false
    },
    cursor:{
        visible: false
    },
    overview: {
        title: '',
        description: ''
    }
});

function waitFor(ms) {
    return new Promise((resolve, reject) => {
        try
        {
            setTimeout(() => resolve(), ms);

        } catch (error) {
            reject(error);
        }
    })
}

const active_cursor = (id) => setInterval(() => {

    let cursor = document.querySelectorAll('span.cursor')[id - 1];

    if(data.cursor.active) {
        cursor.style.display = 'inline';

    } else {
        cursor.style.display = 'none';
    }

    data.cursor.active = !data.cursor.active;
}, 500);

const desactive_cursor = (cursorId, intervalId) => {

    let cursor = document.querySelectorAll('span.cursor')[cursorId - 1];

    cursor.style.display = 'none'

    data.cursor.active = false;

    clearInterval(intervalId);
}

onMounted(async () => {
    let idt, idc;

    idc = 1;
    idt = active_cursor(idc);

    for(let ctitle of title.split('')){
        data.overview.title += ctitle
    }
    data.shields.visible = true;

    desactive_cursor(idc, idt)

    idc = 2;
    idt = active_cursor(idc);

    for(let cdescription of description.split('')){
        await waitFor(30);
        data.overview.description += cdescription
    }

    desactive_cursor(idc, idt)

    data.shields.visible = true;
})

</script>
<template>
    <div id="overview">
        <div id="overview-name">
            <h3>
                {{ data.overview.title }} <span class="cursor">|</span>
            </h3>
            <div class="description">
                {{ data.overview.description }}
                <span class="cursor">|</span>
            </div>
            <ShieldsComponent v-show="data.shields.visible"/>
        </div>
        <div id="overview-image">
            <img :src="image" alt="perfil"/>
        </div>
    </div>
</template>
<style>

    #overview
    {
        position: relative;
        top: 50px;
        display: grid;
        z-index: 1;
        color: white;
        grid-template-columns: 40% 10%;
        font-family: "Lucida" Grande, sans-serif;
        justify-content: center;
    }

    #overview-name
    {
        text-align: center;
    }

    .description
    {
        color: rgba(240, 248, 255, 0.726);
    }

    #overview-name > h3
    {
        font-weight: bold;
    }

    #overview-image > img
    {
        width: 250px;
        border-radius: 100%;
    }

    .cursor
    {
        display: none;
        font-weight: 1900;
        font-size: 20px;
        color: wheat;
    }
   
</style>