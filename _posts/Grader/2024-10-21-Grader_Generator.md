---
toc: false
layout: my own thing
title: Grader Project
description: Generate hacks
courses: { csa: {week: 7}}
categories: [Collaboration]
type: ccc
---

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
    font-size: 15px;
    margin-top: 10px;
    padding: 15px;
    background-color: #333;  /* Gray background for output box */
    color: white;            /* White text color */
    border: none;
    text-align: center;
    width: 500px;
    box-sizing: border-box;
    margin: 0 auto;
    border-radius: 8px;      /* Optional: Rounded corners */
}

.output p {
    margin: 0;
    padding: 5px 0;
}

.output strong {
    display: block;
    font-size: 18px;
    margin-top: 10px;
}

.output pre {
    color: #f8f8f2;
    font-size: 14px;
    padding: 12px;
    border: none;
    border-radius: 5px;
    font-family: 'Courier New', monospace;
    white-space: pre-wrap;
    overflow-x: auto;
    margin: 15px 0;
    text-align: left;
    background: none;
}

.output code {
    font-size: 15px;
    color: #f8f8f2;
    background: none;
    padding: 0;
    font-family: 'Courier New', monospace;
}

.output .keyword { color: #cc99cd; }
.output .string { color: #f0c674; }
.output .number { color: #8abeb7; }

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
    async function submitRequirements() {
        const topic = document.getElementById('topicInput').value;
        const requirements = document.getElementById('requirementsInput').value;

        const userRequest = {
            topic: topic,
            requirements: requirements
        };

        try {
            const response = await fetch('http://localhost:8764/generate/question', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(userRequest)
            });

            if (!response.ok) {
                throw new Error('Network response was not ok: ' + response.statusText);
            }

            const generatedQuestion = await response.text();
            displayQuestion(generatedQuestion); // Display raw response
        } catch (error) {
            console.error('Error:', error);
            alert('An error occurred while generating the question. Please try again.');
        }
    }

    // Function to display the generated question in the output box
function displayQuestion(question) {
    const outputElement = document.getElementById('output');

    // Replace ** with <strong> tags
    let formattedQuestion = question
        .replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>') // Make text inside ** bold
        .replace(/(?:\r\n|\r|\n)/g, '<br>')  // Replace newline characters with <br>
        .replace(/(A\.\s|B\.\s|C\.\s|D\.\s)/g, '<br><strong>$1</strong>') // Bold options for multiple choice
        .replace(/```([\s\S]*?)```/g, '<pre><code>$1</code></pre>'); // Wrap code blocks with <pre><code>

    outputElement.innerHTML = formattedQuestion;
}



    document.addEventListener('DOMContentLoaded', () => {
        document.getElementById('submitButton').addEventListener('click', submitRequirements);
    });
</script>