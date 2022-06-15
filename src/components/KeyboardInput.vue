<template lang="">
    <div>
        <textarea class="input-area" :value="areaContent"></textarea>
    </div>
</template>
<script>
export default {
    props: {
        areaContent: {
            type: String,
        },
    }
}
</script>
<style scoped>
.input-area {
    width: 900px;
    border: 2px solid black;
    padding: 10px;
    margin-left: 15px;
    margin-bottom: 20px;
}
</style>