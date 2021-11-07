<template>
    <div>
        <h1>Indecision</h1>
        <img v-if="image" :src="image" alt="no imag" height="250px" width="250px">

        <div class="insecision-container">
            
            <input 
            v-model="question"
            type="text" 
            placeholder="Hazme una pregunta"
            />
            <p>Recuerda terminar con un signo de interrogación (?)</p>
            <div>
                <h2>{{question}}</h2>
                <h1>{{answer}}</h1>
            </div>

        </div>

        
        
    </div>
</template>

<script >
export default {
  name: 'Indecision',

    data(){
        return {
            question: null,
            answer: null,
            image: null
        }  
    },

    methods: {
        async getAnswer(){
            this.answer = 'Pensando...'
            const {answer,image} = await fetch('https://yesno.wtf/api').then(r=>r.json())
             this.answer=answer
             this.image=image


        }

    },

    watch: {
        question(  value,   ){

            if( !value.includes('?') ) return
            this.getAnswer()

            
        }
    }

}


</script>

<style scoped>
img {
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0px;
  left: 0px;
}

.insecision-container {
    position: relative;
    z-index: 99;
}

h1, h2 , p {
    color: white;
}

</style>