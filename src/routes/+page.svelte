<script lang="ts">
  const numbers = ["1", "2", "3", "4", "5", "6", "7", "8", "9", "0", "."];
  const operations = ["/", "x", "-", "+", "="];

  let selectedOperation = "";
  let display = "";
  let firstNumber = "";
  let secondNumber = "";
  let isDisplayingResults = false;

  const handleOperationClick = (operation: string) => {
    if (!firstNumber) return;
    if (operation === "=") {
      if (!secondNumber) return;
      const firstNum = parseInt(firstNumber);
      const secondNum = parseInt(secondNumber);

      let results = "";

      switch (selectedOperation) {
        case "/":
          results = (firstNum / secondNum).toFixed(2);
          break;
        case "x":
          results = (firstNum * secondNum).toFixed(2);
          break;
        case "+":
          results = (firstNum + secondNum).toFixed(2);
          break;
        case "-":
          results = (firstNum - secondNum).toFixed(2);
          break;
      }

      display = results;
      isDisplayingResults = true;
    }
    selectedOperation = operation;
  };

  const handleClear = () => {
    firstNumber = "";
    secondNumber = "";
    selectedOperation = "";
    display = "";
    isDisplayingResults = false;
  };

  const handleNumberClick = (number: string) => {
    if (isDisplayingResults) {
      handleClear();
    }
    if (display === "" && number === "0") return;
    if (number === "." && display.includes(".")) return;

    if (!selectedOperation) {
      if (display === "" && number === ".") {
        firstNumber = "0.";
        return (display = firstNumber);
      }
      firstNumber = `${firstNumber}${number}`;
      return (display = firstNumber);
    } else {
      if (display === "" && number === ".") {
        secondNumber = "0.";
        return (display = secondNumber);
      }
      secondNumber = `${secondNumber}${number}`;
      return (display = secondNumber);
    }
  };
</script>

<main>
  <div class="calculator">
    <div class="results"></div>
    <div class="digits">
      <div class="numbers"></div>
      <div class="operations"></div>
    </div>
  </div>
</main>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  main {
    background-color: rgb(78, 78, 78);
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .calculator {
    background-color: rgb(28, 28, 28);
    width: 240px;
    padding: 15px;
    border-radius: 7px;
  }
  .results {
    height: 60px;
    color: white;
    font-size: 50px;
    display: flex;
    flex-direction: row-reverse;
    margin-right: 10px;
  }
  .digits {
    display: flex;
  }
  .operations {
    display: flex;
    flex-direction: column;
  }
  .numbers {
    display: flex;
    flex-wrap: wrap;
    width: 200px;
  }
</style>
