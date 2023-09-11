---
toc: true
comments: false
layout: post
title: Roulette
description: A Roulette game commonly found in casino's
courses: { compsci: {week: 3}}
type: tangibles
---

![Roulette_image](/student/images/download.jpeg)

<html>
<head>
    <title>Roulette Game</title>
    <style>

    </style>
</head>
<body>
    <h1>Roulette Game</h1>
    <div id="wheel-container">
        <div id="wheel"></div>
    </div>
    <p>Your Money: $<span id="money">1000</span></p>
    <p>Choose your bet:</p>
    <label><input type="radio" name="betType" value="even"> Even</label>
    <label><input type="radio" name="betType" value="odd"> Odd</label>
    <label><input type="radio" name="betType" value="black"> Black</label>
    <label><input type="radio" name="betType" value="red"> Red</label>
    <label><input type="radio" name="betType" value="number"> Specific Number</label>
    <input type="number" id="betAmount" placeholder="Enter your bet amount">
    <input type="number" id="specificNumber" placeholder="Enter specific number (0-36 or 00)">
    <button onclick="spinWheel()">Spin the Wheel</button>
    <p id="result"></p>

    <script>
        let money = 1000;

        function spinWheel() {
            const betAmount = parseInt(document.getElementById("betAmount").value);
            const betType = document.querySelector('input[name="betType"]:checked').value;
            const specificNumber = parseInt(document.getElementById("specificNumber").value);

            if (isNaN(betAmount) || betAmount <= 0 || betAmount > money) {
                alert("Invalid bet amount. Please enter a valid amount.");
                return;
            }

            if (betType === "number" && (isNaN(specificNumber) || (specificNumber !== 0 && specificNumber !== 00 && (specificNumber < 0 || specificNumber > 36)))) {
                alert("Invalid specific number. Please enter a valid number (0-36 or 00).");
                return;
            }

            const winningNumber = Math.floor(Math.random() * 37);
            const resultElement = document.getElementById("result");

            money -= betAmount;
            document.getElementById("money").textContent = money;

            resultElement.textContent = `Winning number: ${winningNumber}`;

            if (winningNumber === 0) {
                resultElement.textContent += " (0)";
            } else if (winningNumber === 37) {
                resultElement.textContent += " (00)";
            } else if (winningNumber % 2 === 0) {
                resultElement.textContent += " (Even)";
            } else {
                resultElement.textContent += " (Odd)";
            }

            if (betType === "even" && winningNumber % 2 === 0) {
                money += betAmount * 2;
                resultElement.textContent += ` - You win $${betAmount * 2}!`;
            } else if (betType === "odd" && winningNumber % 2 !== 0) {
                money += betAmount * 2;
                resultElement.textContent += ` - You win $${betAmount * 2}!`;
            } else if ((betType === "black" && winningNumber >= 1 && winningNumber <= 10) || 
                       (betType === "red" && (winningNumber === 0 || winningNumber === 37) || (betType === "red" && winningNumber >= 11 && winningNumber <= 18))) {
                money += betAmount * 2;
                resultElement.textContent += ` - You win $${betAmount * 2}!`;
            } else if (betType === "number" && winningNumber === specificNumber) {
                money += betAmount * 36;
                resultElement.textContent += ` - You win $${betAmount * 36}!`;
            } else {
                resultElement.textContent += " - You lose!";
            }

            document.getElementById("money").textContent = money;
        }
    </script>
</body>
</html>

