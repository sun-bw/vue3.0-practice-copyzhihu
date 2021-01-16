<template>
    <div class="row">
        <div v-for="column in colunmList" :key="column.id" class="col-4 mb-4">
            <div class="card h-100 shadow-sm">
                <div class="card-body text-center">
                    <img :src="column.avatat" :alt="column.title" class="rounded-circle border border-light w-25 my-3">
                    <h5 class="card-title">{{column.title}}</h5>
                    <p class="card-text text-left">{{column.description}}</p>
                    <a href="#" class="btn btn-outline-primary">进入专栏</a>
                </div>
            </div>
        </div>
    </div>
</template>
<script lang="ts">
import { defineComponent, PropType, computed } from 'vue'
export interface ColumnProps {
    id: number;
    title: string;
    avatat?: string;
    description: string;
}
export default defineComponent({
    name: 'ColumnList',
    props: {
        list: {
            //把一个构造函数，断言为一个类型
            //好处：属性自动补全
            type: Array as PropType<ColumnProps[]>,
            required: true
        }
    },
    setup(props) {
        const colunmList = computed(() => {
            return props.list.map(column => {
                if(!column.avatat) {
                    column.avatat = require('@/assets/column.jpg')
                }
                return column
            })
        })
        return {
            colunmList
        }
    }
})
</script>
<style>

</style>