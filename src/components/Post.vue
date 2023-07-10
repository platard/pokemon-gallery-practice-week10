<template>
    <h2>Title</h2>
    <slot></slot>
    <p>Description... {{ myMessage }}</p>
</template>

<script>
export default {
    name: 'Post',
    props: ['myMessage']
}

</script>