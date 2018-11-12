<template>
    <div class="header">
        <img class="logo" alt="SVV logo" src="../assets/logo_light.png" >
        <h3 class="headline">
            SVV Ergebnisanzeige
        </h3>
    </div>
</template>


<script>
export default {
  name: 'Headline',
}
</script>

<style scoped>
.header {
    height: 20vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background-color: #2c3e50;
}

.headline {
    color: #eeeeee;
    line-height: 1em;
    height: 15%;
    font-weight: bolder;
    font-size: 1.5em;
    margin: 1% 0 0 0;
}

img.logo {
    height: 74%;
}
</style>
