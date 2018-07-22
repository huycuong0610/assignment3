<template>
  <div id="menu">
    <h1>Accessible Drop Down Menu</h1>
    <p><button tabindex="0" @click="startRecord()">Record</button></p>
    <p
      class="script"
      :style="{display: results && results.length ? 'block' : 'none'}">
      {{results}}
    </p>
    <nav role="navigation">
        <ul class="access-menu">
            <li v-for="(value, key) in menu" :key="key">
                <a v-shortkey.focus="[value.key]" href="#" >{{ key }}</a>
                <ul class="access-submenu">
                  <a v-for="children in value.childs" :key="children" href="#"><li> {{children}} </li></a>
                </ul>
            </li>
        </ul>
    </nav>
  </div>
</template>

<script>

export default {
  name: 'Menu',
  data () {
    return {
      results: '',
      menu: {
        Womens: {
          childs: [
            'Featured',
            'Shoes',
            'Clothing',
            'Accessories',
            'Sports',
            'Sale'
          ],
          key: 1
        },
        Mens: {
          childs: [
            'Featured',
            'Shoes',
            'Clothing',
            'Accessories',
            'Sports',
            'Sale'
          ],
          key: 2
        },
        Kids: {
          childs: [
           'Featured',
           'Boys',
           'Girls',
           'Infant',
           'Sale'],
           key: 3
        },
        Sale: {
          childs: [
              'Men\'s Sale',
              'Women\'s Sale',
              'Plus Sale',
              'Kids\' Sale'
              ],
              key: 4
        }
      },
      
    }
  },
  mounted() {
          var SpeechRecognition = SpeechRecognition || webkitSpeechRecognition;
          var SpeechGrammarList = SpeechGrammarList || webkitSpeechGrammarList;
          var SpeechRecognitionEvent = SpeechRecognitionEvent || webkitSpeechRecognitionEvent;
let speechList = {
      functions: ['open'],
      methods: ['link'],
      numbers: ['one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine']
    }
    let grammarNumbers = ''
    for (let i = 0; i < speechList.numbers.length; ++i) {
      grammarNumbers += `${i === 0 ? '' : ' '}(${i} | ${speechList.numbers[i]})`
    }
    let grammar = `#JSGF V1.0;
                    grammar menu;
                    <functions> = ${speechList.functions.join(' | ')} ;
                    <methods> = ${speechList.methods.join(' | ')} ;
                    <numbs> = ${grammarNumbers} ;
                    public <command> = <functions> <methods> number <numbs> `;
          if (SpeechRecognition) {
                let speechRecognitionList = new SpeechGrammarList()
                speechRecognitionList.addFromString(grammar, 1)
                this.recognition = new SpeechRecognition()
                this.recognition.grammars = speechRecognitionList
                this.recognition.lang = 'en-US'
                this.recognition.interimResults = true
                this.recognition.maxAlternatives = 1
                this.recognition.onstart = () => {
                    this.results = 'Recording'
                    this.synth('Recording')
                }
                this.recognition.onspeechend = () => {
                    this.results = ''
                    this.recognition.stop()
                }

                this.recognition.onend = () => {
                    
                }
                this.recognition.onresult = e => {
                    result = e.results[0][0]['transcript']
                    this.results = result
                }
            }
      },
    methods: {
        startRecord () {
        try {
            this.recognition.start()
        } catch (e) {
            let text = 'Speech recognition stopped.'
            this.recognition.stop()
            this.results = text
            this.synth(text)
        }
        },
        synth (text = '') {
            let synth = window.speechSynthesis
            if (synth && text.length) {
                synth.speak(new SpeechSynthesisUtterance(text))
            }
        },
      }
}
</script>

<!-- Add 'scoped' attribute to limit CSS to this component only -->
<style scoped>
</style>
