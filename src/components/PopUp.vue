<template>
    <div class="popup-wrapper" 
        v-bind:class="handlePopUpClass">
        <div class="rules">
            <p class="title">Rules</p>
            <p>1. If you get dice number 1, you will lose your turn and your points.</p>
            <p>2. Whoever gets to the final point first is the winner.</p>
            <button 
                class="confirm"
                v-on:click="confirmToPlay">
                Confirm
            </button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'popUp',
    props: {
        isPopUpOpen: { type: Boolean, default: false},
    },
    data() {
        return {
        }
    },
    computed: {
        handlePopUpClass() {
            return {
                'popup-open' : this.isPopUpOpen
            };
        }
    },
    methods : {
        confirmToPlay() {      
            console.log('ok');
            this.$emit('confirmToPlay');
        }
    }
}
</script>

<style scoped>
    .popup-wrapper {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        opacity: 0;
        visibility: hidden;
        transition: all .25s ease;
        border-radius: 10px;

    }
    .popup-wrapper.popup-open {
        opacity: 1;
        visibility: visible;
    }

    .rules {
        position: absolute;
        top: 50%;
        left: 50%;
        height: 100%;
        width: 100%;
        background-color: rgba(109, 105, 105, .9);
        opacity: 1;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        padding: 30px;
        color: white;
        transition: all .25s ease;
    }
    .popup-wrapper .rules {
        transform: translate(-50%,-50%) scale(1);
    }
    .popup-wrapper.popup-open .rules {
        transform: translate(-50%,-50%) scale(1.2);
    }
    .title {
        font-size: 50px;
        width: 100%;
        text-align: center;
    }
    h3 {
        text-align: center;
    }
    p {
        font-size: 32px;
        padding: 10px;
        width: 80%;
    }
    button {
        border: none;
        background-color: rgb(197, 196, 196);
        border-radius: 10px;
        font-size: 18px;
        align-self: center;
        margin-top: 20px;
        padding: 10px;
        width: 20%;
        letter-spacing: 1px;
        transition: all .25s ease;
        cursor: pointer;
    }
    button:hover {
        letter-spacing: 4px;
        background-color: rgb(243, 243, 243);
    }
</style>
