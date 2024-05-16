<template>
    <div class="my-3">
        <ul class="list-group">
            <li class="list-group-item" 
            v-for="(todo,index) in todos" 
            :key="index">
                <div class="row">
                    <div class="col">
                        <span v-if="todo.isDone == true"> 
                            <del>{{ todo.activity }}</del>
                        </span>
                        <span v-else>
                            {{ todo.activity }}
                        </span>
                    </div>
                    <div class="col-auto">
                        <button @click="done(index)" 
                        class="btn btn-info text-light">
                            Done
                        </button>
                    </div>
                    <div class="col-auto">
                        <button @click="deletetodo(index)" 
                        class="btn btn-danger">
                            x
                        </button>
                    </div>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    props: {
        todos: {
            type: Array,
            default: {}
        }
    },
    methods: {
        deletetodo(index){
            this.$emit('deletetodo', index);
        },
        done(index){
            this.$emit('donetodo', index);
        }
    }
}
</script>