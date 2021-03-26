<template>
  <div>
    <header>
      <h1>Todo-app</h1>
    </header>
    <label class="newTodoWrapper">
      <input class="newTodo" v-model="newTask" placeholder="Your todo..." @keyup.enter="add"/> <button class="submit" variant="primary" @click="add">Add</button>
    </label>
    <section class="Column" id="todo">
      <div class="head"></div>
      <h1>🗒️ Todo</h1>
      <draggable class="Column-fix" :list="arrTodo" group="tasks" item-key="id">
        <template #item="{element}">
          <div class="ticket">
            <p>{{element.name}}</p>
          </div>
        </template>
      </draggable>
    </section>
    <section class="Column" id="in-progress">
      <div class="head"></div>
      <h1>💻 In progress</h1>
      <draggable class="Column-fix" :list="arrInProgress" group="tasks" item-key="id">
        <template #item="{element}">
          <div class="ticket">
            <p>{{element.name}}</p>
          </div>
        </template>
      </draggable>
    </section>
    <section class="Column" id="review">
      <div class="head"></div>
      <h1>🖍 Review</h1>
      <draggable class="Column-fix" :list="arrReview" group="tasks" item-key="id">
        <template #item="{element}">
          <div class="ticket">
            <p>{{element.name}}</p>
          </div>
        </template>
      </draggable>
    </section>
    <section class="Column" id="done">
      <div class="head"></div>
      <h1>🚀 Done</h1>
      <draggable class="Column-fix" :list="arrDone" group="tasks" item-key="id">
        <template #item="{element}">
          <div class="ticket">
            <p>{{element.name}}</p>
          </div>
        </template>
      </draggable>
    </section>
  </div>
</template>

<script>

import "./assets/card.scss"
import "./assets/mainstyle.scss"
import draggable from "vuedraggable";

export default {
  name: "App",
  components: {
    draggable,
  },
  data() {
    return {
      // for new tasks
      newTask: "",
      // 4 arrays to keep track of our 4 statuses
      arrTodo: [
        { name: "Gör dina saker!" },
        { name: "Fixa denna sida :(" },
        { name: "Fixa buggar" },
        { name: "Publisera" }
      ],
      arrInProgress: [],
      arrReview: [],
      arrDone: []
    };
  },
  methods: {
    //add new tasks method
    add: () => {
      if (this.newTask) {
        this.arrBackLog.push({ name: this.newTask });
        this.newTask = "";
      }
    }
  }
};
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Lato&display=swap');
  * {
    padding: 0;
    margin: 0;
  }
  html, body {
    width: 100%;
    height: 100vh
  }
  body {
    background-color: #EAF6FF;
  }
  header h1 {
    font-size: 5vh;
    color: #171717;
    font-family: 'Lato', sans-serif;
    font-style: normal;
    position: absolute;
    top: 2vh;
    left: 1.5vw;
    width: 20vw;
  }

  .ticket {
  position: relative;
  left: 50%;
  transform: translateX(-50%);
  cursor: grab;
  width: 90%;
  min-height: 2.5vh;
  background-color: white;
  padding: 1vh;
  border-radius: 1vh;
  margin-bottom: 4vh;
}

.ticket p {
  font-family: 'Lato', sans-serif;
  font-size: 2.3vh;
}

.ticket .profile {
  margin-top: 1.5vh;
  height: 3.5vh;
  width: 3.5vh;
  border-radius: 50%;
}

.newTodoWrapper {
  position: relative;
  top: 5vh;
  left: 75vw;
}

.newTodo {
  height: 4vmin;
  width: 25vmin;
  padding: 0.5vmin;
  border-radius: 0.5vh;
  border: none;
}

.submit {
  border: none;
  border-radius: 0.5vh;
  height: 5vmin;
  width: 10vmin;
  margin-left: 2vmin;
  background-color: #3D5A6C; 
}

</style>
