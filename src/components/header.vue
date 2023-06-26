<template>
    <header>
        <h1>
            Simple Camera Orbit
        </h1>
        
    </header>
    <Button />

</template>


<script>
import Button from './button'

export default {
    name: 'header',
    components: {
        Button,
    }
}

</script>


<style scoped>
    header {
        display: flex;
        align-items: center;
        margin-bottom: 20px;
    }

</style>