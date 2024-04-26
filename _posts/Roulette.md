---
toc: true
comments: false
layout: post
title: Roulette Game
description: Roulette is a game commonly found in casino's. It has multiple kinds of bets such as even, odd, black
courses: { compsci: {week: 4}}
type: hacks
permalink: /Roulette
---

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Roulette Game</title>
  <style>
    table {
      border-collapse: collapse;
    }
    table, th, td {
      border: 1px solid black;
    }
    th, td {
      padding: 10px;
      text-align: center;
    }
  </style>
</head>
<body>
  <h1>Roulette Game</h1>
  <p>Balance: $<span id="balance">100</span></p>
  <table>
    <tr>
      <th>Bet Type</th>
      <th>Bet Amount</th>
      <th>Winning Multiplier</th>
      <th>Action</th>
    </tr>
    <tr>
      <td>Even</td>
      <td><input type="number" id="evenAmount" min="1" value="1"></td>
      <td>2x</td>
      <td><button onclick="placeBet('even')">Place Bet</button></td>
    </tr>
    <tr>
      <td>Odd</td>
      <td><input type="number" id="oddAmount" min="1" value="1"></td>
      <td>2x</td>
      <td><button onclick="placeBet('odd')">Place Bet</button></td>
    </tr>
    <tr>
      <td>Black</td>
      <td><input type="number" id="blackAmount" min="1" value="1"></td>
      <td>2x</td>
      <td><button onclick="placeBet('black')">Place Bet</button></td>
    </tr>
    <tr>
      <td>Red</td>
      <td><input type="number" id="redAmount" min="1" value="1"></td>
      <td>2x</td>
      <td><button onclick="placeBet('red')">Place Bet</button></td>
    </tr>
    <tr>
      <td>Individual Number (0-36)</td>
      <td><input type="number" id="number" min="0" max="36"></td>
      <td>36x</td>
      <td><input type="number" id="numberAmount" min="1" value="1"><button onclick="placeBet('number')">Place Bet</button></td>
    </tr>
  </table>
  
  <script>
    let balance = 100;

    function placeBet(betType) {
      let betAmount;
      switch (betType) {
        case 'even':
          betAmount = parseInt(document.getElementById('evenAmount').value);
          if (betAmount <= balance && betAmount > 0) {
            balance -= betAmount;
            let payout = betAmount * 2;
            balance += payout;
            alert(`You won $${payout}!`);
          } else {
            alert('Invalid bet amount!');
          }
          break;
        case 'odd':
          betAmount = parseInt(document.getElementById('oddAmount').value);
          if (betAmount <= balance && betAmount > 0) {
            balance -= betAmount;
            let payout = betAmount * 2;
            balance += payout;
            alert(`You won $${payout}!`);
          } else {
            alert('Invalid bet amount!');
          }
          break;
        case 'black':
          betAmount = parseInt(document.getElementById('blackAmount').value);
          if (betAmount <= balance && betAmount > 0) {
            balance -= betAmount;
            let payout = betAmount * 2;
            balance += payout;
            alert(`You won $${payout}!`);
          } else {
            alert('Invalid bet amount!');
          }
          break;
        case 'red':
          betAmount = parseInt(document.getElementById('redAmount').value);
          if (betAmount <= balance && betAmount > 0) {
            balance -= betAmount;
            let payout = betAmount * 2;
            balance += payout;
            alert(`You won $${payout}!`);
          } else {
            alert('Invalid bet amount!');
          }
          break;
        case 'number':
          const selectedNumber = parseInt(document.getElementById('number').value);
          betAmount = parseInt(document.getElementById('numberAmount').value);
          if (selectedNumber >= 0 && selectedNumber <= 36 && betAmount <= balance && betAmount > 0) {
            balance -= betAmount;
            let payout = betAmount * 36;
            balance += payout;
            alert(`You won $${payout}!`);
          } else {
            alert('Invalid bet amount or number!');
          }
          break;
        default:
          alert('Invalid bet type!');
      }
      
      document.getElementById('balance').innerText = balance;
    }
  </script>
</body>
</html>
