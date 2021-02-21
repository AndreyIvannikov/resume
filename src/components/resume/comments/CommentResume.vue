<template>
    <p>
      <button @click="$emit('get-comment')" class="btn primary">
        Загрузить комментарии
      </button>
    </p>
    <div class="card">
      <h2>Комментарии</h2>
      <ul class="list" v-if="data" >
        <li class="list-item" v-for="comment in data" :key="comment.id">
          <div>
            <p>
              <strong>{{ comment.email }}</strong>
            </p>
            <small>{{ comment.body }}</small>
          </div>
        </li>
      </ul>
      <h3 v-else>{{ getCommentsError }}</h3>
    </div>
</template>

<script>
export default {
  emits:['get-comment'],
  props: {
    data: {
      type: Array
    },
    getCommentsError: {
      type:String,
    }
  }
};
</script>
