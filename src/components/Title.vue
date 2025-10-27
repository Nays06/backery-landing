<template>
    <div class="title-main">
        <img src="/img/main/Line 7.svg" alt="">
        <div class="container">
            <div class="title">{{ title }}</div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        title: {
            type: String,
            required: true
        }
    }
}
</script>

<style scoped>
.title-main {
    width: 95%;
    position: relative;
    margin: 100px auto 60px;
    display: flex;
    justify-content: center;
}

img {
    width: 100%;
    position: absolute;
    top: 50%;
}

.container {
    padding: 0 20px;
    background-color: #fef8f8;
    z-index: 1;
}

.title {
    font-size: 50px;
    font-weight: bold;
    background: linear-gradient(90deg,
            #81008C 0%,
            #540096 25%,
            #81008C 50%,
            #540096 75%,
            #81008C 100%);
    background-size: 400% 100%;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    animation: flow-gradient 6s linear infinite;
}

@keyframes flow-gradient {
    0% {
        background-position: 100% 0%;
    }

    100% {
        background-position: -100% 0%;
    }
}
</style>