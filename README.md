<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2×2 Ceiling Calculator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
            color: #333;
        }
        
        .calculator {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            overflow: hidden;
        }
        
        .header {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }
        
        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
        
        .input-section {
            padding: 30px;
            background: #f8f9fa;
        }
        
        .input-group {
            margin-bottom: 25px;
        }
        
        .input-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #555;
            font-size: 1.1em;
        }
        
        .input-group input {
            width: 100%;
            padding: 15px;
            border: 2px solid #e1e5e9;
            border-radius: 10px;
            font-size: 1.1em;
            transition: all 0.3s ease;
        }
        
        .input-group input:focus {
            outline: none;
            border-color: #4facfe;
            box-shadow: 0 0 0 3px rgba(79, 172, 254, 0.1);
        }
        
        .calculate-btn {
            width: 100%;
            padding: 15px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 1.2em;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-top: 20px;
        }
        
        .calculate-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.2);
        }
        
        .results {
            padding: 30px;
            background: white;
        }
        
        .result-card {
            background: #f8f9fa;
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 20px;
            border-left: 5px solid #4facfe;
            transition: all 0.3s ease;
        }
        
        .result-card:hover {
            transform: translateX(5px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .result-title {
            font-size: 1.3em;
            font-weight: 600;
            color: #333;
            margin-bottom: 10px;
        }
        
        .result-value {
            font-size: 1.5em;
            font-weight: 700;
            color: #4facfe;
        }
        
        .result-detail {
            font-size: 0.9em;
            color: #666;
            margin-top: 5px;
        }
        
        .hidden {
            display: none;
        }
        
        .main-t-selector {
            margin: 15px 0;
        }
        
        .main-t-selector label {
            display: inline-block;
            margin-right: 20px;
            font-weight: normal;
            cursor: pointer;
        }
        
        .main-t-selector input[type="radio"] {
            margin-right: 5px;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <div class="header">
            <h1>2×2 Ceiling Calculator</h1>
            <p>Professional ceiling system calculation tool</p>
        </div>
        
        <div class="input-section">
            <div class="input-group">
                <label for="length">Length (L) in feet:</label>
                <input type="number" id="length" step="0.1" min="0" placeholder="Enter length">
            </div>
            
            <div class="input-group">
                <label for="width">Width (W) in feet:</label>
                <input type="number" id="width" step="0.1" min="0" placeholder="Enter width">
            </div>
            
            <div class="input-group">
                <label>Main T Direction:</label>
                <div class="main-t-selector">
                    <label>
                        <input type="radio" name="mainTDirection" value="length" checked>
                        Along Length (L)
                    </label>
                    <label>
                        <input type="radio" name="mainTDirection" value="width">
                        Along Width (W)
                    </label>
                </div>
            </div>
            
            <button class="calculate-btn" onclick="calculate()">Calculate Materials</button>
        </div>
        
        <div class="results hidden" id="results">
            <div class="result-card">
                <div class="result-title">Wall Angles (WA)</div>
                <div class="result-value" id="wallAngles">-</div>
                <div class="result-detail" id="wallAnglesDetail">-</div>
            </div>
            
            <div class="result-card">
                <div class="result-title">Main T (MT)</div>
                <div class="result-value" id="mainT">-</div>
                <div class="result-detail" id="mainTDetail">-</div>
            </div>
            
            <div class="result-card">
                <div class="result-title">Cross T (CT)</div>
                <div class="result-value" id="crossT">-</div>
                <div class="result-detail" id="crossTDetail">-</div>
            </div>
            
            <div class="result-card">
                <div class="result-title">Cross T Packs & Loose</div>
                <div class="result-value" id="crossTPacks">-</div>
                <div class="result-detail" id="crossTPacksDetail">-</div>
            </div>
            
            <div class="result-card">
                <div class="result-title">Eltoro Sheets (ES)</div>
                <div class="result-value" id="eltoroSheets">-</div>
                <div class="result-detail" id="eltoroSheetsDetail">-</div>
            </div>
            
            <div class="result-card">
                <div class="result-title">Eltoro Sheet Packs & Loose</div>
                <div class="result-value" id="eltoroSheetPacks">-</div>
                <div class="result-detail" id="eltoroSheetPacksDetail">-</div>
            </div>
            
            <div class="result-card">
                <div class="result-title">Wire Quantity (WQ)</div>
                <div class="result-value" id="wireQuantity">-</div>
                <div class="result-detail" id="wireQuantityDetail">-</div>
            </div>
            
            <div class="result-card">
                <div class="result-title">Concrete Nails (N)</div>
                <div class="result-value" id="concreteNails">-</div>
                <div class="result-detail" id="concreteNailsDetail">-</div>
            </div>
        </div>
    </div>

    <script>
        function calculate() {
            const length = parseFloat(document.getElementById('length').value);
            const width = parseFloat(document.getElementById('width').value);
            const mainTDirection = document.querySelector('input[name="mainTDirection"]:checked').value;
            
            if (!length || !width || length <= 0 || width <= 0) {
                alert('Please enter valid length and width values');
                return;
            }
            
            // 1. Wall Angles (WA)
            const waRaw = ((length * 2) + (width * 2)) / 10;
            const wallAngles = Number.isInteger(waRaw) ? waRaw : Math.ceil(waRaw);
            
            // 2. Main T (MT)
            let mtRaw;
            if (mainTDirection === 'length') {
                mtRaw = width / 2;
            } else {
                mtRaw = length / 2;
            }
            const mainT = Number.isInteger(mtRaw) ? mtRaw - 1 : mtRaw - 0.5;
            
            // 3. Cross T (CT)
            const ctRaw = (length * width) / 4;
            const crossT = Number.isInteger(ctRaw) ? ctRaw : Math.ceil(ctRaw);
            
            // 3.1. Cross T Packs & Loose
            const ctPacksRaw = crossT / 75;
            const crossTPacks = Math.floor(ctPacksRaw);
            const crossTLoose = crossT - (crossTPacks * 75);
            
            // 4. Eltoro Sheets (ES)
            const eltoroSheets = crossT;
            
            // 4.1. Eltoro Sheet Packs & Loose
            const esPacksRaw = eltoroSheets / 15;
            const eltoroSheetPacks = Math.floor(esPacksRaw);
            const eltoroSheetLoose = eltoroSheets - (eltoroSheetPacks * 15);
            
            // 5. Wire Quantity (WQ)
            const area = width * length;
            const wireQuantity = Math.ceil(area / 500);
            
            // 6. Concrete Nails (N)
            const concreteNails = Math.ceil(area / 1000);
            
            // Display results
            document.getElementById('wallAngles').textContent = wallAngles;
            document.getElementById('wallAnglesDetail').textContent = `Formula: [(${length}×2) + (${width}×2)] ÷ 10 = ${waRaw.toFixed(2)}`;
            
            document.getElementById('mainT').textContent = mainT;
            document.getElementById('mainTDetail').textContent = `Direction: ${mainTDirection}, Raw: ${mtRaw}, Final: ${mainT}`;
            
            document.getElementById('crossT').textContent = crossT;
            document.getElementById('crossTDetail').textContent = `Formula: (${length} × ${width}) ÷ 4 = ${ctRaw.toFixed(2)}`;
            
            document.getElementById('crossTPacks').textContent = `${crossTPacks} packs + ${crossTLoose} loose`;
            document.getElementById('crossTPacksDetail').textContent = `${crossT} ÷ 75 = ${ctPacksRaw.toFixed(2)}`;
            
            document.getElementById('eltoroSheets').textContent = eltoroSheets;
            document.getElementById('eltoroSheetsDetail').textContent = `Same as Cross T quantity`;
            
            document.getElementById('eltoroSheetPacks').textContent = `${eltoroSheetPacks} packs + ${eltoroSheetLoose} loose`;
            document.getElementById('eltoroSheetPacksDetail').textContent = `${eltoroSheets} ÷ 15 = ${esPacksRaw.toFixed(2)}`;
            
            document.getElementById('wireQuantity').textContent = `${wireQuantity} KG`;
            document.getElementById('wireQuantityDetail').textContent = `Area: ${area.toFixed(2)} sq ft, 1 KG per 500 sq ft`;
            
            document.getElementById('concreteNails').textContent = `${concreteNails} KG`;
            document.getElementById('concreteNailsDetail').textContent = `Area: ${area.toFixed(2)} sq ft, 1 KG per 1000 sq ft`;
            
            document.getElementById('results').classList.remove('hidden');
        }
        
        // Add enter key support
        document.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                calculate();
            }
        });
    </script>
</body>
</html>
