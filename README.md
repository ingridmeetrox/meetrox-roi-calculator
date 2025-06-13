# meetrox-roi-calculator
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de ROI Estratégico MeetRox</title>
    <!-- Inclui o Tailwind CSS para estilização rápida e responsiva -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Define a fonte Inter para todo o documento */
        body {
            font-family: 'Inter', sans-serif;
            /* Fundo degradê com as cores da MeetRox (roxo, azul, rosa) */
            background: linear-gradient(135deg, #6A1B9A 0%, #303F9F 50%, #EC407A 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            padding: 1rem; /* Adiciona um padding para mobile */
        }
        /* Estilos personalizados para a calculadora, garantindo responsividade e apelo visual */
        .container {
            max-width: 960px; /* Largura máxima para o conteúdo principal */
            background-color: rgba(255, 255, 255, 0.95); /* Fundo branco semitransparente para o container */
            border-radius: 1rem; /* Bordas mais arredondadas */
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2); /* Sombra mais proeminente */
        }
        input[type="number"], input[type="text"] {
            border: 1px solid #c2c2c2; /* Borda padrão para campos de entrada - cinza mais suave */
            border-radius: 0.5rem; /* Bordas arredondadas maiores */
            padding: 0.75rem 1rem; /* Preenchimento interno */
            width: 100%; /* Largura total */
            box-sizing: border-box; /* Garante que padding e borda não aumentem a largura */
            background-color: #fefefe; /* Fundo mais claro para os inputs */
            font-size: 1rem; /* Tamanho da fonte dos inputs */
        }
        /* Cores da paleta MeetRox (roxo, azul, rosa) */
        .meetrox-purple { background-color: #6A1B9A; } /* Roxo profundo */
        .meetrox-purple-dark { background-color: #4A148C; }
        .meetrox-purple-text { color: #6A1B9A; }
        .meetrox-purple-bg-light { background-color: #EDE7F6; } /* Fundo leve para seção roxa */

        .meetrox-blue { background-color: #303F9F; } /* Azul escuro */
        .meetrox-blue-dark { background-color: #1A237E; }
        .meetrox-blue-text { color: #303F9F; }
        .meetrox-blue-bg-light { background-color: #E8EAF6; } /* Fundo leve para seção azul */

        .meetrox-pink { background-color: #EC407A; } /* Rosa vibrante */
        .meetrox-pink-dark { background-color: #C2185B; }
        .meetrox-pink-text { color: #EC407A; }
        .meetrox-pink-bg-light { background-color: #FCE4EC; } /* Fundo leve para seção rosa */

        /* Estilo para os botões usando as novas classes */
        button {
            color: white !important; /* Força a cor do texto para branco */
            padding: 0.75rem 1.5rem; /* Preenchimento interno */
            border-radius: 0.5rem; /* Bordas arredondadas maiores */
            font-weight: bold; /* Texto em negrito */
            transition: all 0.3s ease; /* Transição suave em todas as propriedades */
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15); /* Sombra mais acentuada */
            text-transform: uppercase; /* Texto do botão em maiúsculas */
            letter-spacing: 0.05em; /* Espaçamento entre letras */
        }
        /* Estilos específicos para os botões de cada seção */
        .btn-purple { background-color: #6A1B9A; color: white !important; }
        .btn-purple:hover { background-color: #4A148C; transform: translateY(-2px); }
        .btn-blue { background-color: #303F9F; color: white !important; }
        .btn-blue:hover { background-color: #1A237E; transform: translateY(-2px); }
        .btn-pink { background-color: #EC407A; color: white !important; }
        .btn-pink:hover { background-color: #C2185B; transform: translateY(-2px); }

        .result-box {
            background-color: #ffffff; /* Fundo branco puro para os resultados */
            border: 1px solid #e0e0e0; /* Borda mais clara */
            border-radius: 0.75rem; /* Bordas ainda mais arredondadas */
            padding: 1.5rem; /* Preenchimento interno */
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1); /* Sombra suave */
            color: #333; /* Cor de texto padrão mais escura */
        }
        .section-title {
            font-size: 1.75rem; /* Títulos maiores */
            font-weight: bold; /* Título em negrito */
            margin-bottom: 1.25rem; /* Margem inferior aumentada */
            padding-bottom: 0.5rem;
            border-bottom: 2px solid; /* Linha de destaque para o título */
        }
        .section-title.purple-border { border-color: #6A1B9A; }
        .section-title.blue-border { border-color: #303F9F; }
        .section-title.pink-border { border-color: #EC407A; }

        /* Estilo para os valores dos resultados */
        .result-value {
            font-size: 1.125rem; /* Texto maior nos resultados */
        }
        .text-highlight-purple { color: #6A1B9A; font-weight: bold; }
        .text-highlight-blue { color: #303F9F; font-weight: bold; }
        .text-highlight-pink { color: #EC407A; font-weight: bold; }

        /* Ajustes para telas menores */
        @media (max-width: 768px) {
            .grid-cols-1.md\\:grid-cols-2 {
                grid-template-columns: 1fr; /* Uma coluna em telas menores */
            }
            .w-full.md\\:w-auto {
                width: 100%; /* Botões com largura total em telas menores */
            }
            .section-title {
                font-size: 1.5rem; /* Ajuste para títulos em mobile */
            }
        }
    </style>
</head>
<body class="bg-gradient-to-br from-purple-800 via-indigo-800 to-pink-600 flex items-center justify-center min-h-screen p-4">
    <div class="container mx-auto p-8 rounded-lg shadow-xl">
        <h1 class="text-4xl font-extrabold text-center meetrox-purple-text mb-10">Calculadora de ROI Estratégico MeetRox</h1>
        <p class="text-center text-gray-700 mb-8 text-lg">Ferramenta de projeção de valor para líderes executivos. Estime o Retorno Sobre o Investimento (ROI) e o Período de Retorno com a MeetRox, impulsionando a sua decisão estratégica.</p>

        <!-- Seção de Cálculo de Otimização Operacional (Produtividade) -->
        <div class="mb-10 p-6 meetrox-blue-bg-light rounded-lg">
            <h2 class="section-title meetrox-blue-text blue-border">1. Otimização Operacional (Produtividade)</h2>
            <p class="text-gray-700 mb-4">Quantifique a economia gerada pela automação e otimização de tarefas manuais que atualmente consomem tempo valioso da sua equipe de vendas.</p>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
                <div>
                    <label for="tempoCrm" class="block text-gray-700 text-sm font-bold mb-2">Tempo médio gasto por vendedor para atualizar CRM/Tarefas administrativas (minutos/reunião):</label>
                    <input type="number" id="tempoCrm" value="20" class="shadow-sm focus:ring-meetrox-blue focus:border-meetrox-blue block w-full">
                </div>
                <div>
                    <label for="reunioesDia" class="block text-gray-700 text-sm font-bold mb-2">Número médio de interações/reuniões por dia (por vendedor):</label>
                    <input type="number" id="reunioesDia" value="3" class="shadow-sm focus:ring-meetrox-blue focus:border-meetrox-blue block w-full">
                </div>
                <div>
                    <label for="salarioMensal" class="block text-gray-700 text-sm font-bold mb-2">Custo mensal médio de um profissional de vendas (R$):</label>
                    <input type="number" id="salarioMensal" value="5000" class="shadow-sm focus:ring-meetrox-blue focus:border-meetrox-blue block w-full">
                </div>
                 <div>
                    <label for="numeroVendedores" class="block text-gray-700 text-sm font-bold mb-2">Total de profissionais de vendas na equipe:</label>
                    <input type="number" id="numeroVendedores" value="500" class="shadow-sm focus:ring-meetrox-blue focus:border-meetrox-blue block w-full">
                </div>
            </div>
            <button onclick="calcularProdutividade()" class="w-full md:w-auto px-6 py-3 btn-blue">Calcular Impacto na Produtividade</button>
            <div id="resultadoProdutividade" class="result-box mt-6 hidden">
                <h3 class="text-lg font-semibold text-gray-800 mb-2">Análise de Produtividade:</h3>
                <p class="text-gray-700 result-value">Custo operacional anual atual (tempo manual): <span id="custoAnualProdutividade" class="text-highlight-blue"></span></p>
                <p class="text-gray-700 result-value">Economia anual projetada com MeetRox: <span id="economiaAnualProdutividade" class="text-highlight-blue"></span></p>
            </div>
        </div>

        <!-- Seção de Cálculo de Crescimento de Receita (Performance) -->
        <div class="mb-10 p-6 meetrox-pink-bg-light rounded-lg">
            <h2 class="section-title meetrox-pink-text pink-border">2. Crescimento de Receita (Performance)</h2>
            <p class="text-gray-700 mb-4">Projete o aumento de receita direto através da melhoria das taxas de conversão de vendas impulsionada pela MeetRox.</p>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
                <div>
                    <label for="conversaoAtual" class="block text-gray-700 text-sm font-bold mb-2">Taxa de conversão atual da equipe de vendas (%):</label>
                    <input type="number" id="conversaoAtual" value="5.3" step="0.1" class="shadow-sm focus:ring-meetrox-pink focus:border-meetrox-pink block w-full">
                </div>
                <div>
                    <label for="conversaoMeetRox" class="block text-gray-700 text-sm font-bold mb-2">Taxa de conversão esperada com MeetRox (%):</label>
                    <input type="number" id="conversaoMeetRox" value="7.0" step="0.1" class="shadow-sm focus:ring-meetrox-pink focus:border-meetrox-pink block w-full">
                </div>
                <div>
                    <label for="volumeVendas" class="block text-gray-700 text-sm font-bold mb-2">Receita bruta anual atual da equipe de vendas (R$):</label>
                    <input type="number" id="volumeVendas" value="2455557" class="shadow-sm focus:ring-meetrox-pink focus:border-meetrox-pink block w-full">
                </div>
            </div>
            <button onclick="calcularPerformance()" class="w-full md:w-auto px-6 py-3 btn-pink">Calcular Potencial de Receita</button>
            <div id="resultadoPerformance" class="result-box mt-6 hidden">
                <h3 class="text-lg font-semibold text-gray-800 mb-2">Análise de Crescimento de Receita:</h3>
                <p class="text-gray-700 result-value">Receita anual adicional projetada com MeetRox: <span id="receitaAdicional" class="text-highlight-pink"></span></p>
            </div>
        </div>

        <!-- Seção de Cálculo de Custo de Inércia (Custo de Oportunidade) -->
        <div class="mb-10 p-6 meetrox-purple-bg-light rounded-lg">
            <h2 class="section-title meetrox-purple-text purple-border">3. Custo de Inércia (O Custo de Não Agir)</h2>
            <p class="text-gray-700 mb-4">Mensure o impacto financeiro da não otimização dos processos de vendas e o potencial de receita que está sendo perdido.</p>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
                <div>
                    <label for="perdaLeads" class="block text-gray-700 text-sm font-bold mb-2">Número estimado de leads/oportunidades que sua equipe não consegue atender ou perde por mês:</label>
                    <input type="number" id="perdaLeads" value="100" class="shadow-sm focus:ring-meetrox-purple focus:border-meetrox-purple block w-full">
                </div>
                <div>
                    <label for="ticketMedio" class="block text-gray-700 text-sm font-bold mb-2">Ticket médio de uma oportunidade convertida (R$):</label>
                    <input type="number" id="ticketMedio" value="15000" class="shadow-sm focus:ring-meetrox-purple focus:border-meetrox-purple block w-full">
                </div>
                <div>
                    <label for="percentualRecuperavel" class="block text-gray-700 text-sm font-bold mb-2">Percentual de leads/oportunidades que poderiam ser recuperados com MeetRox (%):</label>
                    <input type="number" id="percentualRecuperavel" value="10" step="0.1" class="shadow-sm focus:ring-meetrox-purple focus:border-meetrox-purple block w-full">
                </div>
            </div>
            <button onclick="calcularCustoOportunidade()" class="w-full md:w-auto px-6 py-3 btn-purple">Calcular Custo de Inércia</button>
            <div id="resultadoCustoOportunidade" class="result-box mt-6 hidden">
                <h3 class="text-lg font-semibold text-gray-800 mb-2">Análise de Custo de Inércia:</h3>
                <p class="text-gray-700 result-value">Custo anual de inércia (receita potencial perdida): <span id="custoOportunidadeAnual" class="text-highlight-pink"></span></p>
            </div>
        </div>

        <!-- Nova Seção: Ganho por Otimização do Investimento em Marketing -->
        <div class="mb-10 p-6 meetrox-blue-bg-light rounded-lg">
            <h2 class="section-title meetrox-blue-text blue-border">4. Ganho por Otimização do Investimento em Marketing</h2>
            <p class="text-gray-700 mb-4">Entenda como a MeetRox maximiza o retorno sobre seus investimentos em campanhas de marketing, convertendo mais leads em vendas sem aumentar o orçamento de mídia.</p>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
                <div>
                    <label for="investimentoAdsMensal" class="block text-gray-700 text-sm font-bold mb-2">Valor do investimento mensal em campanhas de anúncios (R$):</label>
                    <input type="number" id="investimentoAdsMensal" value="100000" class="shadow-sm focus:ring-meetrox-blue focus:border-meetrox-blue block w-full">
                </div>
                <div>
                    <label for="leadsGeradosAdsMensal" class="block text-gray-700 text-sm font-bold mb-2">Número de leads gerados mensalmente por essas campanhas:</label>
                    <input type="number" id="leadsGeradosAdsMensal" value="1000" class="shadow-sm focus:ring-meetrox-blue focus:border-meetrox-blue block w-full">
                </div>
                <div>
                    <label for="conversaoAtualMktVendas" class="block text-gray-700 text-sm font-bold mb-2">Taxa de conversão atual de leads de marketing para vendas (%):</label>
                    <input type="number" id="conversaoAtualMktVendas" value="1.0" step="0.1" class="shadow-sm focus:ring-meetrox-blue focus:border-meetrox-blue block w-full">
                </div>
                <div>
                    <label for="conversaoMeetRoxMktVendas" class="block text-gray-700 text-sm font-bold mb-2">Taxa de conversão esperada de leads de marketing para vendas com MeetRox (%):</label>
                    <input type="number" id="conversaoMeetRoxMktVendas" value="1.5" step="0.1" class="shadow-sm focus:ring-meetrox-blue focus:border-meetrox-blue block w-full">
                </div>
                 <div>
                    <label for="ticketMedioMkt" class="block text-gray-700 text-sm font-bold mb-2">Ticket médio de uma venda proveniente de leads de marketing (R$):</label>
                    <input type="number" id="ticketMedioMkt" value="15000" class="shadow-sm focus:ring-meetrox-blue focus:border-meetrox-blue block w-full">
                </div>
            </div>
            <button onclick="calcularOtimizacaoMarketing()" class="w-full md:w-auto px-6 py-3 btn-blue">Calcular Otimização de Marketing</button>
            <div id="resultadoOtimizacaoMarketing" class="result-box mt-6 hidden">
                <h3 class="text-lg font-semibold text-gray-800 mb-2">Análise de Otimização de Marketing:</h3>
                <p class="text-gray-700 result-value">Receita anual adicional gerada pelos mesmos leads de marketing: <span id="otimizacaoMarketingAnual" class="text-highlight-blue"></span></p>
            </div>
        </div>

        <!-- Seção de Investimento na MeetRox (agora Seção 5) -->
        <div class="mb-10 p-6 meetrox-pink-bg-light rounded-lg">
            <h2 class="section-title meetrox-pink-text pink-border">5. Investimento Estratégico na MeetRox</h2>
            <p class="text-gray-700 mb-4">Insira o custo anual para a implementação e uso da plataforma MeetRox.</p>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
                <div>
                    <label for="custoMeetRoxAnual" class="block text-gray-700 text-sm font-bold mb-2">Custo anual total da MeetRox (R$):</label>
                    <input type="number" id="custoMeetRoxAnual" value="86112" class="shadow-sm focus:ring-meetrox-pink focus:border-meetrox-pink block w-full">
                </div>
            </div>
            <button onclick="calcularROICompleto()" class="w-full md:w-auto px-6 py-3 btn-pink">Gerar Projeção de Valor Completa</button>
            <div id="resultadoROICompleto" class="result-box mt-6 hidden">
                <h3 class="text-lg font-semibold text-gray-800 mb-2">Projeção de Valor Total:</h3>
                <p class="text-gray-700 result-value">Ganhos operacionais e de receita anuais projetados: <span id="ganhosTotaisAnuais" class="text-highlight-purple"></span></p>
                <p class="text-gray-700 result-value">ROI Geral da MeetRox: <span id="roiFinal" class="text-highlight-purple"></span></p>
                <p class="text-gray-700 result-value">Período de Retorno (Payback Period): <span id="paybackPeriod" class="text-highlight-purple"></span></p>
                <div class="mt-4">
                    <h4 class="text-md font-semibold text-gray-800">Sumário Executivo:</h4>
                    <p id="sumarioExecutivo" class="text-gray-700 text-sm leading-relaxed"></p>
                </div>
            </div>
        </div>

        <div class="text-center mt-8">
            <p class="text-gray-500 text-sm">Esta ferramenta oferece uma projeção estratégica. Os resultados podem ser otimizados com dados específicos da sua organização e são fundamentais para discussões de viabilidade.</p>
        </div>
    </div>

    <script>
        // Variáveis globais para armazenar os ganhos e usar no cálculo de ROI completo
        let economiaAnualProdutividade = 0;
        let aumentoReceitaPerformance = 0;
        let otimizacaoMarketingAnual = 0; // Nova variável para o ganho de marketing

        // Função auxiliar para formatar números como moeda brasileira
        function formatarMoeda(valor) {
            return new Intl.NumberFormat('pt-BR', {
                style: 'currency',
                currency: 'BRL'
            }).format(valor);
        }

        // Função para calcular a economia de produtividade
        function calcularProdutividade() {
            const tempoCrm = parseFloat(document.getElementById('tempoCrm').value);
            const reunioesDia = parseFloat(document.getElementById('reunioesDia').value);
            const salarioMensal = parseFloat(document.getElementById('salarioMensal').value);
            const numeroVendedores = parseFloat(document.getElementById('numeroVendedores').value);

            // Validação robusta dos inputs
            if (isNaN(tempoCrm) || isNaN(reunioesDia) || isNaN(salarioMensal) || isNaN(numeroVendedores) ||
                tempoCrm <= 0 || reunioesDia <= 0 || salarioMensal <= 0 || numeroVendedores <= 0) {
                alert('Por favor, insira valores numéricos válidos e positivos em todos os campos de "Otimização Operacional".');
                return;
            }

            // Cálculos ajustados para impacto em escala
            const diasUteisAno = 220; // Aproximadamente 22 dias úteis por mês * 10-11 meses (considerando férias)
            const horasTrabalhadasDia = 8;

            const minutosPorVendedorPorDia = tempoCrm * reunioesDia;
            const horasPorVendedorPorDia = minutosPorVendedorPorDia / 60;
            const horasPorVendedorPorAno = horasPorVendedorPorDia * diasUteisAno;

            const custoHoraVendedor = salarioMensal / (diasUteisAno / 12 * horasTrabalhadasDia); // Custo hora considerando salário e horas trabalhadas
            const custoOperacionalVendedorAnual = horasPorVendedorPorAno * custoHoraVendedor;
            const custoOperacionalTotalAnual = custoOperacionalVendedorAnual * numeroVendedores;

            // Assumimos uma redução de tempo de 70% com MeetRox para tarefas operacionais (benchmark de automação)
            const economiaMeetRoxPercentual = 0.70;
            economiaAnualProdutividade = custoOperacionalTotalAnual * economiaMeetRoxPercentual;

            // Exibe os resultados
            document.getElementById('custoAnualProdutividade').innerText = formatarMoeda(custoOperacionalTotalAnual);
            document.getElementById('economiaAnualProdutividade').innerText = formatarMoeda(economiaAnualProdutividade);
            document.getElementById('resultadoProdutividade').classList.remove('hidden');
        }

        // Função para calcular o aumento de receita por performance
        function calcularPerformance() {
            const conversaoAtual = parseFloat(document.getElementById('conversaoAtual').value);
            const conversaoMeetRox = parseFloat(document.getElementById('conversaoMeetRox').value);
            const receitaBrutaAnual = parseFloat(document.getElementById('volumeVendas').value);

            // Validação robusta dos inputs
            if (isNaN(conversaoAtual) || isNaN(conversaoMeetRox) || isNaN(receitaBrutaAnual) ||
                conversaoAtual <= 0 || conversaoMeetRox <= 0 || receitaBrutaAnual <= 0 ||
                conversaoMeetRox < conversaoAtual) {
                alert('Por favor, insira valores numéricos válidos e positivos em todos os campos de "Crescimento de Receita". A conversão esperada deve ser maior que a atual.');
                return;
            }

            // Cálculos: aumento da receita proporcional ao aumento da taxa de conversão
            const aumentoPercentualConversao = (conversaoMeetRox - conversaoAtual) / conversaoAtual;
            aumentoReceitaPerformance = receitaBrutaAnual * aumentoPercentualConversao;

            // Exibe os resultados
            document.getElementById('receitaAdicional').innerText = formatarMoeda(aumentoReceitaPerformance);
            document.getElementById('resultadoPerformance').classList.remove('hidden');
        }

        // Função para calcular o custo de oportunidade (Custo de Inércia)
        function calcularCustoOportunidade() {
            const perdaLeads = parseFloat(document.getElementById('perdaLeads').value);
            const ticketMedio = parseFloat(document.getElementById('ticketMedio').value);
            const percentualRecuperavel = parseFloat(document.getElementById('percentualRecuperavel').value) / 100;

            // Validação robusta dos inputs
            if (isNaN(perdaLeads) || isNaN(ticketMedio) || isNaN(percentualRecuperavel) ||
                perdaLeads < 0 || ticketMedio <= 0 || percentualRecuperavel < 0 || percentualRecuperavel > 1) {
                alert('Por favor, insira valores numéricos válidos em todos os campos de "Custo de Inércia". O percentual recuperável deve ser entre 0 e 100.');
                return;
            }

            // Cálculos
            const leadsPotenciaisRecuperaveisMensal = perdaLeads * percentualRecuperavel;
            const receitaPotencialRecuperavelMensal = leadsPotenciaisRecuperaveisMensal * ticketMedio;
            const custoOportunidadeAnual = receitaPotencialRecuperavelMensal * 12;

            // Exibe os resultados
            document.getElementById('custoOportunidadeAnual').innerText = formatarMoeda(custoOportunidadeAnual);
            document.getElementById('resultadoCustoOportunidade').classList.remove('hidden');
        }

        // Nova Função: Calcular Otimização de Marketing
        function calcularOtimizacaoMarketing() {
            const investimentoAdsMensal = parseFloat(document.getElementById('investimentoAdsMensal').value);
            const leadsGeradosAdsMensal = parseFloat(document.getElementById('leadsGeradosAdsMensal').value);
            const conversaoAtualMktVendas = parseFloat(document.getElementById('conversaoAtualMktVendas').value);
            const conversaoMeetRoxMktVendas = parseFloat(document.getElementById('conversaoMeetRoxMktVendas').value);
            const ticketMedioMkt = parseFloat(document.getElementById('ticketMedioMkt').value);

            // Validação robusta dos inputs
            if (isNaN(investimentoAdsMensal) || isNaN(leadsGeradosAdsMensal) || isNaN(conversaoAtualMktVendas) ||
                isNaN(conversaoMeetRoxMktVendas) || isNaN(ticketMedioMkt) ||
                investimentoAdsMensal < 0 || leadsGeradosAdsMensal <= 0 || conversaoAtualMktVendas <= 0 ||
                conversaoMeetRoxMktVendas <= 0 || ticketMedioMkt <= 0 ||
                conversaoMeetRoxMktVendas < conversaoAtualMktVendas) {
                alert('Por favor, insira valores numéricos válidos e positivos em todos os campos de "Otimização do Investimento em Marketing". A conversão esperada deve ser maior que a atual.');
                return;
            }

            // Cálculos
            const vendasAtuaisMktMensal = leadsGeradosAdsMensal * (conversaoAtualMktVendas / 100);
            const receitaAtualMktMensal = vendasAtuaisMktMensal * ticketMedioMkt;

            const vendasOtimizadasMktMensal = leadsGeradosAdsMensal * (conversaoMeetRoxMktVendas / 100);
            const receitaOtimizadaMktMensal = vendasOtimizadasMktMensal * ticketMedioMkt;

            otimizacaoMarketingAnual = (receitaOtimizadaMktMensal - receitaAtualMktMensal) * 12;

            // Exibe os resultados
            document.getElementById('otimizacaoMarketingAnual').innerText = formatarMoeda(otimizacaoMarketingAnual);
            document.getElementById('resultadoOtimizacaoMarketing').classList.remove('hidden');
        }

        // Função para calcular o ROI completo e o Período de Retorno
        function calcularROICompleto() {
            const custoMeetRoxAnual = parseFloat(document.getElementById('custoMeetRoxAnual').value);

            if (isNaN(custoMeetRoxAnual) || custoMeetRoxAnual <= 0) {
                alert('Por favor, insira um valor numérico válido e positivo para o "Custo anual total da MeetRox".');
                return;
            }

            // Garante que os cálculos das seções de ganho foram feitos
            if (economiaAnualProdutividade === 0 && aumentoReceitaPerformance === 0 && otimizacaoMarketingAnual === 0) {
                alert('Por favor, calcule as seções de "Otimização Operacional", "Crescimento de Receita" e "Otimização de Marketing" para ter uma projeção completa de ganhos.');
                return;
            }

            const ganhosTotaisAnuais = economiaAnualProdutividade + aumentoReceitaPerformance + otimizacaoMarketingAnual;
            const ganhoLiquido = ganhosTotaisAnuais - custoMeetRoxAnual;
            let roi = 0;
            if (custoMeetRoxAnual > 0) {
                roi = (ganhoLiquido / custoMeetRoxAnual) * 100;
            }

            let paybackPeriodMeses = "N/A";
            if (ganhosTotaisAnuais > 0) {
                paybackPeriodMeses = (custoMeetRoxAnual / ganhosTotaisAnuais) * 12;
                paybackPeriodMeses = paybackPeriodMeses.toFixed(1) + ' meses';
                if (paybackPeriodMeses < 0) { // If there's a loss, payback period is infinite.
                    paybackPeriodMeses = "Não Aplicável (investimento não se paga em 1 ano)";
                } else if (paybackPeriodMeses > 60) { // Cap at 5 years
                    paybackPeriodMeses = "> 60 meses (mais de 5 anos)";
                }
            } else {
                paybackPeriodMeses = "Não Aplicável (ganhos insuficientes)";
            }

            document.getElementById('ganhosTotaisAnuais').innerText = formatarMoeda(ganhosTotaisAnuais);
            document.getElementById('roiFinal').innerText = roi.toFixed(2) + '%';
            document.getElementById('paybackPeriod').innerText = paybackPeriodMeses;
            document.getElementById('resultadoROICompleto').classList.remove('hidden');

            // Geração do sumário executivo
            const sumarioExecutivo = `
                A implementação da MeetRox representa um investimento estratégico com um potencial de ganhos anuais de
                <span class="text-highlight-purple">${formatarMoeda(ganhosTotaisAnuais)}</span>.
                Isso se traduz em um Retorno Sobre o Investimento (ROI) de
                <span class="text-highlight-purple">${roi.toFixed(2)}%</span>, com um Período de Retorno (Payback Period) estimado em
                <span class="text-highlight-purple">${paybackPeriodMeses}</span>.

                Este retorno é impulsionado por uma significativa otimização operacional, liberando tempo valioso dos seus profissionais de vendas para atividades de alto impacto; por um crescimento direto na receita através da elevação das taxas de conversão; e pela maximização do seu investimento em marketing, garantindo que cada lead gerado se converta em mais receita.
                A MeetRox não é apenas uma ferramenta, mas um catalisador para uma nova era de eficiência e crescimento escalável na sua organização.
            `;
            document.getElementById('sumarioExecutivo').innerHTML = sumarioExecutivo;
        }
    </script>
</body>
</html>
