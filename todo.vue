 const app = new Vue({
            el: '#app',
            data: {
                text: '',
                onlyComplited: false,
                onlyInProgress: false,
                todos: [
                    { text: 'Learn JavaScript', isDone: true },
                    { text: 'Learn Vue', isDone: false },
                    { text: 'Get a job offer', isDone: false }
                ]
            },
            methods: {
                newTodo: function () {
                    const inputValue = document.getElementById("createTask").value
                    if (inputValue != '' || inputValue === null) {
                        this.todos.push({
                            text: inputValue,
                            isDone: false
                        })
                    }
                    document.getElementById("createTask").value = ""
                },
                removeTodo: function (index) {
                    this.todos.splice(index, 1)
                },
                markAsDone: function (index) {
                    if (this.todos[index]) {
                        this.todos[index].isDone = !this.todos[index].isDone
                    }
                },
                completedTodo: function () {
                    this.onlyComplited = true
                    this.onlyInProgress = false
                },
                inProgress: function () {
                    this.onlyComplited = false
                    this.onlyInProgress = true
                },
                allTodos: function () {
                    this.onlyComplited = false
                    this.onlyInProgress = false
                }
            },computed: {
                filteredList: function () {
                    const search = this.text;
                    let comp = this.onlyComplited
                    let prog = this.onlyInProgress
                    return this.todos.filter(function (elem) {

                        if (search === '') return true;
                        else return elem.text.indexOf(search) > -1;
                    }).filter(function (elem) {
                        if (!comp) {
                            return true
                        } else return elem.isDone
                    }).filter(function (elem){
                        if (!prog) {
                            return true
                        } else return !elem.isDone
                    })
                },
                allTodo() {
                    return this.todos.length;
                },
                doneTodo() {
                    let doneTodos = this.todos.filter(todo => { return todo.isDone === true }).length;
                    return doneTodos
                },
                inProgressTodo() {
                    let inProgress = this.todos.filter(todo => { return todo.isDone === false }).length;
                    return inProgress
                },
                progress() {
                    if (this.doneTodo > 0) {
                        return Math.floor(this.doneTodo * 100 / this.allTodo);
                    } else {
                        return percents = 0
                    }
                }
            }
        })