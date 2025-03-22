<template>
  <div id="app">
    <h1>Weekly Game Schedule</h1>
    <h4><i>A quick reminder of what days your players league is on</i></h4>
    <fieldset style="max-width: 300px">
      <legend>Select your gender:</legend>
      <label>
        <input type="radio" value="male" v-model="gender" />
        Male
      </label>
      <label>
        <input type="radio" value="female" v-model="gender" />
        Female
      </label>
    </fieldset>
    <br />
    <label v-if="gender"
      ><input
        type="checkbox"
        :checked="pick === 'tb_one'"
        @change="getDow('tb_one')"
      />Tee Ball I</label
    ><br />
    <label v-if="gender"
      ><input
        type="checkbox"
        :checked="pick === 'tb_two'"
        @change="getDow('tb_two')"
      />Tee Ball II</label
    ><br />
    <div v-if="gender === 'male'">
      <label
        ><input
          type="checkbox"
          :checked="pick === '8u_baseball'"
          @change="getDow('8u_baseball')"
        />8U Coach Pitch Baseball</label
      ><br />
      <label
        ><input
          type="checkbox"
          :checked="pick === '10u_baseball'"
          @change="getDow('10u_baseball')"
        />10U Kid Pitch Baseball</label
      ><br />
      <label
        ><input
          type="checkbox"
          :checked="pick === '12u_baseball'"
          @change="getDow('12u_baseball')"
        />12U Kid Pitch Baseball</label
      ><br />
      <label
        ><input
          type="checkbox"
          :checked="pick === '14u_baseball'"
          @change="getDow('14u_baseball')"
        />14U Kid Pitch Baseball</label
      ><br />
      <label
        ><input
          type="checkbox"
          :checked="pick === '18u_baseball'"
          @change="getDow('18u_baseball')"
        />18U Kid Pitch Baseball</label
      ><br />
    </div>
    <div v-if="gender === 'female'">
      <label
        ><input
          type="checkbox"
          :checked="pick === '8u_softball'"
          @change="getDow('8u_softball')"
        />8U Coach Pitch Softball</label
      ><br />
      <label
        ><input
          type="checkbox"
          :checked="pick === '10u_softball'"
          @change="getDow('10u_softball')"
        />10U Kid Pitch Softball</label
      ><br />
      <label
        ><input
          type="checkbox"
          :checked="pick === '12u_softball'"
          @change="getDow('12u_softball')"
        />12U Kid Pitch Softball</label
      ><br />
      <label
        ><input
          type="checkbox"
          :checked="pick === '17u_softball'"
          @change="getDow('17u_softball')"
        />17U Kid Pitch Softball</label
      ><br />
    </div>

    <hr v-if="resultText" />
    <div v-if="resultText" class="resultText">
      {{ resultText }}
    </div>
  </div>
</template>

<script>
import { ref, watch } from "vue";

export default {
  setup() {
    const gender = ref("");
    const pick = ref("");
    const resultText = ref("");

    watch(gender, () => {
      pick.value = "";
      resultText.value = "";
    });

    const getLeagueDowText = (pick) => {
      const scheduleMap = {
        tb_one:
          "1 game weekly on Saturday mornings, potentially some Sunday mid-afternoon",
        tb_two: "2 games weekly on Monday, Wednesday, or Friday",
      };

      const twoGamesMWF = [
        "10u_baseball",
        "14u_baseball",
        "10u_softball",
        "17u_softball",
      ];
      const twoGamesTWT = [
        "8u_baseball",
        "12u_baseball",
        "18u_baseball",
        "8u_softball",
        "12u_softball",
      ];

      if (twoGamesMWF.includes(pick))
        return "2 games weekly on Monday, Wednesday, or Friday";
      if (twoGamesTWT.includes(pick))
        return "2 games weekly on Tuesday, Wednesday, or Thursday";

      return scheduleMap[pick] || "";
    };

    const getDow = (pickVal) => {
      pick.value = pickVal;
      resultText.value = getLeagueDowText(pickVal);
      return;
    };

    return {
      gender,
      pick,
      resultText,
      getDow,
    };
  },
};
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  margin: 20px;
}
</style>
