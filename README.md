# Smart-feeds-
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ID Number Generator</title>
    <style>
        body {
            background-color: #f2f2f2; /* Grey background color */
            font-family: Arial, sans-serif; /* Default font */
            margin: 0;
            padding: 0;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #fff; /* White container background color */
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* Box shadow for container */
            border-radius: 10px; /* Rounded corners for container */
            animation: fadeInUp 0.5s ease forwards; /* Fade-in animation */
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        #title {
            text-align: center;
            font-size: 32px;
            font-weight: bold;
            color: #333; /* Dark grey title color */
            margin-bottom: 30px;
            animation: pulse 1.5s infinite alternate; /* Pulse animation */
        }

        @keyframes pulse {
            from {
                transform: scale(1);
            }
            to {
                transform: scale(1.05);
            }
        }

        #flag {
            position: absolute;
            top: 20px;
            right: 20px;
            width: 100px; /* Adjust width as needed */
            height: auto; /* Maintain aspect ratio */
            animation: rotateFlag 4s linear infinite; /* Rotate animation */
        }

        @keyframes rotateFlag {
            to {
                transform: rotate(360deg);
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1 id="title">Smart Feeding</h1>
        
        <img id="flag" src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/cf/Flag_of_Canada.svg/1200px-Flag_of_Canada.svg.png" alt="Canadian Flag">
        
        <h2>Generate ID</h2>
        <form id="idForm">
            <label for="milk">Do you like milk?</label>
            <select id="milk" name="milk">
                <option value="1">Yes</option>
                <option value="0">No</option>
            </select><br><br>
            
            <label for="refrigerator">Do you have a refrigerator?</label>
            <select id="refrigerator" name="refrigerator">
                <option value="1">Yes</option>
                <option value="0">No</option>
            </select><br><br>
            
            <label for="food">How much food do you eat?</label>
            <select id="food" name="food">
                <option value="00">None</option>
                <option value="01">Little</option>
                <option value="10">Moderate</option>
                <option value="11">A lot</option>
            </select><br><br>
            
            <label for="allergies">Do you have allergies?</label><br>
            <input type="checkbox" id="peanut" name="peanut" value="1">
            <label for="peanut">Peanut</label><br>
            <input type="checkbox" id="treenuts" name="treenuts" value="1">
            <label for="treenuts">Tree Nuts</label><br>
            <input type="checkbox" id="sesame" name="sesame" value="1">
            <label for="sesame">Sesame</label><br>
            <input type="checkbox" id="milkAllergy" name="milkAllergy" value="1">
            <label for="milkAllergy">Milk</label><br>
            <input type="checkbox" id="egg" name="egg" value="1">
            <label for="egg">Egg</label><br>
            <input type="checkbox" id="fish" name="fish" value="1">
            <label for="fish">Fish</label><br><br>

            <label for="people">How many people live in your home?</label>
            <select id="people" name="people">
                <option value="1">1</option>
                <option value="2">2</option>
                <option value="3">3</option>
                <option value="4">4</option>
                <option value="5">5 or more</option>
            </select><br><br>

            <label for="meals">How many times do you eat at home?</label>
            <select id="meals" name="meals">
                <option value="1">1</option>
                <option value="2">2</option>
                <option value="3">3</option>
                <option value="4">4 or more</option>
            </select><br><br>
            
            <button type="button" onclick="generateID()">Generate ID</button>
        </form>
        
        <div id="idOutput"></div>
        
        <h2>Lookup ID</h2>
        <form id="lookupForm">
            <label for="idInput">Enter your ID:</label>
            <input type="text" id="idInput" name="idInput"><br><br>
            <button type="button" onclick="lookupAnswers()">Lookup Answers</button>
        </form>
        
        <div id="lookupOutput"></div>
    </div>

    <script>
        function generateID() {
            var milk = document.getElementById('milk').value;
            var refrigerator = document.getElementById('refrigerator').value;
            var food = document.getElementById('food').value;
            var peanut = document.getElementById('peanut').checked ? '1' : '0';
            var treenuts = document.getElementById('treenuts').checked ? '1' : '0';
            var sesame = document.getElementById('sesame').checked ? '1' : '0';
            var milkAllergy = document.getElementById('milkAllergy').checked ? '1' : '0';
            var egg = document.getElementById('egg').checked ? '1' : '0';
            var fish = document.getElementById('fish').checked ? '1' : '0';
            var people = document.getElementById('people').value;
            var meals = document.getElementById('meals').value;
            
            var id = milk + refrigerator + food + peanut + treenuts + sesame + milkAllergy + egg + fish + people + meals;
            
            document.getElementById('idOutput').innerText = "Your ID Number is: " + id;
        }
        
        function lookupAnswers() {
            var idInput = document.getElementById('idInput').value;
            
            if (idInput.length !== 12) {
                document.getElementById('lookupOutput').innerText = "Please enter a valid 12-digit ID.";
                return;
            }
            
            var milk = idInput.charAt(0) === '1' ? 'Yes' : 'No';
            var refrigerator = idInput.charAt(1) === '1' ? 'Yes' : 'No';
            var food = '';
            switch (idInput.substring(2, 4)) {
                case '00':
                    food = 'None';
                    break;
                case '01':
                    food = 'Little';
                    break;
                case '10':
                    food = 'Moderate';
                    break;
                case '11':
                    food = 'A lot';
                    break;
            }
            
            var allergies = [];
            if (idInput.charAt(4) === '1') allergies.push('Peanut');
            if (idInput.charAt(5) === '1') allergies.push('Tree Nuts');
            if (idInput.charAt(6) === '1') allergies.push('Sesame');
            if (idInput.charAt(7) === '1') allergies.push('Milk');
            if (idInput.charAt(8) === '1') allergies.push('Egg');
            if (idInput.charAt(9) === '1') allergies.push('Fish');

            var people = '';
            switch (idInput.charAt(10)) {
                case '1':
                    people = '1';
                    break;
                case '2':
                    people = '2';
                    break;
                case '3':
                    people = '3';
                    break;
                case '4':
                    people = '4';
                    break;
                case '5':
                    people = '5 or more';
                    break;
            }

            var meals = '';
            switch (idInput.charAt(11)) {
                case '1':
                    meals = '1';
                    break;
                case '2':
                    meals = '2';
                    break;
                case '3':
                    meals = '3';
                    break;
                case '4':
                    meals = '4 or more';
                    break;
            }
            
            document.getElementById('lookupOutput').innerText = "Answers for ID " + idInput + ":\n" +
                "Do you like milk? " + milk + "\n" +
                "Do you have a refrigerator? " + refrigerator + "\n" +
                "How much food do you eat? " + food + "\n" +
                "Do you have allergies? " + (allergies.length > 0 ? allergies.join(', ') : 'None') + "\n" +
                "How many people live in your home? " + people + "\n" +
                "How many times do you eat at home? " + meals;
        }
    </script>
</body>
</html>​
