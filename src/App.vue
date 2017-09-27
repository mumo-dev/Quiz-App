<template>
    <div class="container">
        <div class="row">
            <div class="col-sm-6 col-sm-offset-2">
                <div class="panel panel-default">

                    <div class="panel-primary panel-heading text-center ">
                        <h3>Quiz App</h3>
                    </div>

                    <div class="progress">
                        <div class="progress-bar" role="progressbar" aria-valuenow="60"
                             aria-valuemin="0" aria-valuemax="100"
                             :style="{width: index /questions.length *100 +'%'}">
                            <!--<span class="sr-only">60% Complete</span>-->
                            {{ index }} /{{ questions.length }}
                        </div>
                    </div>


                    <div class="panel-body">
                        <p> {{ questions[currentIndex].question }} </p>
                        <div class="well well-lg bg-info">
                            <!--<form>-->
                                <template v-for="answer in questions[currentIndex].answers">

                                    <input type="radio"   :value="answer" id="answer"
                                           @click="updateAnswer(currentIndex)" v-model="choice" >
                                    <label for="answer"> {{ answer }}</label>
                                    <br>
                                </template>

                            <!--</form>-->
                        </div>
                        <div class="form-group" v-if="display">
                            <button class="btn btn-primary pull-right"
                                    :disabled="choice===''"
                                    @click="updateQuestion">
                                {{ index < questions.length?'Next':'Finish'}} </button>
                        </div>
                        <div class="alert alert-info" v-else>
                            Your score is {{ Math.round(score/questions.length * 100,2) }} %
                            <br>
                            <button class="btn btn-primary" @click="reset">Reset Quiz</button>
                        </div>
                    </div>

                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data(){
            return {
                questions:[
                    {
                        question:'Capital city of Kenya?',
                        answers:['Nairobi','Mombasa','Kisii'],
                        correct:'Nairobi'
                    },
                    {
                        question:'Capital city of Uganda?',
                        answers:['Luanda','Mombasa','Kampala'],
                        correct:'Kampala'
                    },
                    {
                        question:'Capital city of TZ?',
                        answers:['Dodoma','Daresalam','Maputo'],
                        correct:'Dodoma'
                    },
                    {
                        question:'Capital city of Ethiopia?',
                        answers:['Furaha','Mombasa','Wherever'],
                        correct:'Wherever'
                    },
                    {
                        question:'Capital city of Egypt',
                        answers:['Cairo','Misri','Red Sea'],
                        correct:'Cairo'
                    },
                    {
                        question:'Capital city of Tunisia',
                        answers:['Tunis','Mombasa','Maputo'],
                        correct:'Tunis'
                    }

                ],
                score:0,
                currentIndex:0,
                display:true,
                choice:''

            }
        },
        methods:{
            updateQuestion(){
                if (this.currentIndex < this.questions.length -1){
                    this.currentIndex++;
                    this.choice='';
                }else {
                        this.display = false;
                }
            },
            updateAnswer(index){
                if (this.choice === this.questions[index].correct){
                    this.score++;
                }

            },
            reset(){
                this.currentIndex =0;
                this.score =0;
                this.display =true;
                this.choice=''
            }
        },
        created() {
           this.reset();


        },
        computed:{
            index(){
                return this.currentIndex +1;
            }
        },

    }
</script>

<style scoped>

    /*h3 {*/
        /*color: blue;*/
    /*}*/
    .panel-primary{
        background-color: #337ab7;
        color:white;
    }

    p {
        font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
        font-size: 24px;
        font-style: italic;
        color: blue;
    }

    .bg-info {
        background-color: #d9edf7 !important;
    }

    button {
        padding-left: 20px !important;
        padding-right: 20px !important;
    }
    .progress{
        margin-top:30px;

    }
</style>
