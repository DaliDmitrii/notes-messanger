<template>
  <main>
    <div class="container">
      <div class="header">
        <div class="search">
          <input
              type="text"
              placeholder="Поиск"
              v-model="search"
          >
        </div>
      </div>

      <div v-if="sortedDialogs && sortedDialogs.length" class="dialogs">
        <router-link
            v-for="dialog in sortedDialogs"
            :to="`/messages/${dialog.id}`"
            :key="dialog.id"
        >
          <div class="dialog">
            <div class="title">
              <h3>{{ dialog.title }}</h3>
              <time>{{ dialog.dateLastMessage }}</time>
            </div>
            <div class="last-message">
              <p>{{ dialog.lastMessage }}</p>
            </div>
          </div>
        </router-link>
      </div>

      <div v-else class="dialogs">
        Нет диалогов
      </div>

      <div class="footer">
        <div class="form">
          <div class="new-dialog">
            <input
                type="text"
                placeholder="Название"
                v-model="title"
            >
          </div>
          <button @click="addDialog">
            Добавить новый дилог
          </button>
        </div>
      </div>
    </div>
  </main>
</template>

<script>

export default {
  props: {},

  data() {
    return {
      dialogs: [
        {
          id: 1,
          title: 'Избарнное 2',
          lastMessage: 'Купить что-то',
          dateLastMessage: '10:20'
        },
        {
          id: 0,
          title: 'Избарнное',
          lastMessage: 'Купить что-то',
          dateLastMessage: '10:20'
        },
        {
          id: 2,
          title: 'Избарнное 3',
          lastMessage: 'Купить что-то',
          dateLastMessage: '10:20'
        },
      ],
      title: '',
      search: ''
    };
  },

  computed: {
    sortedDialogs() {
      return this.dialogs.filter(dialog => {
        return dialog.title.toLowerCase().includes(this.search.toLowerCase())
      })
    },
  },

  watch: {
  },

  created() {
    this.getDialogs()
  },

  mounted() {
  },

  methods: {
    addDialog() {
      this.dialogs.push({
        id: Date.now(),
        title: this.title,
        lastMessage: 'Нет сообщений',
        dateLastMessage: new Date().toLocaleString()
      })
      this.title = ''
      this.saveDialogs();
    },

    saveDialogs() {
      localStorage.setItem('dialogs', JSON.stringify(this.dialogs));
    },

    getDialogs() {
      this.dialogs = JSON.parse(localStorage.getItem('dialogs') || '[]');
    }
  },
}
</script>

<style scoped lang="scss">
.dialogs {
  margin-top: 10px;
  height: 100%;
  overflow-y: auto;
}

.dialog {
  margin-top: 5px;
  border-radius: 5px;
  padding: 10px 15px;

  .title {
    display: flex;
    justify-content: space-between;
    align-items: end;

    h3 {
      text-overflow: ellipsis;
      overflow: hidden;
      white-space: nowrap;
    }

    time {
      font-size: 12px;
      color: #999;
    }
  }

  .last-message {
    margin-top: 5px;

    p {
      color: #717579;
      text-overflow: ellipsis;
      overflow: hidden;
      white-space: nowrap;
    }
  }

  &:hover {
    background: #2c2c2c;
  }
}

.footer {
  height: 100px;

  .form {
    .new-dialog {
      width: 100%;
    }

    button {
      width: 100%;
      padding: 10px;
      border: 0;
      border-radius: 5px;
      font-size: 16px;
      color: #fff;
      background: #2c2c2c;
      outline: none;
      cursor: pointer;
      margin-top: 10px;
    }
  }
}
</style>
