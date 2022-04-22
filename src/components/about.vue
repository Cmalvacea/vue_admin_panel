<template>
    <div class="About_Section" v-if="About">
        <h1>About this project</h1>
        <p>This project was made by myself for my portfolio, feel free to use it as a base for your own project or as you wish, just make sure to add some changes or even some improvements, don't be so lazy</p>
    </div>
</template>

<script>
export default {
    props: {
        About: Boolean
    }
}
</script>

<style lang="scss">
.About_Section {
    text-align: center;
    font-family: sans-serif;
    border: 1px solid gainsboro;
    border-radius: 10px;
    box-shadow: 0px 5px 7px rgb(223, 223, 223);
    margin: auto;
    width: 50%;
    padding: 10px;
    background-color: white;

    p {
        font-size: 1.4em;
    }
}
</style>