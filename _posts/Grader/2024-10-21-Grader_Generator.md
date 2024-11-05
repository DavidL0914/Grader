---
toc: false
layout: my own thing
title: Grader Project
description: Generate hacks
courses: { csa: {week: 7}}
categories: [Collaboration]
type: ccc
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SAGAI Generator</title>
    <style>
        body {
            background-color: black;
            color: white;
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 0;
            padding: 0;
        }

        h1, h2 {
            margin-top: 10px;
        }

        .nav-buttons {
            margin-top: 20px;
        }

        .nav-buttons button {
            background-color: black;
            color: white;
            border: 1px solid white;
            padding: 10px 20px;
            margin: 0 10px;
            cursor: pointer;
            font-size: 16px;
        }

        .nav-buttons button:hover {
            background-color: gray;
        }

        .signout {
            text-align: right;
            padding: 10px;
            margin-right: 20px;
        }

        .container {
            margin-top: 40px;
        }

        .section-title {
            font-size: 36px;
            margin-bottom: 30px;
        }

        .form-box {
            text-align: left;
            margin: 0 auto;
            width: 500px;
        }

        .form-box label {
            display: block;
            margin-bottom: 10px;
            font-size: 18px;
        }

        .form-box input[type="text"] {
            width: 100%;
            padding: 10px;
            margin-bottom: 20px;
            background-color: white;
            color: black;
            border: none;
            font-size: 16px;
        }

        .submit-btn {
            display: block;
            width: 100%;
            background-color: white;
            color: black;
            border: 1px solid white;
            padding: 10px;
            cursor: pointer;
            text-align: center;
            font-size: 18px;
            margin-top: 10px;
            margin-bottom: 20px;
        }

        .submit-btn:hover {
            background-color: gray;
            color: white;
        }

        .output {
            font-size: 18px;
            margin-top: 20px;
            padding: 10px;
            background-color: white;
            color: black;
            border: none;
            text-align: center;
            width: 500px; /* Match input box width */
            box-sizing: border-box;
            margin: 0 auto; /* Center the output box */
        }
    </style>
</head>

<body>

    <!-- Sign out link -->
    <div class="signout">
        <a href="#" style="color: white; text-decoration: none;">Sign out</a>
    </div>

    <!-- SAGAI Header -->
    <h1>SAGAI</h1>
    <h2>Super Advanced Grader Artificial Intelligence</h2>

    <!-- Navigation buttons -->
    <div class="nav-buttons">
        <a href="{{site.baseurl}}/collaboration/2024/10/21/Grader_Home.html">
            <button>Home</button>
        </a>
        <a href="{{site.baseurl}}/collaboration/2024/10/21/Grader_Grader.html">
            <button>Grader</button>
        </a>
        <a href="{{site.baseurl}}/collaboration/2024/10/21/Grader_QNA.html">
            <button>QNA</button>
        </a>
    </div>

    <!-- Main Generator Section -->
    <div class="container">
        <h1 class="section-title">GENERATOR</h1>

        <!-- Generator Form -->
        <div class="form-box">
            <label for="topicInput">Generate a hack:</label>
            <input type="text" id="topicInput" required placeholder="Insert topic here">

            <input type="text" id="requirementsInput" required placeholder="MC, FRQ, or other instructions">

            <button class="submit-btn" type="button" id="submitButton">Generate</button>
        </div>

        <!-- Output Section -->
        <h2>Output question:</h2>
        <div class="output" id="output">Hack will display here</div>

        <script>
            // Function to handle form submission
            async function submitRequirements() {
                // Get user input values
                const topic = document.getElementById('topicInput').value;
                const requirements = document.getElementById('requirementsInput').value;
    
                // Prepare the request payload
                const userRequest = {
                    topic: topic,
                    requirements: requirements
                };
    
                try {
                    const response = await fetch('http://localhost:8085/generate/question', {
                        method: 'POST',
                        headers: {
                            'Content-Type': 'application/json'
                        },
                        body: JSON.stringify(userRequest)
                    });
    
                    if (!response.ok) {
                        throw new Error('Network response was not ok: ' + response.statusText);
                    }
    
                    const generatedQuestion = await response.text(); // Adjust based on actual response structure
                    displayQuestion(generatedQuestion); // Call function to display the question
                } catch (error) {
                    console.error('Error:', error);
                    alert('An error occurred while generating the question. Please try again.');
                }
            }
    
            // Function to display the generated question on the screen
            function displayQuestion(question) {
                const outputElement = document.getElementById('output');
                outputElement.textContent = question; // Set the output to the generated question
            }
    
            // Ensure the DOM is fully loaded before adding event listeners
            document.addEventListener('DOMContentLoaded', () => {
                document.getElementById('submitButton').addEventListener('click', submitRequirements);
            });
        </script>