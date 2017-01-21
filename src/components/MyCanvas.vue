<template>
  <canvas id="goodCanvas"></canvas>
</template>

<script>
export default {
  name: 'mycanvas',
  mounted: function () {
    // this.$http.headers.common['Access-Control-Allow-Origin'] = '*'
    // this.$http.headers.common['Access-Control-Request-Method'] = '*'
    console.log(this.$http.headers.common)
    this.$http.get('http://52.79.155.110:3000/getPosition', {headers: {'Access-Control-Allow-Origin': 'http://localhost:8080'}}).then((response) => {
      for (let i = 0; i < list.length; i++) {
        $('#goodCanvas').drawImage({
          layer: true,
          name: decodeURIComponent(list[i].imgURL),
          source: decodeURIComponent(list[i].imgURL),
          x: list[i].posX,
          y: list[i].posY,
          draggable: true,
          bringToFront: true,
          dragstop: function (layer) {
            updatePosition(encodeURIComponent(layer.source), layer.x, layer.y).then(function () {
              console.log('pos saved')
            })
          },
          dblclick: function (layer){
            $('#goodCanvas').removeLayer(layer.name).drawLayers()
            removePosition(encodeURIComponent(layer.source)).then(function () {
              console.log('byebye')

              console.log($('#goodCanvas'))
              console.log('here?')
              console.log(this)
            })
          }
        })
      }
    })
  }
}
</script>
