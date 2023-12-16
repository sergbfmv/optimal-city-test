<script setup lang="ts">
import botAva from "./components/icons/bot-avatar.svg"
import bookAva from "./components/icons/book-icon.svg"
import fbIcon from "./components/icons/fb.png"
import xIcon from "./components/icons/x-icon.svg"
import {ref} from "vue";

const messages = ref<string[]>(['Бот: Привет! Что я могу для Вас сделать?'])
const phrase = ref<string>('')

const onClickHandler = (text: string) => {
  const userMessage = text;
  addBotResponse(userMessage);
  phrase.value = userMessage;

  setTimeout(() => {
    let botResponse = '';

    switch (phrase.value) {
      case 'Заказать пиццу':
        botResponse = 'Бот: Хорошо, я закажу пиццу. Что еще могу сделать?';
        break;

      case 'Установить будильник':
        botResponse = 'Бот: К сожалению, функция установки будильника пока не реализована.';
        break;

      case 'Вывести погоду':
        botResponse = 'Бот: Извините, я не могу предоставить информацию о погоде в данный момент.';
        break;

      default:
        botResponse = 'Бот: Извините, я не понял ваш запрос.';
        break;
    }

    addBotResponse(botResponse);
    phrase.value = '';
  }, 1000);
};

const addBotResponse = (response: string) => {
  messages.value.push(response);
};
</script>

<template>
  <main class="main">
    <div class="main-text">
      <h1 class="main-heading">Vue Simple Chatbot</h1>
      <p class="main-paragraph">A simple react chatbot component</p>
      <div class="social-btns">
        <a class="social-fb"><img class="social-icon" :src="fbIcon" alt="fb icon">Поделиться <span>104</span></a>
        <a class="social-x"><img class="social-icon-x" :src="xIcon" alt="x icon">Post</a>
      </div>
      <div class="git">
        <iframe
            src="https://ghbtns.com/github-btn.html?user=lucasbassetti&repo=react-simple-chatbot&type=star&count=true&size=large"></iframe>
        <iframe
            src="https://ghbtns.com/github-btn.html?user=lucasbassetti&repo=react-simple-chatbot&type=fork&count=true&size=large"></iframe>
      </div>
      <a class="doca-btn"><img class="book-icon" :src="bookAva" alt="book icon">Documentation</a>
    </div>
    <!--    <TheWelcome />-->
    <div class="bot-wrapper">
      <div class="bot-display">
        <div v-for="msg in messages" class="bot-messages">
          <template v-if="msg.startsWith('Бот: ')">
            <img :src="botAva" alt="bot avatar" class="bot-avatar">
            <p class="text left">{{ msg }}</p>
          </template>
          <template v-else>
            <p class="text right">{{ msg }}</p>
          </template>
        </div>
      </div>
      <div class="bot-btns">
        <button class="request-btn" @click="onClickHandler('Заказать пиццу')">Заказать пиццу</button>
        <button class="request-btn" @click="onClickHandler('Установить будильник')">Установить будильник</button>
        <button class="request-btn" @click="onClickHandler('Вывести погоду')">Вывести погоду</button>
      </div>
    </div>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

iframe {
  width: 158px;
  height: 30px;
  border: none;
}

span {
  margin-left: 5px;
}

.main {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-around;

}

.main-text {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  max-width: 400px;
  width: 100%;
  padding: 20px;


}

.main-heading {
  font-size: 2.4rem;
  text-align: center;
  color: white;
  white-space: nowrap;
}

.main-paragraph {
  font-size: 1.4rem;
  margin: 0;
  text-align: center;
  color: white;
  white-space: nowrap;
}

.bot-display {
  width: 300px;
  height: calc(400px);
  display: block;
  background-color: white;
  border-radius: 10px;
  padding: 5px;
  font-size: 14px;
  box-shadow: rgba(0, 0, 0, 0.15) 0 12px 24px 0;
  overflow: scroll;
  overflow-x: hidden;
}

.bot-messages {
  display: flex;
  gap: 5px;
  align-items: flex-end;
}

.bot-avatar {
  width: 40px;
  height: 40px;
  margin-bottom: 20px;
}

.bot-btns {
  margin-top: 20px;
  display: flex;
  gap: 5px;
  flex-direction: column;
}

.text {

}

.text.left {
  background-color: #6e48aa;
  border-radius: 15px;
  color: white;
  padding: 12px;
  line-height: 12px;
  margin-bottom: 5px;
  margin-top: 10px;
  position: relative;
  align-self: flex-start;
  width: 60%;
}

.text.left:after {
  content: '';
  position: absolute;
  bottom: 10px;
  left: -16px;
  width: 0;
  height: 0;
  border-top: 20px solid transparent;
  border-right: 20px solid #6e48aa;
}

.text.right {
  background-color: #447aff;
  border-radius: 15px;
  color: white;
  padding: 12px;
  line-height: 12px;
  margin-bottom: 5px;
  margin-top: 10px;
  position: relative;
  align-self: flex-end;
  display: inline-block;
  margin-left: auto;
}

.text.right:after {
  content: '';
  position: absolute;
  bottom: 0;
  right: -5px;
  width: 0;
  height: 0;
  border-top: 10px solid transparent;
  border-left: 25px solid #447aff;
}

.social-btns {
  margin-top: 24px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
}

.social-fb {
  color: white;
  font-weight: bold;
  background-color: #447aff;
  border-radius: 2px;
  cursor: pointer;
  font-size: 12px;
  display: flex;
  align-items: center;
  padding: 5px 10px;
}

.social-x {
  color: white;
  background-color: #000000;
  border-radius: 25px;
  cursor: pointer;
  font-size: 12px;
  padding: 3px 10px;
  display: flex;
  align-items: center;
}

.social-icon {
  width: 15px;
  height: 15px;
  margin-right: 5px;
}

.social-icon-x {
  width: 25px;
  height: 25px;
}

.git {
  margin-top: 24px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.doca-btn {
  font-size: 14px;
  margin-top: 24px;
  border-radius: 50px;
  color: white;
  border: 2px solid white;
  padding: 5px 30px;
  cursor: pointer;
  display: flex;
  align-items: center;
}

.doca-btn:hover {
  background-color: white;
  color: black;
}

.request-btn {
  border-radius: 5px;
  padding: 5px 10px;
  border: none;
  cursor: pointer;
}

.request-btn:hover {
  background-color: white;
  border: 2px solid white;
}

.book-icon {
  width: 15px;
  height: 15px;
  fill: white;
  margin-right: 5px;
}

@media (max-width: 780px) {
  .main {
    display: flex;
    align-items: center;
    flex-direction: column;
    gap: 50px;
  }
}

</style>
