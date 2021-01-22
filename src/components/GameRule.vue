<template lang="pug">
    .wrapper-game-rule(:class="getOpenPopupClass")
        .rule
            h3 Game rule
            p Game có 2 xúc xác, chơi theo lượt, 2 người chơi
            p Lựa chọn số điểm để thắng cuộc
            p Người thứ nhất xoay xúc xắc. Số lần xoay không giới hạn. Nếu chấp nhận số điểm thì ấn 'Hold'. Kết thúc lượt chơi.
            p Nếu 1 trong 2 xúc xắc ra số 1, thì mất lượt đồng thời không nhận được điểm ở lượt đó.
            p Bên nào đạt được số điểm đã đặt ra ở ban đầu thì thắng cuộc.
            button.confirm(@click="onAgreeRule") I agree
</template>

<script>
    export default {
        name: "game-rule",
        props: {
            isOpenPopup : {
                type: Boolean,
                default: false,
            }
        },
        data() {
            return {

            }
        },
        computed: {
            getOpenPopupClass: function () {
                return {
                    'open-popup': this.isOpenPopup,
                }
            }
        },
        methods: {
            onAgreeRule() {
                this.$emit('agreeRule')
            }
        },
    }
</script>

<style scoped>
    .wrapper-game-rule {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background-color: #cccccc;
        opacity: 0;
        visibility: hidden;
        transition: all .3s ease;
    }
    .wrapper-game-rule.open-popup {
        opacity: 1;
        visibility: visible;
    }
    .rule {
        position: absolute;
        padding: 20px;
        background-color: #ffffff;
        width: 400px;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%) scale(1.2);
        font-family: Arial, Helvetica, sans-serif;
        transition: all .3s ease;
    }
    .rule h3 {
         margin-bottom: 10px;
    }
    .open-popup .rule {
        transform: translate(-50%, -50%) scale(1);
    }
    .rule .confirm {
        cursor: pointer;
        border: 2px solid #333;
        padding: 8px 15px;
        margin-top: 20px;
        background-color: #fff;
        transition: all .3s ease;
    }
    .rule .confirm:hover {
        color: #fff;
        background-color: #333;
    }
</style>
