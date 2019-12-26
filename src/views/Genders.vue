<template>
    <div :class="['genders', correct !== null ? (correct ? 'correct' : 'incorrect') : '']">
        <div :class="['display', loading ? 'loading' : '']">
            <div class="word">
                {{ word }}
            </div>

            <div v-html="sentence" class="sentence"></div>
        </div>

        <div class="controls">
            <div id="der" @click="answer('masculine')" class="button">der</div>
            <div id="die" @click="answer('feminine')" class="button">die</div>
            <div id="das" @click="answer('neutral')" class="button">das</div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                loading: false,
                correct: null,
                word: 'Wilkommen',
                sentence: 'Herzlich <b>Willkommen</b> bei langnexus.io ❤️',
                gender: 'masculine'
            };
        },
        methods: {
            fetchWord() {
                this.loading = true;

                fetch('https://api.langnexus.io/german/word', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    }
                }).then(res => {
                    res.json().then(data => {
                        this.word = data.word.wordBase;
                        this.gender = data.word.gender;
                        this.sentence = data.context.replace(data.word.word, `<b>${data.word.word}</b>`);

                        this.loading = false;
                    });
                });
            },
            answer(ans) {
                if(this.gender.includes(ans)) {
                    this.correct = true;
                    this.fetchWord();
                } else {
                    this.correct = false;
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
    .genders {
        width: 100%;
        height: 100%;

        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;

        &.correct {background: $correct;}
        &.incorrect {background: $incorrect;}

        transition: 300ms;

        .display {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;

            margin-bottom: 4em;

            opacity: 1;

            transition: 300ms;
            width: 40%;
            height: 50%;

            &.loading {
                opacity: 0;
            }

            .word {
                font-size: 3em;
                margin-bottom: 0.5em;
            }

            .sentence {
                text-align: center;

                b {
                    font-weight: 800;
                }
            }
        }

        .controls {
            display: flex;
            flex-direction: row;
            justify-content: space-evenly;
            width: 40%;

            .button {
                width: 7em;
                height: 3em;
                line-height: 3em;
                text-align: center;
                border-radius: 0.25em;
                cursor: pointer;

                &#der {background: $der;}
                &#die {background: $die;}
                &#das {background: $das;}
            }
        }
    }
</style>