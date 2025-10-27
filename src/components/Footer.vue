<template>
    <footer>
        <div class="left">
            <div class="title">Bakery</div>
            <div class="description">Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor
                incididunt ut labore et dolore magna aliqua.</div>
            <div class="links">
                <img src="/img/main/facebook.svg" alt="">
                <img src="/img/main/linkedin.svg" alt="">
                <img src="/img/main/instagram.svg" alt="">
            </div>
        </div>
        <div class="right">
            <div class="column">
                <div class="title">OUR STORES</div>
                <div class="rows">
                    <div class="row">SLOVAKIA</div>
                    <div class="row">CZECH REPUBLIC</div>
                    <div class="row">FINLAND</div>
                    <div class="row">POLAND</div>
                </div>
            </div>

            <div class="column">
                <div class="title">USEFUL LINKS</div>
                <div class="rows">
                    <a href="#" class="row">HOME</a>
                    <a href="#" class="row">PRIVACY POLICY</a>
                    <a href="#" class="row">TERMS CONDITIONS</a>
                    <a href="#" class="row">CONTACT US</a>
                </div>
            </div>
        </div>
    </footer>
</template>

<script></script>

<style scoped>
footer {
    display: flex;
    justify-content: space-between;
    padding: 50px 3%;
    margin-top: 120px;
    border-top: 1px solid #919191;
}

.left {
    width: 500px;
}

.left .title {
    font-family: "Arbutus Slab", serif;
    font-size: 35px;
    color: #CE44E4;
}

.left .description {
    font-size: 20px;
    margin-top: 30px;
}

.left .links {
    display: flex;
    align-items: center;
    margin-top: 45px;

    &>img:not(:first-child) {
        margin-left: 12px;
    }
}

.right {
    display: flex;
    justify-content: space-between;
}

.right .title {
    font-size: 20px;
    font-weight: 600;
}

.right .column:not(:first-child) {
    margin-left: 70px;
}

.right .rows {
    margin-top: 30px;
    display: flex;
    flex-direction: column;

    &>.row:not(:first-child) {
        margin-top: 20px;
    }

    a {
        text-decoration: none;
        color: #000;
    }
}
</style>