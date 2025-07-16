# Secret Angel
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Value Input App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
            line-height: 1.6;
        }
        h1 {
            color: #2c3e50;
            text-align: center;
        }
        .container {
            background-color: #f9f9f9;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        input, textarea, button {
            width: 100%;
            padding: 10px;
            margin-bottom: 15px;
            border: 1px solid #ddd;
            border-radius: 4px;
            box-sizing: border-box;
        }
        button {
            background-color: #3498db;
            color: white;
            border: none;
            cursor: pointer;
            font-size: 16px;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #2980b9;
        }
        #output {
            margin-top: 20px;
            padding: 15px;
            background-color: #e8f4fc;
            border-radius: 4px;
        }
        .value-item {
            padding: 8px;
            margin: 5px 0;
            background-color: white;
            border-radius: 4px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Value Input App</h1>
        
        <div>
            <label for="valueInput">Enter a value:</label>
            <input type="text" id="valueInput" placeholder="Type something...">
            <button onclick="addValue()">Add Value</button>
        </div>
        
        <div>
            <label for="bulkInput">Or add multiple values (one per line):</label>
            <textarea id="bulkInput" rows="5" placeholder="Value 1
Value 2
Value 3"></textarea>
            <button onclick="addBulkValues()">Add Multiple Values</button>
        </div>
        
        <div id="output">
            <h3>Your Values:</h3>
            <div id="valuesList"></div>
        </div>
    </div>

    <script>
        // Array to store all values
        let values = [];
        
        // Add single value
        function addValue() {
            const input = document.getElementById('valueInput');
            const value = input.value.trim();
            
            if (value) {
                values.push(value);
                input.value = '';
                updateDisplay();
            }
        }
        
        // Add multiple values
        function addBulkValues() {
            const textarea = document.getElementById('bulkInput');
            const lines = textarea.value.split('\n');
            
            lines.forEach(line => {
                const value = line.trim();
                if (value) {
                    values.push(value);
                }
            });
            
            textarea.value = '';
            updateDisplay();
        }
        
        // Update the displayed list
        function updateDisplay() {
            const listDiv = document.getElementById('valuesList');
            listDiv.innerHTML = '';
            
            if (values.length === 0) {
                listDiv.innerHTML = '<p>No values entered yet.</p>';
                return;
            }
            
            values.forEach((value, index) => {
                const item = document.createElement('div');
                item.className = 'value-item';
                item.innerHTML = `
                    <span>${index + 1}. ${value}</span>
                    <button onclick="removeValue(${index})" style="float: right; width: auto; padding: 2px 8px;">×</button>
                `;
                listDiv.appendChild(item);
            });
        }
        
        // Remove a value
        function removeValue(index) {
            values.splice(index, 1);
            updateDisplay();
        }
        
        // Initialize display
        updateDisplay();
    </script>
</body>
</html>
