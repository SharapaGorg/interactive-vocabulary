<template>
  <div ref="root">

    <div @click='newWord = false' class="h-screen overflow-y-auto">
      <search class="relative block mx-auto"/>

      <div class="toolkit">
        <div class="trash">
          <svg fill="#000000" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 30 30">
            <path
              d="M 13 3 A 1.0001 1.0001 0 0 0 11.986328 4 L 6 4 A 1.0001 1.0001 0 1 0 6 6 L 24 6 A 1.0001 1.0001 0 1 0 24 4 L 18.013672 4 A 1.0001 1.0001 0 0 0 17 3 L 13 3 z M 6 8 L 6 24 C 6 25.105 6.895 26 8 26 L 22 26 C 23.105 26 24 25.105 24 24 L 24 8 L 6 8 z"/>
          </svg>
        </div>

        <div class="plus" ref="addButton">
          <svg fill="#000000" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 50 50">
            <path
              d="M25,2C12.317,2,2,12.317,2,25s10.317,23,23,23s23-10.317,23-23S37.683,2,25,2z M37,26H26v11h-2V26H13v-2h11V13h2v11h11V26z"/>
          </svg>
        </div>
      </div>

      <div
        class="grid
        lg:grid-cols-6 md:grid-cols-4 grid-cols-2 xl:grid-cols-8
        lg:gap-10 md:gap-7 gap-3
        justify-items-center disable-select mt-8"
      >
        <div v-for="word in wordsList" :key="word" @click="showWord(word)" class="w-4/5">
          <div class="translation">
            {{ words[word] }}
          </div>
          <div
            class="word cursor-pointer"
            :style="{
            transform : showedWord === word || showedWord === 'translateAll'
            ? 'translateY(3px)'
            : 'translateY(-44px)'}"
          >
            {{ word }}
          </div>
        </div>
      </div>
    </div>

    <div class="w-screen fixed top-[-250px]">
      <div
        class="new-word"
        :style="{ transform : newWord ? 'translateY(250px)' : '' }"
      >
        <div>
          <span>Word: </span>
          <input
            v-model="word"
            class="new-word-field"
            placeholder="watermellon"
            style="transform : translateX(38px)"
          />
        </div>
        <div class="mt-2">
          <span>Translation:</span>
          <input
            v-model="translation"
            class="new-word-field"
            placeholder="арбуз"/><br>
        </div>
        <div class="add-button left-1/3" style="background : transparent; cursor: auto"></div>
        <div class="add-button float-right mt-2 left-1/3" style="left : 0" @click="addWord">add</div>
      </div>
    </div>

    <div class="words-actions">
      <div class="translate-all" @click="showedWord='translateAll'">Translate all</div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      word: '',
      translation: '',
      showedWord: '',
      newWord: false,
      wordsList: ['pleasure', 'kind of dumb', 'unleashed', 'cuz', 'wind up', 'admit'],
      words: {
        pleasure: 'удовольствие',
        'kind of dumb': 'тупость',
        unleashed: 'освобожденный',
        cuz: 'потому что',
        'wind up': 'заводить (часы)',
        'admit': 'признаться'
      }
    }
  },
  mounted() {
    this.$refs.addButton.onclick = (event) => {
      this.newWord = true;
      event.stopPropagation()
    }
  },
  methods: {
    showWord(word) {
      if (word !== this.showedWord) {
        this.showedWord = word
      } else {
        this.showedWord = ''
      }
    },
    addWord() {
      if (this.word && this.translation) {
        this.wordsList.push(this.word)
        this.words[this.word] = this.translation
      }
    }
  }
}
</script>
