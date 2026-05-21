<template>
    <div class="col-12 col-md-4">
        <div class="d-flex align-items-center gap-3 mb-4">
            <span class="material-symbols-outlined toolbox-category-icon">{{tool.icon}}</span>
            <h3 class="fs-4 fw-bold fst-italic mb-0">{{tool.skill}}</h3>
        </div>
        <div class="d-flex flex-wrap gap-2">
            <div
                class="skill-pill pencil-guide"
                v-for="toolName in tool.toolArray"
                :key="toolName"
            >
                {{ toolName }}
            </div>
        </div>
    </div>
</template>

<script setup>
	defineProps({
		tool: Object
	})
</script>