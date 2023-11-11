<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <input type="number" v-model="message" placeholder="도감번호를 입력하세요" @change="Calc">
    <p>{{ message }}</p>
  </div>
</template>

<script>

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      message: ""
    }
  },
  methods: {
    Calc(e) {
      const firstInput = e.target.value;
      if (firstInput == "" || Number(firstInput <= 0)) {
        this.Output("번호를 똑바로 입력 바람");
      } else {
        const first_divide = firstInput / 9;
        const number = first_divide.toFixed(2);
        const getPage = this.Page(number);
        const getPosition = this.Position(number);
        let OddEven = "";
        getPage % 2 == 0 ? OddEven = "뒷면" : OddEven = "앞면";
        this.Output(`${getPage}번째 페이지 (${OddEven}), ${getPosition}번칸`);
      }
    },
    Page(value) {
      const mypage = Number(value.toString().split('.')[0]); //소수점을 제외한 정수값만 뽑기
      const set_location = value.toString().split('.')[1]; //정수값을 제외한 소수값만 뽑기
      const set_position = Number(set_location.substring(0, 1)); //소수값 두자리 중 첫번째 자리만 뽑기
      if (set_position) {
        return (mypage + 1); //0페이지부터 시작하기 때문에 + 1을 해줌
      } else if (!set_position) {
        return (mypage); //9배 배수일 경우 자동적으로 +1이 되므로 냅둠
      }
    },
    Position(value) {
      const set_location = value.toString().split('.')[1]; //소수점을 제외한 정수값만 뽑기
      const set_position = Number(set_location.substring(0, 1)); //정수값을 제외한 소수값만 뽑기
      if (set_position) { //소수점 첫번째 자리가 0이 아닐 경우
        return set_position; //몇번째 칸인지 값을 반환
      } else if (!set_position) { //소수점 첫번째 자리가 0일 경우
        return 9; //9의 배수일 경우 0으로 출력되므로 값을 9로 변형
      }
    },
    Output(value) {
      this.message = value;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
