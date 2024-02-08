<template>
  <section class="schedule content_line">
    <day-elem
      v-for="day in week"
      :key="day.idDay"
      :day="day"
      @switch="switchImportance"
      @clearDay="clearDay"
      @deleteTask="deleteTask"
    >
    </day-elem>
  </section>
</template>


<script>
import DayElem from './DayElem.vue';

export default {
  components: {
    DayElem,
  },
  props: ['week'],
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
.schedule {
  display: flex;
  flex-direction: column;
  gap: 23px;
}

</style>