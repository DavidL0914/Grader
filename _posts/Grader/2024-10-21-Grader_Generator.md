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

        .nav-buttons a button {
            background-color: black;
            color: white;
            border: 1px solid white;
            padding: 10px 20px;
            margin: 0 10px;
            cursor: pointer;
            font-size: 16px;
        }

        .nav-buttons a button:hover {
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

        .form-box .output {
            font-size: 18px;
            margin-top: 20px;
        }

        /* Submit Button */
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
        <a href="{{site.baseurl}}/collaboration/2024/10/21/Grader_QNA.html"><button>QNA</button></a>
    </div>

    <!-- Main Generator section -->
    <div class="container">
        <h1 class="section-title">GENERATOR</h1>

        <!-- Generator Form -->
        <div class="form-box">
            <label for="requirements">Generate a hack:</label>
            <textarea id="requirements" placeholder="Insert requirements for hacks here"></textarea>
            <!-- Submit Button for the first textarea -->
            <button class="submit-btn" onclick="submitRequirements()">Submit Requirements</button>

            <label for="output">Output question:</label>
            <textarea id="output" placeholder="Hack will display here"></textarea>
        </div>
    </div>

    <script>
        function submitRequirements() {
            alert("Requirements Submitted!");
            // Logic for handling requirements submission
        }

        function submitOutput() {
            alert("Output Submitted!");
            // Logic for handling output submission
        }
    </script>

</body>
</html>
