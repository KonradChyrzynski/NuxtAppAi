<script setup>
const props = defineProps({
  tel: {
    type: String,
    default: () => '700 000 000'
  },
  email: {
    type: String,
    default: () => 'testemail@notascam.com'
  },
});
</script>

<template>
    <div class="info">
        <span>Tel: {{ tel }}</span>
        <span>email: {{ email }}</span>
    </div>
</template>

<style scoped lang="scss">
.info {
    display: flex;
    flex-wrap: wrap;
    width: 100%;
    height: 50px;
    color: white;
    justify-content: center;
    align-items: center;
    font-size: 20px;

    @media (max-width: 465px) {
        height: 100px;
    }

    span {
        margin: 0 10px 0 10px;
    }
}
</style>
