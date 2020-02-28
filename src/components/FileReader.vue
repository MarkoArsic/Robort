<template>
  <div class="container" >
    <div class="row flex" v-show="combinationCounter!=0">
      <p>
        CharactersNo | N =
        <b>{{ n_characters }}</b>
      </p>
      <p>
        Number of command sets | K =
        <b>{{ k_arrays }}</b>
      </p>
      <p ><b>Correct combinations: {{combinationCounter}}</b></p>
    </div>
    <div class="row">
      <div class="col main">
        <div class="custom-file">
          <input type="file" ref="myFile" class="custom-file-input" id="file" @change="readFile" />
          <label class="custom-file-label" for="file">{{fileName}}</label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "FileReader",
  data() {
    return {
      fileName: "Choose File",
      text: "",
      startingArr: [],
      n_characters: null,
      k_arrays: null,
      combinationCounter: 0
    };
  },
  methods: {
    readFile() {
      let file = this.$refs.myFile.files[0];
      this.fileName = this.$refs.myFile.files[0].name;
      let reader = new FileReader();
      reader.readAsText(file, "UTF-8");
      reader.onload = event => {
        this.text = event.target.result;
        this.rearrangeArr();
      };
      reader.onerror = event => {
        console.error(event);
      };
    },
    rearrangeArr() {
      this.startingArr = Array.from(this.text.split(/[\s ]+/));
      this.startingArr.pop();
      let params = this.startingArr.splice(0, 2);
      this.k_arrays = parseInt(params[0]);
      this.n_characters = parseInt(params[1]);
      this.heapPermutation(
        this.startingArr,
        this.startingArr.length,
        this.k_arrays
      );
    },
    heapPermutation(arr, size, n) {
      // if size becomes 1 then check for goal path with obtained permutation
      if (size == 1) {    
        this.willRobotComeBackToZero(arr.join(""));
      }
      for (let i = 0; i < size; i++) {
        this.heapPermutation(arr, size - 1, n);
        // if size is odd, swap first and last element
        if (size % 2 == 1) {
          let temp = arr[0];
          arr[0] = arr[size - 1];
          arr[size - 1] = temp;
        }
        // If size is even, swap with and last element
        else {
          let temp = arr[i];
          arr[i] = arr[size - 1];
          arr[size - 1] = temp;
        }
      }
    },
    willRobotComeBackToZero(pathString) {
      let direction = 0;
      let x = 0;
      let y = 0;
      for (let i = 0; i < pathString.length; i++) {
        // If move is left or right, change direction
        if (pathString[i] == "D") {
          direction = (direction + 1) % 4;
        } else if (pathString[i] == "L") {
          direction = (4 + direction - 1) % 4;
        } else if (pathString[i] == 'P'){
           // If move is P, then  change x or y according to current direction if (pathString.charAt(i) == 'P') 
          if (direction == 0) y++;
          else if (direction == 1) x++;
          else if (direction == 2) y--;
          else x--; // direction == 3
        }
      }
      if (x == 0 && y == 0) {
        this.combinationCounter += 1;
        //console.log("WINNER STRING IS: " + pathString);   
      }
    },
  }
};
</script>
<style lang="css" scoped>
.col {
  margin-top: 3rem;
  padding: 3rem;
}
.main {
  background-color: #42b983;
  border-radius: 10px;
}
input {
  margin: 0;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  cursor: pointer;
}
textarea {
  margin-top: 1rem;
  width: 100%;
  height: 14rem;
  box-sizing: border-box;
  border: none;
}
.flex {
  display: flex;
  flex-direction: column;
}
</style>
