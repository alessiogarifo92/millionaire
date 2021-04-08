<template>
  <div class="home">

    <HelloWorld msg="Who wants to be a MILLIONAIRE?" />

    <img alt="millionario logo" src="../assets/who-wants-to-be-a-millionaire.svg"/>

    <div class="winner" v-if="questionIndex == 7 && startButton == true">
      <h3>{{this.questions[7].quest}}</h3>
    </div>
    <div class="none" v-else>
    </div>

    <button v-if="startButton" type="button" name="button" @click="start()">Start the game</button>

    <div v-if="!startButton &&  questionIndex < 7" class="question">
      <h3>{{this.questions[questionIndex].quest}}</h3>

      <div class="answers">
        <h3
        v-for="(ans, ind) in questions[questionIndex].answers" :key="ind"
        @click="chooseAnswer(ind)"
        :class="{ 'accendiamo' : clicked == ans.correct}">
        {{ans.name}}
      </h3>
      </div>
    </div>

    <button type="button" id="correct" name="button" v-if="prossima" :class="{'none' : startButton == true}" @click="nextQuestion()">Next</button>

    <button type="button" id="wrong" name="button" v-if="ritenta" :class="{'none' : startButton == true}" @click="wrongAnswer()">Restart</button>

  </div>

</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "Home",
  components: {
    HelloWorld,
  },
  data: () => ({
        startButton: true,
        questionIndex: 0,
        clicked: null,
        // illuminazione per settimeout prima di conferma
        illuminazione: '',
        ritenta: false,
        prossima: false,
        questions:[
          {
            id:1,
            quest:"What sort of animal is Walt Disney's Dumbo?",
            answers:[

                {name:'Deer'},
                {name:'Elephant', correct: true},
                {name:'Rabbit'},
                {name:'Donkey'}

            ]
          },
          {
            id:2,
            quest:"Where did Scotch whisky originate?",
            answers:[
              {name:'Ireland'},
              {name:'Scotland', correct: true},
              {name:'Wales'},
              {name:'USA'}
            ]
          },
          {
            id:3,
            quest:"In fancy hotels, it is traditional for what tantalizing treat to be left on your pillow?",
            answers:[
              {name:'A pretzel'},
              {name:'A mint', correct: true},
              {name:'An apple'},
              {name:'A photo of Wolf Blitzer'}
            ]
          },
          {
            id:4,
            quest:"In the United States, what is traditionally the proper way to address a judge?",
            answers:[
              {name:'Your holiness'},
              {name:'Your honor', correct: true},
              {name:'Your eminance'},
              {name:'You da man'}
            ]
          },
          {
            id:5,
            quest:"In which of these films does Whoopi Goldberg dress up as a nun?",
            answers:[
              {name:'Ghost'},
              {name:'Sister Act', correct: true},
              {name:'The Color Purple'},
              {name:'How Judas Got His Groove Back'}
            ]
          },
          {
            id:6,
            quest:"If someone asked to see your ID, what might you show them?",
            answers:[
              {name:'Your tongue'},
              {name:'Your passport', correct: true},
              {name:'Your teeth'},
              {name:'The door'}
            ]
          },
          {
            id:7,
            quest:"Due to the geographical areas they represented, the opposing sides of the US Civil War were known by what names?",
            answers:[
              {name:'The Hills and the Valleys'},
              {name:'The North and the South', correct: true},
              {name:'The Cities and the Farms'},
              {name:'The Kool and the Gang'}
            ]
          },
          {
            id:8,
            quest: "CONGRATULATION!!! YOU JUST WON 1 MILLION BUCKS!!!"
          }

        ]
      }),
  methods: {
    start() {
      this.startButton = false;
      this.questionIndex = 0;
      this.clicked = '';
      return this.questions[this.questionIndex];

      // console.log(this.info);
    },

    chooseAnswer(ind){
      this.clicked = ind;
      // this.questionIndex= this.questions.id;
      let cliccato = this.questions[this.questionIndex].answers[ind].correct;

      if (cliccato !== true) {
        setTimeout(() => { this.ritenta = true, console.log('hai perso')}, 2000);
        ;

      } else {
        setTimeout(() => { this.prossima= true,console.log('puoi procedere alla prossima domanda')}, 2000);
        ;


      }
      // console.log(cliccato);
    },

    nextQuestion(){

      if (this.questionIndex == 6) {
        this.startButton = true;
        this.questionIndex++;
        this.prossima = false;
        console.log('CONGRATULATION!!! YOU JUST WON 1 MILLION BUCKS!!!');
      } else {
        this.questionIndex++;
        this.prossima = false;
        this.clicked = '';
      }
      console.log(this.questionIndex);
    },

    wrongAnswer(){
      this.startButton = true;
       this.clicked = '';
       this.ritenta = false;
       this.prossima = false;
    }
  },
};


</script>

<style media="screen">
  .home{
    color: white;
    display : flex;
    flex-direction: column;
    align-items: center;
  }

  img{
    width: 250px;
    background: none;
    fill: white;
    margin: 20px 0;
  }

  button:hover{
    box-shadow: 0 0 15px white;
  }

  .question{
    border: 1px solid white;
    border-radius: 30px;
    padding: 10px 50px;
    max-width: 900px;
  }

  .answers{
    display: flex;
    justify-content: space-evenly;
    flex-wrap: wrap;
  }

  .answers h3{
    width: 200px;
    border: 1px solid white;
    border-radius: 30px;
    padding: 10px 50px;
  }

  .answers h3:hover{
    background: orange;
  }

  .accendiamo{
    background: green;
    animation: blinking 0.3s;
     animation-iteration-count: 5;
  }

  @keyframes blinking {
  0% { background: green; }
  50% { background: orange; }
  100% { background: green; }
  }

  .winner{
    color:green;
    font-size:50px;
    animation: color-change 3s infinite;
  }

  @keyframes color-change {
  0% { color: red; }
  50% { color: yellow; }
  100% { color: green; }
  }

  .none{
    display:none;
  }

  #correct{
    background: green;
    border: none;
    padding: 15px;
    margin-top: 20px;
    color: white;
    font-size: 20px;
  }

  #wrong{
    background: red;
    border: none;
    padding: 15px;
    margin-top: 20px;
    color: white;
    font-size: 20px;
    animation: error 3s infinite;
  }

  @keyframes error {
  0% { transform: scale(1.0);
      box-shadow: none; }
  50% { transform: scale(1.7);
        box-shadow: 0 0 25px red;}
  100% { transform: scale(1.0);
      box-shadow: none; }
  }


</style>
