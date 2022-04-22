<script setup>

</script>

<template>
  <form class="Passwordform" v-if="Generate" @submit.prevent="GeneratePassword">
      <h1>Password Generator</h1>
      <div class="Password_Generated">
          <p>
              {{Generated_Password}}
          </p>
      </div>
      <label for="length">Lenght</label>
      <select name="length" id="length" v-model="Password_Length">
          <option value="7">7</option>
          <option value="8">8</option>
          <option value="9">9</option>
          <option value="10">10</option>
          <option value="11">11</option>
          <option value="12">12</option>
          <option value="13">13</option>
      </select>
        <div>
            <label for="uppercase">Uppercase</label>
            <input type="checkbox" name="uppercase" id="uppercase" v-model="Uppercase">
        </div>
        <div>
            <label for="numbers">Numbers</label>
            <input type="checkbox" name="numbers" id="numbers" v-model="Numbers">
        </div>
        <div>
            <label for="spechar">Special Characters</label>
            <input type="checkbox" name="spechar" id="spechar" v-model="Special_Characters">
        </div>
        <button @click="Clean()">Clean Preferences</button>
        <button type="submit">Generate Password</button>
  </form>
</template>

<script>
export default {
    props: {
        Generate: Boolean
    },
    data() {
        return {
            Generated_Password: '',
            Password_Length: String,
            Uppercase: Boolean,
            Numbers: Boolean,
            Special_Characters: Boolean,
            Characters: Array.from('abcdefghijklmnñopqrstuvwxyz'),
            UppercaseList: Array.from('ABCDEFGHIJKLMNÑOPQRSTUVWXYZ'),
            NumberList: Array.from('1234567890'),
            Spechar_List: Array.from('!@#$%^&*()_+~`|}{[]:;?><,./-='),
        }
    },
    methods: {
        AddPreference(arg1, arg2) {
            if(arg1 == true) {
                arg2.forEach((ele) => {
                    this.Characters.push(ele)
                })
            }
        },
        Clean() {
            this.Uppercase = false,
            this.Numbers = false,
            this.Special_Characters = false,
            this.Characters = Array.from('abcdefghijklmnñopqrstuvwxyz')
        },
        GeneratePassword() {
            let Password_Length = Math.floor(Number(this.Password_Length))
            this.AddPreference(this.Uppercase, this.UppercaseList)
            this.AddPreference(this.Numbers, this.NumberList)
            this.AddPreference(this.Special_Characters, this.Spechar_List)
            var NewPw = []
            for (let i = 0; i < Password_Length; i++) {
                let RandomI = Math.floor(Math.random() * this.Characters.length)
                NewPw.push(this.Characters[RandomI])
            }
            let Raw = `${NewPw.toString()}`
            let Result = Raw.replace(/,/g, '')
            this.Generated_Password = `${Result}`
        }
    }
}
</script>

<style lang="scss">


.Passwordform {
    background-color: white;
    padding: 40px 0px 40px 0px;
    font-family: sans-serif;
    border: 1px solid gainsboro;
    box-shadow: 2px 2px 4px gainsboro;
    border-radius: 10px;
    margin: auto;
    width: 50%;
    display: flex;
    align-items: center;
    flex-direction: column;
    gap: 15px;

    select, div, button {
        width: 90%;
    }
    div {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    button {
        padding: 20px 0px 20px 0px;
        background-color: green;
        color:white;
        border: none;
        font-size: 1.3em;
    }

    .Password_Generated {
    background-color: rgb(226, 226, 226);
    border-radius: 5px;
    border: 1px solid gainsboro;
    display: block;
    text-align: center;
    font-size: 1.3em;
    }
}
</style>