<script setup>
import { ref, shallowRef, watch, computed, nextTick } from 'vue'
import Chart from 'chart.js/auto'

const weights = ref([])
const weightChartEl = ref(null)
const weightChart = shallowRef(null)
const weightInput = ref(60.0)

const currentWeight = computed(() => weights.value.sort((a, b) => b.date - a.date)[0] || { weight: 0 })

const addWeight = () => {
	weights.value.push({
		weight: weightInput.value,
		date: new Date().getTime()
	})
}

</script>
<template>
	<main>
		<h1>Weight Tracker</h1>

		<div class="current">
			<span>{{ currentWeight.weight }}</span>
			<small>Current Weight (kg)</small>
		</div>

		<form @submit.prevent="addWeight">
			<input
				type="number"
				stop="0.1"
				v-model="weightInput"
			/>
			<input type="submit" value="Add weight">
		</form>
	</main>
</template>
