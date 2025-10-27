<template>
    <div class="background-rectangle">
        <img src="/img/main/Rectangle.svg" alt="">
    </div>

    <main>
        <div class="main">
            <div class="left">
                <div class="title">Sweet moments, freshly baked with love</div>
                <div class="description">Customized cakes, treats and every thing sweet for all your special moments.
                </div>
                <button class="button">Shop Now</button>
                <div class="links">
                    <img src="/img/main/facebook.svg" alt="facebook">
                    <img src="/img/main/linkedin.svg" alt="linkedin">
                    <img src="/img/main/instagram.svg" alt="instagram">
                </div>
            </div>
            <div class="right">
                <img src="/img/main/donuts.png" alt="">
            </div>
        </div>

        <div class="arrows-down" @click="scrollToCollection">
            <img src="/img/main/arrows_down.svg" alt="">
        </div>

        <div class="collection" ref="collectionBlock">
            <div class="left">
                <div class="name">See Collection</div>
                <div class="title">OUR FINE HOME MADE CHOCOLATES</div>
            </div>

            <div class="right">
                <div class="line-main">
                    <img src="/img/main/Line.svg" alt="">
                    <div class="points">
                        <div class="point" v-for="value in 3"></div>
                    </div>
                    <div class="lines">
                        <div class="line" v-for="value in 3"></div>
                    </div>
                    <div class="cards">
                        <div class="card" v-for="value in 3">
                            <div class="img">
                                <img src="/img/main/Delicious_vanilla_cake_decorated_with_berries_-3-removebg-preview 1.png"
                                    alt="">
                            </div>
                            <div class="text">
                                There are some redeming factors in greeking text
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="best-sellers">
            <Title :title="'OUR BEST SELLERS'" />

            <div class="see-all"><a href="#">See All</a></div>

            <div class="cards">
                <div class="card" v-for="value in 4">
                    <div class="img"><img src="/img/main/Rectangle 332.png" alt=""></div>
                    <div class="title">3-tier red velvet cake</div>
                    <div class="description">Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor.</div>
                    <div class="dop">
                        <div class="price">45.90 €</div>
                        <button>Add to Cart</button>
                    </div>
                </div>
            </div>
        </div>

        <div class="new-articles">
            <Title :title="'OUR NEW ARTICLES'" />

            <div class="cards">
                <div class="card" v-for="value in 4">
                    <div class="img">
                        <img src="/img/main/Rectangle 332.png" alt="">
                    </div>
                    <div class="date">23 MAR</div>
                    <div class="title">How to make perfect cakes at home</div>
                </div>
            </div>
        </div>

        <div class="our-customers">
            <Title :title="'OUR CUSTOMERS'" />

            <div class="cards">
                <div class="card" v-for="value in 3">
                    <div class="user-info">
                        <div class="avatar"><img src="/img/main/avatar.png" alt="avatar"></div>
                        <div class="dop">
                            <div class="name">Khutiev A.</div>
                            <div class="location">Russia, Republic of Ingushetia</div>
                        </div>
                    </div>
                    <div class="description">Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco.</div>
                </div>
            </div>
        </div>
    </main>
</template>

<script>
import Title from './Title.vue';

export default {
    components: {
        Title
    },
    methods: {
        scrollToCollection() {
            const element = this.$refs.collectionBlock;
            if (element) {
                const elementPosition = element.getBoundingClientRect().top;
                const offsetPosition = elementPosition + window.pageYOffset - 100;

                window.scrollTo({
                    top: offsetPosition,
                    behavior: 'smooth'
                });
            }
        }
    }

}
</script>

<style scoped>
.background-rectangle {
    position: absolute;
    z-index: -1;
    width: 100%;
    top: 800px;

    img {
        width: 100%;
    }
}

.main {
    display: flex;
    width: 85%;
    align-items: center;
    justify-content: space-between;
    margin: 127px auto 0;
}

.main .left {
    width: 574px;
}

.main .title {
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

.main .description {
    font-size: 20px;
    color: #282828;
    margin-top: 32px;
}

.main .button {
    background-color: #973499;
    border: none;
    color: #fff;
    padding: 12px 16px;
    font-size: 18px;
    font-weight: 600;
    border-radius: 10px;
    cursor: pointer;
    user-select: none;
    margin-top: 32px;
}

.main .links {
    display: flex;
    margin-top: 32px;

    &>img:not(:first-child) {
        margin-left: 12px;
    }
}

.main .right img {
    width: 900px;
}

.arrows-down {
    margin: 40px auto;
    width: fit-content;
    cursor: pointer;
}

.collection {
    display: flex;
    justify-content: space-between;
    width: 80%;
    margin: 350px auto 0;
}

.collection .name {
    font-size: 18px;
}

.collection .title {
    color: #E35050;
    font-size: 30px;
    font-weight: 600;
    width: 321px;
    margin-top: 24px;
}

.line-main .points {
    width: 100%;
    display: flex;
    justify-content: space-around;
}

.line-main .point {
    background-color: #BC7AFF;
    width: 20px;
    height: 20px;
    margin-top: -10px;
    border-radius: 50%;
}

.line-main .lines {
    width: 100%;
    display: flex;
    justify-content: space-around;
}

.line-main .line {
    width: 1px;
    height: 60px;
    background-color: #919191;
}

.line-main .cards {
    width: 100%;
    display: flex;
    justify-content: space-around;
}

.line-main .card {
    width: 167px;

    .img {
        width: 167px;
        height: 167px;
        border-radius: 50%;
        background-color: #fff;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .text {
        text-align: center;
        margin-top: 24px;
    }
}

.best-sellers .see-all {
    text-align: right;
    width: 94%;
    margin: 0 auto;

    a {
        color: #E35050;
        font-size: 20px;
        font-weight: 600;
        text-decoration: none;
    cursor: pointer;
    user-select: none;
    }
}

.best-sellers .cards {
    width: 94%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin: 40px auto 0;
}

.best-sellers .card {
    width: 400px;
    background-color: #fff;
    padding: 17px;

    .title {
        font-size: 25px;
        font-weight: 600;
        margin-top: 16px;
    }
    
    .description {
        font-size: 18px;
        margin-top: 16px;
    }

    .dop {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-top: 26px;
    }

    .price {
        font-size: 25px;
        font-weight: 600;
    }

    button {
        background-color: #973499;
        border-radius: 10px;
        color: white;
        padding: 12px 16px;
        border: none;
        font-weight: 600;
        cursor: pointer;
        user-select: none;
    }
}

.new-articles .cards {
    display: flex;
    width: 94%;
    align-items: center;
    justify-content: space-between;
    margin: 0 auto;
}

.new-articles .card {
    padding: 17px;
    position: relative;
    background-color: #fff;
    border-radius: 15px;

    .img {
        width: 365px;
        height: 475px;
        overflow: hidden;
        display: flex;
        align-items: center;
        justify-content: center;
        position: relative;
        border-radius: 5px;

        &::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 70%;
            background: linear-gradient(to top, rgba(0,0,0,0.9) 0%, transparent 100%);
            pointer-events: none;
        }

        img {
            height: 100%;
            object-fit: cover;
            width: 100%;
        }
    }

    .date {
        position: absolute;
        top: 30px;
        left: 30px;
        width: 70px;
        background-color: #0000002d;
        color: #fff;
        font-size: 20px;
        text-align: center;
        border-radius: 15px;
        padding: 15px 3px;
        z-index: 2;
    }

    .title {
        position: absolute;
        bottom: 30px;
        left: 30px;
        color: #fff;
        font-size: 20px;
        z-index: 2;
        width: 300px;
        font-size: 25px;
        font-weight: 600;
    }
}

.our-customers .cards {
    width: 94%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin: 0 auto;
}

.our-customers .card {
    padding: 50px;
    width: 570px;
    background-color: #fff;
    border-bottom: 5px solid #FF9AE96d;
    border-radius: 15px;

    .avatar {
        border-radius: 50%;
        overflow: hidden;
            width: 70px;
            height: 70px;

        img {
            width: 100%;
            height: 100%;
        }
    }

    .user-info {
        display: flex;
        align-items: center;
    }

    .dop {
        margin-left: 20px;
    }

    .name {
        font-size: 25px;
        font-weight: 600;
    }

    .location {
        font-size: 18px;
    }

    .description {
        margin-top: 20px;
    }
}
</style>