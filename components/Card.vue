<template>
    <view class="card">
        <text class="name">{{student.name}}</text>
        <text class="email">{{student.email}}</text>
        <text class="graduation" :style="{
            textAlign: 'right'
        }">Class of {{student.graduation}}</text>
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
.card {
    border-width: 2px;
    border-color: gray;
    border-radius: 5px;
    padding: 15px;
    margin-top: 30px;
    position: relative;
}

.name {
    font-weight: 500;
    font-size: 20px;
}

.email {
    color: gray;
    font-size: 10px;
    font-weight: 200;
}

.graduation {
    font-size: 10px;
    font-weight: 200;
    margin-top: 30px;
}
</style>