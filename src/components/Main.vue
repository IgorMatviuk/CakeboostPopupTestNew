<template>
    <div>
        <div v-if="IsPushMessage" class="push-message">
            <p>You have successfully subscribed to the newsletter</p>
        </div>
        <div v-if="IsErrorMessage" class="push-message m-red">
            <p>You have already subscribed to the newsletter</p>
        </div>
        <div class="popup__container__btn">
            <button @click="showPopup">Open popup</button>
        </div>
        <div v-if="IsPopupShow" class="popup-overlay">
            <div class="popup">
                <div @click="hidePopup" class="popup-close">
                    <img src="../assets/close.svg" alt="">
                </div>
                <div class="popup__container">
                    <div class="popup__container__discount">
                        10%<p>off</p>
                    </div>
                    <h1>your first order</h1>
                    <div class="popup__container__line"></div>
                    <div class="popup__container__description">
                        Subscrive to recieve 10% off promocode plus exclusive offers and deals
                    </div>
                    <div class="popup__container__inp-title">
                        Email-adress
                    </div>
                    <div class="popup__container__input">
                        <input type="email" placeholder="email" v-model="email">
                    </div>
                    <div class="popup__container__btn">
                        <button :disabled="btnToggle" @click="newEmail">Subscribe!</button>
                    </div>
                    <div class="popup__container__pp">
                        <label class="custom-checkbox">
                            <input class="hidden-checkbox" type="checkbox" v-on:click="btnToggle = !btnToggle">
                            <div class="checkbox"></div>
                        </label>
                        <p>I’m agree with privacy policy</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            IsPopupShow: false,
            btnToggle: true,
            email: '',
            arrayEmails: [],
            IsPushMessage: false,
            IsErrorMessage: false
        }
    },
    computed: {

    },
    methods: {
        showPopup() {
            this.IsPopupShow = true;
        },
        hidePopup() {
            this.IsPopupShow = false;
        },
        activeSub() {
            this.btnToggle = false;
        },
        newEmail() {

            if (this.arrayEmails.includes(this.email) === false) {
                this.arrayEmails.push(this.email)
                console.log(this.arrayEmails)
                this.email = ''
                this.IsPushMessage = true
                setTimeout(() => {
                    this.IsPushMessage = false
                }, 4000);
            }
            if (this.arrayEmails.includes(this.email) === true) {
                console.log('error')
                this.email = ''
                
                this.IsErrorMessage = true
                setTimeout(() => {
                    this.IsErrorMessage = false
                }, 4000);
            }
        }
    }
}
</script>
  
<style lang="scss">
body {
    display: flex;
    justify-content: center;
    align-items: center;
}

.popup-overlay {
    position: fixed;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 9999;
    top: 0;
    left: 0;
}

.popup {
    display: flex;
    position: relative;
    background-image: url(../assets/Group-2.webp);
    background-repeat: no-repeat;
    background-position: right;
    width: 864px;
    height: 502px;
    background-color: #FFFFFF;
    box-shadow: 0px 8px 20px rgba(68, 75, 77, 0.15);
    border-radius: 8px;
    font-family: 'Roboto', sans-serif;

    &-close {
        display: flex;
        width: 100%;
        justify-content: flex-end;
        position: absolute;

        img {
            display: flex;
            width: 15px;
            height: 15px;
            margin: 10px 10px 0px 0px;
        }
    }

    &__container {
        display: flex;
        flex-direction: column;
        margin: 40px 0px 40px 31px;
        height: auto;
        align-items: flex-start;

        &__discount {
            display: flex;
            font-weight: 700;
            font-size: 104px;
            line-height: 100%;
            color: #2F3639;

            p {
                margin: 27px 0px -27px 0px;
                font-size: 24px;
            }
        }

        h1 {
            font-weight: 700;
            font-size: 24px;
            line-height: 100%;
        }

        &__line {
            display: flex;
            width: 67px;
            height: 2px;
            background: #C24DFE;
            border-radius: 10px;
            margin: 10px 0px 0px 0px;
        }

        &__description {
            display: flex;
            text-align: left;
            font-weight: 400;
            font-size: 14px;
            line-height: 120%;
            margin: 27px 0px 0px 0px;
            width: 373px;

        }

        &__inp-title {
            font-weight: 700;
            font-size: 12px;
            line-height: 14px;
            color: #828688;
            margin: 40px 0px 0px 0px;
        }

        &__input {
            input {
                width: 297px;
                height: 36px;
                background: #FFFFFF;
                border: 1px solid #D5D7D7;
                border-radius: 6px;
                margin: 8px 0px 0px 0px;
            }
        }

        &__btn {
            margin: 16px 0px 0px 0px;

            button {
                display: flex;
                justify-content: center;
                align-items: center;
                width: 106px;
                height: 40px;
                background: #C24DFE;
                border-radius: 35px;
                font-weight: 700;
                font-size: 12px;
                line-height: 14px;
                color: #FFFFFF;
                border: none;
            }
        }

        &__pp {
            display: flex;
            margin: 15px 0px 0px 0px;

            p {
                font-weight: 500;
                font-size: 14px;
                line-height: 16px;
                color: #595E61;
                margin: 1px 0px 0px 9px;
            }
        }
    }
}

.custom-checkbox input {
    -webkit-appearance: none;
    position: absolute;
}

.checkbox {
    position: relative;
    width: 16px;
    height: 16px;
    content: url(../assets/check.svg);
}

.custom-checkbox input:checked~.checkbox {
    display: block;
}

.custom-checkbox input:checked~.checkbox {
    content: url(../assets/check-active.svg);
}

button:disabled,
button[disabled] {
    background-color: #cccccc;
    color: #ffffff;
}

.push-message {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100px;
    width: auto;
    background-color: #27ae60;
    border-radius: 8px;
    position: absolute;
    z-index: 999999;

    p {
        font-size: 20px;
        color: #ffffff;
        font-family: Roboto;
        margin: 10px 20px 10px 20px;
    }
}

.m-red{
    background-color: #c0392b;
}
</style>
