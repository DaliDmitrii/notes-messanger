<template>
  <main>
    <div class="container">
      <div class="messages">
        <div class="message">
          <div class="text">
            <p>Сообщение 1</p>
          </div>
          <div class="time">
            <time>10:00</time>
          </div>
        </div>

        <div class="message">
          <div class="text">
            <p>Сообщение 2</p>
          </div>
          <div class="time">
            <time>10:00</time>
          </div>
        </div>

        <div class="message">
          <div class="text">
            <p>Сообщение 3</p>
          </div>
          <div class="time">
            <time>10:00</time>
          </div>
        </div>
      </div>
      <div class="footer">
        <div class="input">
          <input
              type="text"
              placeholder="Введите сообщение"
          >
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  props: {},

  data() {
    return {};
  },

  computed: {},

  watch: {},

  created() {
  },

  mounted() {
  },

  methods: {},
}
</script>

<style lang="scss" scoped>
.messages {
  margin-top: 10px;
  height: 100%;
  overflow-y: auto;
}

.message {
  margin-left: auto;
  border-radius: 5px;
  border: 1px solid #545454;
  padding: 10px 15px;
  margin-bottom: 10px;
  width: fit-content;

  .text {
    p {
      text-align: end;
    }
  }

  .time {
    margin-top: 5px;
    text-align: right;
    font-size: 12px;
    color: #999;
  }
}
</style>
