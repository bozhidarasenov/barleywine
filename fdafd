<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Brite Metric Calc</title>
    <style>
        body { font-family: sans-serif; background-color: #0f172a; color: #f8fafc; display: flex; justify-content: center; padding: 20px; }
        .card { background: #1e293b; padding: 25px; border-radius: 16px; box-shadow: 0 10px 25px rgba(0,0,0,0.3); max-width: 450px; width: 100%; border: 1px solid #334155; }
        h2 { color: #38bdf8; text-align: center; margin-top: 0; }
        .grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-bottom: 20px; }
        label { display: block; font-size: 0.75rem; color: #94a3b8; margin-bottom: 5px; font-weight: bold; }
        input { width: 100%; padding: 12px; border-radius: 8px; border: 1px solid #334155; background: #0f172a; color: #fff; box-sizing: border-box; font-size: 1rem; }
        .section-title { grid-column: span 2; border-bottom: 1px solid #334155; padding-bottom: 5px; margin-top: 10px; color: #38bdf8; font-size: 0.85rem; }
        .result-box { background: #0f172a; padding: 20px; border-radius: 12px; text-align: center; border: 2px solid #38bdf8; grid-column: span 2; margin-top: 10px; }
        .val { font-size: 2.5rem; font-weight: bold; color: #38bdf8; display: block; }
        .unit { font-size: 0.9rem; color: #94a3b8; }
        .info { grid-column: span 2; font-size: 0.75rem; color: #64748b; line-height: 1.5; margin-top: 15px; }
    </style>
</head>
<body>

<div class="card">
    <h2>Brite Metric 🍺</h2>
    
    <div class="grid">
        <div class="section-title">Inputs</div>
        <div>
            <label>Target CO₂ (g/L)</label>
            <input type="number" id="gl" value="5.0" step="0.1" oninput="calc()">
        </div>
        <div>
            <label>Beer Temp (°C)</label>
            <input type="number" id="temp" value="2.0" step="0.5" oninput="calc()">
        </div>
        <div>
            <label>Tank Size (hL/BBL)</label>
            <input type="number" id="tsize" value="20" oninput="calc()">
        </div>
        <div>
            <label>Beer Vol (hL/BBL)</label>
            <input type="number" id="bvol" value="18" oninput="calc()">
        </div>

        <div class="result-box">
            <label style="color:#38bdf8">Equilibrium Headspace Pressure</label>
            <span class="val" id="bar">--</span>
            <span class="unit">Bar (Gauge)</span>
            <div style="margin-top:5px; font-size: 0.8rem; color: #94a3b8;" id="psi-alt">-- PSI</div>
        </div>

        <div class="info">
            <strong>Headspace Ratio:</strong> <span id="h-ratio">--</span>% <br>
            Set your top-pressure regulator to this value overnight to maintain your <strong><span id="target-gl">5.0</span> g/L</strong> without using the stone.
        </div>
    </div>
</div>

<script>
function calc() {
    const gl = parseFloat(document.getElementById('gl').value);
    const tc = parseFloat(document.getElementById('temp').value);
    const tsize = parseFloat(document.getElementById('tsize').value);
    const bvol = parseFloat(document.getElementById('bvol').value);

    if (gl && !isNaN(tc)) {
        // Convert Celsius to Fahrenheit for the standard ASBC formula
        const tf = (tc * 9/5) + 32;
        // Convert g/L to Volumes (1 vol = 1.96 g/L)
        const vols = gl / 1.96;

        // Calculate PSIG
        const term1 = -14.699;
        const term2 = 0.018225 * tf;
        const term3 = 0.001515 * Math.pow(tf, 2);
        const vMult = 5.5476 + (0.04105 * tf) + (0.000657 * Math.pow(tf, 2));
        const psig = term1 + term2 - term3 + (vols * vMult);

        // Convert PSIG to Bar (1 bar = 14.5038 psi)
        const bar = psig / 14.5038;

        // UI Updates
        document.getElementById('bar').innerText = bar.toFixed(2);
        document.getElementById('psi-alt').innerText = psig.toFixed(1) + " PSI";
        document.getElementById('target-gl').innerText = gl.toFixed(1);
        
        if (tsize > 0) {
            const ratio = ((tsize - bvol) / tsize) * 100;
            document.getElementById('h-ratio').innerText = ratio.toFixed(0);
        }
    }
}
calc();
</script>

</body>
</html>
