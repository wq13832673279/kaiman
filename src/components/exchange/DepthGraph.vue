<template>
  <div id="depth_chart" style="position: relative;width: 100%;height: 100%;">
    <canvas id="depthGraph"></canvas>
  </div>
</template>

<script>
    export default {
        name: "depth-graph",
        data:function(){
            return {
              xObj:{},
              yObj:{},
              canvas:null,
              context:null,
              pWidth:600,
              pHeight:500,
              buyPoints:[],
              sellPoints:[]
            }
        },
        props:{
            values:{
              type:Object,
              required:true
            }
        },
        computed:{
            xMin:function () {
              return buyArr[0].price;
            },
            xMax:function () {
              return sellArr[sellArr.length - 1].price;
            },
            yMin:function () {
              return 0;
            },
            yMax:function () {
             return  buyArr[0].amount * 1.2;
            }
        },
        created:function(){
            this.initCanvas();
            this.initPoints();
            this.draw();
        },
        methods: {
          initCanvas(){
            this.canvas = document.getElementById("depthGraph");
            this.canvas.width = this.pWidth = document.getElementById("depth_chart").offsetWidth
            this.canvas.height = this.pHeight = document.getElementById("depth_chart").offsetHeight
            this.context = this.canvas.getContext("2d");
          },
          initPoints(){
            var buy = this.values.bid, sell = this.values.ask;
            if (buy != undefined && sell != undefined) {
              this.xObj.min = buy.lowestPrice;
              this.xObj.max = sell.highestPrice;
            }
          },
          draw() {
            this.drawAxis()

            this.drawBuy()
            this.drawSell()
          },
          drawBuy(){
            this.context.beginPath();
            this.context.moveTo(0, 450)
            for(var i=0;i<this.buyPoints.length;i++){
              this.context.lineTo(this.buyPoints[i].x, this.buyPoints[i].y)
            }
            this.context.fillStyle="#243235" //#392231
            this.context.fill();
          },
          drawSell(){

          },
          drawAxis(){
            this.context.beginPath();
            this.context.moveTo(10,10)
            this.context.lineTo(100,100)
            this.context.lineTo(50,200)
            this.context.strokeStyle="red"
            this.context.stroke()
            this.context.closePath();

            this.context.beginPath();
            this.context.moveTo(0,450)
            this.context.lineTo(600,450)
            this.context.lineTo(600,0)
            this.context.strokeStyle="#61688a"
            this.context.stroke()
            this.context.closePath();

            this.context.beginPath();
            this.context.moveTo(600,450)
            this.context.lineTo(610,450)
            this.context.strokeStyle="#61688a"
            this.context.stroke()
            this.context.closePath();

            this.context.fillStyle ="#61688a"
            this.context.font = '16px Adobe Ming Std'
            this.context.fillText('0',620,455);
          }
        }
    }
</script>

<style scoped>

</style>
