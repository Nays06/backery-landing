<template>
    <div class="customers-slider">
        <Title :title="'OUR CUSTOMERS'" />

        <div class="slider-container">
            <div class="slider-track" :style="trackStyle">
                <div class="slide" v-for="(slideGroup, index) in slideGroups" :key="index" :style="slideStyle">
                    <div class="cards" :class="{ 'two-cards': slideGroup.length === 2 }">
                        <div class="card" v-for="(card, cardIndex) in slideGroup" :key="cardIndex">
                            <div class="user-info">
                                <div class="avatar">
                                    <img :src="card.avatar" alt="avatar">
                                </div>
                                <div class="dop">
                                    <div class="name">{{ card.name }}</div>
                                    <div class="location">{{ card.location }}</div>
                                </div>
                            </div>
                            <div class="description">{{ card.description }}</div>
                        </div>
                        <div v-if="slideGroup.length === 2" class="card-placeholder"></div>
                    </div>
                </div>
            </div>

            <button class="slider-nav slider-prev" @click="prevSlide">‹</button>
            <button class="slider-nav slider-next" @click="nextSlide">›</button>

            <div class="slider-indicators">
                <button v-for="index in slideGroups.length" :key="index" class="indicator"
                    :class="{ active: currentSlide === index - 1 }" @click="goToSlide(index - 1)"></button>
            </div>

            <div class="slider-add">
                <button @click="openModal">Добавить отзыв</button>
            </div>
        </div>

        <div v-if="isModalOpen" class="modal-overlay" @click="closeModal">
            <div class="modal-content" @click.stop>
                <button class="modal-close" @click="closeModal">×</button>
                <h2>Добавить отзыв</h2>
                <form @submit.prevent="submitReview" class="review-form">
                    <div class="form-group">
                        <label for="name">Имя:</label>
                        <input type="text" id="name" v-model="newReview.name" required placeholder="Введите ваше имя">
                    </div>

                    <div class="form-group">
                        <label for="location">Местоположение:</label>
                        <input type="text" id="location" v-model="newReview.location" required
                            placeholder="Введите ваше местоположение">
                    </div>

                    <div class="form-group">
                        <label for="description">Отзыв:</label>
                        <textarea id="description" v-model="newReview.description" required rows="5"
                            placeholder="Напишите ваш отзыв"></textarea>
                    </div>

                    <div class="form-group">
                        <label for="avatar">Аватар (URL):</label>
                        <input type="url" id="avatar" v-model="newReview.avatar"
                            placeholder="Введите URL аватара (опционально)">
                    </div>

                    <div class="form-actions">
                        <button type="button" @click="closeModal" class="btn-cancel">Отмена</button>
                        <button type="submit" class="btn-submit">Добавить отзыв</button>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
import Title from './Title.vue';

export default {
    data() {
        return {
            currentSlide: 0,
            isModalOpen: false,
            newReview: {
                name: '',
                location: '',
                description: '',
                avatar: ''
            },
            customers: [
                {
                    avatar: '/img/main/avatar.png',
                    name: 'Khutiev A.',
                    location: 'Russia, Republic of Ingushetia',
                    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco.'
                },
                {
                    avatar: '/img/main/avatar2.png',
                    name: 'Ivanov B.',
                    location: 'Russia, Moscow',
                    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco.'
                },
                {
                    avatar: '/img/main/avatar3.png',
                    name: 'Petrov C.',
                    location: 'Russia, Saint Petersburg',
                    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco.'
                },
            ]
        }
    },
    components: {
        Title
    },
    computed: {
        slideGroups() {
            const customersFromLocalStorage = localStorage.getItem('reviews') && JSON.parse(localStorage.getItem('reviews')).length ? JSON.parse(localStorage.getItem('reviews')) : []
            let customers = customersFromLocalStorage.concat(this.customers)

            const uniqueCustomers = [];
            const seen = new Set();

            for (const customer of customers) {
                const key = `${customer.name}|${customer.location}|${customer.description}`;
                if (!seen.has(key)) {
                    seen.add(key);
                    uniqueCustomers.push(customer);
                }
            }

            if (uniqueCustomers.length <= 3) {
                return [uniqueCustomers];
            }

            const groups = [];
            const cardsPerSlide = 3;

            for (let i = 0; i < uniqueCustomers.length; i += cardsPerSlide) {
                groups.push(uniqueCustomers.slice(i, i + cardsPerSlide));
            }

            return groups;
        },
        trackStyle() {
            return {
                transform: `translateX(-${this.currentSlide * 100}%)`
            }
        },
        slideStyle() {
            return {
                width: '100%'
            }
        }
    },
    methods: {
        nextSlide() {
            this.currentSlide = (this.currentSlide + 1) % this.slideGroups.length
        },
        prevSlide() {
            this.currentSlide = this.currentSlide === 0 ? this.slideGroups.length - 1 : this.currentSlide - 1
        },
        goToSlide(index) {
            this.currentSlide = index
        },
        openModal() {
            this.isModalOpen = true;
        },
        closeModal() {
            this.isModalOpen = false;
            this.resetForm();
        },
        resetForm() {
            this.newReview = {
                name: '',
                location: '',
                description: '',
                avatar: ''
            };
        },
        submitReview() {
            const newReview = {
                avatar: this.newReview.avatar || '/img/main/avatar4.png',
                name: this.newReview.name,
                location: this.newReview.location,
                description: this.newReview.description
            }

            this.customers.unshift(newReview);

            this.closeModal();
            this.currentSlide = 0;

            if (localStorage.getItem('reviews') && JSON.parse(localStorage.getItem('reviews'))?.length) {
                let reviews = JSON.parse(localStorage.getItem('reviews'))
                reviews.unshift(newReview)
                localStorage.setItem('reviews', JSON.stringify(reviews))
            } else {
                localStorage.setItem('reviews', JSON.stringify([newReview]))
            }
        }
    }
}
</script>

<style scoped>
.customers-slider {
    width: 100%;
    overflow: hidden;
}

.slider-container {
    position: relative;
    width: 94%;
    margin: 0 auto;
    overflow: hidden;
}

.slider-track {
    display: flex;
    transition: transform 0.3s ease;
}

.slide {
    flex: 0 0 100%;
    box-sizing: border-box;
}

.cards {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 20px;
    width: 94%;
    margin: auto;
}

.cards.two-cards {
    justify-content: flex-start;
}

.card {
    padding: 50px;
    max-width: calc(33.333% - 20px);
    background-color: #fff;
    border-bottom: 5px solid #FF9AE96d;
    border-radius: 15px;
    box-sizing: border-box;
    flex: 1;
    min-width: 0;
    height: -webkit-fill-available;
}

.card-placeholder {
    flex: 1;
    max-width: calc(33.333% - 20px);
    visibility: hidden;
    pointer-events: none;
}

.avatar {
    border-radius: 50%;
    overflow: hidden;
    width: 70px;
    height: 70px;
}

.avatar img {
    width: 100%;
    height: 100%;
    object-fit: cover;
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
    line-height: 1.4;
}

.slider-nav {
    position: absolute;
    top: 30%;
    transform: translateY(-50%);
    background: rgba(255, 255, 255, 0.8);
    border: none;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    font-size: 20px;
    cursor: pointer;
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: background-color 0.3s ease;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
}

.slider-nav:hover {
    background: rgba(255, 255, 255, 1);
}

.slider-prev {
    left: 10px;
}

.slider-next {
    right: 10px;
}

.slider-indicators {
    display: flex;
    justify-content: center;
    margin-top: 20px;
    gap: 10px;
}

.indicator {
    width: 12px;
    height: 12px;
    border-radius: 50%;
    border: none;
    background: #ccc;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

.indicator.active {
    background: #FF9AE9;
}

.slider-add {
    width: 100%;
    display: flex;
    justify-content: center;
    margin-top: 40px;
}

.slider-add button {
    background: #FF9AE9;
    padding: 12px 24px;
    color: #fff;
    border: none;
    cursor: pointer;
    font-size: 18px;
    border-radius: 5px;
    transition: background-color 0.3s ease;
}

.slider-add button:hover {
    background: #ff7ad4;
}

.modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1000;
}

.modal-content {
    background: white;
    padding: 30px;
    border-radius: 15px;
    width: 90%;
    max-width: 500px;
    max-height: 90vh;
    overflow-y: auto;
    position: relative;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

.modal-close {
    position: absolute;
    top: 15px;
    right: 15px;
    background: none;
    border: none;
    font-size: 24px;
    cursor: pointer;
    color: #666;
    width: 30px;
    height: 30px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    transition: background-color 0.3s ease;
}

.modal-close:hover {
    background: #f0f0f0;
}

.modal-content h2 {
    margin-bottom: 20px;
    color: #333;
    text-align: center;
}

.review-form {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.form-group {
    display: flex;
    flex-direction: column;
}

.form-group label {
    margin-bottom: 5px;
    font-weight: 600;
    color: #333;
}

.form-group input,
.form-group textarea {
    padding: 10px;
    border: 2px solid #e0e0e0;
    border-radius: 5px;
    font-size: 16px;
    transition: border-color 0.3s ease;
}

.form-group input:focus,
.form-group textarea:focus {
    outline: none;
    border-color: #FF9AE9;
}

.form-actions {
    display: flex;
    gap: 10px;
    justify-content: flex-end;
    margin-top: 20px;
}

.btn-cancel {
    padding: 10px 20px;
    background: #f0f0f0;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
    transition: background-color 0.3s ease;
}

.btn-cancel:hover {
    background: #e0e0e0;
}

.btn-submit {
    padding: 10px 20px;
    background: #FF9AE9;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
    transition: background-color 0.3s ease;
}

.btn-submit:hover {
    background: #ff7ad4;
}

@media (max-width: 1024px) {
    .card {
        padding: 40px 30px;
    }

    .name {
        font-size: 22px;
    }

    .location {
        font-size: 16px;
    }
}

@media (max-width: 768px) {
    .slider-container {
        width: 100%;
    }

    .cards {
        flex-direction: column;
        gap: 15px;
    }

    .cards.two-cards {
        justify-content: flex-start;
    }

    .card,
    .card-placeholder {
        max-width: 100%;
        width: 100%;
    }

    .card {
        width: 100%;
        padding: 30px 20px;
    }

    .user-info {
        flex-direction: column;
        text-align: center;
    }

    .dop {
        margin-left: 0;
        margin-top: 15px;
    }

    .name {
        font-size: 20px;
    }

    .location {
        font-size: 16px;
    }

    .slider-nav {
        width: 35px;
        height: 35px;
        font-size: 18px;
    }

    .modal-content {
        padding: 20px;
        margin: 20px;
    }

    .form-actions {
        flex-direction: column;
    }
}

@media (max-width: 480px) {
    .card {
        padding: 20px 15px;
    }

    .avatar {
        width: 60px;
        height: 60px;
    }

    .name {
        font-size: 18px;
    }

    .location {
        font-size: 14px;
    }

    .description {
        font-size: 14px;
    }

    .slider-nav {
        display: none;
    }

    .modal-content {
        padding: 15px;
    }
}
</style>