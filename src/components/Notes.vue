<template>
    <!-- note list -->
    <div class="notes">
    <!-- получаем все объекты из массива data.notes -->
        <div class="note" :class="{full: !grid}" v-for="(note, index) in notes" :key="index">
            <div class="note-header" :class="{full: !grid}">
                <!-- вывод заголовка data.notes.title -->
                <div :class="'pr--all '+'pr--'+note.priority"></div>
                <p>{{note.title}}</p>
                <p style="cursor: pointer;" @click="noteRemove(index)">x</p>
            </div>
            <div class="note-body" :class="{full: !grid}">
                <!-- вывод описания data.notes.description -->
                <p>{{note.description}}</p>
                <!-- вывод даты data.notes.date -->
                <span>{{note.date}}</span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        notes: {
            type: Array,
            required: true
        },
        grid: {
            type: Boolean,
            required: true
        }
    },
    methods: {
        noteRemove (index) {
            console.log(`Note id - ${index} removed`);
            this.$emit('remove', index)
        }
    },
}
</script>

<style lang="scss">
    .notes {
        display: flex;
        align-items: center;
        justify-content: space-between;
        flex-wrap: wrap;
        padding: 40px 0;
    }

    .note {
        width: 48%;
        padding: 18px 20px;
        margin-bottom: 20px;
        background-color: #ffffff;
        transition: all .25s cubic-bezier(.02,.01,.47,1);
        box-shadow: 0 30px 30px rgba(0,0,0,.02);
        &:hover {
            box-shadow: 0 30px 30px rgba(0,0,0,.04);
            transform: translate(0,-6px);
            transition-delay: 0s !important;
        }
        &.full {
            width: 100%;
            text-align: center;
        }
    }

    .note-header {
        display: flex;
        align-items: center;
        justify-content: space-between;
        h1 {
            font-size: 32px;
        }
        p {
            font-size: 22px;
            color: #402caf;
        }
        .pr--all {
            width: 10px;
            height: 10px;
            border-radius: 50%;
        }
        .pr--Standart {
            background-color: green;
        }
        .pr--Great {
            background-color: gold;
        }
        .pr--Important {
            background-color: red;
        }
        svg {
            margin-right: 12px;
            color: #999999;
            &.active {
                color: #402caf;
            }
            &:last-child {
                margin-right: 0;
            }
        }
        &.full {
            justify-content: center;
            p {
                margin-right: 16px;
                &:last-child {
                    margin-right: 0;
                }
            }
        }
    }

    .note-body {
        p {
            margin: 20px 0;
        }

        span {
            font-size: 14px;
            color: #999999;
        }
    }
</style>
