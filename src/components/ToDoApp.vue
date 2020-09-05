<template>
  <div id="app">
      <h4 class="bg-primary text-white text-center p-2">
          {{name}}'s To Do List
      </h4>
      <div class="container-fluid p-4">
          <div class="row">
              <div class="col font-weight-bold">Task</div>
              <div class="col-2 font-weight-bold">Done</div>
          </div>
          <div class="row" v-for="t in filteredTasks" :key="t.action">
              <div class="col">{{ t.action }}</div>
              <div class="col-2 text-center">
                  <input type="checkbox" v-model="t.done"  class="form-check-input">
                  {{ t.done }}
              </div>
          </div>
          <div class="row py-2">
              <div class="col">
                  <input v-model="newItemText" class="form-control">
              </div>
              <div class="col-2">
                  <button class="btn btn-primary" @click="addNewTodo">Add</button>
              </div>
          </div>
          <div class="row bg-secondary py-2 mt-2 text-white">
              <div class="col text-center">
                  <input type="checkbox" v-model="hideCompleted" class="form-check-input">
                  <label class="form-check-label font-weight-bold">
                      Hide completed tasks
                  </label>
              </div>
          </div>
      </div>
  </div>
</template>

<script>
    export default {
        name: "ToDoApp",
        data() {
            return {
                name: "Mariusz",
                tasks: [
                    { action: "Kup kwiatki", done: false },
                    { action: "Odbierz buty", done: true },
                    { action: "Kup bilety do kina", done: false },
                    { action: "Zadzwoń do Piotra", done: false },

                ],
                hideCompleted: true,
                newItemText: ""
            }
        },
        computed: {
            filteredTasks() {
                return this.hideCompleted ? this.tasks.filter( t => !t.done ) : this.tasks;
            }
        },
        methods: {
            addNewTodo() {
                this.tasks.push({
                    action: this.newItemText,
                    done: false
                });
                localStorage.setItem("todos",JSON.stringify(this.tasks));
                this.newItemText = "";
            }
        },
        
    }
</script>

<style lang="css" scoped>
</style>