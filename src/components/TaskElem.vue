<template> 
  <div 
    :class="`task_item ${task.urgent ? 'urgent' : ''}`"
    @click="switchImportance(dayId, task.id)"
  >
    {{ task.title }}
    <img
      src="../assets/delete.svg"
      alt="delete_button"
      class="delete_button"
      @click="handler"
    >
  </div>


</template>

<script>
export default {
  props: ['task', 'dayId' ],
  emits: ['switch', 'deleteTask'],
  methods: {
    switchImportance(idDay, idTask) {
      this.$emit('switch', idDay, idTask)
    },
    deleteTask() {
      this.$emit('deleteTask', this.dayId, this.task.id)
    },
    handler(e) {
      e.stopPropagation();
      this.deleteTask()
    }

  }
}
</script>

<style>
  .task_item {
    position: relative;
    font-size: 30px;
    font-weight: 400;
    line-height: 36px;
    letter-spacing: 0em;
    text-align: left;
    padding: 4px 17px;
    width: fit-content;
    min-width: 286px;
    background: #1ABC9C;
    color: white;
  }

  .urgent {
    background: #E74C3C;
  }

  .delete_button {
    position: absolute;
    top: -14px;
    right: -14px;
    display: none;
  }

  .task_item:hover .delete_button {
    display: block;
  }

  .task_item:hover {
    cursor: pointer;
  }

  

</style>