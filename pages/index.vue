<script setup>
        const articles = ref( null );
	const baseURL = 'http://127.0.0.1:8000/media/';

	const searchData = async() => await useFetch('http://127.0.0.1:8000/articles/')
	.then((res) => { 
	    articles.value = res.data.value; 
	    console.log(articles.value);
	});

	onBeforeMount( async ()=> {
	    searchData()
	});

	const loadArticle = ref(false)
	const showPredictionRef = ref(false)

	const showPrediction = () => {
	    alert("Załaduj predykcję...")
	    showPredictionRef.value = !showPredictionRef.value
	}

	const showArticle = async() => {
	    alert("Załaduj zdjęcia...")
	    await searchData()
	    loadArticle.value = !loadArticle.value
	}

	let response = {
	    fileName: "Sunglasses.jpg",
	    image: "https://www.w3schools.com/w3images/lights.jpg",
	    percentage: "100%",
	    prediction: "Sunglasses"
	}

</script>

<template>
	<!--
	<h1 class="title container">
		Nie masz jeszcze strony internetowej? To nie problem! Stwórzmy ją razem i zautomatyzujmy Twoje zadania IT, abyś mógł skupić się na rozwijaniu biznesu.
		Wchodź do cyfrowego świata z nami - szybko, prosto i efektywnie!
	</h1>
	-->
	<div class="main-wrap-container"> 
		<h1 class="title container"> Przetestuj nasz model AI, który odgaduję co znajduję się na zdjęciu, oraz na podstawie predykcji generuje tekst w formie artykułu na bloga!</h1>
		<button class="button is-primary mt-4 mb-4 ml-4" @click="showArticle">
			Wyświetl zdjęcia
		</button>
		<button v-if="loadArticle" class="button is-primary ml-4 mt-4 mb-4 " @click="showPrediction">Wyświetl predykcję</button>
	</div>
	<br/>
	<span v-if="loadArticle">
		<section>
			<div class="ai-response-container-display" v-for="(item, index) in articles" :key="index">
				<span>Co znajduję się na zdjęciu według naszego modelu AI: {{ item.fields.title }}</span>
				<img :src="baseURL + item.fields.photo" alt="Lights">
				<br/>
				<span> {{item.fields.articleBlogPostContent}}... </span>
				<br/>
				<span v-show="showPredictionRef">Prawdopodobieństwo trafionej predykcji: {{ item.fields.content }}</span>
			</div>
		</section>
	</span>
	<br/>
</template>

<style scoped lang="scss">
.main-wrap-container{
	h1{
		padding-left: 20px;
		padding-right: 20px;
		margin-left: auto;
		margin-right: auto;
		max-width: 1200px;
		margin-top: 70px;
		margin-bottom: 70px;
	}
	p{
		margin-left: 20px;
		margin-right: 20px;
		font-size: 20px;
	}
	button{
		font-size: 20px;
	}
}

h3 {
    span {
	color: red
    }
    
}

.ai-response-container-display {
    margin-top: 40px;
    display: flex;
    flex-direction: column;
    height: 100%;
    width: 100%;
    color: black;
    justify-content: center;
    align-items: center;
    font-size: 20px;

    span {
	margin: 0 auto;
    }

    //Fit image to container;
    img {
	    width: 400px;
	    height: 500px;
	    object-fit: scale-down;
    }
}

</style>
