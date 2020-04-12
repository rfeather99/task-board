<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <ul class="kanban-board">
      <li>
        <ul class="header">
          <li class="area group" style="min-width: 200px; max-width: 200px;">
            PBI
          </li>
          <li class="statusses">
            <draggable
              tag="ul"
              v-model="statusses"
              draggable=".status"
              group="statusses"
            >
              <li
                v-for="status in statusses"
                :key="status.id"
                class="area status"
                :style="{
                  'min-width': status.width + 'px',
                  'max-width': status.width + 'px'
                }"
              >
                {{ status.name }}
              </li>
            </draggable>
          </li>
        </ul>
      </li>
      <draggable
        tag="li"
        class="pbis"
        v-model="pbis"
        draggable=".tasks"
        group="pbi"
      >
        <ul v-for="pbi in pbis" :key="pbi.id" class="tasks">
          <li class="area" style="min-width: 200px; max-width: 200px;">
            <div class="pbi">
              <h3>{{ pbi.title }}</h3>
            </div>
          </li>
          <draggable
            tag="li"
            v-for="(status, index) in statusses"
            :class="'area li0' + (index + 1)"
            :key="status.id"
            v-model="pbi.tasks[status.id]"
            draggable=".task"
            group="task"
            :style="{
              'min-width': status.width + 'px',
              'max-width': status.width + 'px'
            }"
          >
            <div
              v-for="task in pbi.tasks[status.id]"
              :key="task.id"
              class="task"
            >
              <h3>{{ task.title }}</h3>
              <p>{{ task.description }}</p>
            </div>
          </draggable>
        </ul>
      </draggable>
    </ul>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import draggable from "vuedraggable";

type Status = {
  id: number;
  name: string;
  width: number;
};
type PBI = {
  id: number;
  title: string;
  tasks: { [key: number]: Array<Task> };
};
type Task = {
  id: number;
  title: string;
  description: string;
  assignee: string | null;
  status: number;
  point: number | null;
};

@Component({ components: { draggable } })
export default class HelloWorld extends Vue {
  @Prop() private msg!: string;
  private statusses: Array<Status> = [
    { id: 0, name: "TODO", width: 400 },
    { id: 1, name: "DOING", width: 200 },
    { id: 2, name: "REVIEW", width: 200 },
    { id: 3, name: "DONE", width: 200 }
  ];
  private pbis: Array<PBI> = [
    {
      id: 0,
      title: "一つ目",
      tasks: {
        0: [
          {
            id: 0,
            title: "あああああ",
            description: "あああああ",
            assignee: null,
            status: 0,
            point: 1.0
          }
        ],
        1: [
          {
            id: 1,
            title: "あああああ",
            description: "あああああ",
            assignee: "山田一浪",
            status: 1,
            point: 0.5
          }
        ],
        2: [],
        3: [
          {
            id: 2,
            title: "あああああ",
            description: "あああああ",
            assignee: "山田一浪",
            status: 3,
            point: 1.0
          }
        ]
      }
    },
    {
      id: 1,
      title: "二つ目",
      tasks: {
        0: [
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
          }
        ],
        1: [],
        2: [
          {
            id: 5,
            title: "2あああああ",
            description: "あああああ",
            assignee: "山田一浪",
            status: 2,
            point: 1.0
          }
        ],
        3: [
          {
            id: 6,
            title: "2あああああ",
            description: "あああああ",
            assignee: "山田一浪",
            status: 3,
            point: 1.0
          }
        ]
      }
    },
    {
      id: 2,
      title: "三つ目",
      tasks: {
        0: [
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
          }
        ],
        1: [],
        2: [
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
        ],
        3: []
      }
    },
    {
      id: 3,
      title: "四つ目",
      tasks: {
        0: [
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
          }
        ],
        1: [],
        2: [
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
    }
  ];
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
ul {
  list-style-type: none;
  padding: 0px;
  margin: 0px;
  border: none;
}
li {
  padding: 0px;
  margin: 0px;
  border: none;
}
li.area {
  margin-left: 5px;
  margin-right: 5px;
  flex-grow: 1;
  box-sizing: border-box;
  border-top: 1px solid #ccc;
  border-right: 1px solid #ccc;
  border-left: 1px solid #ccc;
  text-align: center;
  padding: 10px;
}
ul.kanban-board ul {
  display: flex;
}
li.area.group {
  background-color: #ff9191;
}
li.area.status {
  background-color: #ffeaea;
}
.pbis ul:last-child li {
  border-bottom: 1px solid #ccc;
}
div.pbi {
  margin: 1px;
  border: 1px solid #ccc;
}
div.task {
  margin: 1px;
  border: 1px solid #ccc;
}
</style>
