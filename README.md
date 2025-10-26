<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Student Result Management</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>🎓 Student Result Management</h1>

  <div class="form-container">
    <input type="text" id="name" placeholder="Enter Student Name">
    <input type="text" id="roll" placeholder="Enter Roll Number">
    <input type="number" id="mark1" placeholder="Subject 1 Marks">
    <input type="number" id="mark2" placeholder="Subject 2 Marks">
    <input type="number" id="mark3" placeholder="Subject 3 Marks">
    <button id="addBtn">Add Student</button>
  </div>

  <h2>Student Records</h2>
  <table id="resultTable">
    <thead>
      <tr>
        <th>Name</th>
        <th>Roll No</th>
        <th>Total</th>
        <th>Average</th>
        <th>Grade</th>
        <th>Action</th>
      </tr>
    </thead>
    <tbody id="tableBody">
      <!-- Data will appear here -->
    </tbody>
  </table>

  <script src="script.js"></script>
</body>
</html>[10/25, 3:35 PM] Kavi Priya Frnd✨: body {
  font-family: Arial, sans-serif;
  background: #f2f7ff;
  color: #333;
  text-align: center;
  margin: 0;
  padding: 20px;
}

h1 {
  color: #004aad;
  margin-bottom: 20px;
}

.form-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 10px;
  margin-bottom: 20px;
}

input {
  padding: 8px;
  width: 180px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  padding: 8px 16px;
  background: #004aad;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background: #0066cc;
}

table {
  width: 90%;
  margin: 0 auto;
  border-collapse: collapse;
  background: white;
  box-shadow: 0 0 5px rgba(0,0,0,0.1);
}

th, td {
  border: 1px solid #ddd;
  padding: 10px;
}

th {
  background: #004aad;
  color: white;
}

td button {
  background: red;
  color: white;
  padding: 4px 8px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

td button:hover {
  background: darkred;
}
[10/25, 3:35 PM] Kavi Priya Frnd✨: // Get references
const nameInput = document.getElementById('name');
const rollInput = document.getElementById('roll');
const mark1Input = document.getElementById('mark1');
const mark2Input = document.getElementById('mark2');
const mark3Input = document.getElementById('mark3');
const addBtn = document.getElementById('addBtn');
const tableBody = document.getElementById('tableBody');

// Load saved data
let students = JSON.parse(localStorage.getItem('students')) || [];

// Display saved data
displayStudents();

// Add student
addBtn.addEventListener('click', () => {
  const name = nameInput.value.trim();
  const roll = rollInput.value.trim();
  const m1 = Number(mark1Input.value);
  const m2 = Number(mark2Input.value);
  const m3 = Number(mark3Input.value);

  if (!name || !roll || isNaN(m1) || isNaN(m2) || isNaN(m3)) {
    alert('Please enter all fields correctly.');
    return;
  }

  const total = m1 + m2 + m3;
  const avg = (total / 3).toFixed(2);
  let grade = '';

  if (avg >= 90) grade = 'A+';
  else if (avg >= 75) grade = 'A';
  else if (avg >= 60) grade = 'B';
  else if (avg >= 40) grade = 'C';
  else grade = 'Fail';

  const student = { name, roll, total, avg, grade };
  students.push(student);
  localStorage.setItem('students', JSON.stringify(students));

  displayStudents();
  clearInputs();
});

// Display table
function displayStudents() {
  tableBody.innerHTML = '';
  students.forEach((student, index) => {
    const row = document.createElement('tr');
    row.innerHTML = `
      <td>${student.name}</td>
      <td>${student.roll}</td>
      <td>${student.total}</td>
      <td>${student.avg}</td>
      <td>${student.grade}</td>
      <td><button onclick="deleteStudent(${index})">Delete</button></td>
    `;
    tableBody.appendChild(row);
  });
}

// Delete student
function deleteStudent(index) {
  students.splice(index, 1);
  localStorage.setItem('students', JSON.stringify(students));
  displayStudents();
}

// Clear input fields
function clearInputs() {
  nameInput.value = '';
  rollInput.value = '';
  mark1Input.value = '';
  mark2Input.value = '';
  mark3Input.value = '';
}# Program-1
