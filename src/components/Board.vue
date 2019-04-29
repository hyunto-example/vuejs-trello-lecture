<template>
    <div>
        Board
        <div>bid: {{bid}}</div>
    </div>
</template>

<script>
export default {
    created() {
        this.bid = this.$route.params.bid
    },
    data() {
        return {
            bid: 0
        }
    },
}
</script>

<style>

</style>
