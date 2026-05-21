<template>
    <div class="bento-card bento-wide pencil-guide">
        <img :src="project.image" :alt="project.title" />
        <div class="bento-overlay">
            <h4>{{project.title}}</h4>
            <p>{{project.description}}</p>
        </div>
    </div>
</template>

<script setup>
	defineProps({
		project: Object
	})
</script>