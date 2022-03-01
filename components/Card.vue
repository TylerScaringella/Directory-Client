<template>
    <view class="card">
        <touchable-opacity 
            :on-press="() => openEmail()"
            >
            <text class="name">{{student.name}}</text>
            <text class="email">{{student.email}}</text>
            <text class="graduation" :style="{
                textAlign: 'right'
            }">Class of {{student.graduation}}</text>
        </touchable-opacity>
    </view>
</template>

<script>
import { Linking } from 'react-native'

export default {
    props: {
        student: {}
    },
    methods: {
        openEmail() {
            Linking.openURL(`mailto:${this.student.email}`)
        }
    }
}
</script>

<style>
.card {
    border-width: 2px;
    border-color: gray;
    border-radius: 5px;
    padding: 15px;
    margin-top: 15px;
    margin-bottom: 15px;
    position: relative;
    width: 400px;
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