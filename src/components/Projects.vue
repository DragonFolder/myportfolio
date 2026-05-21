<template>
    <section class="py-5" id="projects">
        <div class="d-flex flex-column flex-md-row justify-content-between align-items-md-end mb-5 gap-3">
            <div>
                <p class="section-eyebrow mb-1">Selected Works</p>
                <h2 class="section-title fs-1 mb-0">Project Gallery</h2>
            </div>
        </div>
        <!-- Bento Grid -->
        <div class="bento-grid">
            <ProjectCard
                v-for="project in projects"
                :key="project.id"
                :project="project"
            />
        </div>
    </section>
</template>

<script setup>
    import ProjectCard from './ProjectCard.vue';
    import projects from '../data/projects.json';
</script>