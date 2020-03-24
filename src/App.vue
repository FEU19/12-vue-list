<template>
	<div id="app">
		<h1>Stadsturist</h1>
		<div class="filterHeader">
			<input type="text" placeholder="Skriv vad du vill söka efter"
				@keyup="handleKeyUp" />
		</div>
		<div class="sortHeader">
			Hur vill du sortera?
			<button @click="sorteringsNyckel = 'namn'"
				:class="{ selected: sorteringsNyckel == 'namn' }">Namn</button> /
			<button @click="sorteringsNyckel = 'aktivitet'"
				:class="{ selected: sorteringsNyckel == 'aktivitet' }">Aktivitet</button>
			<button @click="sorteringsNyckel = 'restaurang'"
				:class="{ selected: sorteringsNyckel == 'restaurang' }">Restaurang</button>
			<button @click="sorteringsNyckel = 'sightseeing'"
				:class="{ selected: sorteringsNyckel == 'sightseeing' }">Sightseeing</button>
		</div>
		<div class="list">
			<PlatsRad v-for="plats in sorteradePlatser" :key="plats.id" :plats="plats" />
		</div>
	</div>
</template>

<!-- slider -->
<!-- input-fält -->
<!-- buttons +1 -1 -->

<script>
import PlatsRad from './components/PlatsRad.vue'

export default {
	name: 'App',
	components: {
		PlatsRad
	},
	data: () => ({
		platser: [
			{ id: 1, namn: 'Nordic wellness', adress: 'Såggatan 6', aktivitet: 4, restaurang: 1, sightseeing: 1 },
			{ id: 2, namn: 'Sjömagasinet', adress: 'Adolf Edelsvärds gata 5', aktivitet: 1, restaurang: 4, sightseeing: 1 },
			{ id: 3, namn: 'Älvsborgs fästning', adress: 'Nya Älvsborgs Fästning', aktivitet: 1, restaurang: 1, sightseeing: 5 },
			{ id: 5, namn: 'Miami Design District', adress: '110 NE 40th St, Miami, FL 33137, United States', aktivitet: 3, restaurang: 4, sightseeing: 4 },
			{ id: 6, namn: 'Liseberg', adress: 'Örgrytevägen 5, 402 22 Göteborg', aktivitet: 4, restaurang: 1, sightseeing: 1 },
			{ id: 7, namn: 'Villa Belparc', adress: 'A O Elliots Väg 10', aktivitet: 1, restaurang: 3, sightseeing: 2 },
			{ id: 8, namn: 'Donald Trump', adress: '1600 Pennsylvania Avenue, Washington DC', aktivitet: 4, sightseeing: 1, restaurang: 3 }
			// namn: 'Almedal Club', adress: 'Ebbe Lieberathsgatan 18C', 412 65 Göteborg, aktivitetet: 3, restaurang: 1, sightseeing: 4
		],
		sorteringsNyckel: 'namn', // sortKey
		filter: ''  // decides which items in the list should be visible
	}),
	computed: {
		sorteradePlatser() {
			console.log('sorteradePlatser körs');
			let copy = [ ...this.platser ];  // make a copy of the list, because SORT changes the list
			// maybe filter the list
			if( this.filter == '' ) {
				// no filter
			} else {
				copy = this.filtreraPlatser(copy);
			}


			if( this.sorteringsNyckel == 'namn' ) {
				let sorterad = copy.sort( (a, b) => {
					if( a.namn.toLowerCase() < b.namn.toLowerCase() ) return -1;
					else if( a.namn.toLowerCase() > b.namn.toLowerCase() ) return 1;
					else return 0;
				} )
				return sorterad;
			} else {
				let sorterad = copy.sort( (a, b) => {
					if( a[this.sorteringsNyckel] > b[this.sorteringsNyckel] ) return -1;
					else if( a[this.sorteringsNyckel] < b[this.sorteringsNyckel] ) return 1;
					else return 0;
				} )
				return sorterad;
			}
		} // sorteradePlatser
	},  // computed
	methods: {
		filtreraPlatser(lista) {
			// om namnet innehåller strängen som vi har skrivit i input-fältet, ska platsen tas med
			return lista.filter(plats => plats.namn.toLowerCase().includes(this.filter.toLowerCase()));
		},
		handleKeyUp(event) {
			this.filter = event.target.value;
		}
	}
}
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	color: #2c3e50;
}

* {
	margin: 0;
}
body {
	min-height: 100%;
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
}
.list {
	background-color: #99E6E6;
	padding: .5rem;
	border: 1px solid grey;
	width: 80vw;
}
.list > .item:nth-child(even) {
	background-color: #CCFFCC;
}


button {
	font-family: 'Franklin Gothic Medium';
	letter-spacing: 2px;
	color: #686767;
	text-transform: uppercase;
	text-decoration: none;
	background: rgb(208, 238, 206);
	padding:2px 6px 2px 6px;
	border-radius: 2px;
	border: 1.5px solid grey;
	display: inline-block;
	transition: all 0.1s;
	cursor: pointer;
}
button:hover, button:focus, button.selected {
	color: #F3F2F2;
	background: rgb(115, 163, 163);
	transition: all 0.3s;
}

.filterHeader {
    border: 1px solid gray;
    border-radius: 5px;
    padding: 1em;
    background-color: gray;
}
.filterHeader input {
    border: 1px solid lightblue;
    border-radius: 0.2em;
    width: 30%;
    padding: 1em;
}
</style>
