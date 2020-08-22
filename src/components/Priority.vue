<template>
    <div class="priority-box">
    <h2 class="priority-box__title">Priority</h2>

        <div class="priority-item" v-for="(prItem, index) in priorityItems" :key="index">
            <label :for="prItem" :name="prItem" >{{prItem}}</label>
            <input
                type="radio"
                :id="prItem"
                :value="prItem"
                v-model="itemChecked"
                :is-checked="isChecked"
                />
        </div>
    </div>
</template>

<script>
export default {
    // получаем данные от родителя App
    props: {
        priorityItems: {
            type: Array,
            required: true
        },
        checked: {
            type: String,
            default: 'Standart'
        },
    },
    data() {
        return {
            // создаём локальную переменную для избежания мутации
            itemChecked: this.checked
        }
    },
    computed: {
        // передаём вычесляемые свойства выборки родителю
        isChecked () {
            this.$emit('is-checked', this.itemChecked)
        }
    }
}
</script>

<style lang="scss">
    .priority-box {
        z-index: 10;
        position: absolute;
        right: 3%;
        top: 4% !important;
        display: flex;
        &__title {
            position: absolute;
            top: -75%;
            left: 50%;
            transform: translate(-50%);
            font-size: 16px;
        }
    }
    .priority-item {
        width: 60px;
        &:nth-child(3) {
            border: 0;
        }
        input {
            margin: 0;
        }
        label {
            font-size: 12px;
            &[name="Standart"] {
                font-weight: bold;
                color: green;
            }
            &[name="Great"] {
                font-weight: bold;
                color: gold;
            }
            &[name="Important"] {
                font-weight: bold;
                color: red;
            }
        }
    }
</style>