<template>
  <q-page class="flex flex-center">
    <div class="todo-lista">
      <Logo :src="logoPath" />
      
      <h1>Tvoja To-Do lista</h1>

      <q-input 
        v-model="novi" 
        @keyup.enter="dodaj" 
        type="text" 
        placeholder="Dodaj novi cilj u svoju to-do listu 😊" 
        class="zadatak"
        outlined
      />

      <q-list>
        <q-item v-for="(task, index) in tasks" :key="index" class="zadatak-zadan">
          <q-item-section>
            <q-checkbox 
              v-model="task.completed" 
              label=""
              :true-value="true"
              :false-value="false"
            />
          </q-item-section>

          <q-item-section>
            <span :class="{ completed: task.completed }">{{ task.text }}</span>
          </q-item-section>

          <q-item-section side>
            <q-btn color="red" @click="obrisi(index)">
              Obriši
            </q-btn>
          </q-item-section>
        </q-item>
      </q-list>
    </div>
  </q-page>
</template>

<script>
import Logo from '../components/logo.vue';

export default {
  components: {
    Logo
  },
  data() {
    return {
      novi: "",
      tasks: [],
      logoPath: '/logo.png',

    };
  },

  mounted() {
  setTimeout(() => {
    this.logoPath = '/done.png';
  }, 3000);
},

  methods: {
    dodaj() {
      if (this.novi.trim()) {
        this.tasks.push({
          text: this.novi,
          completed: false,
        });
        this.novi = "";
      }
    },
    obrisi(index) {
      this.tasks.splice(index, 1);
    }
  }
};
</script>

<style scoped>
.todo-lista {
  max-width: 500px;
  margin: 0 ;
  text-align: center;
}

.zadatak-zadan {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
}

.completed {
  text-decoration: line-through;
}

.zadatak {
  margin-bottom: 20px;
  font-size: 16px;
}

.h1 {
  display: inline;
  font-size: 24px;
  margin: 0;
}
</style>
