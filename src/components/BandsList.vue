<template>
  <div>
    <input type="text" placeholder="Add Band.." v-model="newBand" @keyup.enter="addBand">
    <button @click="addBand"> Add </button>

    <ul>
      <BandItem v-for="band in bands" :key="band.id" :band="band">
        {{band.name}}
      </BandItem>
    </ul>
  </div>
</template>


<script>
import BandItem from '@/components/BandItem.vue'

export default {
  name: 'BandList',
  components: {
    BandItem
  },
  created () {
    fetch('https://my-json-server.typicode.com/abhishek97/json/bands')
      .then(res => res.json())
      .then(res => {
        this.bands = res
      })
  },
  data () {
    return {
      newBand: '',
      bands: [{
        id: 1,
        name: 'Black Sabbath',
        songs: ['Iron Man', 'War Pigs']
      }, {
        id: 2,
        name: 'ColdPlay',
        songs: ['Yellow', 'Fix you', 'Mylo xyloto']
      }]
    }
  },
  methods: {
    addBand () {
      this.bands.push({
        id: Math.floor(Math.random() * 100),
        name: this.newBand,
        songs: []
      })
      this.newBand = ''
    }
  }
}
</script>
