# FRONTEND-1<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Student Dashboard Form</title>
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background-color: #f0f2f5;
    }

    header {
      background-image: url('https://images.unsplash.com/photo-1580587771525-78b9dba3b914?auto=format&fit=crop&w=1350&q=80');
      background-size: cover;
      background-position: center;
      height: 200px;
      color: white;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 32px;
      font-weight: bold;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.7);
    }

    .dashboard {
      max-width: 800px;
      margin: -80px auto 20px;
      background-color: #fff;
      border-radius: 15px;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
      padding: 30px;
      position: relative;
      z-index: 2;
    }

    .form-section {
      display: none;
      animation: fadeIn 0.5s ease;
    }

    .form-section.active {
      display: block;
    }

    h2 {
      text-align: center;
      color: #333;
      margin-bottom: 20px;
    }

    label {
      display: block;
      margin-bottom: 5px;
      font-weight: 600;
      color: #444;
    }

    input, select, button {
      width: 100%;
      padding: 10px;
      margin-bottom: 15px;
      border-radius: 8px;
      border: 1px solid #ccc;
      font-size: 16px;
    }

    button {
      background-color: #007bff;
      color: #fff;
      border: none;
      font-weight: bold;
      cursor: pointer;
    }

    button:hover {
      background-color: #0056b3;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .section-title {
      border-bottom: 2px solid #eee;
      padding-bottom: 10px;
      margin-bottom: 20px;
    }
  </style>
</head>
<body>

<header>
  Welcome to College Dashboard
</header>

<div class="dashboard">
  
  <!-- Step 1: Student Info -->
  <div class="form-section active" id="studentForm">
    <h2 class="section-title">Student Information</h2>
    <form onsubmit="nextStep(event, 'collegeForm')">
      <label>Name:</label><input required>
      <label>Father's Name:</label><input required>
      <label>Roll Number:</label><input required>
      <label>University:</label><input required>
      <label>City:</label><input required>
      <button type="submit">Next</button>
    </form>
  </div>

  <!-- Step 2: College Info -->
  <div class="form-section" id="collegeForm">
    <h2 class="section-title">College Details</h2>
    <form onsubmit="nextStep(event, 'examForm')">
      <label>Year of Study:</label>
      <select id="year" onchange="autoSubjects()">
        <option value="1">1st Year</option>
        <option value="2">2nd Year</option>
        <option value="3">3rd Year</option>
        <option value="4">4th Year</option>
      </select>
      <label>Semester:</label>
      <input type="number" min="1" max="8" required>
      <label>Number of Subjects:</label>
      <input type="number" id="subjects" min="1" max="10" onchange="renderSubjects()" required>
      <div id="subjectInputs"></div>
      <button type="submit">Next</button>
    </form>
  </div>

  <!-- Step 3: Exam Dates -->
  <div class="form-section" id="examForm">
    <h2 class="section-title">Exam Dates</h2>
    <form onsubmit="submitForm(event)">
      <div id="examDates"></div>
      <button type="submit">Submit</button>
    </form>
  </div>

</div>

<script>
  function nextStep(e, nextId) {
    e.preventDefault();
    document.querySelector('.form-section.active').classList.remove('active');
    document.getElementById(nextId).classList.add('active');
  }

  function autoSubjects() {
    const year = document.getElementById('year').value;
    document.getElementById('subjects').value = (year == 1 ? 5 : 6);
    renderSubjects();
  }

  function renderSubjects() {
    const num = +document.getElementById('subjects').value;
    const subjectDiv = document.getElementById('subjectInputs');
    const examDiv = document.getElementById('examDates');
    subjectDiv.innerHTML = '';
    examDiv.innerHTML = '';

    for (let i = 1; i <= num; i++) {
      subjectDiv.innerHTML += <input type="text" name="subject${i}" placeholder="Subject ${i}" required>;
      examDiv.innerHTML += `
        <label>Subject ${i} Exam Date:</label>
        <input type="date" name="exam${i}" required>`;
    }
  }

  function submitForm(e) {
    e.preventDefault();
    alert("Form submitted successfully!");
  }
</script>

</body>
</html>
