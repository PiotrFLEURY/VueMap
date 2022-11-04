<script>
export default {
  // reactive state
  data() {
    return {
      cities: [],
      canvas: null,
      zoom: 0.0,
    }
  },

  // functions that mutate state and trigger updates
  methods: {
    loadCities() {
        fetch('city.json')
            .then(response => response.json())
            .then(data => {
                this.cities = data;
                console.log('loaded ' + this.cities.length + ' cities');
                this.drawPoints();
            });
    },
    loadRoutes() {
        // TODO
    },
    drawLine(x1, y1, x2, y2) {
      let ctx = this.canvas;
      ctx.beginPath();
      ctx.strokeStyle = 'black';
      ctx.lineWidth = 1;
      ctx.moveTo(x1, y1);
      ctx.lineTo(x2, y2);
      ctx.stroke();
      ctx.closePath();
    },
    drawPoints() {
        console.log('drawPoints');
        let ctx = this.canvas;

        // clear canvas first
        ctx.clearRect(0, 0, ctx.canvas.width, ctx.canvas.height);

        ctx.fillStyle = 'black';
        // draw cities points on canvas
        for (let i = 0; i < this.cities.length; i++) {
            //console.log('drawPoint', this.cities[i]);
            let city = this.cities[i];
            ctx.fillRect(city.x, city.y, 2, 2);
        }
    },
    zoomIn() {
        // TODO
    },
    zoomOut() {
        // TODO
    },
  },

  // lifecycle hooks
  mounted() {
      var c = document.getElementById("myCanvas");
      this.canvas = c.getContext('2d');
      
  }
}
</script>

<template>
    <div id="map" class="map">
        <canvas id="myCanvas" width="560" height="360" />
    </div>
    <div class="button-bar">
        <div class="button" @click="zoomIn">Zoom in</div>
        
        <div class="button" @click="zoomOut">Zoom out</div>
    </div>
    <div class="button-bar">
        <div class="button" @click="goUp">Go up</div>
        
    </div>
    <div class="button-bar">
        <div class="button" @click="goLeft">Go left</div>
        <div class="button" @click="loadCities">Load cities</div>
        <div class="button" @click="goRight">Go right</div>
        
    </div>
    <div class="button-bar">
        <div class="button" @click="goDown">Go down</div>
    </div>
</template>

<style>
.button {
    background-color: hsla(160, 100%, 37%, 1);
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: center;
    color: white;
    border-radius: 1em;
    width: 64px;
    height: 64px;
    cursor: pointer;
}
.button-bar {
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
    align-items: center;
    margin-top: 1rem;
}
.map {
    display: block;
    margin-left: auto;
    margin-right: auto;
    width: 560px;
    height: 360px;
    background-color: #eee;
}
#myCanvas {
  border: 1px solid grey;
}
</style>