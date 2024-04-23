<script setup>
	const searchQuery = ref("star");
        const resultQuery = ref( null );

	const searchData = async() => await useFetch('https://images-api.nasa.gov/search?q=' + searchQuery.value)
	.then((res) => { 
	    resultQuery.value = JSON.stringify(resultQuery.value);	   
	});

	//onBeforeMount( async ()=> {
	    //searchData()
	//});

	const loadArticle = ref(false)
	const showPredictionRef = ref(false)

	const showPrediction = () => {
	    alert("Click")
	    showPredictionRef.value = !showPredictionRef.value
	}

	const showArticle = () => {
	    alert("Click")
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
	<div>
		<input type="text" v-model="searchQuery" />
		<button class="button is-primary mt-4 mb-4" @click="searchData">Search</button>
	</div>

	<span v-if="loadArticle">
		<div v-for="(item, index) in resultQuery.value" :key="index">
			<h3>{{ item.data[0].title }}</h3>
			<p>{{ item.data[0].description }}</p>
			<img :src="item.links[0].href" alt="Lights">
		</div>
	</span>

    <button class="button is-primary mt-4 mb-4 ml-4" @click="showArticle">Display article</button>
    <br/>
    <span v-if="loadArticle">
	    <section class="ai-response-container-display">
		    <span>This is the name of the file: {{ response.fileName }}</span>
		    <img :src="response.image" alt="Lights">
		    <button class="button is-primary mt-4 mb-4 " @click="showPrediction">Display prediction</button>
		    <span v-show="showPredictionRef" >{{response.prediction}}: {{response.percentage}}</span>
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
	margin: 0 10px 0 10px;
        height: 100%; // Add this line
    }
    //Fit image to container;
    img {
	    width: 400px;
	    height: 600px;
	    object-fit: scale-down;
    }
}

</style>
