<template>
    <view>
        <image :style="{width: 200, height: 200}" :source="{uri: `${student.picture}`}" />
        <text>Name: {{student.name}}</text>
        <text>Email: {{student.email}}</text>
    </view>
</template>

<script>
export default {
    props: {
        student: {}
    }
}
</script>

<style>

</style>