<template>
  <div class="app flex flex-col items-center gap-10">
    <h1 class="new-date p-5 rounded shadow-xl">{{ newdate }}</h1>

    <div class="new-day  p-5 rounded shadow-xl">
      <p >
        Day: {{ newDay }}
        <span>
          {{ addedDay === 0 ? null : ` (+ ${addedDay} day)` }}
        </span>
      </p>
      <button @click="handleAddedDay" class="rounded py-2 shadow-md">Add Days</button>
    </div>

    <div class="new-month p-5 rounded shadow-xl">
      <p>
        Month: {{ newMonth }}
        <span>
          {{ addedMonth === 0 ? null : ` (+ ${addedMonth} month)` }}
        </span>
      </p>
      <button @click="handleAddedMonth" class="rounded py-2 shadow-md">Add Months</button>
    </div>

    <div class="action-btn button-last p-5 rounded shadow-xl" >
      <button
        @click="handleAddedDaysAndMonths"
        class="change-btn rounded py-2 shadow-md"
        title="Click to set new date"
      >
        Set Date
      </button>
      <button @click="handleReset" class="reset-btn  rounded mx-5 py-2 shadow-md">Reset</button>
    </div>
  </div>
</template>

<script>
import { ref, computed } from "vue";

const date = new Date();

const addDay = (numberOfDays, baseDate = date) => {
  const newDate = new Date(baseDate);
  newDate.setDate(newDate.getDate() + numberOfDays);

  return newDate;
};

const addMonth = (numberOfMonths, baseDate = date) => {
  const newDate = new Date(baseDate);
  newDate.setMonth(newDate.getMonth() + numberOfMonths);

  return newDate;
};

export default {
  setup() {
    const newdate = ref(date.toString());
    const addedDay = ref(0);
    const addedMonth = ref(0);

    const handleAddedDay = () => {
      addedDay.value++;
    };

    const handleAddedMonth = () => {
      addedMonth.value++;
    };

    const handleAddedDaysAndMonths = () => {
      const resultDate = addMonth(addedMonth.value, addDay(addedDay.value));
      newdate.value = resultDate.toString();
    };

    const newMonth = computed(() => {
      return addMonth(addedMonth.value).getMonth() + 1;
    });

    const newDay = computed(() => {
      return addDay(addedDay.value).getDate();
    });

    const handleReset = () => {
      newdate.value = date.toString();
      addedDay.value = 0;
      addedMonth.value = 0;
    };

    return {
      newdate,
      addedDay,
      addedMonth,
      newMonth,
      newDay,
      handleAddedDay,
      handleAddedMonth,
      handleAddedDaysAndMonths,
      handleReset,
    };
  },
};
</script>

<style scoped>



</style>
