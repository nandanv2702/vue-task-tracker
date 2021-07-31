<template>
    <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Task</label>
      <input type="text" v-model="text" name="text" placeholder="Add Task" />
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <div class="datetime">
          <input
        type="date"
        v-model="day"
        name="day"
        placeholder="Add Day"
      />
      <input
        type="time"
        v-model="time"
        name="time"
        placeholder="Add Day & Time"
      />
      </div>
      
    </div>
    <div class="form-control form-control-check">
      <label>Set Reminder</label>
      <input type="checkbox" v-model="reminder" name="reminder" />
    </div>

    <input type="submit" value="Save Task" class="btn btn-block" />
  </form>
</template>

<script>
export default {
    name: 'AddTask',
    data() {
      const today = new Date()
        return {
            text: 'Add a Task!',
            day: today.getFullYear(),
            time: '',
            reminder: true
        }
    },
    methods: {
        onSubmit(e){
            e.preventDefault()

            if(!this.text){
                alert("Please add a task")
            } else {
                const newTask = {
                    id: Math.floor(Math.random() * 100000),
                    text: this.text,
                    day: this.day,
                    time: this.time,
                    reminder: this.reminder
                }

                console.log(`new task is ${JSON.stringify(newTask)}`)

            this.text = ''
            this.day = ''
            this.reminder = false

            let oldItems = Array(localStorage.getItem("todoItems"))
            
            let newItems = []
            if(oldItems[0] == ""){
                newItems = [newTask]
            } else {
                let oldParsedItems = JSON.parse(oldItems)
                newItems = [...oldParsedItems, newTask]
            }

            console.log(newItems)

            localStorage.setItem("todoItems", JSON.stringify(newItems))

            this.$emit('add-task', newTask);
            }


        }
    }
}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px 0;
  padding: 3px 7px;
  font-size: 17px;
  font-family: sans-serif, 'Inter';
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}

.datetime {
    display: flex;
    justify-content: space-between;
}

.datetime input {
    margin-left: 2px;
    margin-left: 2px;
}
</style>