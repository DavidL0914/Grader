---
toc: false
layout: my own thing
title: QNA
description: Post questions and get replies from peers
categories: [Collaboration]
type: ccc
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Q&A Page</title>
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
            width: 80%; /* Limit container width for consistency */
            margin-left: auto;
            margin-right: auto;
        }

        #ask-question {
            margin-top: 30px;
        }

        textarea {
            width: 50%; /* Adjust the width to a narrower size */
            padding: 10px;
            margin: 10px 0;
            box-sizing: border-box;
            background-color: #333;
            border: 1px solid #555;
            color: white;
            resize: none;
        }

        button {
            padding: 10px 20px;
            margin: 10px;
            background-color: black;
            border: 1px solid white;
            color: white;
            cursor: pointer;
        }

        button:hover {
            background-color: gray;
        }

        .question {
            background-color: #222;
            padding: 10px;
            margin-top: 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .reply-box {
            display: none;
            background-color: #333;
            padding: 10px;
            margin-top: 10px;
        }

        .arrow {
            cursor: pointer;
            font-size: 24px;
            padding: 0 10px;
        }

        .section-title {
            font-size: 36px;
            margin-bottom: 30px;
        }

        .output {
            margin-top: 20px;
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
        <a href="{{site.baseurl}}/collaboration/2024/10/21/Grader_Home.html"><button>Home</button></a>
        <a href="{{site.baseurl}}/collaboration/2024/10/21/Grader_Grader.html"><button>Grader</button></a>
        <a href="{{site.baseurl}}/collaboration/2024/10/21/Grader_Generator.html"><button>Generator</button></a>
    </div>

    <!-- Main Q&A Section -->
    <div class="container">
        <h1 class="section-title">QNA</h1>

        <!-- Question submission section -->
        <div id="ask-question">
            <h2>Ask a Question:</h2>
            <textarea id="question-input" placeholder="Insert question here..."></textarea><br>
            <button onclick="submitQuestion()">Submit Question</button>
        </div>

        <!-- Questions container -->
        <div id="questions-container">
            <h2>Questions</h2>
            <!-- Questions will be dynamically inserted here -->
        </div>
    </div>

    <script>
        let questionCount = 0;

        // Function to submit a new question and append it to the list of questions
        function submitQuestion() {
            const questionText = document.getElementById('question-input').value;
            if (questionText.trim() !== "") {
                const questionContainer = document.getElementById('questions-container');

                // Create the new question element
                const questionDiv = document.createElement('div');
                questionDiv.classList.add('question');
                questionDiv.id = `question-${questionCount}`;

                const questionTextDiv = document.createElement('div');
                questionTextDiv.innerHTML = questionText;

                const arrowDiv = document.createElement('div');
                arrowDiv.classList.add('arrow');
                arrowDiv.innerHTML = '&#9662;'; // Down arrow symbol
                arrowDiv.onclick = () => toggleReplyBox(questionCount);

                questionDiv.appendChild(questionTextDiv);
                questionDiv.appendChild(arrowDiv);

                // Create the reply box (hidden by default)
                const replyDiv = document.createElement('div');
                replyDiv.classList.add('reply-box');
                replyDiv.id = `reply-box-${questionCount}`;

                const replyTextArea = document.createElement('textarea');
                replyTextArea.placeholder = 'Insert your reply here...';

                const replyButton = document.createElement('button');
                replyButton.innerHTML = 'Submit Reply';
                replyButton.onclick = () => submitReply(questionCount, replyTextArea);

                replyDiv.appendChild(replyTextArea);
                replyDiv.appendChild(replyButton);

                // Add everything to the DOM
                questionContainer.appendChild(questionDiv);
                questionContainer.appendChild(replyDiv);

                // Clear input field after submission
                document.getElementById('question-input').value = "";

                questionCount++;
            }
        }

        // Function to toggle reply box visibility
        function toggleReplyBox(questionId) {
            const replyBox = document.getElementById(`reply-box-${questionId}`);
            replyBox.style.display = replyBox.style.display === 'block' ? 'none' : 'block';
        }

        // Function to submit the reply to a question
        function submitReply(questionId, replyTextArea) {
            const replyText = replyTextArea.value;
            if (replyText.trim() !== "") {
                const replyBox = document.getElementById(`reply-box-${questionId}`);
                replyBox.innerHTML = `<p>To answer your question: ${replyText}</p>`;
            }
        }
    </script>

</body>