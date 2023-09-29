<script setup>
    import OverviewComponent from './OverviewComponent.vue';
    import ProjectsComponent from './ProjectsComponent.vue';
</script>
<template>
    <div id="layout">
        <OverviewComponent />
        <ProjectsComponent />
    </div>
</template>
<style>

body{
    background: #444654;

}

#layout
{
    z-index: -1;
    background: #444654;
    position: relative;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
}
</style>