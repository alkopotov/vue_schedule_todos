<template>
  <form-elem
   :week="week"
   @addTask="addTask"
  >
  </form-elem>
  <schedule-elem
   :week="week"
   @switch="switchImportance"
   @clearDay="clearDay"
   @deleteTask="deleteTask"
  >

  </schedule-elem>

</template>


<script>
  
  import ScheduleElem from './components/ScheduleElem.vue'
  import FormElem from './components/FormElem.vue'

  let initialData = [
          {
            idDay: 1,
            nameDay: 'ПН',
            tasks: [
              {id: 1, title: 'Купить дверь', urgent: true},
              {id: 2, title: 'Сходить в зал', urgent: false}
            ]
          },
          {
            idDay: 2,
            nameDay: 'ВТ',
            tasks: [
              {id: 1, title: 'Купить дверь', urgent: true},
              {id: 2, title: 'Сходить в зал', urgent: true},
              {id: 3, title: 'Купить ручку', urgent: false},
              {id: 4, title: 'Помыть кота', urgent: false},
              {id: 5, title: 'Починить свет', urgent: false},
            ]
          },
          {
            idDay: 3,
            nameDay: 'CР',
            tasks: []
          },
          {
            idDay: 4,
            nameDay: 'ЧТ',
            tasks: []
          },
          {
            idDay: 5,
            nameDay: 'ПТ',
            tasks: [
              {id: 1, title: 'Зарядить воду', urgent: true}
            ]
          },
          {
            idDay: 6,
            nameDay: 'СБ',
            tasks: []
          },
          {
            idDay: 7,
            nameDay: 'ВС',
            tasks: []
          },
        ]

  export default {
    components: {
      ScheduleElem, FormElem
    },
    data() {
      return {
        week: JSON.parse(localStorage.getItem('weekSchedule')) ?? initialData
      }
    },
    watch: {
      week() {
        localStorage.setItem('weekSchedule', JSON.stringify([...this.week]))
      }
    },
    methods: {

      addTask(idDay, title, urgent) {
        console.log(idDay, title, urgent);
        this.week = this.week.map(day => {
          if (day.idDay === idDay) {
            day.tasks.push({id: Date.now(), title: title, urgent: urgent})
            day.tasks.sort((a, b) => b.urgent - a.urgent)
            return day
          } else {
            return day
          }
        })
      },

      switchImportance(idDay, idTask){
        this.week = this.week.map(day => {
          if (day.idDay === idDay) {
            day.tasks = day.tasks.map(task => {
              if (task.id === idTask) {
                task.urgent = !task.urgent;
                return task;
              } else {
                return task;
              }
            });
            day.tasks.sort((a, b) => b.urgent - a.urgent)
            return day;
          } else {
            return day;
          }
        })
      },

      clearDay(idDay) {
        this.week = this.week.map(day => {
          if (day.idDay === idDay) {
            day.tasks = [];
            return day;
          } else {
            return day;
          }
        })
      },

      deleteTask(idDay, idTask) {
        this.week = this.week.map(day => {
          if (day.idDay === idDay) {
            console.log(day);
            day.tasks = day.tasks.filter(task => task.id !== idTask)
            return day;
          } else {
            return day;
          }
        })
      }
    }
  }

</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@100;200;300;400;500;600;700;800;900&display=swap');

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Inter', sans-serif;
  }
  body {
    background: #1ABC9C;
  }
  .content_line {
    width: 100%;
    max-width: 1088px;
    margin-left: auto;
    margin-right: auto;
  }
</style>