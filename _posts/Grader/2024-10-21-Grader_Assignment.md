---
toc: true
layout: post
title: Assignment Management
description: Assignment management system
categories: [Collaboration]
type: ccc
---

<!-- Section for Adding Assignments -->
<div>
  <h3>Add Assignment</h3>
  <form id="addAssignmentForm">
    <label for="assignmentName">Assignment Name:</label>
    <input type="text" id="assignmentName" required>
    <button type="submit">Add Assignment</button>
  </form>
</div>

<!-- Display All Assignments -->
<div>
  <h3>All Assignments</h3>
  <table>
    <thead>
      <tr>
        <th>Assignment ID</th>
        <th>Assignment Name</th>
      </tr>
    </thead>
    <tbody id="assignmentTable">
      <!-- Rows will be dynamically added here -->
    </tbody>
  </table>
</div>

<!-- Section for Fetching Assignments by User ID -->
<div>
  <h3>Fetch Assignments by User ID</h3>
  <label for="userid">User ID:</label>
  <input type="number" id="userid" required>
  <button id="fetchButton">Get Assignments</button>
</div>

<!-- Display User Assignments -->
<div>
  <h3>User Assignments</h3>
  <table>
    <thead>
      <tr>
        <th>Name</th>
        <th>Assignment Name</th>
        <th>Grade</th>
      </tr>
    </thead>
    <tbody id="userAssignmentsTable">
      <!-- Rows will be dynamically added here -->
    </tbody>
  </table>
</div>

<script type="module">
  const getAllAssignmentsURL = 'http://localhost:8085/api/assignments/get';
  const addAssignmentURL = 'http://localhost:8085/api/assignments/add';
  const getUserAssignmentsURL = 'http://localhost:8085/api/userassignments/get'; // Correct endpoint for user assignments

  const assignmentTable = document.getElementById("assignmentTable");
  const userAssignmentsTable = document.getElementById("userAssignmentsTable");
  const addAssignmentForm = document.getElementById("addAssignmentForm");
  const assignmentNameInput = document.getElementById("assignmentName");
  const useridInput = document.getElementById("userid");
  const fetchButton = document.getElementById("fetchButton");

  // Function to fetch all assignments
  async function fetchAllAssignments() {
    try {
      const response = await fetch(getAllAssignmentsURL, {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json',
        }
      });

      if (!response.ok) {
        console.error(`Failed to fetch all assignments. Status: ${response.status} - ${response.statusText}`);
        alert("Failed to fetch all assignments. Check the console for more details.");
        return;
      }

      const assignments = await response.json();
      displayAssignments(assignments);
    } catch (error) {
      console.error('Error fetching all assignments:', error);
      alert("An error occurred while fetching all assignments. Check the console for details.");
    }
  }

  // Function to display fetched assignments in the table
  function displayAssignments(assignments) {
    assignmentTable.innerHTML = ""; // Clear any existing rows

    assignments.forEach(assignment => {
      const tr = document.createElement("tr");

      const idCell = document.createElement("td");
      idCell.textContent = assignment.id || "N/A"; // Display the assignment ID

      const nameCell = document.createElement("td");
      nameCell.textContent = assignment.assignmentName || "N/A"; // Display the assignment name

      tr.appendChild(idCell);
      tr.appendChild(nameCell);
      assignmentTable.appendChild(tr);
    });
  }

  // Function to add a new assignment
  async function addAssignment(event) {
    event.preventDefault(); // Prevent form submission

    const assignmentName = assignmentNameInput.value.trim();
    if (!assignmentName) {
      alert("Please enter a valid assignment name.");
      return;
    }

    const data = { assignmentName };

    try {
      const response = await fetch(addAssignmentURL, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(data)
      });

      if (!response.ok) {
        console.error(`Failed to add assignment. Status: ${response.status}`);
        alert("Failed to add assignment.");
        return;
      }

      alert("Assignment added successfully.");
      assignmentNameInput.value = ''; // Clear input field
      fetchAllAssignments(); // Refresh the list after adding an assignment
    } catch (error) {
      console.error('Error adding assignment:', error);
      alert("An error occurred while adding the assignment.");
    }
  }

  // Function to fetch assignments for a specific user ID
  async function fetchUserAssignments() {
    const userid = useridInput.value;

    if (!userid) {
      alert("Please enter a valid User ID");
      return;
    }

    try {
      const response = await fetch(`${getUserAssignmentsURL}/${userid}`, { // Use the correct endpoint
        method: 'GET',
        headers: {
          'Content-Type': 'application/json',
        }
      });

      if (!response.ok) {
        console.error(`Failed to fetch assignments. Status: ${response.status}`);
        alert("Failed to fetch assignments for this User ID.");
        return;
      }

      const userAssignments = await response.json();
      displayUserAssignments(userAssignments);
    } catch (error) {
      console.error('Error fetching user assignments:', error);
      alert("An error occurred while fetching assignments.");
    }
  }

  // Function to display fetched user assignments in the user assignments table
  function displayUserAssignments(userAssignments) {
    userAssignmentsTable.innerHTML = ""; // Clear any existing rows

    userAssignments.forEach(userAssignment => {
      const tr = document.createElement("tr");

      const nameCell = document.createElement("td");
      nameCell.textContent = userAssignment.name || "N/A"; // Display the user's name

      const assignmentNameCell = document.createElement("td");
      assignmentNameCell.textContent = userAssignment.assignmentName || "N/A"; // Display the assignment name

      const gradeCell = document.createElement("td");
      gradeCell.textContent = userAssignment.grade !== null ? userAssignment.grade : "N/A"; // Display the grade

      tr.appendChild(nameCell);
      tr.appendChild(assignmentNameCell);
      tr.appendChild(gradeCell);
      userAssignmentsTable.appendChild(tr);
    });
  }

  // Event listeners
  fetchButton.addEventListener("click", fetchUserAssignments);
  addAssignmentForm.addEventListener("submit", addAssignment);

  // Fetch all assignments on page load
  fetchAllAssignments();
</script>
