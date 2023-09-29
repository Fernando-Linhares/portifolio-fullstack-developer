<script setup>
import { onMounted, reactive } from 'vue';

    const data = reactive({repositories :[]});

    onMounted(async () => {
        const url = `https://api.github.com/users/Fernando-Linhares/repos`;
        let repositoriesReponse = await fetch(url).then(res => res.json());

        data.repositories = repositoriesReponse
            .map(item => {
                return {
                    id:item.id,
                    name: item.name,
                    language: item.language,
                    created_at: item.created_at
                }
            });
        
        console.log(repositoriesReponse)
    })

</script>

<template>
    <div id="projects">
        <h3>
            Projetos | Repositórios Github
        </h3>

        <div id="repos">
            <div class="repo" v-for="repo in data.repositories" :key="repo.id">
                {{ repo.name }}
            </div>
        </div>
    </div>
</template>

<style>
    #projects
    {
        position: relative;
        top: 90px;
        display: grid;
        z-index: 1;
        color: white;
        font-family: "Lucida" Grande, sans-serif;
        justify-content: center;
    }

    #repos
    {
        position: relative;
        display: grid;
        grid-template-columns: 400px 400px;
    }

    .repo
    {
        border: solid 1px white;
        margin: 5px;
        padding: 5px;
        border-radius: 4px;
    }

    .repo:hover
    {
        font-style: underline;
    }
</style>