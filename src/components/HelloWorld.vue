<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <ul class="kanban-board">
      <li class="status">
        <ul class="ul01">
          <li class="li00">PBI</li>
          <li
            v-for="(status, index) in statusses"
            :key="status.id"
            :class="'li0' + (index + 1)"
          >
            {{ status.name }}
          </li>
        </ul>
      </li>
      <li class="tasks">
        <ul v-for="pbi in pbis" :key="pbi.id">
          <li class="li00">
            <div class="pbi">
              <h3>{{ pbi.title }}</h3>
            </div>
          </li>
          <li
            v-for="(status, index) in statusses"
            :class="'li0' + (index + 1)"
            :key="status.id"
          >
            <div
              v-for="task in pbi.tasks.filter(t => t.status == status.id)"
              :key="task.id"
              class="task"
            >
              <h3>{{ task.title }}</h3>
              <p>{{ task.description }}</p>
            </div>
          </li>
        </ul>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

type Status = {
  id: number;
  name: string;
};
type PBI = {
  id: number;
  title: string;
  tasks: Array<Task>;
};
type Task = {
  id: number;
  title: string;
  description: string;
  assignee: string | null;
  status: number;
  point: number | null;
};

@Component
export default class HelloWorld extends Vue {
  @Prop() private msg!: string;
  private statusses: Array<Status> = [
    { id: 0, name: "TODO" },
    { id: 1, name: "DOING" },
    { id: 2, name: "REVIEW" },
    { id: 3, name: "DONE" }
  ];
  private pbis: Array<PBI> = [
    {
      id: 0,
      title: "一つ目",
      tasks: [
        {
          id: 0,
          title: "あああああ",
          description: "あああああ",
          assignee: null,
          status: 0,
          point: 1.0
        },
        {
          id: 1,
          title: "あああああ",
          description: "あああああ",
          assignee: "山田一浪",
          status: 1,
          point: 0.5
        },
        {
          id: 2,
          title: "あああああ",
          description: "あああああ",
          assignee: "山田一浪",
          status: 3,
          point: 1.0
        }
      ]
    },
    {
      id: 1,
      title: "二つ目",
      tasks: [
        {
          id: 3,
          title: "2あああああ",
          description: "あああああ",
          assignee: null,
          status: 0,
          point: 1.0
        },
        {
          id: 4,
          title: "2あああああ",
          description: "あああああ",
          assignee: null,
          status: 0,
          point: 2.0
        },
        {
          id: 5,
          title: "2あああああ",
          description: "あああああ",
          assignee: "山田一浪",
          status: 2,
          point: 1.0
        },
        {
          id: 6,
          title: "2あああああ",
          description: "あああああ",
          assignee: "山田一浪",
          status: 3,
          point: 1.0
        }
      ]
    },
    {
      id: 2,
      title: "三つ目",
      tasks: [
        {
          id: 7,
          title: "3あああああ",
          description: "あああああ",
          assignee: null,
          status: 0,
          point: 1.0
        },
        {
          id: 8,
          title: "3あああああ",
          description: "あああああ",
          assignee: null,
          status: 0,
          point: 2.0
        },
        {
          id: 9,
          title: "3あああああ",
          description: "あああああ",
          assignee: "山田一浪",
          status: 2,
          point: 1.0
        },
        {
          id: 10,
          title: "3あああああ",
          description: "あああああ",
          assignee: "山田一浪",
          status: 2,
          point: 1.0
        }
      ]
    },
    {
      id: 3,
      title: "四つ目",
      tasks: [
        {
          id: 11,
          title: "4あああああ",
          description: "あああああ",
          assignee: null,
          status: 0,
          point: 1.0
        },
        {
          id: 12,
          title: "4あああああ",
          description: "あああああ",
          assignee: null,
          status: 0,
          point: 2.0
        },
        {
          id: 13,
          title: "4あああああ",
          description: "あああああ",
          assignee: "山田一浪",
          status: 2,
          point: 1.0
        },
        {
          id: 14,
          title: "4あああああ",
          description: "あああああ",
          assignee: "山田一浪",
          status: 2,
          point: 1.0
        }
      ]
    }
  ];
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
ul {
  list-style-type: none;
  padding-left: 0px;
}
li {
  margin-left: 5px;
  margin-right: 5px;
}
ul.kanban-board {
  width: 100%;
}
ul.kanban-board ul {
  display: flex;
}
ul.kanban-board ul.ul01 {
  border-bottom: 0;
}
ul.kanban-board ul li {
  flex-grow: 1;
  width: 25%;
  box-sizing: border-box;
  border-top: 1px solid #ccc;
  border-right: 1px solid #ccc;
  border-left: 1px solid #ccc;
  text-align: center;
  padding: 10px;
}
.tasks ul:last-child li {
  border-bottom: 1px solid #ccc;
}
ul.kanban-board ul.ul01 li {
  background-color: #ffeaea;
}
ul.kanban-board ul.ul01 li.li00 {
  background-color: #ff9191;
}
.pbi {
  margin: 1px;
  border: 1px solid #ccc;
}
.task {
  margin: 1px;
  border: 1px solid #ccc;
}
</style>
