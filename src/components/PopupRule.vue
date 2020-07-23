<template>
    <div class="wrapper-popup" v-bind:class="getClassPopup">
        <div class="rule">
            <h3>Luật chơi</h3>
            <p>
                Lorem ipsum dolor sit, amet consectetur adipisicing elit. Quas sunt aperiam veniam quod blanditiis nam sint. Maiores totam ullam distinctio pariatur voluptate velit dolor aperiam excepturi eligendi maxime? Rerum, veniam!
            </p>
            <button
                v-on:click="confirm" 
                class="confirm"
            >Bắt đầu</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'popup-rule',
    props: {
        isOpenPopup: {type: Boolean, default: false}
    },
    methods: {
        confirm() {
            // console.log('confirm')
            this.$emit('handleConfirm')
        }
    },
    computed:{
        getClassPopup() {
            return {
                'open-popup': this.isOpenPopup
            }
        }
    },
    data() {
        return {

        }
    }
}
</script>

<style>
    .wrapper-popup{
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background-color: rgba(0, 0, 0,0.4);
        opacity: 0;
        visibility: hidden;
        transition: all .3s ease;
    }
    .wrapper-popup.open-popup {
        opacity: 1;
        visibility: visible;
    }
    .rule{
        position: absolute;
        background-color: #fff;
        width: 300px;
        padding: 20px;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%) scale(1.2);
        font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        transition: all .3s ease;
    }
    .rule h3 {
        margin-bottom: 10px;
    }
    .rule .confirm {
        border: 2px solid #333;
        background-color: #fff;
        padding: 8px 12px;
        margin-top: 20px;
        cursor: pointer;
    }
    .rule .confirm:hover {
        color: #fff;
        background-color: #333;
    }
    .open-popup .rule{
        transform: translate(-50%, -50%) scale(1);
    }
</style>