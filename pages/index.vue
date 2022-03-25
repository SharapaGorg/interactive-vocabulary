<template>
  <div ref="root">


    <div @click='newWord = false' class="h-screen overflow-y-auto">
      <div>
        <search class="relative md:left-1/3"/>
        <div class="add-button disable-select md:left-1/3" ref="addButton">
          <span>[+]</span>
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
        <div class="add-button left-1/3" style="background : transparent"></div>
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
      wordsList: ['pleasure', 'kind of dumb', 'unleashed', 'cuz', 'wind up'],
      words: {
        pleasure: 'удовольствие',
        'kind of dumb': 'тупость',
        unleashed: 'освобожденный',
        cuz: 'потому что',
        'wind up': 'заводить (часы)'
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

<style>

.new-word {
  width: fit-content;
  font-family: 'Lato', sans-serif;
  transition: all .5s ease;
  @apply px-5 py-8 mx-auto my-4 rounded-md bg-[#dad5d5]
}

.new-word-field {
  font-family: 'Lato', sans-serif;
  @apply md:w-[300px] outline-none rounded-md bg-[#dad5d5];
  @apply ml-4 py-1 px-2 border-[#6254FF];
  @apply border-[2px];
}

.word {
  font-family: 'Lato', sans-serif;
  transition: all .5s ease;
  @apply px-4 py-2 bg-[#dad5d5] rounded-md text-center;
  @apply font-bold mx-auto border-[#6254FF];
  @apply border-[2px]
}

.translation {
  @apply font-bold mx-auto bg-[#dad5d5] rounded-md;
  @apply border-[0px] border-[#6254FF];
  @apply text-center py-2
}

.add-button {
  @apply px-2 py-1 inline-block relative bg-[#6254FF];
  @apply cursor-pointer w-[120px] text-center text-white font-bold rounded-md
}

.words-actions {
  @apply fixed right-0 bottom-0 bg-[#dad5d5] px-3 py-2 rounded-sm;
}

.translate-all {
  font-family: 'Lato', sans-serif;
  @apply px-2 py-1 text-center bg-[#6254FF] text-white rounded-sm;
  @apply font-bold cursor-pointer;
}

.disable-select {
  user-select: none; /* supported by Chrome and Opera */
  -webkit-user-select: none; /* Safari */
  -khtml-user-select: none; /* Konqueror HTML */
  -moz-user-select: none; /* Firefox */
  -ms-user-select: none; /* Internet Explorer/Edge */
}

</style>
