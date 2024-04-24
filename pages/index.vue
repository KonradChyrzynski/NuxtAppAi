<script setup>
        const articles = ref( null );
	const baseURL = 'http://127.0.0.1:8000/media/';

	const searchData = async() => await useFetch('http://127.0.0.1:8000/articles/')
	.then((res) => { 
	    articles.value = res.data.value; 
	    console.log(articles.value);
	    console.log(res.data.value[0].fields);
	    console.log(res.data.value);
	});

	onBeforeMount( async ()=> {
	    searchData()
	});

	const loadArticle = ref(false)
	const showPredictionRef = ref(false)

	const showPrediction = () => {
	    alert("Click")
	    showPredictionRef.value = !showPredictionRef.value
	}

	const showArticle = async() => {
	    alert("Click")
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
	<button class="button is-primary mt-4 mb-4 ml-4" @click="showArticle">Display articles</button>
	<br/>
	<span v-if="loadArticle">
		<section>
			<div class="ai-response-container-display" v-for="(item, index) in articles" :key="index">
				<span>This is the name of the file: {{ item.fields.title }}</span>
				<img :src="baseURL + item.fields.photo" alt="Lights">
				<button class="button is-primary mt-4 mb-4 " @click="showPrediction">Display prediction</button>
				<span v-show="showPredictionRef">{{ item.fields.content }}</span>
			</div>
		</section>
	</span>
	<br/>
</template>

<style scoped lang="scss">
h3 {
    span {
	color: red
    }
    
}

.ai-response-container-display {
    display: flex;
    flex-direction: column;
    height: 100%;
    width: 100%;
    background-color: black;
    color: white;
    justify-content: center;
    align-items: center;
    font-size: 20px;

    span {
	margin: 0 auto;
    }

    //Fit image to container;
    img {
	    width: 400px;
	    height: 600px;
	    object-fit: scale-down;
    }
}

</style>
