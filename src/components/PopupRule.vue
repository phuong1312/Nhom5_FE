<template>
    <div class="wrapper-popup" v-bind:class="getClassPopup">
        <div class="rule">
            <h3>Luật Chơi</h3>
            <p>1. Thiết lập điểm cuối cùng và bắt đầu trò chơi</p>
            <br>
            <p>2. Khi người chơi đỗ được 1 nút thì điểm tạm thời sẽ tự trả về 0</p>
            <br>
            <p>3. Nhấp vào nút lưu để lưu lại điểm tạm thời vào và sẽ chuyển lượt cho người chơi tiếp</p>
            <br>
            <p>4. Khi một trong hai người chơi có số điểm đã lưu bằng với số điểm cuối cùng sẽ chiến thắng</p>
            <p style="color: red;">Lưu ý: Điểm để chiến thắng là điểm mà bạn đã lưu từ điểm tạm thời nên hãy nhớ lưu lại nhé!!!</p>
            <button
            v-on:click="confirm"
            class="btn">Đã Hiểu</button>
        </div>
    </div>
</template>

<script>
    export default {
        name: "popup-rule",
        props: {
            isOpenPopup: {type: Boolean, default: false}
        },
        data() {
            return {
                
            }
        },
        methods: {
            confirm() {
                //Truyen event sang App.vue
                console.log("Confirm PopupRule.vue");
                this.$emit("handleConfirm");
            }
        },
        computed: {
            getClassPopup: function() {
                return {
                    'open-popup': this.isOpenPopup
                }
            }
        }
    }
</script>

<style>
.wrapper-popup {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.5);
    opacity: 0;
    visibility: hidden;
    transition: all .3s ease;
    text-align: center;
}
.wrapper-popup.open-popup{
    opacity: 1;
    visibility: visible;
}
.rule {
    width: 500px;
    padding: 20px;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) scale(1.2);
    background-color: #fff;
    position: absolute;
    font-family: Arial, Helvetica, sans-serif;
    transition: all .3s ease;
}
.open-popup .rule{
    transform: translate(-50%, -50%) scale(1);
}
.rule h3 {
    margin-bottom: 10px;
}
.rule .btn{
    cursor: pointer;
    margin-top: 20px;
    padding: 8px 15px;
    border: 2px solid #333;
    background-color: #fff;
    transition: all .3s ease;
}
.rule .btn:hover {
    color: #fff;
    background-color: #333;
}
/* ket hop css3 voi Vuejs de xay dung hieu ung Zoom in va Zom out */
</style>