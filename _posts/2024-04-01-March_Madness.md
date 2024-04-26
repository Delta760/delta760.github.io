---
toc: true
comments: false
title: March Madness
layout: post
description: I got a glock in my rari 17 shot from 38
type: tangibles
courses: { compsci: {week: 2}}
permalink: /MM
---

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>March Madness Predictor</title>
</head>
<body>
    <h1>March Madness Predictor</h1>
    <form id="teamForm">
        <label for="teamName">Team Name:</label>
        <input type="text" id="teamName" name="teamName" required><br><br>
        
        <label for="ppg">Points Per Game:</label>
        <input type="number" id="ppg" name="ppg" min="0" required><br><br>
        
        <label for="oppg">Opponent Points Per Game:</label>
        <input type="number" id="oppg" name="oppg" min="0" required><br><br>
        
        <label for="apg">Assists Per Game:</label>
        <input type="number" id="apg" name="apg" min="0" required><br><br>
        
        <label for="rpg">Rebounds Per Game:</label>
        <input type="number" id="rpg" name="rpg" min="0" required><br><br>
        
        <button type="submit">Predict</button>
    </form>
    
    <div id="result"></div>

    <script>
        document.getElementById('teamForm').addEventListener('submit', function(event) {
            event.preventDefault();
            
            // Collect form data
            const teamName = document.getElementById('teamName').value;
            const ppg = parseFloat(document.getElementById('ppg').value);
            const oppg = parseFloat(document.getElementById('oppg').value);
            const apg = parseFloat(document.getElementById('apg').value);
            const rpg = parseFloat(document.getElementById('rpg').value);
            
            // Make POST request to backend API
                        fetch('http://127.0.0.1:5000/predict', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({
                    teamName: teamName,
                    PPG: ppg,
                    OPPG: oppg,
                    APG: apg,
                    RPG: rpg
                })
            })
            .then(response => response.json())
            .then(data => {
                document.getElementById('result').innerHTML = `<p>Predicted outcome: ${data.outcome}</p>`;
            })
            .catch(error => {
                console.error('Error:', error);
                document.getElementById('result').innerHTML = `<p>Error: ${error.message}</p>`;
            });
        });
    </script>
</body>
</html>
