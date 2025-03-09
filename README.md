/Fake-News-Detector  
  ├── index.html        (Frontend UI)  
  ├── style.css         (Design and styling)  
  ├── script.js         (Logic for fake news detection)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fake News Detector</title>
    <link rel="stylesheet" href="style.css">
    <script defer src="script.js"></script>
</head>
<body>
    <div class="container">
        <h1>📰 Fake News Detector</h1>
        <input type="text" id="newsInput" placeholder="Enter news headline or URL">
        <button onclick="checkNews()">Check News</button>
        <p id="result"></p>
    </div>
</body>
</html>
body {
    background-color: #f4f4f4;
    font-family: Arial, sans-serif;
    text-align: center;
    color: #333;
}

.container {
    margin-top: 50px;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.2);
    background-color: white;
    max-width: 400px;
    margin: auto;
}

h1 {
    font-size: 24px;
    color: #d63384;
}

input {
    width: 80%;
    padding: 10px;
    border: 2px solid #d63384;
    border-radius: 5px;
    margin-top: 10px;
}

button {
    margin-top: 10px;
    background-color: #d63384;
    color: white;
    padding: 10px 15px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-weight: bold;
}

button:hover {
    background-color: #b02a74;
}

#result {
    margin-top: 20px;
    font-size: 18px;
    font-weight: bold;
}
async function checkNews() {
    let input = document.getElementById("newsInput").value;
    let result = document.getElementById("result");

    if (input.trim() === "") {
        result.innerText = "⚠️ Please enter a headline or URL!";
        result.style.color = "red";
        return;
    }

    result.innerText = "🔍 Checking...";

    // Fake News API Call (Replace with real API key)
    let response = await fetch(`https://factchecktools.googleapis.com/v1alpha1/claims:search?query=${input}&key=YOUR_API_KEY`);
    let data = await response.json();

    if (data.claims && data.claims.length > 0) {
        result.innerText = "🚨 Fake News Alert!";
        result.style.color = "red";
    } else {
        result.innerText = "✅ This news looks real.";
        result.style.color = "green";
    }
}
