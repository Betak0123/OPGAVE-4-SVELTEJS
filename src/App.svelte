
<script>
	let number 
	let face

    let counter = 0
	let juiceIMG
	let gifPicker
	let text
	let tema = ''
    let gifs = []
	let ranPic
	let randomPicker

	const gifHenter = (inf) => {
		fetch('https://api.giphy.com/v1/gifs/search?q=' + inf + '&limit=20&api_key=bZtpERwaxr8KjBTC3STQKMTPpxrGIkYl')
			.then(res => res.json())
			.then(json =>{
				console.log(json)
				gifPicker = Math.floor(Math.random()*json.data.length)
					// console.log(json.data[0].images.original.url)
					juiceIMG = json.data[gifPicker].images.original.url
					console.log('Længden af arrayet er: '+ json.data.length)
					gifs = [...gifs, {text: inf, img: juiceIMG}]
					// console.log('giffen er nu gemt')
					// console.log(gifs, gifPicker)	
			})
	} 
	const tilfældigt = () =>{
		console.log('det virker')
		randomPicker = Math.floor(Math.random()*gifs.length)
		ranPic = gifs[randomPicker]
	}

</script>
<main>
	<div id="header">
		<div id="vælger">
			<p>Hvad skal din liste handle om?</p>
			<input id="tema" type="text" bind:value={tema}>
		</div>
		<div id="finder">
			<button class="button" on:click={gifHenter(text)}>
				  Vælg en ny ting til listen
			  </button>
			  <input id="inf" type="text" bind:value={text}>
		</div>
		<div id="random">
			<button class="button" id="heh" on:click={tilfældigt}>Tilfældigt fra listen</button>
			{#if ranPic}
			<div class="container2">
				<img  class='billede2' src= "{ranPic.img}" alt="">
				<p class="overtext">{ranPic.text}</p>
			</div>
			{/if}

		</div>
	</div>  

	<div id="main">
		<h2>Her er din liste om: {tema}</h2>
		<div id="liste">
			{#each gifs as gif}
				<div class="container">
					<img  class='billede' src= "{gif.img}" alt="">
					<p class="overtext">{gif.text}</p>
				</div>
			{/each}
		</div>
	</div>


</main>

<style>

:global(*){
	box-sizing: border-box;
	margin:0;
	padding:0;
}
.billede{
    width:200px;
    height:200px;
    object-fit: cover;
    border-radius: 25%;
	border: 2px solid black;
}
.billede2{
    width:100px;
    height:100px;
    object-fit: cover;
    border-radius: 25%;
	border: 2px solid black;
}
#header{
	display: grid;
	border-bottom: 1px black;
	width: 100vw;
	grid-template-columns: 1fr 1fr 1fr;
	place-items: center;
	border-bottom: solid 2px black;
	padding: 1rem;
}
#main{
	padding: 1rem;
}

#finder{
	display: grid;
	place-items: center;
}

#random{
	display: grid;
	grid-template-columns: 1fr 1fr;
}


.overtext{
	display: grid;
	position: absolute;
	color: rgb(0, 0, 0);
	border-radius: 0.5rem;
	background-color: rgba(255, 255, 255, 0.605);
	padding: 0.2rem;
}

.container{
    display:grid;
	position: relative;
    width:200px;
    height:200px;
	margin: 2rem;
	place-items: center;
}
.container2{
    display:grid;
	position: relative;
    width:100px;
    height:100px;
	margin: 2rem;
	place-items: center;
}

#liste{
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(230px, 1fr));
		gap: 1rem;
		/* padding: 1rem; */
}

#vælger{
	display: grid;
	place-items: center;
}

button{
		color: white;
		background-color: grey;
		position:relative;
		border: 1px solid black;
		border-radius: .5rem ;
		/* height: 2rem; */

	}
		button:hover{
			background-image: linear-gradient(90deg, #00C0FF 0%, #FFCF00 49%, #FC4F4F 80%, #00C0FF 100%);
   			animation:slidebg 5s linear infinite;

	}
#heh{
	height: 3rem;
}
	@keyframes slidebg {
  to {
    background-position:20vw;
  }
}

</style>