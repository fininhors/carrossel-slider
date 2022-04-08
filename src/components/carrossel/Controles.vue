<template>
	<button class="carrossel-control left" @click="backward">Prev</button>
	<button class="carrossel-control right" @click="forward">Next</button>
</template>

<script setup>

const emit = defineEmits(['prev', 'next']);

function forward () {
	emit('next')
}
function backward () {
	emit('prev')
}

</script>

<style>
.carrossel-control {
	background-color: rgba(0, 0, 0, 0.5);
	border: none;
	color: #f3f3f3;
	cursor: pointer;
	display: inline-block;
	position: absolute;
	height: 50px;
	width: 70px;
	top: calc(50% - 25px);
}
.carrossel-control.left {
	left: 0;
}
.carrossel-control.right {
	right: 0;
}
</style>
