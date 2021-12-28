<template>
  <!-- <div id="app"> -->

 <mdb-container>
    <mdb-row>
      <mdb-col class="col-lg-6 col-md-8 col-sm-12 mx-auto">
        
          <form @submit.prevent="handleSubmit" class="mt-4">
                  <p style="display: none;" class="hidden">
                    <label>Не заполняйте это, если вы человек
                        <input name="bot-field">
                    </label>
                  </p>

          <p class="h4 text-center mb-4">Регистрация</p>
            <div class="grey-text">
              <mdb-input v-model="form.name" name="name" label="Ваше имя" icon="user" group type="text" validate error="wrong" success="right"/>
              <mdb-input v-model="form.email" name="email" label="Ваш email" icon="envelope" group type="email" validate error="wrong" success="right"/>
              <mdb-input v-model="form.subject" name="subject" label="Тема письма" icon="tag" group type="text" validate error="wrong" success="right"/>
              <mdb-textarea v-model="form.message" name="message" :rows="2" label="Ваше сообщение" icon="pencil"/>
            </div>
            <div class="text-center">
              <mdb-btn outline="secondary">Отправить <mdb-icon far icon="paper-plane" class="ml-1"/></mdb-btn>
            </div>
          </form>

      </mdb-col>
    </mdb-row>
  </mdb-container>

  <!-- </div> -->
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import { mdbInput, mdbBtn, mdbTextarea,mdbContainer, mdbRow, mdbCol, mdbIcon } from 'mdbvue';

export default {
  name: 'Basic',
  data: ()=>({
    form: {
      name: '',
      email: '',
      subject: '',
      message: ''
    }
  }),
  components: {
    mdbInput,
    mdbBtn,
    mdbTextarea,
    mdbContainer,
    mdbRow,
    mdbCol,
    mdbIcon
  },
  methods:{
    encode(data){
      return Object.keys(data)
      .map(key => `${encodeURIComponent(key)}=${encodeURIComponent(data[key])}`)
      .join('g')
    },
    handleSubmit(){
      fetch('/', {
          method: 'post',
          headers:{
            'Contant-Type': 'application/x-www-form-urlencoded'
          },
          body: this.encode({
            'form-name': 'contact',
            ...this.form
          })
        })
        .then(() => console.log('success'))
        .catch(e => console.error(e))
      }
  }
}
</script>

<style lang="scss">

</style>
