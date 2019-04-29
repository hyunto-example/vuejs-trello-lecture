<template>
    <div>
        Card
        <div>
            cid: {{cid}}
        </div>
    </div>
</template>

<script>
export default {
    created() {
        this.cid = this.$route.params.cid
    },
    watch: {
        '$route'() {
            this.cid = this.$route.params.cid
        }
    },
    data() {
        return {
            cid: 0
        }
    },
}
</script>

<style>

</style>
