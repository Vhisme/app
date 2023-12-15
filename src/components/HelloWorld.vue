 <template>
  <div class="app">
    <h1>{{ newdate }}</h1>
    
    <div>
      <p>
        Day: {{ newDay }}
        <span v-if="addedDay !== 0">
          {{ addedDay === 1 ? `(+ ${addedDay} day)` : `(+ ${addedDay} days)` }}
        </span>
      </p>
      <button @click="handleAddedDay">Add Days</button>
    </div>

    <div>
      <p>
        Month: {{ newMonth }}
        <span v-if="addedMonth !== 0">
          {{ addedMonth === 1 ? `(+ ${addedMonth} month)` : `(+ ${addedMonth} months)` }}
        </span>
      </p>
      <button @click="handleAddedMonth">Add Months</button>
    </div>

    <div class="action-btn">
      <button @click="handleChangeDate" class="change-btn" title="Click to set new date">
        Change The World!
      </button>
      <button @click="handleReset" class="reset-btn">Reset</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      date: new Date(),
      addedDay: 0,
      addedMonth: 0,
      newdate: new Date().toString()
    };
  },
  methods: {
    addDay(numberOfDays, baseDate = this.date) {
      const newDate = new Date(baseDate);
      newDate.setDate(newDate.getDate() + numberOfDays);

      return newDate;
    },
    addMonth(numberOfMonths, baseDate = this.date) {
      const newDate = new Date(baseDate);
      newDate.setMonth(newDate.getMonth() + numberOfMonths);

      return newDate;
    },
    handleAddedDay() {
      this.addedDay += 1;
    },
    handleAddedMonth() {
      this.addedMonth += 1;
    },
    handleReset() {
      this.newdate = this.date.toString();
      this.addedDay = 0;
      this.addedMonth = 0;
    },
    handleChangeDate() {
      const resultDate = this.addMonth(this.addedMonth, this.addDay(this.addedDay));
      this.newdate = resultDate.toString();
    }
  },
  computed: {
    newMonth() {
      return this.addMonth(this.addedMonth).getMonth() + 1;
    },
    newDay() {
      return this.addDay(this.addedDay).getDate();
    }
  }
};
</script>



<style>
/* Reset default margin and padding */
body,
html,
div,
h1,
p,
button {
  margin: 0;
  padding: 0;
  font-family: Arial, sans-serif;
  color: #30194f;
}

/* App container */
.app {
  max-width: 400px;
  margin: 0 auto;
  text-align: center;
  padding: 20px;
  border: 1px solid #f7f2f2;
  border-radius: 5px;
  background-color: aqua;
  background-image: url('/src/assets/R.png')
  }

/* Header style */
h1 {
  margin-bottom: 20px;
}

/* Date info section */
div {
  margin-bottom: 20px;
}

/* Action buttons */
.action-btn {
  display: flex;
  justify-content: space-between;
  margin-top: 20px;
}

/* Regular button style */
button {
  padding: 10px 20px;
  border: none;
  border-radius: 3px;
  cursor: pointer;
  background-color: #317984;
  color: #fff;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #00b371;
}

/* Change button style */
.change-btn {
  background-color: #28a77d;
}

.change-btn:hover {
  background-color: #218838;
}

/* Reset button style */
.reset-btn {
  background-color: #685089;
}

.reset-btn:hover {
  background-color: #9923c8;
}
</style>

