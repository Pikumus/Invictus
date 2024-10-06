<template>
  <div class="poem-button">
    <div class="controls">
      <button
        v-for="(stanza, index) in visibleStanzas"
        :key="index"
        :class="{ active: !visibleStanzas[index] }"
        @click="toggleVisibility(index)"
        class="btn"
      ></button>
    </div>
    <div class="poem">
      <div class="description">
        <h1 class="title">Invictus</h1>
        <span class="sub-title">By William Ernest Henley</span>
      </div>
      <div v-if="visibleStanzas[0]" class="stanza">
        <span>Out of the night that covers me,</span>
        <span>Black as the pit from pole to pole,</span>
        <span>I thank whatever gods may be</span>
        <span>For my unconquerable soul.</span>
      </div>
      <div v-if="visibleStanzas[1]" class="stanza">
        <span> In the fell clutch of circumstance, </span>
        <span> I have not winced nor cried aloud. </span>
        <span> Under the bludgeonings of chance </span>
        <span> My head is bloody, but unbowed. </span>
      </div>
      <div v-if="visibleStanzas[2]" class="stanza">
        <span>Beyond this place of wrath and tears </span>
        <span>Looms but the Horror of the shade, </span>
        <span>And yet the menace of the years </span
        ><span>Finds and shall find me unafraid. </span>
      </div>
      <div v-if="visibleStanzas[3]" class="stanza">
        <span>It matters not how strait the gate,</span>
        <span>How charged with punishments the scroll,</span>
        <span>I am the master of my fate,</span>
        <span>I am the captain of my soul.</span>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

// Состояние видимости каждого четверостишия
const visibleStanzas = ref([true, true, true, true]);

// Функция переключения видимости четверостиший
const toggleVisibility = (index: number) => {
  // Подсчет количества видимых четверостиший
  const visibleCount = visibleStanzas.value.filter(Boolean).length;

  // Не даем отключить последнее видимое четверостишие
  if (visibleCount === 1 && visibleStanzas.value[index]) {
    return;
  }

  // Используем spread оператор для обновления состояния
  visibleStanzas.value = [
    ...visibleStanzas.value.slice(0, index),
    !visibleStanzas.value[index],
    ...visibleStanzas.value.slice(index + 1),
  ];
};
</script>

<style scoped lang="scss">
.poem-button {
  background-color: #f5f5f5;
  font-family: serif;
  padding: 20px;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  min-height: 100vh;

  .controls {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
    margin-right: 20px;
    margin-top: 3rem;

    .btn {
      border: 1px solid black;
      background-color: #000;
      color: white;
      padding: 0.5rem 0.5rem;
      border-radius: 0;
      cursor: pointer;

      &:hover {
        background-color: #444;
      }

      &.active {
        background-color: transparent;
      }
    }
  }

  .poem {
    display: flex;
    flex-direction: column;
    text-align: center;
    max-width: 700px;

    .description {
      display: flex;
      align-items: center;
      gap: 5rem;
      justify-content: center;

      .title {
        margin-left: 5rem;
        font-size: 2rem; /* Размер заголовка */
      }

      .sub-title {
        font-size: 1rem; /* Размер подзаголовка */
        margin-top: 0.5rem;
        color: gray;
      }
    }

    .stanza {
      margin-top: 1rem;
      font-size: 1rem;
      text-align: left;
      letter-spacing: 1px;

      span {
        display: block; /* Каждая строка на новой строке */
      }

      span:nth-child(even) {
        text-indent: 2em; /* Отступ для каждой второй строки */
      }
    }
  }

  @media (max-width: 768px) {
    .poem {
      max-width: 90%; /* Уменьшение ширины на мобильных */

      .title {
        font-size: 1.5rem; /* Меньший заголовок на мобильных */
      }

      .stanza {
        font-size: 1rem; /* Меньший текст на мобильных */
      }
    }
  }

  @media (min-width: 1600px) {
    .poem {
      max-width: 50%; /* Уменьшение ширины на очень больших экранах */

      .title {
        font-size: 2.5rem; /* Увеличение заголовка */
      }

      .stanza {
        font-size: 1.5rem; /* Увеличение текста для удобства чтения */
      }
    }
  }
}
</style>
