<template>
    <section class="py-5" id="tools">
        <div class="d-flex flex-column align-items-center mb-5">
            <h2 class="section-title ink-bleed fs-1 mb-3 text-center">Technical Toolbox</h2>
            <div class="section-divider"></div>
        </div>
        <div class="row g-5">
            <ToolCard
                v-for="tool in tools"
                :key="tool.id"
                :tool="tool"
            />
        </div>
    </section>
</template>

<script setup>
    import ToolCard from './ToolCard.vue';
    import tools from '../data/tools.json';
</script>
