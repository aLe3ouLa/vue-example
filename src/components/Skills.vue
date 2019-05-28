<template>
  <div class="container">
    <div class="holder">
      <form @submit.prevent="addSkill">
        <input
          type="text"
          placeholder="Enter a skill you have.."
          v-model="skill"
          v-validate="'min:5'"
          name="skill"
        >

        <transition name="alert-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
          <p class="alert" v-if="errors.has('skill')">{{errors.first('skill')}}</p>
        </transition>
      </form>

      <ul>
       <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
          <li v-for="(data, index) in skills" :key='index'>
            {{data.skill}}
            <i class="fa fa-minus-circle" v-on:click="removeSkill"></i>
          </li>
        </transition-group>
      </ul>
      <p>These are the skills that you possess.</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Skills",
  data() {
    return {
      skills: [{ skill: "Vue.js" }, { skill: "Front end developer" }],
      skill: ""
    };
  },
  methods: {
    addSkill() {
      this.$validator.validateAll().then((result) => {
        console.log(result)
        if (result) {
          this.skills.push({ skill: this.skill });
          this.skill = "";
        } else {
          console.log("Not valid");
        }
      });
    },
    removeSkill(id) {
      this.skills.splice(id,1);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style src="./Skills.css" scoped></style>
