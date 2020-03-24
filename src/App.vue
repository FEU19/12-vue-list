<template>
	<div id="app">
		<h1>Stadsturist</h1>
		<div>
			Hur vill du sortera?
			<button @click="sorteringsNyckel = 'namn'">Namn</button> /
			<button @click="sorteringsNyckel = 'aktivitet'">Aktivitet</button>
			<button @click="sorteringsNyckel = 'restaurang'">Restaurang</button>
			<button @click="sorteringsNyckel = 'sightseeing'">Sightseeing</button>
		</div>
		<div class="list">
			<div class="item" v-for="plats in sorteradePlatser" :key="plats.id">
				{{ plats.namn }}
				{{ plats.adress }}
				Aktivitet: {{ plats.aktivitet}}
				Restaurang: {{plats.restaurang}}
				Sightseeing: {{plats.sightseeing}}
			</div>
		</div>
	</div>
</template>

<script>
// import ?? from './components/??.vue'

export default {
	name: 'App',
	components: {
		// ??
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
		sorteringsNyckel: 'namn' // sortKey
	}),
	computed: {
		sorteradePlatser() {
			console.log('sorteradePlatser körs');
			let copy = [ ...this.platser ];  // make a copy of the list, because SORT changes the list
			if( this.sorteringsNyckel == 'namn' ) {
				let sorterad = copy.sort( (a, b) => {
					if( a.namn < b.namn ) return -1;
					else if( a.namn > b.namn ) return 1;
					else return 0;
				} )
				return sorterad;

			} else if( this.sorteringsNyckel == 'aktivitet' ) {
				let sorterad = copy.sort( (a, b) => {
					if( a.aktivitet > b.aktivitet ) return -1;
					else if( a.aktivitet < b.aktivitet ) return 1;
					else return 0;
				} )
				return sorterad;

			} else if( this.sorteringsNyckel == 'restaurang' ) {
					let sorterad = copy.sort( (a, b) => {
						if( a.restaurang > b.restaurang ) return -1;
						else if( a.restaurang < b.restaurang ) return 1;
						else return 0;
					} )
					return sorterad;

			} else if( this.sorteringsNyckel == 'sightseeing' ) {
				let sorterad = copy.sort( (a, b) => {
					if( a.sightseeing > b.sightseeing ) return -1;
					else if( a.sightseeing < b.sightseeing ) return 1;
					else return 0;
				} )
				return sorterad;
			}
			return this.platser;
		} // sorteradePlatser
	}  // computed
}
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	color: #2c3e50;
}

/* .list{
    padding: 1em;
    display: flex;
    justify-content: space-evenly;
    align-items: center;
}
.item:nth-child(odd){
    background-color: lightgray;
}
.item:nth-child(even){
    background-color: whitesmoke;
} */
*{
  margin: 0;
}
body{
  min-height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
div {
  background-color: #99E6E6;
  padding: .5rem;
  border: 1px solid grey;
  width: 80vw;
}
div:nth-child(even){
  background-color: #CCFFCC;
}
</style>
