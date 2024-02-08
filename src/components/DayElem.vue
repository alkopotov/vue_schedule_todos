<template>
  <div v-if="day.tasks.length > 0" class="day_field">
    <div class="day_name"> {{ day.nameDay }}</div>
    <section class="task_list">
      <task-elem
        v-for="task in day.tasks"
        :key="task.id"
        :task="task"
        :dayId="day.idDay"
        @switch="switchImportance"
        @deleteTask="deleteTask"
      >
      </task-elem>
      <img 
        src="../assets/delete.svg"
        alt="delete_button"
        class="clear_day_button"
        @click="clearDay(day.idDay)"
      >
    </section>
  </div>
  <div v-else class="empty_day"></div>

</template>


<script>
import TaskElem from './TaskElem.vue';
export default {
  components: {
    TaskElem,
  },
  props: ['day'],
  emits: ['switch', 'clearDay', 'deleteTask'],
  methods: {
    switchImportance(idDay, idTask) {
      this.$emit('switch', idDay, idTask)
    },
    clearDay(idDay) {
      this.$emit('clearDay', idDay)
    },
    deleteTask(idDay, idTask) {
      this.$emit('deleteTask', idDay, idTask)
    }
  }
}

</script>


<style>
.day_field {
  position: relative;
  background: #ECF0F1;
  display: flex;
  border-radius: 20px;
}
.task_list {
  display: flex;
  gap: 15px;
  flex-wrap: wrap;
  padding: 11px 32px 11px 32px;
  width: calc(100% - 80px);

}
.day_name {
  width: 80px;
  background: #34495E;
  border-radius: 20px 0 0 20px;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  /* padding: 0 16px; */
  font-size: 30px;
  font-weight: 400;
  line-height: 36px;
  letter-spacing: 0em;
  text-align: center;
}
.clear_day_button {
  position: absolute;
  top: -14px;
  right: -14px;
  display: none;
}
.day_field:hover .clear_day_button {
  display: block;
}
.task_item:hover ~ .clear_day_button {
    display: none;
  } 
</style>