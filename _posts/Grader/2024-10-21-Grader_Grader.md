---
toc: false
layout: my own thing
title: Grading Page
description: Grade popcorn hacks and get feedback
categories: [Collaboration]
type: ccc
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SAGAI Grader</title>
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

        .form-box textarea {
            width: 100%;
            height: 150px;
            padding: 10px;
            margin-bottom: 20px;
            background-color: white;
            color: black;
            border: none;
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
        <a href="{{site.baseurl}}/collaboration/2024/10/21/Grader_Generator.html"><button>Generator</button></a>
        <a href="{{site.baseurl}}/collaboration/2024/10/21/Grader_QNA.html"><button>QNA</button></a>
    </div>

    <!-- Main Grader section -->
    <div class="container">
        <h1 class="section-title">GRADER</h1>

        <!-- Grading Form -->
        <div class="form-box">
            <label for="requirements">Requirements:</label>
            <textarea id="requirements" placeholder="Insert code requirements here"></textarea>
            <!-- Submit button for Requirements -->

            <label for="code">Code:</label>
            <textarea id="code" placeholder="Insert your code here"></textarea>
            <!-- Submit button for Code -->
            <button class="submit-btn" onclick="submitCode()">Submit Requirement and Code</button>

            <!-- Displayed output -->
            <div class="output">
                <p><strong>Grade:</strong></p>
                <p><strong>Feedback:</strong></p>
            </div>
        </div>
    </div>

    <script>
        function submitRequirements() {
            alert("Requirements submitted!");
            // Handle the submission of the requirements
        }

        function submitCode() {
            alert("Code submitted!");
            // Handle the submission of the code
        }
    </script>

</body>