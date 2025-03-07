<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Basic Calculator</title>
  <style>
    /* Center the calculator on the page */
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh; /* Full viewport height */
      margin: 0;
      background-color: #f4f4f4; /* Light gray background */
      font-family: Arial, sans-serif; /* Use Arial font */
    }

    /* Styling for the calculator container */
    .calculator {
      background-color: #333; /* Dark gray background */
      padding: 20px;
      border-radius: 10px; /* Rounded corners */
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.5); /* Shadow effect */
    }
    /* Styling for the display input */
    #display {
      width: 100%;
      height: 50px;
      font-size: 24px; /* Larger font size */
      text-align: right; /* Align text to the right */
      padding: 10px;
      margin-bottom: 10px;
      border: none; /* Remove border */
      border-radius: 5px; /* Rounded corners */
      background-color: #444; /* Darker gray background */
      color: #fff; /* White text */
    }
    /* Grid layout for the buttons */
    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr); /* 4 equal columns */
      gap: 10px; /* Space between buttons */
    }

    /* Styling for the buttons */
    button {
      padding: 20px;
      font-size: 18px; /* Medium font size */
      border: none; /* Remove border */
      border-radius: 5px; /* Rounded corners */
      background-color: #555; /* Gray background */
      color: #fff; /* White text */
      cursor: pointer; /* Pointer cursor on hover */
      transition: background-color 0.2s; /* Smooth hover effect */
    }
    /* Hover effect for buttons */
    button:hover {
      background-color: #777; /* Lighter gray on hover */
    }

    /* Active (click) effect for buttons */
    button:active {
      background-color: #999; /* Even lighter gray on click */
    }
  </style>
</head>
<body>
  <!-- Calculator container -->
  <div class="calculator">
    <!-- Display for input and results -->
    <input type="text" id="display" disabled> <!-- Disabled to prevent manual input -->
    <!-- Buttons for digits, operators, and actions -->
    <div class="buttons">
      <!-- Clear button -->
      <button onclick="clearDisplay()">C</button>
      <!-- Division button -->
      <button onclick="appendOperator('/')">/</button>
      <!-- Multiplication button -->
      <button onclick="appendOperator('*')">*</button>
      <!-- Delete last character button -->
      <button onclick="deleteLast()">DEL</button>
      <!-- Digit buttons -->
      <button onclick="appendNumber('7')">7</button>
      <button onclick="appendNumber('8')">8</button>
      <button onclick="appendNumber('9')">9</button>
      <!-- Subtraction button -->
      <button onclick="appendOperator('-')">-</button>
      <!-- Digit buttons -->
      <button onclick="appendNumber('4')">4</button>
      <button onclick="appendNumber('5')">5</button>
      <button onclick="appendNumber('6')">6</button>
      <!-- Addition button -->
      <button onclick="appendOperator('+')">+</button>
      <!-- Digit buttons -->
      <button onclick="appendNumber('1')">1</button>
      <button onclick="appendNumber('2')">2</button>
      <button onclick="appendNumber('3')">3</button>
      <!-- Equals button -->
      <button onclick="calculateResult()">=</button>
      <!-- Digit 0 button -->
      <button onclick="appendNumber('0')">0</button>
      <!-- Decimal point button -->
      <button onclick="appendNumber('.')">.</button>
    </div>
  </div>
  <script>
    // Get the display element
    let display = document.getElementById('display');

    // Function to append numbers to the display
    function appendNumber(number) {
      // Prevent adding multiple decimal points in a single number
      if (number === '.' && display.value.includes('.')) return;
      // Append the number to the display
      display.value += number;
    }
    // Function to append operators to the display
    function appendOperator(operator) {
      // Prevent adding operators if the display is empty
      if (display.value === '') return;
      // Get the last character in the display
      const lastChar = display.value.slice(-1);
      // Prevent adding multiple operators in a row
      if (['+', '-', '*', '/'].includes(lastChar)) return;
      // Append the operator to the display
      display.value += operator;
    }

    // Function to clear the display
    function clearDisplay() {
      // Set the display value to an empty string
      display.value = '';
    }
    // Function to delete the last character
    function deleteLast() {
      // Remove the last character from the display value
      display.value = display.value.slice(0, -1);
    }
    // Function to calculate the result
    function calculateResult() {
      try {
        // Evaluate the expression in the display
        let result = eval(display.value);
        // Check if the result is invalid (NaN or Infinity)
        if (isNaN(result) || !isFinite(result)) {
          throw new Error('Invalid operation');
        }
        // Display the result
        display.value = result;
      } catch (error) {
        // Handle errors (e.g., division by zero)
        display.value = 'Error';
      }
    }
  </script>
</body>
</html>
