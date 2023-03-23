<script>

import axios from 'axios' 

export default {
    data() { 
        return {
            city: "",
            error: "",
            info: null
        }
    },
    computed: {
        cityName() {
            return this.city
        },
        showTemp() {

            return "Температура:" + this.info.main.temp
        },
        showFeelsLike() { 
            return "Ощущается как:" + this.info.main.feels_like
        },
        showMaxTemp() { 
            return "Максимальная температура:" + this.info.main.temp_max
        }

        
                
    },
    methods: {
        getWeather() { 
            if (this.city.trim().length < 2) {
                this.error = "Нужно название места"
                return false
            }
            this.error = ""

            axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=542ffd081e67f4512b705f89d2a611b2`)
            .then(res => (this.info = res.data))
        }
    }
}

</script>

<template>

    <div class="wrapper">

        <h1>Погодное приложение </h1>
        <P>Узнать погоду  {{ city == "" ? "в вашем городе ": cityName }}</P>
        <input type="text" v-model="city" placeholder="Введите город">
        
        <button v-if="city !='' "  @click="getWeather()">Получить погоду</button>
        <button v-else>Введите другое</button>
        
        <p class="error">{{ error }}</p>

        <div  v-if="info != null">
            
            <p>{{ showTemp }}</p>
              <p>{{ showFeelsLike }}</p>
          

        </div>
     

        


    </div>

</template>

<style scoped>

.error {
    color:red;
}

.wrapper {
     width: 900px;
     height: 500px;
     border-radius: 50px;
     background: rgb(0, 0, 0);
     text-align: center;
     color: white;
}

.wrapper h1 {
margin-top: 50px;
}



.wrapper p {
    margin-top: 45px;
}

.wrapper input {
    margin-top: 30px;
    background: transparent;
    border: 0;
    border-bottom: 2px solid black;
    color: white;
    font-size: 14px;
    padding: 5px 8px;
    outline: none;
    border-radius: 50px ;
}

.wrapper input:focus {
    border-bottom-color: green;
}

.wrapper button {

    background: green;
    color: white;
    cursor: pointer;
    border-radius: 10px;
}


</style>
