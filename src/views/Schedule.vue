<template>
  <div class="about">
    <h1>UltraLoop full schedule</h1>
    <b-card v-for="entry in entries" v-bind:key="entry.sys.id"
      :title="entry.fields.showName"
      :img-src="entry.fields.picture.fields.file.url"
      img-right
    >
      <p v-for="line in displaySchedule(entry.fields.scheduleRules)" v-bind:key="line">{{ line }}</p>
      
    </b-card>
  </div>
</template>

<script>

const contentful = require("contentful");
const client = contentful.createClient({
  space: "n4jg1qqwyfc5",
  // This is the access token for this space. Normally you get both ID and the token in the Contentful web app
  accessToken: "mLkIwhOgoNpIZgm5S6Q4gmB_GNcH4K8LTwIFVcvPS48"
});

export default {
  data() {
    return {
      entries: []

    }
  },
  mounted() {
    client.getEntries({'content_type': 'schedule'})
      .then(res => res.items)
      .then(entries => this.entries = entries)
      .catch(err => console.log(err));
  },
  methods: {
    displaySchedule(rules) {
      let out = []
      if (rules.recurring == "weekly") {
        rules.days.forEach(day => {
          let startTime = day.startTimeCentral
          let hour = startTime.split(':')[0]
          let minute = startTime.split(':')[1]
          let period = 'AM'

          if (parseInt(hour) > 12) {
            hour = (parseInt(hour) - 12).toString()
            period = 'PM'
          }

          let duration = day.duration
          let deltaHours = Math.floor(duration / 60)
          let endHours = parseInt(hour) + deltaHours
          let endPeriod = period
          let deltaMinutes = duration % 60
          let endMinutes = parseInt(minute) + deltaMinutes
          
          if (endMinutes >= 60) {
            endHours += 1
            endMinutes -= 60
          }

          endMinutes = endMinutes.toString()

          if (endMinutes.length == 1) {
            endMinutes = '0' + endMinutes
          }

          console.log(endHours)
          if (endHours > 11) {
            endHours = endHours - 12
            endPeriod = 'AM'
          }
          out.push(`${day.day.charAt(0).toUpperCase() + day.day.slice(1)}s from ${hour}:${minute}${period} until ${endHours}:${endMinutes}${endPeriod} Central`)
        })
      }
      return out
    }
  }
}
</script>