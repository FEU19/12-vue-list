<template>
	<div class="item">
		<div>
			<div v-show="visaNamn" @click="visaNamn = false"> {{ plats.namn }} </div>
			<input v-show="!visaNamn" type="text" v-model="plats.namn"
				@blur="visaNamn = true" />
		</div>

		<div>
			<div v-show="visaAdress" @click="visaAdress = false"> {{ plats.adress }} </div>
			<input v-show="!visaAdress" type="text" v-model="plats.adress"
				@blur="visaAdress = true" />
		</div>

		<div class="sliderContainer">
			<div class="slider">
				<div> Aktivitet: {{ plats.aktivitet}} </div>
				<input type="range" min="1" max="5" v-model="plats.aktivitet" />
			</div>
			<div class="slider">
				<div> Restaurang: {{plats.restaurang}} </div>
				<input type="range" min="1" max="5" v-model="plats.restaurang" />
			</div>
			<div class="slider">
				<div> Sightseeing: {{plats.sightseeing}} </div>
				<input type="range" min="1" max="5" v-model="plats.sightseeing" />
			</div>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		plats: Object(null)
	},
	data: () => ({
		visaNamn: true,
		visaAdress: true
	})
}
</script>

<style scoped>
.item {
	display: grid;
	grid-template-columns: repeat(4, 1fr);
}
.item > div {
	display: inline-block;
}
.sliderContainer {
	grid-column: 3 / span 2;
}
.slider {
	display: grid;
	grid-template-columns: 1fr 1fr;
}
</style>
