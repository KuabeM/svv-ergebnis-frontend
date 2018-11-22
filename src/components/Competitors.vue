<template>
    <div class="competitors">
        <div class="inputs-row">
            <DisplayText  v-model="nameHome" v-on:team-change="updateTeam(1, $event)"/>:
            <DisplayText  v-model="nameAway" v-on:team-change="updateTeam(2, $event)"/>
        </div>
        <div class="inputs-row">
            <DisplayNum v-model="scoreHome"  v-on:score-change="updateScore(1, $event)"/>:
            <DisplayNum v-model="scoreHome"  v-on:score-change="updateScore(2, $event)"/>
        </div>
        <div class="control-area">
            <button v-on:click="send_request()">Update</button>
        </div>
    </div>
</template>


<script>
import DisplayNum from './DisplayNum.vue'
import DisplayText from './DisplayText.vue'
// var axios = require('axios')
// import * as http from "http";
// const httpModule = require("http");
// import VueResource from 'vue-resource';

export default {
    name: 'Competitors',
    components: {
        DisplayText,
        DisplayNum,
    },
    data: function () {
        return {
            nameHome: "Heim",
            nameAway: "Gast",
            scoreHome: 0,
            scoreAway: 0,
            backend_url: 'localhost:3000',
            postResult: []
        }
    },
    methods: {
        updateTeam(HoA, val) {
            if (HoA == 1) {
                this.nameHome = val;
            } else {
                this.nameAway = val;
            }
        },
        updateScore(HoA, val) {
            if (HoA == 1) {
                this.scoreHome = val;
            } else {
                this.scoreAway = val;
            }
        },
        send_request() {
            var msg = { 
                "home": this.nameHome,
                "away": this.nameAway,
                "scoreHome": this.scoreHome,
                "scoreAway": this.scoreAway,
            };
            var headers = { "Content-Type": "application/json" };
            // httpModule.request({
            //     url: this.backend_url,
            //     method: "POST",
            //     headers: { "Content-Type": "application/json" },
            //     content: JSON.stringify({ 
            //         "home": this.nameHome,
            //         "away": this.nameAway,
            //         "scoreHome": this.scoreHome,
            //         "scoreAway": this.scoreAway,
            //     }),
            // }).then((response) => {
            //         var result = response.content.toJSON();
            //         console.log(result);
            //     }, error => {
            //         console.log('we caught an error');
            //         console.error(error);
            // });
            // this.$http.get('http://localhost:3000').then(response => {
            //     var someData = response.body;
            //     console.log(someData);
            // }, response => {
            //     console.log(response);
            // });
            this.$http.post('http://localhost:3000', msg, headers).then(response => {
                console.log('status: ' + response.status)
                var someData = response.body;
                console.log(someData);
            }, response => {
                console.log('status: ' + response.status);
            });
        },
    },
}


</script>

<style scoped>
.competitors {
    width: 80vw;
    margin-left: 10%;
    font-size: 2.5em;
    font-weight: bold;
}

.inputs-row {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
}

.control-area {
    margin-top: 2vh;
}

</style>
