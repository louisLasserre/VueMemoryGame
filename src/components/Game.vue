<template>
    
    <p ref="super ref">Vous avez trouvé {{ score }} paires</p>

    <div v-if="ismounted">
        <div v-for="n in parseInt(nbrCards)" :id="orderArray[n-1]"  class="card" @click="cardClick">
            <article @click="show(n-1)">{{ this.dictShow[n-1]["un"] }}</article>
        </div>
    </div>  
    
        
    
    <!-- 
    
    <div id="2" ref="2" class="card" @click="cardClick">card 2</div>
    <div id="1" ref="3" class="card" @click="cardClick">card 1</div> -->
</template>

<script>
export default {
    methods: {
        cardClick(e){
            // console.log(this.$refs)
            
            if(this.firstReturn == null){
                this.firstReturn = e['srcElement']['id']
            }else{
                if(this.firstReturn == e['srcElement']['id']){
                    this.score += 1
                    console.log("trouvé")
                    this.firstReturn = null

                }else{
                    console.log("erreur")
                    this.firstReturn = null
                }
            }
            
        },
        show(i){
            console.log("first return : ",this.firstReturn)

            
            if(this.firstReturn != null){
                if(this.firstReturn == i+1){
                    alert("double click")
                }else{
                    this.dictShow[i]["un"] = "deux"
                }
                

            }else{
                this.dictShow[i]["un"] = "premier"
            }
            
        }
        
    },
    data(){
        return{
            firstReturn: null,
            score: 0,
            nbrCards: 4,
            orderArray: null,
            numberArray: null,
            ismounted: false,
            i: null,

            dictShow: [],

            numberOne: null,
            numberTwo: null
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
         this.ismounted = true

        for(let k=1; k < (this.nbrCards + 1); k++){
            this.dictShow.push({
                un : null,
                deux : null
            })

        }
        console.log("dictionnaire : ", this.dictShow)
        
        console.log(this.dictShow[0]["un"])
        
     
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

