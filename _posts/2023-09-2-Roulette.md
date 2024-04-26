---
toc: true
comments: false
layout: post
title: Roulette
description: Roulette is a game commonly found in casino's. It has multiple kinds of bets such as even, odd, black, red or even specific numbers. This version of Roulette includes the numbers 0-36 with 0 not counting as even, odd, black, or, red
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
    <p>Place your bets:</p>
    <div id="betOptions">
        <label><input type="radio" name="betType" value="even"> Even</label>
        <label><input type="radio" name="betType" value="odd"> Odd</label>
        <label><input type="radio" name="betType" value="black"> Black</label>
        <label><input type="radio" name="betType" value="red"> Red</label>
        <label><input type="radio" name="betType" value="number"> Specific Number</label>
        <input type="number" id="betAmount" placeholder="Enter your bet amount">
        <input type="number" id="specificNumber" placeholder="Enter specific number (0-36)">
        <button onclick="placeBet()">Place Bet</button>
    </div>
    <button onclick="spinWheel()">Spin the Wheel</button>
    <p id="result"></p>
    <p id="winningNumber"></p>
    <div id="placedBets"></div>

    <script>
        let money = 1000;
        let bets = [];

        function placeBet() {
            const betAmount = parseInt(document.getElementById("betAmount").value);
            const betType = document.querySelector('input[name="betType"]:checked');
            const specificNumber = parseInt(document.getElementById("specificNumber").value);

            if (isNaN(betAmount) || betAmount <= 0 || betAmount > money) {
                alert("Invalid bet amount. Please enter a valid amount.");
                return;
            }

            if (!betType) {
                alert("Select a bet type.");
                return;
            }

            // Clear previous bet outcomes and winning number
            document.getElementById("result").textContent = "";
            document.getElementById("winningNumber").textContent = "";

            const newBet = {
                type: betType.value,
                amount: betAmount,
                specificNumber: betType.value === "number" ? specificNumber : null
            };

            bets.push(newBet);
            displayPlacedBet(newBet);

            document.getElementById("betAmount").value = "";
            document.getElementById("specificNumber").value = "";
            document.querySelectorAll('input[name="betType"]').forEach(input => input.checked = false);

            console.log(bets); // For testing, remove in production
        }

        function displayPlacedBet(bet) {
            const placedBetsDiv = document.getElementById("placedBets");
            const betDiv = document.createElement("div");
            let betText = `Bet: ${bet.type}, Amount: $${bet.amount}`;
            if (bet.type === "number") {
                betText += `, Number: ${bet.specificNumber}`;
            }
            betDiv.textContent = betText;
            placedBetsDiv.appendChild(betDiv);
        }

        function spinWheel() {
            if (bets.length === 0) {
                alert("Place your bets first!");
                return;
            }

            const winningNumber = Math.floor(Math.random() * 36);
            const resultElement = document.getElementById("result");
            const winningNumberElement = document.getElementById("winningNumber");

            winningNumberElement.textContent = `The wheel landed on: ${winningNumber}`;

            // Determine if the winning number is black or red
            const blackNumbers = [15, 4, 2, 17, 6, 13, 11, 8, 10, 24, 33, 20, 31, 22, 29, 28, 35, 26];
            const redNumbers = [32, 19, 21, 25, 34, 27, 36, 30, 23, 5, 16, 1, 14, 9, 18, 7, 12, 3];
            let payoutRatio = 1; // Default payout ratio

            if (blackNumbers.includes(winningNumber)) {
                payoutRatio = 2; // Black number payout ratio
            } else if (redNumbers.includes(winningNumber)) {
                payoutRatio = 2; // Red number payout ratio
            }

            bets.forEach(function(bet) {
                money -= bet.amount;
                resultElement.textContent += `Bet: ${bet.type}, Amount: $${bet.amount} - `;

                if (bet.type === "number" && winningNumber === bet.specificNumber) {
                    money += bet.amount * 36;
                    resultElement.textContent += `You win $${bet.amount * 36}! `;
                } else if (bet.type === "even" && winningNumber % 2 === 0) {
                    money += bet.amount * 2;
                    resultElement.textContent += `You win $${bet.amount * 2}! `;
                } else if (bet.type === "odd" && winningNumber % 2 !== 0) {
                    money += bet.amount * 2;
                    resultElement.textContent += `You win $${bet.amount * 2}! `;
                } else if (bet.type === "black" && blackNumbers.includes(winningNumber)) {
                    money += bet.amount * payoutRatio;
                    resultElement.textContent += `You win $${bet.amount * payoutRatio}! `;
                } else if (bet.type === "red" && redNumbers.includes(winningNumber)) {
                    money += bet.amount * payoutRatio;
                    resultElement.textContent += `You win $${bet.amount * payoutRatio}! `;
                } else {
                    resultElement.textContent += "You lose! ";
                }

                resultElement.innerHTML += "<br>";
            });

            document.getElementById("money").textContent = money;

            // Clear bets array after each spin
            bets = [];
            document.getElementById("placedBets").innerHTML = "";
        }
    </script>
</body>
</html>
