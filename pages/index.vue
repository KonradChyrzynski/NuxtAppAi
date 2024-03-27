<script setup>
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
