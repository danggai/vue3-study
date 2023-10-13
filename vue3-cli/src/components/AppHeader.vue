<template>
    <div>
        <h1> {{ appTitle }} </h1>
        <button @click="changeTitle"> 바꿔잇 </button>
    </div>
</template>

<script>
export default {
    props: [
        'appTitle'
    ],
    methods: {
        changeTitle() {
            this.$emit('change')
        }
    },
    // setup() {
    //     const changeTitle = () => {
    //         this.$emit('change')
    //     }
    //     return { changeTitle }
    // }
}

</script>

<style scoped></style>