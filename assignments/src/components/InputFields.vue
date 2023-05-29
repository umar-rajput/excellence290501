<template>

    <div class="input-fields">

        <div class="email">
            <slot name="email"/>
        </div>
        <div class="name">
            <slot name="name"/>
        </div>
        <div class="dob">
            <slot name="dob"/>
        </div>
        <div class="password">
            <slot name="password"/>
        </div>
        <div class="confirm">
            <slot name="confirm"/>
        </div>
        <div class="checkbox">
            <slot name="checkbox"/>
        </div>
        <div class="submit">
            <slot name="submit"/>
        </div>

    </div>
    
</template>

<script>

export default {
    name:'InputFields',
    data() {
        
    },
}
</script>

<style scoped>



</style>