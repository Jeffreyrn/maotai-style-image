<script setup>
import { ref,onMounted } from 'vue'

defineProps({
  msg: String,
})
const drawMyCanvas = ()=>{
  const canvas = document.getElementById('patternCanvas');
        const ctx = canvas.getContext('2d');
        const canvasWidth = canvas.width;
        const canvasHeight = canvas.height;


        // 创建临时画布
        const tempCanvas = document.createElement('canvas');
        tempCanvas.width = canvasWidth;
        tempCanvas.height = canvasHeight;
        const tempCtx = tempCanvas.getContext('2d');

        // 绘制红色长方形（上）
        tempCtx.fillStyle = 'red';
        tempCtx.fillRect(0, 0, canvasWidth, canvasHeight * 0.2);

        // 绘制金色长方形
        tempCtx.fillStyle = '#b29426';
        tempCtx.fillRect(0, canvasHeight * 0.2, canvasWidth, 285);

        // 绘制红色长方形（下）
        tempCtx.fillStyle = 'red';
        tempCtx.fillRect(0, canvasHeight * 0.8, canvasWidth, canvasHeight * 0.2);

        // 绘制文字
        tempCtx.fillStyle = '#171983';
        tempCtx.font = 'italic bold 40px xingkai';
        tempCtx.textAlign = 'center';
        tempCtx.fillText('这是一行文字', canvasWidth / 2, canvasHeight * 0.3);

        // 绘制白色长方形
        tempCtx.fillStyle = 'white';
      const whiteRectH = 0.35
        tempCtx.fillRect(0, canvasHeight * whiteRectH, canvasWidth, canvasHeight * whiteRectH);

        // 绘制蓝色条纹
        tempCtx.fillStyle = '#171983';
        let stripeHeight = 5;
        let stripeSpacing = 7;
        let stripeMinus = 0.8;
        const numStripes = 5;
        const stripeWidth = canvasWidth;

        for (let i = 0; i < numStripes; i++) {
            const y = canvasHeight * 0.34 + i * (stripeHeight + stripeSpacing);
            tempCtx.fillRect(0, y, stripeWidth, stripeHeight);
            stripeHeight -= stripeMinus
        }

        // 绘制居中的文字
        tempCtx.fillStyle = 'red';
        tempCtx.strokeStyle = 'gold';
        tempCtx.lineWidth = 1.5;
        tempCtx.font = 'italic bold 100px xingkai';
        tempCtx.textAlign = 'center';
        const text = '这是居中的文字';
        const textX = canvasWidth / 2;
        const textY = (canvasHeight * 0.35 + canvasHeight * 0.8) / 2;
        tempCtx.fillText(text, textX, textY);
        tempCtx.strokeText(text, textX, textY);

        tempCtx.fillStyle = '#171983';
        stripeHeight += stripeMinus
        stripeSpacing = 3
        for (let i = 0; i < numStripes; i++) {
            const y = canvasHeight * 0.64 + i * (stripeHeight + stripeSpacing);
            tempCtx.fillRect(0, y, stripeWidth, stripeHeight);
            stripeHeight += stripeMinus
        }
        // 清空原始画布
        ctx.clearRect(0, 0, canvasWidth, canvasHeight);

        ctx.fillStyle='red'
        ctx.fillRect(0, 0, canvasWidth, canvasHeight);
        // 保存当前画布状态
        ctx.save();

        // 平移画布以便旋转后内容居中
        ctx.translate(canvasWidth / 2, canvasHeight / 2);

        // 旋转20度
        const angle = 20 * (Math.PI / 180);
        ctx.rotate(-angle);

        // 计算缩放比例以填满画面
        const scaleFactor = Math.min(canvasWidth / tempCanvas.width, canvasHeight / tempCanvas.height)*1.2;
        ctx.scale(scaleFactor, scaleFactor);

        // 绘制旋转和缩放后的内容
        ctx.drawImage(tempCanvas, -tempCanvas.width / 2, -tempCanvas.height / 2);

        // 恢复画布状态
        ctx.restore();
}
const count = ref(0)
onMounted(()=>{
  window.addEventListener('load',()=>{
  drawMyCanvas()
  })
  
})
</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
    <canvas id="patternCanvas" width="960" height="540"></canvas>
  </div>

</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
