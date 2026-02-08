# <!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora Profissional CDI e Taxa Básica de Juros</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f7fa;
            color: #333;
            line-height: 1.6;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            background: linear-gradient(135deg, #1a237e, #283593);
            color: white;
            padding: 30px 0;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            margin-bottom: 30px;
        }
        
        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 30px;
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .logo i {
            font-size: 2.5rem;
        }
        
        .logo h1 {
            font-size: 1.8rem;
            font-weight: 600;
        }
        
        .logo span {
            font-size: 1rem;
            opacity: 0.9;
        }
        
        .header-info {
            text-align: right;
            font-size: 0.9rem;
        }
        
        .rate-indicator {
            background: rgba(255, 255, 255, 0.1);
            padding: 8px 15px;
            border-radius: 20px;
            margin-top: 5px;
            display: inline-block;
        }
        
        .calculator-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-bottom: 40px;
        }
        
        @media (max-width: 900px) {
            .calculator-container {
                grid-template-columns: 1fr;
            }
            .header-content {
                flex-direction: column;
                text-align: center;
                gap: 20px;
            }
            .header-info {
                text-align: center;
            }
        }
        
        .input-section, .results-section {
            background-color: white;
            border-radius: 10px;
            padding: 30px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
        }
        
        .section-title {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 25px;
            color: #1a237e;
            font-size: 1.4rem;
        }
        
        .section-title i {
            font-size: 1.5rem;
        }
        
        .input-group {
            margin-bottom: 20px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #444;
        }
        
        input, select {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
            transition: border 0.3s;
        }
        
        input:focus, select:focus {
            border-color: #283593;
            outline: none;
            box-shadow: 0 0 0 2px rgba(40, 53, 147, 0.1);
        }
        
        .range-container {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .range-container input {
            flex: 1;
        }
        
        .range-value {
            font-weight: 600;
            color: #283593;
            min-width: 50px;
        }
        
        .info-text {
            font-size: 0.9rem;
            color: #666;
            margin-top: 5px;
            font-style: italic;
        }
        
        .taxas-config {
            background-color: #f0f5ff;
            border-radius: 8px;
            padding: 20px;
            margin-top: 30px;
        }
        
        .taxas-title {
            font-weight: 600;
            margin-bottom: 20px;
            color: #1a237e;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .taxa-input-group {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-bottom: 15px;
        }
        
        @media (max-width: 500px) {
            .taxa-input-group {
                grid-template-columns: 1fr;
            }
        }
        
        .taxa-input-item {
            display: flex;
            flex-direction: column;
        }
        
        .taxa-input-item label {
            font-size: 0.9rem;
            margin-bottom: 5px;
        }
        
        .taxa-input-item input {
            padding: 10px 12px;
            font-size: 0.95rem;
        }
        
        .buttons {
            display: flex;
            gap: 15px;
            margin-top: 30px;
        }
        
        button {
            padding: 14px 25px;
            border: none;
            border-radius: 5px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .btn-calculate {
            background: linear-gradient(to right, #1a237e, #283593);
            color: white;
            flex: 2;
        }
        
        .btn-reset {
            background-color: #f0f0f0;
            color: #333;
            flex: 1;
        }
        
        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 10px rgba(0, 0, 0, 0.1);
        }
        
        .btn-calculate:hover {
            background: linear-gradient(to right, #283593, #303f9f);
        }
        
        .btn-reset:hover {
            background-color: #e0e0e0;
        }
        
        .results-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .result-box {
            background-color: #f9fafc;
            border-radius: 8px;
            padding: 20px;
            text-align: center;
            border-left: 4px solid #283593;
        }
        
        .result-label {
            font-size: 0.9rem;
            color: #666;
            margin-bottom: 8px;
        }
        
        .result-value {
            font-size: 1.8rem;
            font-weight: 700;
            color: #1a237e;
        }
        
        .result-unit {
            font-size: 1rem;
            color: #666;
            font-weight: 600;
        }
        
        .chart-container {
            height: 250px;
            margin-top: 30px;
            position: relative;
        }
        
        .chart-placeholder {
            height: 100%;
            background-color: #f9fafc;
            border-radius: 8px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            color: #888;
        }
        
        .chart-placeholder i {
            font-size: 3rem;
            margin-bottom: 15px;
            color: #c5d0e6;
        }
        
        .projecao-section {
            background-color: white;
            border-radius: 10px;
            padding: 30px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            margin-bottom: 40px;
        }
        
        .projecao-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        
        .projecao-table th {
            background-color: #f0f5ff;
            padding: 15px;
            text-align: left;
            color: #1a237e;
            font-weight: 600;
            border-bottom: 2px solid #ddd;
        }
        
        .projecao-table td {
            padding: 15px;
            border-bottom: 1px solid #eee;
        }
        
        .projecao-table tr:hover {
            background-color: #f9fafc;
        }
        
        footer {
            text-align: center;
            padding: 20px;
            color: #666;
            font-size: 0.9rem;
            border-top: 1px solid #eee;
            margin-top: 30px;
        }
        
        .disclaimer {
            background-color: #fff8e1;
            border-radius: 8px;
            padding: 20px;
            margin-top: 30px;
            font-size: 0.9rem;
            color: #666;
            border-left: 4px solid #ffc107;
        }
        
        .highlight {
            color: #1a237e;
            font-weight: 600;
        }
        
        .taxa-note {
            font-size: 0.8rem;
            color: #666;
            margin-top: 20px;
            font-style: italic;
            text-align: center;
        }
        
        .input-with-icon {
            position: relative;
        }
        
        .input-with-icon i {
            position: absolute;
            left: 12px;
            top: 50%;
            transform: translateY(-50%);
            color: #666;
        }
        
        .input-with-icon input {
            padding-left: 40px;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="header-content">
                <div class="logo">
                    <i class="fas fa-chart-line"></i>
                    <div>
                        <h1>Calculadora Financeira Profissional</h1>
                        <span>CDI e Taxa Básica de Juros (SELIC)</span>
                    </div>
                </div>
                <div class="header-info">
                    <p>Data: <span id="current-date"></span></p>
                    <div class="rate-indicator">
                        <i class="fas fa-percentage"></i> Taxas Editáveis
                    </div>
                </div>
            </div>
        </header>
        
        <div class="calculator-container">
            <div class="input-section">
                <h2 class="section-title"><i class="fas fa-calculator"></i> Parâmetros de Cálculo</h2>
                
                <div class="input-group">
                    <label for="investment-amount">Valor do Investimento (R$)</label>
                    <div class="input-with-icon">
                        <i class="fas fa-money-bill-wave"></i>
                        <input type="number" id="investment-amount" min="100" step="100" value="10000">
                    </div>
                    <div class="info-text">Valor mínimo: R$ 100,00</div>
                </div>
                
                <div class="input-group">
                    <label for="investment-period">Período de Investimento</label>
                    <div class="range-container">
                        <input type="range" id="investment-period" min="30" max="720" value="180">
                        <span class="range-value" id="period-value">180 dias</span>
                    </div>
                    <div class="info-text">Período em dias (30 a 720 dias)</div>
                </div>
                
                <div class="input-group">
                    <label for="tax-type">Tipo de Investimento</label>
                    <select id="tax-type">
                        <option value="cdi">CDI (Certificado de Depósito Interbancário)</option>
                        <option value="selic">SELIC (Taxa Básica de Juros)</option>
                        <option value="lc">LCI/LCA (Isentos de IR)</option>
                        <option value="poupanca">Poupança</option>
                        <option value="prefixado">Pré-fixado</option>
                        <option value="ipca">IPCA + Taxa</option>
                        <option value="custom">Taxa Personalizada</option>
                    </select>
                </div>
                
                <div class="input-group">
                    <label for="percent-taxa">Percentual da Taxa (% da taxa base)</label>
                    <div class="range-container">
                        <input type="range" id="percent-taxa" min="80" max="120" value="100">
                        <span class="range-value" id="percent-taxa-value">100%</span>
                    </div>
                    <div class="info-text">Ajuste o percentual em relação à taxa base (80% a 120%)</div>
                </div>
                
                <div class="taxas-config">
                    <h3 class="taxas-title"><i class="fas fa-sliders-h"></i> Configurar Taxas (%)</h3>
                    
                    <div class="taxa-input-group">
                        <div class="taxa-input-item">
                            <label for="taxa-cdi-input">CDI (ao ano)</label>
                            <input type="number" id="taxa-cdi-input" step="0.01" value="13.65">
                        </div>
                        <div class="taxa-input-item">
                            <label for="taxa-selic-input">SELIC (ao ano)</label>
                            <input type="number" id="taxa-selic-input" step="0.01" value="14.25">
                        </div>
                        <div class="taxa-input-item">
                            <label for="taxa-ipca-input">IPCA (12 meses)</label>
                            <input type="number" id="taxa-ipca-input" step="0.01" value="4.51">
                        </div>
                        <div class="taxa-input-item">
                            <label for="taxa-poupanca-input">Poupança (ao ano)</label>
                            <input type="number" id="taxa-poupanca-input" step="0.01" value="8.28">
                        </div>
                    </div>
                    
                    <div class="taxa-input-group">
                        <div class="taxa-input-item">
                            <label for="taxa-prefixado-input">Taxa Pré-fixada (% a.a.)</label>
                            <input type="number" id="taxa-prefixado-input" step="0.01" value="13.0">
                        </div>
                        <div class="taxa-input-item">
                            <label for="taxa-ipca-mais-input">IPCA + (% a.a.)</label>
                            <input type="number" id="taxa-ipca-mais-input" step="0.01" value="5.5">
                        </div>
                    </div>
                    
                    <div class="taxa-note">
                        <i class="fas fa-edit"></i> Edite as taxas conforme as atualizações do mercado
                    </div>
                </div>
                
                <div class="buttons">
                    <button class="btn-calculate" id="calculate-btn">
                        <i class="fas fa-calculator"></i> Calcular Rendimentos
                    </button>
                    <button class="btn-reset" id="reset-btn">
                        <i class="fas fa-redo"></i> Limpar
                    </button>
                </div>
            </div>
            
            <div class="results-section">
                <h2 class="section-title"><i class="fas fa-chart-bar"></i> Resultados da Projeção</h2>
                
                <div class="results-grid">
                    <div class="result-box">
                        <div class="result-label">Valor Investido</div>
                        <div class="result-value" id="result-invested">R$ 10.000</div>
                    </div>
                    <div class="result-box">
                        <div class="result-label">Rendimento Bruto</div>
                        <div class="result-value" id="result-earnings">R$ 0</div>
                    </div>
                    <div class="result-box">
                        <div class="result-label">Valor Final Bruto</div>
                        <div class="result-value" id="result-final">R$ 10.000</div>
                    </div>
                    <div class="result-box">
                        <div class="result-label">Rentabilidade no Período</div>
                        <div class="result-value" id="result-yield">0%</div>
                    </div>
                </div>
                
                <div class="chart-container">
                    <div class="chart-placeholder" id="chart-placeholder">
                        <i class="fas fa-chart-pie"></i>
                        <p>Clique em "Calcular Rendimentos" para visualizar o gráfico</p>
                    </div>
                    <canvas id="results-chart" style="display: none;"></canvas>
                </div>
                
                <div class="disclaimer">
                    <p><i class="fas fa-exclamation-circle"></i> <strong>Atenção:</strong> Esta calculadora fornece uma projeção teórica com base nos parâmetros informados. Os resultados são meramente ilustrativos e não garantem rendimentos futuros. Consulte um profissional financeiro para orientações personalizadas.</p>
                </div>
            </div>
        </div>
        
        <div class="projecao-section">
            <h2 class="section-title"><i class="fas fa-calendar-alt"></i> Projeção de Rendimentos</h2>
            <table class="projecao-table">
                <thead>
                    <tr>
                        <th>Período</th>
                        <th>Valor Investido</th>
                        <th>Rendimento Acumulado</th>
                        <th>Valor Total</th>
                        <th>Rentabilidade</th>
                    </tr>
                </thead>
                <tbody id="projecao-body">
                    <tr>
                        <td colspan="5" style="text-align: center; padding: 30px; color: #888;">
                            Execute o cálculo para ver a projeção
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
        
        <footer>
            <p>© 2023 Calculadora Financeira Profissional. Esta ferramenta é fornecida apenas para fins educacionais e informativos.</p>
            <p>As taxas devem ser ajustadas manualmente conforme as atualizações do Banco Central e do mercado.</p>
        </footer>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script>
        // Configuração inicial
        document.addEventListener('DOMContentLoaded', function() {
            // Data atual
            const now = new Date();
            document.getElementById('current-date').textContent = now.toLocaleDateString('pt-BR');
            
            // Configurar sliders
            const periodSlider = document.getElementById('investment-period');
            const periodValue = document.getElementById('period-value');
            const percentSlider = document.getElementById('percent-taxa');
            const percentValue = document.getElementById('percent-taxa-value');
            
            // Atualizar valores dos sliders
            periodSlider.addEventListener('input', function() {
                periodValue.textContent = this.value + ' dias';
            });
            
            percentSlider.addEventListener('input', function() {
                percentValue.textContent = this.value + '%';
            });
            
            // Configurar botões
            document.getElementById('calculate-btn').addEventListener('click', calculate);
            document.getElementById('reset-btn').addEventListener('click', resetForm);
            
            // Calcular automaticamente ao carregar a página
            calculate();
        });
        
        // Função principal de cálculo
        function calculate() {
            // Obter valores dos inputs
            const investmentAmount = parseFloat(document.getElementById('investment-amount').value);
            const investmentPeriod = parseInt(document.getElementById('investment-period').value);
            const percentTaxa = parseInt(document.getElementById('percent-taxa').value) / 100;
            const taxType = document.getElementById('tax-type').value;
            
            // Obter taxas editadas pelo usuário
            const taxaCdi = parseFloat(document.getElementById('taxa-cdi-input').value);
            const taxaSelic = parseFloat(document.getElementById('taxa-selic-input').value);
            const taxaIpca = parseFloat(document.getElementById('taxa-ipca-input').value);
            const taxaPoupanca = parseFloat(document.getElementById('taxa-poupanca-input').value);
            const taxaPrefixado = parseFloat(document.getElementById('taxa-prefixado-input').value);
            const taxaIpcaMais = parseFloat(document.getElementById('taxa-ipca-mais-input').value);
            
            // Determinar a taxa anual base
            let annualRate;
            let rateName;
            
            switch(taxType) {
                case 'cdi':
                    annualRate = taxaCdi * percentTaxa;
                    rateName = 'CDI: ' + taxaCdi + '% a.a. (' + (percentTaxa * 100) + '%)';
                    break;
                case 'selic':
                    annualRate = taxaSelic * percentTaxa;
                    rateName = 'SELIC: ' + taxaSelic + '% a.a. (' + (percentTaxa * 100) + '%)';
                    break;
                case 'lc':
                    annualRate = taxaCdi * percentTaxa;
                    rateName = 'LCI/LCA (Isento IR): ' + taxaCdi + '% a.a. (' + (percentTaxa * 100) + '%)';
                    break;
                case 'poupanca':
                    annualRate = taxaPoupanca;
                    rateName = 'Poupança: ' + taxaPoupanca + '% a.a.';
                    break;
                case 'prefixado':
                    annualRate = taxaPrefixado * percentTaxa;
                    rateName = 'Pré-fixado: ' + taxaPrefixado + '% a.a. (' + (percentTaxa * 100) + '%)';
                    break;
                case 'ipca':
                    annualRate = (taxaIpca + taxaIpcaMais) * percentTaxa;
                    rateName = 'IPCA + ' + taxaIpcaMais + '%: ' + taxaIpca + '% + ' + taxaIpcaMais + '% = ' + (taxaIpca + taxaIpcaMais) + '% a.a.';
                    break;
                case 'custom':
                    annualRate = taxaCdi * percentTaxa;
                    rateName = 'Taxa Personalizada: ' + taxaCdi + '% a.a. (' + (percentTaxa * 100) + '%)';
                    break;
                default:
                    annualRate = taxaCdi * percentTaxa;
                    rateName = 'CDI: ' + taxaCdi + '% a.a. (' + (percentTaxa * 100) + '%)';
            }
            
            // Converter taxa anual para taxa diária (considerando ano comercial de 252 dias)
            const dailyRate = Math.pow(1 + annualRate/100, 1/252) - 1;
            
            // Calcular rendimento
            const earnings = investmentAmount * (Math.pow(1 + dailyRate, investmentPeriod) - 1);
            const finalAmount = investmentAmount + earnings;
            const periodYield = (Math.pow(1 + dailyRate, investmentPeriod) - 1) * 100;
            
            // Atualizar resultados na interface
            document.getElementById('result-invested').textContent = formatCurrency(investmentAmount);
            document.getElementById('result-earnings').textContent = formatCurrency(earnings);
            document.getElementById('result-final').textContent = formatCurrency(finalAmount);
            document.getElementById('result-yield').textContent = periodYield.toFixed(2) + '%';
            
            // Atualizar gráfico
            updateChart(investmentAmount, earnings, rateName);
            
            // Atualizar tabela de projeção
            updateProjecaoTable(investmentAmount, dailyRate, investmentPeriod);
        }
        
        // Função para atualizar o gráfico
        function updateChart(initialAmount, earnings, rateName) {
            const chartPlaceholder = document.getElementById('chart-placeholder');
            const chartCanvas = document.getElementById('results-chart');
            
            // Mostrar canvas e esconder placeholder
            chartPlaceholder.style.display = 'none';
            chartCanvas.style.display = 'block';
            
            // Destruir gráfico anterior se existir
            if (window.myChart) {
                window.myChart.destroy();
            }
            
            // Criar novo gráfico
            const ctx = chartCanvas.getContext('2d');
            window.myChart = new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: ['Valor Investido', 'Rendimentos'],
                    datasets: [{
                        data: [initialAmount, earnings],
                        backgroundColor: [
                            '#1a237e',
                            '#283593'
                        ],
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: {
                                padding: 20,
                                font: {
                                    size: 14
                                }
                            }
                        },
                        title: {
                            display: true,
                            text: 'Distribuição: ' + rateName,
                            font: {
                                size: 16
                            },
                            padding: {
                                bottom: 20
                            }
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    let label = context.label || '';
                                    if (label) {
                                        label += ': ';
                                    }
                                    label += formatCurrency(context.parsed);
                                    return label;
                                }
                            }
                        }
                    }
                }
            });
        }
        
        // Função para atualizar a tabela de projeção
        function updateProjecaoTable(investmentAmount, dailyRate, investmentPeriod) {
            const projecaoBody = document.getElementById('projecao-body');
            projecaoBody.innerHTML = '';
            
            // Definir intervalos para mostrar na tabela
            const intervals = [
                Math.floor(investmentPeriod * 0.25),
                Math.floor(investmentPeriod * 0.5),
                Math.floor(investmentPeriod * 0.75),
                investmentPeriod
            ];
            
            // Adicionar cada período na tabela
            intervals.forEach((period, index) => {
                const earnings = investmentAmount * (Math.pow(1 + dailyRate, period) - 1);
                const total = investmentAmount + earnings;
                const yield = (Math.pow(1 + dailyRate, period) - 1) * 100;
                
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${period} dias</td>
                    <td>${formatCurrency(investmentAmount)}</td>
                    <td>${formatCurrency(earnings)}</td>
                    <td>${formatCurrency(total)}</td>
                    <td>${yield.toFixed(2)}%</td>
                `;
                projecaoBody.appendChild(row);
            });
        }
        
        // Função para resetar o formulário
        function resetForm() {
            // Resetar valores principais
            document.getElementById('investment-amount').value = 10000;
            document.getElementById('investment-period').value = 180;
            document.getElementById('percent-taxa').value = 100;
            document.getElementById('tax-type').value = 'cdi';
            
            // Resetar taxas para valores atuais
            document.getElementById('taxa-cdi-input').value = 13.65;
            document.getElementById('taxa-selic-input').value = 14.25;
            document.getElementById('taxa-ipca-input').value = 4.51;
            document.getElementById('taxa-poupanca-input').value = 8.28;
            document.getElementById('taxa-prefixado-input').value = 13.0;
            document.getElementById('taxa-ipca-mais-input').value = 5.5;
            
            // Atualizar os valores dos sliders
            document.getElementById('period-value').textContent = '180 dias';
            document.getElementById('percent-taxa-value').textContent = '100%';
            
            // Resetar resultados
            document.getElementById('result-invested').textContent = formatCurrency(10000);
            document.getElementById('result-earnings').textContent = formatCurrency(0);
            document.getElementById('result-final').textContent = formatCurrency(10000);
            document.getElementById('result-yield').textContent = '0%';
            
            // Resetar gráfico
            const chartPlaceholder = document.getElementById('chart-placeholder');
            const chartCanvas = document.getElementById('results-chart');
            
            chartPlaceholder.style.display = 'flex';
            chartCanvas.style.display = 'none';
            
            if (window.myChart) {
                window.myChart.destroy();
            }
            
            // Resetar tabela de projeção
            const projecaoBody = document.getElementById('projecao-body');
            projecaoBody.innerHTML = `
                <tr>
                    <td colspan="5" style="text-align: center; padding: 30px; color: #888;">
                        Execute o cálculo para ver a projeção
                    </td>
                </tr>
            `;
        }
        
        // Função utilitária para formatar moeda
        function formatCurrency(value) {
            return 'R$ ' + value.toLocaleString('pt-BR', {
                minimumFractionDigits: 2,
                maximumFractionDigits: 2
            });
        }
    </script>
</body>
</html>
