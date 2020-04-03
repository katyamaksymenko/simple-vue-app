<template>
  <div>
    <div>
      <label for="start">myStart</label>
      <input type="text" value="Row" id="start" v-model="task.myStart">
      <br>
      <label for="end">myEnd</label>
      <input type="text" id="end" v-model="task.myEnd">
      <br>
      <label for="label">label</label>
      <input type="text" id="label" v-model="task.label"> 
      <br>
      <label for="configColor">color</label>
      <input type="text" id="configColor" v-model="task.config.color"> 
      <br>
      <label for="configBgColor">background color</label>
      <input type="text" id="configBgColor" v-model="task.config.backgroundColor"> 
      <br>
      <label for="configOpacity">opacity</label>
      <input type="text" id="configOpacity" v-model="task.config.opacity"> 
      <br>
      <label for="configImmobile">immobile</label>
      <input type="radio" id="configImmobile" v-model="task.config.immobile"> 
      <br>
      <label for="bundle">bundle</label>
      <input type="text" id="bundle" v-model="task.config.bundle"> 
      <br>
      <label for="handles">handles</label>
      <input type="radio" id="handles" v-model="task.config.handles"> 
      <br>
      <label for="background">background</label>
      <input type="text" id="background" v-model="task.config.background"> 
      <br>
      <label for="borderRadius">borderRadius</label>
      <input type="text" id="borderRadius" v-model="task.config.borderRadius"> 
      <br>
      <button v-on:click="$emit('add-task', rowIndex, task)">Submit</button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'EventForm',
  props:{
    rowIndex: {type: Number, required: true},
    task: {type: Object, default: null}
  },
  mounted() {
    if (!this.task) {
      this.task = {
          myStart: '2020-03-02 09:00',
          myEnd: '2020-03-02 12:00',
          label: '123',
          config: {
            color: "white",
            backgroundColor: "#404040",
            opacity: 0.5,
            bundle: "",
            handles: "",
            background: "",
            borderRadius: "",
            immobile: true
          }
        };
    }
  },
}

</script>
