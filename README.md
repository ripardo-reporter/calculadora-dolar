<!DOCTYPE html>

<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora VET - Dólar</title>
    <style>
        *{margin:0;padding:0;box-sizing:border-box}
        body{font-family:Arial,sans-serif;background:#f5f5f5;padding:10px}
        .calc{max-width:400px;margin:0 auto;background:#fff;border-radius:8px;box-shadow:0 2px 10px rgba(0,0,0,0.1);overflow:hidden}
        .header{background:#2c3e50;color:#fff;padding:15px;text-align:center}
        .header h2{font-size:1.3rem;margin-bottom:5px}
        .header p{font-size:0.9rem;opacity:0.9}
        .body{padding:20px}
        .info{background:#f8f9fa;padding:10px;border-radius:5px;margin-bottom:15px;font-size:0.85rem}
        .row{display:flex;justify-content:space-between;margin-bottom:3px}
        .form-group{margin-bottom:12px}
        label{display:block;margin-bottom:5px;font-weight:bold;color:#333;font-size:0.9rem}
        input{width:100%;padding:8px;border:1px solid #ddd;border-radius:4px;font-size:0.9rem}
        input:focus{outline:none;border-color:#3498db}
        .btn{width:100%;padding:10px;background:#3498db;color:#fff;border:none;border-radius:4px;font-size:1rem;font-weight:bold;cursor:pointer;margin-top:5px}
        .btn:hover{background:#2980b9}
        .results{background:#27ae60;color:#fff;padding:15px;border-radius:5px;margin-top:15px;display:none}
        .results.show{display:block}
        .result{display:flex;justify-content:space-between;margin-bottom:8px;font-size:0.9rem}
        .result:last-child{font-weight:bold;font-size:1rem;padding-top:8px;border-top:1px solid rgba(255,255,255,0.3)}
    </style>
</head>
<body>
    <div class="calc">
        <div class="header">
            <h2>Calculadora VET</h2>
            <p>Dólar Comercial</p>
        </div>
        <div class="body">
            <div class="info">
                <div class="row"><span>Spread:</span><strong>0,90%</strong></div>
                <div class="row"><span>IOF:</span><strong>3,50%</strong></div>
                <div class="row"><span>Fórmula:</span><strong>Cotação × 1,009 × 1,035</strong></div>
            </div>
            <div class="form-group">
                <label>Cotação USD (R$)</label>
                <input type="number" id="cotacao" step="0.01" placeholder="5.15">
            </div>
            <div class="form-group">
                <label>Valor USD</label>
                <input type="number" id="valor" step="0.01" placeholder="1000.00">
            </div>
            <button class="btn" onclick="calc()">Calcular VET</button>
            <div class="results" id="results">
                <div class="result"><span>Cotação base:</span><span id="base">R$ 0,0000</span></div>
                <div class="result"><span>Cotação + Spread:</span><span id="spread">R$ 0,0000</span></div>
                <div class="result"><span>Cotação VET:</span><span id="iof">R$ 0,0000</span></div>
                <div class="result"><span>Valor Total:</span><span id="vet">R$ 0,00</span></div>
            </div>
        </div>
    </div>
    <script>
        function fmt(v){return new Intl.NumberFormat('pt-BR',{style:'currency',currency:'BRL'}).format(v)}
        function calc(){
            const c=parseFloat(document.getElementById('cotacao').value);
            const v=parseFloat(document.getElementById('valor').value);
            if(!c||!v||c<=0||v<=0){alert('Preencha os campos corretamente');return}

```
        // Aplica spread na cotação
        const cotacaoComSpread = c * 1.009;
        const valorSpread = cotacaoComSpread - c;
        
        // Aplica IOF na cotação já com spread
        const cotacaoVET = cotacaoComSpread * 1.035;
        const valorIOF = cotacaoVET - cotacaoComSpread;
        
        // Valores finais
        const base = c * v;
        const spr = valorSpread * v;
        const iof = valorIOF * v;
        const vet = cotacaoVET * v;
        document.getElementById('base').textContent='R$ '+c.toFixed(4).replace('.',',');
        document.getElementById('spread').textContent='R$ '+cotacaoComSpread.toFixed(4).replace('.',',');
        document.getElementById('iof').textContent='R$ '+cotacaoVET.toFixed(4).replace('.',',');
        document.getElementById('vet').textContent=fmt(vet);
        document.getElementById('results').classList.add('show');
    }
    document.addEventListener('keypress',e=>{if(e.key==='Enter')calc()});
</script>
```

</body>
</html>