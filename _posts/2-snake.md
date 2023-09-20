---
toc: true
comments: false
layout: post
title: Snake
description: 2 Player Snake
courses: { compsci: {week: 5} }
type: tangibles
---

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Two-Player Snake Game</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        canvas {
            border: 2px solid black;
        }
    </style>
</head>
<body>
    <canvas id="gameCanvas" width="400" height="400"></canvas>

    <script>
        const canvas = document.getElementById("gameCanvas");
        const ctx = canvas.getContext("2d");

        // Snake properties
        const gridSize = 20;
        let player1 = {
            x: 5,
            y: 5,
            direction: "right",
            tail: [],
            tailLength: 1
        };
        let player2 = {
            x: 15,
            y: 15,
            direction: "left",
            tail: [],
            tailLength: 1
        };

        // Food properties
        let food = {
            x: Math.floor(Math.random() * (canvas.width / gridSize)) * gridSize,
            y: Math.floor(Math.random() * (canvas.height / gridSize)) * gridSize
        };

        // Score
        let score1 = 0;
        let score2 = 0;

        // Game loop
        function gameLoop() {
            movePlayer(player1, "w", "s", "a", "d");
            movePlayer(player2, "ArrowUp", "ArrowDown", "ArrowLeft", "ArrowRight");

            // Check for collision with food
            if (player1.x === food.x && player1.y === food.y) {
                score1++;
                player1.tailLength++;
                food = generateFood();
            }
            if (player2.x === food.x && player2.y === food.y) {
                score2++;
                player2.tailLength++;
                food = generateFood();
            }

            // Check for collision with walls or self
            if (checkCollision(player1) || checkCollision(player2)) {
                alert("Game Over!");
                player1 = resetPlayer();
                player2 = resetPlayer();
                food = generateFood();
                score1 = 0;
                score2 = 0;
            }

            // Clear canvas
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // Draw food
            ctx.fillStyle = "red";
            ctx.fillRect(food.x, food.y, gridSize, gridSize);

            // Draw players
            drawPlayer(player1, "blue");
            drawPlayer(player2, "green");

            // Draw scores
            ctx.fillStyle = "black";
            ctx.font = "20px Arial";
            ctx.fillText(`Player 1: ${score1}`, 10, 30);
            ctx.fillText(`Player 2: ${score2}`, canvas.width - 150, 30);

            // Repeat the loop
            requestAnimationFrame(gameLoop);
        }

        function movePlayer(player, upKey, downKey, leftKey, rightKey) {
            document.addEventListener("keydown", (event) => {
                switch (event.key) {
                    case upKey:
                        if (player.direction !== "down") player.direction = "up";
                        break;
                    case downKey:
                        if (player.direction !== "up") player.direction = "down";
                        break;
                    case leftKey:
                        if (player.direction !== "right") player.direction = "left";
                        break;
                    case rightKey:
                        if (player.direction !== "left") player.direction = "right";
                        break;
                }
            });

            // Move the player
            switch (player.direction) {
                case "up":
                    player.y -= gridSize;
                    break;
                case "down":
                    player.y += gridSize;
                    break;
                case "left":
                    player.x -= gridSize;
                    break;
                case "right":
                    player.x += gridSize;
                    break;
            }

            // Update the tail
            player.tail.unshift({ x: player.x, y: player.y });
            if (player.tail.length > player.tailLength) {
                player.tail.pop();
            }
        }

        function checkCollision(player) {
            if (
                player.x < 0 ||
                player.x >= canvas.width ||
                player.y < 0 ||
                player.y >= canvas.height
            ) {
                return true;
            }

            for (let i = 1; i < player.tail.length; i++) {
                if (player.x === player.tail[i].x && player.y === player.tail[i].y) {
                    return true;
                }
            }

            return false;
        }

        function resetPlayer() {
            return {
                x: 5,
                y: 5,
                direction: "right",
                tail: [],
                tailLength: 1
            };
        }

        function generateFood() {
            return {
                x: Math.floor(Math.random() * (canvas.width / gridSize)) * gridSize,
                y: Math.floor(Math.random() * (canvas.height / gridSize)) * gridSize
            };
        }

        function drawPlayer(player, color) {
            ctx.fillStyle = color;
            ctx.fillRect(player.x, player.y, gridSize, gridSize);

            ctx.fillStyle = "black";
            for (let i = 0; i < player.tail.length; i++) {
                ctx.fillRect(player.tail[i].x, player.tail[i].y, gridSize, gridSize);
            }
        }

        gameLoop();
    </script>
</body>
</html>
