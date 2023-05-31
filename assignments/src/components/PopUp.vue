<template>
    <div class="popup">
        <div class="popup-main">
            <slot></slot>
            <!-- <button class="closeButton" v-on:click="TogglePopup()">X</button> -->
            <span class="closeButton" v-on:click="TogglePopup()">X</span>
        </div>
    </div>
</template>

<script>

export default {
    name: 'PopUp',
    props: ['TogglePopup']

}
</script>

<style scoped>
.popup-main {
    position: absolute;
    top: 0px;
    left: 0px;
    right: 0px;
    bottom: 0px;
    z-index: 99;
    display: flex;
    flex-direction: column;
    height: 500px;
    width: 400px;
    margin: auto;
}

.closeButton {
    position: absolute;
    right: -34px;
    top: 32px;
    font-size: 20px;
    cursor: pointer;
}
</style>
