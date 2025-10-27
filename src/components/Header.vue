<template>
    <header>
        <div class="name">
            Backery
        </div>

        <nav>
            <a href="#">Home</a>
            <a href="#">Shop</a>
            <a href="#">Services</a>
            <a href="#">Blog</a>
        </nav>

        <div class="actions">
            <a class="auth" href="#">
                Login/Register
            </a>

            <a class="favorite" href="#">
                <img src="/img/header/heart.svg" alt="Избранное">
            </a>
            <a class="basket" href="#">
                <img src="/img/header/basket.svg" alt="Корзина">
            </a>
        </div>
    </header>
</template>

<script>
export default {}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Arbutus+Slab&family=IBM+Plex+Sans:ital,wght@0,100..700;1,100..700&family=Inter:ital,opsz,wght@0,14..32,100..900;1,14..32,100..900&family=Montserrat:ital,wght@0,100..900;1,100..900&family=Roboto:ital,wght@0,100..900;1,100..900&family=Unbounded:wght@200..900&display=swap');

header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 93%;
    margin: 0 auto;
    background-color: #fff;
    padding: 20px;
    border-radius: 0 0 20px 20px;
    box-shadow: 0px 0px 16.3px #CE0BFF8d;
}

.name {
    font-family: "Arbutus Slab", serif;
    font-size: 35px;
    color: #CE44E4;
}

nav a {
    text-decoration: none;
    color: #000;
    font-size: 20px;

    &:not(:first-child) {
        margin-left: 48px;
    }
}

.actions {
    display: flex;
    align-items: center;
}

.auth {
    font-size: 20px;
    margin-right: 24px;
    cursor: pointer;
    color: #000;
    text-decoration: none;
}

.favorite {
    margin-right: 8px;
}
</style>
