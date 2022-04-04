<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar style="min-height: 70px">
        <q-toolbar-title class="text-center">
          <q-img
            class="logo"
            src="https://www.fortics.com.br/wordpress/wp-content/uploads/2017/08/Fortics-Logo-s-slogan-100.png"
          />
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <div class="container mt-5">
        <div class="row q-pa-sm">
          <div class="col col-lg-6 col-12">
            <h4 class="px-lg-4 px-2" color="secondary">
              Mega Tendências 2022: Tecnologias e Negócios com foco na Hiper
              ConveniêncIA
            </h4>
            <p class="px-lg-4 px-2 mt-3" color="secondary">
              Quer saber quais tendências vieram para ficar e devem ser
              implementadas já no seu negócio? Toda tendência de mercado nasce
              em função da mudança de comportamento do consumidor. Então o
              primeiro passo para entender as principais tendências para 2022 é
              descobrir o motivo dessa mudança.
            </p>

            <p class="px-lg-4 px-2">
              Com a pandemia, as pessoas precisaram consumir muito mais no
              ambiente online, e naturalmente passaram a usar todos os canais
              digitais disponíveis, conforme fossem conveniente para elas, para
              se comunicarem com as empresas. O resultado disso?
              <span class="detail"
                >O consumidor mudou, pois descobriu que pode!
              </span>
            </p>
          </div>
          <div class="col col-lg-6 col-12 d-flex justify-content-center">
            <img
              src="https://d335luupugsy2.cloudfront.net/cms/files/80957/1645820819/$x6hsl7y8f7l"
              alt=""
            />
          </div>
        </div>
      </div>

      <div class="q-gutter-md button-chat">
        <q-btn
          @click="changeState()"
          v-show="!state"
          class="float-right button"
          round
          color="secondary"
          icon="message"
          center
        />
      </div>

      <div class="chat mr-lg-5 mb-4" v-show="state">
        <q-btn @click="handleClose()" icon="close" class="close mr-1" round />
        <q-chat-message
          v-show="stateButton"
          class="px-3"
          name="Fortics"
          avatar="https://br.radan.com/images/icons/hexagon/darkblue/MI_DARK_BLUE_ICON_SUPPORT.png"
          :text="['Como posso te ajudar?']"
        />
        <div v-show="stateButton" class="options my-4">
          <q-btn
            unelevated
            rounded
            color="secondary"
            class="mt-2"
            label="1. Iniciar atendimento"
            @click="openChatSuport()"
          />
          <q-btn
            unelevated
            rounded
            color="secondary"
            class="mt-2"
            label="2. Suporte"
          />
          <q-btn
            unelevated
            rounded
            color="secondary"
            class="mt-2"
            label="3. Comercial"
          />
          <q-btn
            unelevated
            rounded
            color="secondary"
            class="mt-2"
            label="4. Encerrar o atendimento"
          />
        </div>

        <q-form @submit.prevent="execChat()" v-show="!stateButton">
          <p class="px-4" style="color: #696969">
            Antes, precisamos de algumas informações suas para prosseguirmos.
          </p>
          <q-input
            center
            rounded
            outlined
            dense
            bg-color="white"
            v-model="user"
            name="Nome"
            placeholder="Nome"
          />
          <q-input
            class="mt-2"
            rounded
            outlined
            dense
            bg-color="white"
            v-model="email"
            name="Email"
            placeholder="Email"
          />
          <button class="login mt-3" icon="send" center @click="!renderChat">
            Login
          </button>
        </q-form>
      </div>
    </q-page-container>

    <div class="q-pa-md row justify-center">
      <div>
        <q-chat-message
          v-for="chat in chats"
          :name="chat.user"
          :key="chat.id"
          :text="[chat.text]"
        />
      </div>
      <div>
        <div class="chat-suport mr-lg-5 mb-4" v-show="renderChat">
          <q-btn @click="handleClose()" icon="close" class="close mr-1" round />
          <div>
            <q-chat-message
              v-for="chat in chats"
              :name="chat.user"
              :key="chat.id"
              :text="[chat.text]"
            />
          </div>
          <button class="primary button-chat-trsp" @click="changeState()">
            {{ state }}
          </button>
          <div>
            <q-form @submit.prevent="handleSandMessage">
              <q-chat-message
                class="mt-4"
                name="me"
                avatar="https://br.radan.com/images/icons/hexagon/darkblue/MI_DARK_BLUE_ICON_SUPPORT.png"
                :text="['Como posso te ajudar?']"
                sent
              />
              <q-toolbar class="toolbar d-flex mt-3">
                <q-input
                  class="input mt-3 col-9"
                  rounded
                  outlined
                  dense
                  bg-color="white"
                  v-model="message"
                  name="message"
                  placeholder="Tire sua dúvida"
                />
                <q-btn
                  class="mt-3 col-2 pr-5"
                  color="secondary"
                  round
                  flat
                  icon="send"
                  type="submit"
                />
              </q-toolbar>
            </q-form>
          </div>
        </div>
      </div>
    </div>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "IndexPage",
  setup() {
    const message = ref("");
    const user = ref("");
    const email = ref("");
    const chats = ref([]);
    const handleSandMessage = async () => {
      try {
        let objectMessage = {
          text: message.value,
          user: user,
          email: email,
          id: 1,
        };
        return chats.value.push(objectMessage);
      } catch (error) {
        alert(error);
      }
    };
    return {
      message,
      handleSandMessage,
      chats,
      email,
      user,
    };
  },
  data() {
    return {
      state: false,
      stateButton: true,
      renderChat: false,
    };
  },
  methods: {
    changeState() {
      this.state = true;
    },
    handleOpen() {
      this.state = true;
    },
    handleClose() {
      this.state = false;
      this.renderChat = false;
    },
    execChat() {
      this.renderChat = true;
      this.stateButton = true;
    },
    openChatSuport() {
      this.stateButton = false;
    },
  },
});
</script>
