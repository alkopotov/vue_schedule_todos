<template>
  <form @submit="handleSubmit" class="content_line form">
    <section class="input_area">
      <div class="select_area">
        <select name="idDay" required>
          <option value="" default disabled selected>Выберите день</option>
          <option v-for="day in week" :key="day.idDay" :value="day.idDay">{{ day.nameDay }}</option>
        </select>
        <select name="urgent" required>
          <option value="" default disabled selected>Выберите важность</option>
          <option value="1">СРОЧНАЯ</option>
          <option value="0">ОБЫЧНАЯ</option>
        </select>
      </div>
      <input type="text" name="title" required class="input_title" placeholder="Описание">
    </section>
    
    <input type="submit" name="submit" value="Добавить" class="submit_button">
  </form>
</template>

<script>
  export default {
    props: ['week'],
    emits: ['addTask'],
    
    methods: {
      addTask(idDay, title, urgent) {
        this.$emit('addTask', idDay, title, urgent)
      },
      handleSubmit(e) {
        e.preventDefault();
        let form_data = new FormData(e.target)
        let data = Object.fromEntries(form_data)
        console.log(data);
        this.addTask(+data.idDay, data.title, +data.urgent === 1)
        e.target.reset();
      }
    }
  }
</script>

<style>
  .form {
    padding: 32px 62px;
    border-radius: 20px;
    border: 1px solid black;
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    margin-bottom: 43px;
    margin-top: 60px;
    background: #ECF0F1;

  }
  .input_area {
    display: flex;
    max-width: 544px;
    flex-wrap: wrap;
    gap: 24px;
  }
  .input_title {
    width: 100%;
    padding: 7px 8px 7px 18px;
    font-size: 20px;
    font-weight: 400;
    line-height: 24px;
    letter-spacing: 0em;
    text-align: left;
    color: #000000;
  }

  .input_title::placeholder {
    font-size: 20px;
    font-weight: 400;
    line-height: 24px;
    letter-spacing: 0em;
    text-align: left;
    color: #000000;
  }
  option[default] {
    display: none;
  }

  select {
    width: 255px;
    font-size: 20px;
    padding: 7px;
  }
  .select_area {
    width: 100%;
    display: flex;
    justify-content: space-between;
  }

  .submit_button {
    background-color: #1ABC9C;
    color: white;
    border-radius: 20px;
    border: solid 1px black;
    width: 163px;
    height: 45px;
    font-size: 20px;
    font-weight: 400;
    line-height: 24px;
    text-align: center;
    cursor: pointer;
  }
</style>