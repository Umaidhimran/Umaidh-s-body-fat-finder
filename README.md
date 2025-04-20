<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Umaidh's Body Fat Finder</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f2f2f2;
      text-align: center;
      padding: 20px;
    }
    .container {
      background: #fff;
      max-width: 400px;
      margin: auto;
      padding: 20px;
      border-radius: 15px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    input, select, button {
      margin: 10px 0;
      width: 100%;
      padding: 10px;
      border-radius: 8px;
      border: 1px solid #ccc;
    }
    button {
      background-color: #4CAF50;
      color: white;
      font-weight: bold;
      border: none;
    }
    .result {
      margin-top: 20px;
      font-size: 18px;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>Umaidh's Body Fat Finder</h2>
    <label>Gender:</label>
    <select id="gender">
      <option value="male">Male</option>
      <option value="female">Female</option>
    </select><label>Age:</label>
<input type="number" id="age" placeholder="Enter your age" />

<label>Height (cm):</label>
<input type="number" id="height" placeholder="Enter your height" />

<label>Neck circumference (cm):</label>
<input type="number" id="neck" placeholder="Measure around your neck" />

<label>Waist circumference (cm):</label>
<input type="number" id="waist" placeholder="Measure at your navel" />

<label id="hipLabel" style="display:none;">Hip circumference (cm):</label>
<input type="number" id="hip" placeholder="Measure around your hips" style="display:none;" />

<button onclick="calculateBF()">Calculate Body Fat %</button>

<div class="result" id="output"></div>

  </div>  <script>
    const genderSelect = document.getElementById("gender");
    const hipInput = document.getElementById("hip");
    const hipLabel = document.getElementById("hipLabel");

    genderSelect.addEventListener("change", () => {
      if (genderSelect.value === "female") {
        hipInput.style.display = "block";
        hipLabel.style.display = "block";
      } else {
        hipInput.style.display = "none";
        hipLabel.style.display = "none";
      }
    });

    function calculateBF() {
      const gender = document.getElementById("gender").value;
      const height = parseFloat(document.getElementById("height").value);
      const neck = parseFloat(document.getElementById("neck").value);
      const waist = parseFloat(document.getElementById("waist").value);
      const hip = parseFloat(document.getElementById("hip").value);

      let bodyFat = 0;

      if (gender === "male") {
        bodyFat = 495 / (1.0324 - 0.19077 * Math.log10(waist - neck) + 0.15456 * Math.log10(height)) - 450;
      } else {
        bodyFat = 495 / (1.29579 - 0.35004 * Math.log10(waist + hip - neck) + 0.22100 * Math.log10(height)) - 450;
      }

      bodyFat = bodyFat.toFixed(1);

      let category = "";
      if (gender === "male") {
        if (bodyFat < 6) category = "Essential Fat";
        else if (bodyFat <= 13) category = "Athlete";
        else if (bodyFat <= 17) category = "Fitness";
        else if (bodyFat <= 24) category = "Average";
        else if (bodyFat <= 29) category = "Overweight";
        else category = "Obese";
      } else {
        if (bodyFat < 14) category = "Essential Fat";
        else if (bodyFat <= 20) category = "Athlete";
        else if (bodyFat <= 24) category = "Fitness";
        else if (bodyFat <= 31) category = "Average";
        else if (bodyFat <= 39) category = "Overweight";
        else category = "Obese";
      }

      const output = `Your Body Fat is ${bodyFat}%<br>Category: <b>${category}</b>`;
      document.getElementById("output").innerHTML = output;
    }
  </script></body>
</html>
