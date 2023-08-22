<template>
  <div>
    <h3 class="text-center mt-5">เกมเป่ายิงฉุบ</h3>

    <div class="box-game d-flex justify-content-center mt-5">
      <div class="user1">
        <h5 class="text-center">ผู้เล่น 1</h5>
        <img :src="player1ChoiceImage" alt="">
      </div>

      <div class="user2">
        <h5 class="text-center">ผู้เล่น 2</h5>
        <img :src="player2ChoiceImage" alt="">
      </div>
    </div>

    <div class="button mt-5 d-flex justify-content-center">
      <button class="btn btn-danger" @click="playGame"  data-bs-toggle="modal" data-bs-target="#exampleModal">เกมเป่ายิงฉุบ</button>
    </div>
  </div>

  <div class="score mt-3 text-center">
      <p class="fs-5">{{ scorePlayer1 }} : {{ scorePlayer2 }}</p>
      
    </div>



    <!-- Modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h1 class="modal-title fs-5 text-center" id="exampleModalLabel">ผล</h1>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
      <p class="text-center fs-5 fw-bold text-danger">{{ resultMessage }}</p>
      <img :src="imagesplayer" width="250" height="250">
      </div>
     
    </div>
  </div>
</div>

</template>

<script>
export default {
  data() {
    return {
      choices: ['ค้อน', 'กระดาษ', 'กรรไกร'],
      player1Choice: '',
      player2Choice: '',
      player1ChoiceImage: 'https://i.pinimg.com/736x/b1/d9/9c/b1d99cbd56304d1267ffd77aa32264b6.jpg', // รูปเริ่มต้น
      player2ChoiceImage: 'https://i.pinimg.com/564x/92/36/09/92360976a54730f1880144b3f5b10132.jpg', // รูปเริ่มต้น
      resultMessage: '',
      resultMessage: '',
      scorePlayer1: 0, // คะแนนผู้เล่น 1
      scorePlayer2: 0,  // คะแนนผู้เล่น 2
      
    };
  },
  methods: {
    playGame() {
      const randomIndex1 = Math.floor(Math.random() * this.choices.length);
      const randomIndex2 = Math.floor(Math.random() * this.choices.length);

      this.player1Choice = this.choices[randomIndex1];
      this.player2Choice = this.choices[randomIndex2];

      this.player1ChoiceImage = this.getImagePath(this.player1Choice);
      this.player2ChoiceImage = this.getImagePath(this.player2Choice);

      this.calculateWinner();
    },
    getImagePath(choice) {
      if (choice === 'ค้อน') {
        return 'https://i.pinimg.com/736x/c5/ff/dd/c5ffddec81527a112a48d168e7dfea01.jpg';
      } else if (choice === 'กระดาษ') {
        return 'https://i.pinimg.com/564x/ba/10/b9/ba10b9d4bedadd109770c22d17fa593c.jpg';
      } else if (choice === 'กรรไกร') {
        return 'https://i.pinimg.com/564x/8e/6e/eb/8e6eebb0a1e4677591e211df1304d8e3.jpg';
      }
    },
    calculateWinner() {
      if (this.player1Choice === this.player2Choice) {
        this.resultMessage = 'เสมอ';
        this.imagesplayer = "https://i.pinimg.com/564x/f9/ec/3d/f9ec3d7144a829eaf8bdaa45746ebfc6.jpg"
      } else if (this.player1Choice ==="ค้อน" && this.player2Choice === "กรรไกร" || 
      this.player1Choice ==="กรรไกร" && this.player2Choice === "กระดาษ" ||
       this.player1Choice ==="กระดาษ" && this.player2Choice === "ค้อน"  ) {
        this.resultMessage = 'ผู้เล่น 1 ชนะ';
        this.scorePlayer1++; // เพิ่มคะแนนผู้เล่น 1
        this.imagesplayer ='https://i.pinimg.com/736x/b1/d9/9c/b1d99cbd56304d1267ffd77aa32264b6.jpg';
      } else {
        this.resultMessage = 'ผู้เล่น 2 ชนะ';
        this.scorePlayer2++; // เพิ่มคะแนนผู้เล่น 2
        this.imagesplayer ='https://i.pinimg.com/564x/92/36/09/92360976a54730f1880144b3f5b10132.jpg';
        
      }
    }
    }
  
};
</script>

<style>
.user1,.user2{
  border: 2px solid black;
  padding: 50px;
}
.box-game img{
  width: 250px;
  height: 250px;
}
.user1{
  margin-right: 60px;
}
.modal-body img{
margin-left: 100px;
}
</style>
