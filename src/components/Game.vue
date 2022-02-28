<template>
    <p>{{nbrCards}}</p>
    <p ref="super ref">Vous avez trouvé {{ score }} paires</p>

    <div v-if="ismounted">
        <div v-for="n in parseInt(nbrCards)" :id="orderArray[n-1]"  class="card" @click="cardClick($event, n-1)">
            carte numéro :
            {{ this.dictShow[n-1]["un"] }}

        </div>
    </div>  
    
        
    
    <!-- 
    
    <div id="2" ref="2" class="card" @click="cardClick">card 2</div>
    <div id="1" ref="3" class="card" @click="cardClick">card 1</div> -->
</template>

<script>
export default {
    props: [
        "nbrCards"
    ],
    methods: {
        cardClick(e, i){
            console.log("i", i)

            console.log("first return : ", this.firstReturn)
            console.log("actuel id", e['srcElement']['id'])
            if(this.firstReturn == null){
                this.PfirstReturn = i
                this.firstReturn = e['srcElement']['id']
                let first = true
                

                this.dictShow[i]["un"] = e['srcElement']['id']
            }else{
                let first = false
                
                if(this.PfirstReturn == i){

                    alert("double click")


                }else if(this.firstReturn == e['srcElement']['id']){
                    this.score += 1
                    
                    this.dictShow[i]["un"] = e['srcElement']['id'] //deuxième

                    this.firstReturn = null
                    if(this.score >= this.nbrCards/2){
                        this.$emit("win")
                    }

                }else{
                    console.log("trompé")
                    this.dictShow[i]["un"] = e['srcElement']['id']

                    setTimeout(() => {
                        this.dictShow[i]["un"] = null
                        this.dictShow[this.PfirstReturn]["un"] = null
                    }, 1500)
                    

                    this.firstReturn = null
                }
            }
            
        },
        
    },
    data(){
        return{
            firstReturn: null,
            score: 0,
            
            orderArray: null,
            numberArray: null,
            ismounted: false,
            i: null,

            dictShow: [],

            numberOne: null,
            numberTwo: null,
            PfirstReturn: null
        }
    },
    mounted(){
        
        this.numberArray = new Array()
        
        for(let k=1; k < (this.nbrCards/2)+1; k++){
            this.numberArray.push(k)
            if(k == this.nbrCards/2 && this.numberArray.length < this.nbrCards){
                k = 0
            }
        }
        console.log("Start:numberArray", this.numberArray)

        console.log("mounted")
        
        this.orderArray = new Array()
        // console.log(this.orderArray)
        
        
        
            

        

        for(let j=0; j < (this.nbrCards); j++){
            // this.orderArray.push(Math.floor(Math.random() * (((this.nbrCards / 2)+1) - 1) + 1))
            
            const random = Math.floor(Math.random() * this.numberArray.length);
            
            
            this.orderArray.push(this.numberArray[random])

            
            this.numberArray.splice(random, 1)
        }
            
            
            
         
         console.log("final", this.orderArray)
         

        for(let k=1; k < (this.nbrCards + 1); k++){
            this.dictShow.push({
                un : null,
                deux : null
            })

        }
        console.log("dictionnaire : ", this.dictShow)
        
        console.log(this.dictShow[0]["un"])
        this.ismounted = true
     
    }

}
</script>

<style lang="scss">
    .card{
        width: 150px;
        height: 100px;
        background: whitesmoke;
        margin: 20px;
        padding: 30px;
        text-align: center;
        display: inline-block;
        article{
            height: 90%;
            width: 90%;
        }
    }
</style>

