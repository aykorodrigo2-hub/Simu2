<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simulado Completo AAP - CFC e CESD (COMAER) - 200+ Questões</title>
    <style>
        :root {
            --primary: #003366;
            --primary-dark: #001f3f;
            --secondary: #1e5c93;
            --accent: #d9534f;
            --light-bg: #f4f7f9;
            --card-bg: #ffffff;
            --text-dark: #2c3e50;
            --text-muted: #6c757d;
            --correct-bg: #d4edda;
            --correct-border: #28a745;
            --correct-text: #155724;
            --incorrect-bg: #f8d7da;
            --incorrect-border: #dc3545;
            --incorrect-text: #721c24;
            --neutral-border: #ced4da;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--light-bg);
            color: var(--text-dark);
            line-height: 1.6;
            padding: 20px;
        }

        .container {
            max-width: 950px;
            margin: 0 auto;
        }

        header {
            background: linear-gradient(135deg, var(--primary-dark), var(--secondary));
            color: white;
            padding: 25px 20px;
            border-radius: 12px;
            text-align: center;
            box-shadow: 0 4px 15px rgba(0,0,0,0.15);
            margin-bottom: 20px;
        }

        header h1 {
            font-size: 1.7rem;
            margin-bottom: 6px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        header p {
            font-size: 0.95rem;
            opacity: 0.9;
        }

        .stats-bar {
            position: sticky;
            top: 10px;
            z-index: 100;
            background-color: var(--card-bg);
            padding: 12px 20px;
            border-radius: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            font-weight: 600;
            border: 1px solid var(--neutral-border);
        }

        .progress-container {
            width: 100%;
            background-color: #e9ecef;
            height: 10px;
            border-radius: 5px;
            margin-top: 6px;
            overflow: hidden;
        }

        .progress-bar {
            height: 100%;
            background-color: var(--secondary);
            width: 0%;
            transition: width 0.3s ease;
        }

        .question-card {
            background-color: var(--card-bg);
            border-radius: 12px;
            padding: 22px;
            margin-bottom: 22px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.06);
            border-left: 6px solid var(--primary);
        }

        .module-tag {
            display: inline-block;
            background-color: #e6f0fa;
            color: var(--primary);
            font-size: 0.78rem;
            font-weight: bold;
            padding: 4px 10px;
            border-radius: 20px;
            margin-bottom: 10px;
            text-transform: uppercase;
        }

        .question-title {
            font-size: 1.05rem;
            font-weight: 600;
            color: var(--text-dark);
            margin-bottom: 16px;
        }

        .options-list {
            list-style: none;
        }

        .option-item {
            border: 1.5px solid var(--neutral-border);
            border-radius: 8px;
            padding: 12px 16px;
            margin-bottom: 10px;
            cursor: pointer;
            transition: all 0.2s ease;
            display: flex;
            align-items: flex-start;
            background-color: #fff;
        }

        .option-item:hover:not(.disabled) {
            border-color: var(--secondary);
            background-color: #f8fbfe;
        }

        .option-letter {
            font-weight: bold;
            width: 26px;
            height: 26px;
            background-color: var(--light-bg);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 12px;
            flex-shrink: 0;
            font-size: 0.85rem;
            color: var(--primary);
        }

        .option-text {
            flex-grow: 1;
            font-size: 0.95rem;
            padding-top: 1px;
        }

        .option-item.selected-correct {
            background-color: var(--correct-bg);
            border-color: var(--correct-border);
            color: var(--correct-text);
        }

        .option-item.selected-correct .option-letter {
            background-color: var(--correct-border);
            color: white;
        }

        .option-item.selected-incorrect {
            background-color: var(--incorrect-bg);
            border-color: var(--incorrect-border);
            color: var(--incorrect-text);
        }

        .option-item.selected-incorrect .option-letter {
            background-color: var(--incorrect-border);
            color: white;
        }

        .option-item.show-correct {
            border-color: var(--correct-border);
            background-color: #e8f5e9;
        }

        .option-item.disabled {
            cursor: default;
        }

        .explanation-box {
            margin-top: 18px;
            padding: 16px;
            border-radius: 8px;
            background-color: #f8f9fa;
            border: 1px solid var(--neutral-border);
            display: none;
        }

        .explanation-title {
            font-weight: bold;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 1rem;
        }

        .explanation-title.correct {
            color: var(--correct-border);
        }

        .explanation-title.incorrect {
            color: var(--incorrect-border);
        }

        .explanation-item {
            margin-bottom: 8px;
            font-size: 0.9rem;
            padding-left: 10px;
            border-left: 3px solid #ccc;
        }

        .explanation-item strong {
            color: var(--primary-dark);
        }

        .explanation-item.is-correct-exp {
            border-left-color: var(--correct-border);
            background-color: rgba(40, 167, 69, 0.05);
            padding: 6px 10px;
            border-radius: 0 4px 4px 0;
        }

        .pagination {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin: 20px 0;
            background-color: white;
            padding: 12px 20px;
            border-radius: 8px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
        }

        .pagination button {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 8px 18px;
            border-radius: 5px;
            cursor: pointer;
            font-weight: 600;
        }

        .pagination button:disabled {
            background-color: #ccc;
            cursor: not-allowed;
        }

        .summary-card {
            background-color: var(--card-bg);
            border-radius: 12px;
            padding: 30px;
            text-align: center;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            display: none;
        }

        .summary-card h2 {
            color: var(--primary);
            margin-bottom: 15px;
        }

        .score-display {
            font-size: 3rem;
            font-weight: bold;
            color: var(--secondary);
            margin: 15px 0;
        }

        .btn-reset {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 12px 28px;
            font-size: 1rem;
            font-weight: bold;
            border-radius: 6px;
            cursor: pointer;
            transition: background-color 0.2s;
            margin-top: 15px;
        }

        .btn-reset:hover {
            background-color: var(--primary-dark);
        }

        @media (max-width: 600px) {
            body { padding: 10px; }
            header { padding: 15px 10px; }
            header h1 { font-size: 1.2rem; }
            .question-card { padding: 15px; }
            .option-item { padding: 8px 10px; }
            .stats-bar { font-size: 0.85rem; padding: 10px; }
        }
    </style>
</head>
<body>

<div class="container">
    <header>
        <h1>Banco de Questões Interativo AAP (200+ Questões)</h1>
        <p>Apostila Técnica do CFC e CESD — Comando da Aeronáutica (Volume Único)</p>
    </header>

    <div class="stats-bar" id="statsBar">
        <div>
            Questão: <span id="currentQNum">1</span> / <span id="totalQNum">200</span>
        </div>
        <div>
            Respondidas: <span id="answeredNum">0</span> | Acertos: <span id="scoreNum" style="color: var(--correct-border);">0</span>
        </div>
    </div>
    
    <div style="margin-bottom: 15px;">
        <div class="progress-container">
            <div class="progress-bar" id="progressBar"></div>
        </div>
    </div>

    <div id="quizContainer">
        <!-- Questões serão injetadas via JS -->
    </div>

    <div class="pagination" id="paginationControls">
        <button id="prevBtn" onclick="changePage(-1)">← Anteriores</button>
        <span id="pageIndicator">Página 1</span>
        <button id="nextBtn" onclick="changePage(1)">Próximas →</button>
    </div>

    <div class="summary-card" id="summaryCard">
        <h2>Simulado Finalizado!</h2>
        <p>Você respondeu às questões abrangendo os Módulos I, II, III e IV da Apostila AAP do COMAER.</p>
        <div class="score-display" id="finalScore">0 / 200</div>
        <p id="performanceMsg"></p>
        <button class="btn-reset" onclick="resetQuiz()">Reiniciar Bateria de Questões</button>
    </div>
</div>

<script>
// Gerador expandido de 200+ questões baseadas em 100% da apostila AAP
const rawQuestionsTemplates = [
    // MÓDULO I - INTRODUÇÃO À INFORMÁTICA E REDAÇÃO OFICIAL
    {
        mod: "Módulo I - Apoio Administrativo",
        topic: "Ressalva de Escopo da Apostila",
        q: "Conforme disposto expressamente na ressalva de escopo operacional da apostila técnica AAP, a conclusão do estudo do compêndio habilita o militar a qual das seguintes ações?",
        opts: [
            "Execução autônoma de manutenções em circuitos elétricos de alta tensão sem ordem técnica.",
            "Diagnóstico mecânico estrutural não supervisionado de viaturas militares.",
            "Nívelamento conceitual e operacional uniforme, NÃO habilitando nem autorizando a execução autônoma de procedimentos especializados.",
            "Prescrição e intervenção assistencial médica direta em ambiente hospitalar da FAB.",
            "Manipulação autônoma de instrumentais cirúrgicos sem supervisão de graduado ou oficial especialista."
        ],
        ans: 2,
        exp: [
            "Incorreta. O estudo não habilita intervenção em sistemas elétricos de alta/baixa tensão sem supervisão.",
            "Incorreta. O diagnóstico mecânico autônomo sem ordem técnica é vedado.",
            "Correta. A ressalva de escopo explicita que o objetivo é o nivelamento conceitual introdutório, NÃO autorizando a execução autônoma de tarefas especializadas.",
            "Incorreta. A prescrição de medicamentos é privativa de profissionais da saúde legalmente habilitados.",
            "Incorreta. A manipulação autônoma de artigos cirúrgicos exige qualificação profissional e supervisão."
        ]
    },
    {
        mod: "Módulo I - Apoio Administrativo",
        topic: "Glossário de Siglas Técnicas",
        q: "No âmbito do Comando da Aeronáutica e do Ministério da Defesa, qual é a definição correta para o acrônimo 'MD33-M-02'?",
        opts: [
            "Manual de Biossegurança e Controle de Infecção Hospitalar da FAB.",
            "Manual de Abreviaturas, Siglas, Símbolos e Convenções Cartográficas das Forças Armadas.",
            "Norma do Sistema do Comando da Aeronáutica para Correspondência e Atos Administrativos.",
            "Diretiva Técnica do Sistema de Material Aeronáutico para Manutenção Preventiva.",
            "Manual do Usuário do Sistema SILOMS para Registro de Suprimentos Sensíveis."
        ],
        ans: 1,
        exp: [
            "Incorreta. Este tema é abordado em normativas da ANVISA e diretrizes hospitalares.",
            "Correta. Conforme o glossário técnico da apostila, o MD33-M-02 é o Manual de Abreviaturas, Siglas, Símbolos e Convenções Cartográficas das Forças Armadas.",
            "Incorreta. A norma para correspondência e atos do COMAER é a NSCA 5-3 / NSCA 10-2.",
            "Incorreta. Trata-se de código de manual de abreviaturas e símbolos cartográficos das FA.",
            "Incorreta. Não se refere ao manual de sistema informatizado SILOMS."
        ]
    },
    {
        mod: "Módulo I - Apoio Administrativo",
        topic: "Unidades de Medida Binária",
        q: "No processamento digital e armazenamento de dados binários no SILOMS, qual é a equivalência lógica e capacidade aproximada de 1 Gigabyte (GB)?",
        opts: [
            "Equivale a 8 bits e comporta exatamente um único caractere alfanumérico.",
            "Em torno de 1.000 Bytes (1.000 KB), comportando aproximadamente 1 mil caracteres.",
            "Em torno de 1 bilhão de Bytes (1.000 MB), comportando cerca de 1 bilhão de caracteres.",
            "Em torno de 1 trilhão de Bytes (1.000 GB), comportando 1 trilhão de caracteres.",
            "Em torno de 1 quatrilhão de Bytes (1.000 TB), com capacidade para 1 quatrilhão de caracteres."
        ],
        ans: 2,
        exp: [
            "Incorreta. 8 bits equivalem a 1 Byte.",
            "Incorreta. 1.000 Bytes equivalem a 1 Kilobyte (KB).",
            "Correta. 1 Gigabyte (GB) equivale a aproximadamente 1 bilhão de Bytes ou 1.000 MB (ex: HDs de 500 GB suportam cerca de 500 bilhões de letras).",
            "Incorreta. 1 trilhão de Bytes equivale a 1 Terabyte (TB).",
            "Incorreta. 1 quatrilhão de Bytes equivale a 1 Petabyte (PB)."
        ]
    },
    {
        mod: "Módulo I - Apoio Administrativo",
        topic: "Tipos de Impressoras",
        q: "Qual tipo de impressora operacional é amplamente utilizado na administração militar em virtude de sua capacidade exclusiva de imprimir formulários contínuos com vias carbonadas simultâneas (guias de trânsito e controle de almoxarifado)?",
        opts: [
            "Impressora a Jato de Tinta Piezelétrica.",
            "Impressora 3D de Extrusão Termoplástica (FDM).",
            "Impressora de Impacto (Matricial).",
            "Impressora a Laser com Fusor Térmico.",
            "Impressora de Fotopolimerização por Resina (SLA)."
        ],
        ans: 2,
        exp: [
            "Incorreta. Impressoras a jato de tinta utilizam microgotículas líquidas em papel comum.",
            "Incorreta. Impressoras 3D realizam manufatura aditiva tridimensional de peças plásticas.",
            "Correta. As impressoras de impacto (matriciais) acionam agulhas mecânicas contra fita tintada, permitindo a impressão em formulários carbonados de vias múltiplas.",
            "Incorreta. Impressoras a laser fundem pigmento seco (toner) por calor, não prensando vias carbonadas.",
            "Incorreta. Impressoras SLA são voltadas à prototipagem tridimensional em resina."
        ]
    },
    {
        mod: "Módulo I - Apoio Administrativo",
        topic: "Teclas de Atalho e Funções",
        q: "No teclado padrão ABNT utilizado nas Organizações Militares do COMAER, qual tecla é responsável por alternar entre os modos de entrada de texto 'Inserir' (preserva o texto adjacente) e 'Substituir' (sobrescreve caracteres)?",
        opts: [
            "BACKSPACE",
            "CAPS LOCK",
            "DELETE",
            "INSERT",
            "ESCAPE (ESC)"
        ],
        ans: 3,
        exp: [
            "Incorreta. BACKSPACE apaga o caractere à esquerda do cursor.",
            "Incorreta. CAPS LOCK habilita a escrita em letras maiúsculas.",
            "Incorreta. DELETE apaga o caractere à direita da posição do cursor.",
            "Correta. A tecla INSERT alterna o modo de digitação entre 'Inserir' (preserva texto) e 'Substituir' (sobrescreve caracteres adjacentes).",
            "Incorreta. ESC serve para cancelar comandos, fechar menus ou sair de programas."
        ]
    },
    {
        mod: "Módulo I - Apoio Administrativo",
        topic: "Classificação de Softwares",
        q: "Os programas computacionais dividem-se hierarquicamente em Software Básico, Utilitário e Aplicativo. É correto classificar como exemplo de Software Básico de gerenciamento mestre do hardware:",
        opts: [
            "Microsoft Word e LibreOffice Writer.",
            "Sistemas Operacionais como Windows e distribuições Linux institucionais.",
            "Módulos de consulta do SILOMS.",
            "Desfragmentadores de disco e programas antivírus.",
            "Microsoft Access e bancos de dados Dbase."
        ],
        ans: 1,
        exp: [
            "Incorreta. Editores de texto são softwares aplicativos de uso genérico.",
            "Correta. Sistemas Operacionais (Windows, Linux, macOS) constituem o Software Básico, criando a camada de abstração entre máquina e usuário.",
            "Incorreta. O SILOMS é um aplicativo de uso específico no âmbito do COMAER.",
            "Incorreta. Antivírus e desfragmentadores são softwares utilitários de manutenção.",
            "Incorreta. Gerenciadores de banco de dados são aplicativos."
        ]
    },
    {
        mod: "Módulo I - Apoio Administrativo",
        topic: "Lei de Acesso à Informação (LAI - Lei nº 12.527/2011)",
        q: "Segundo a Lei nº 12.527/2011 (LAI), qual é o prazo máximo de restrição de acesso para informações classificadas no grau de sigilo 'SECRETA'?",
        opts: [
            "5 anos.",
            "10 anos.",
            "15 anos.",
            "25 anos.",
            "50 anos."
        ],
        ans: 2,
        exp: [
            "Incorreta. 5 anos é o prazo máximo de restrição para a informação RESERVADA.",
            "Incorreta. A lei não estabelece prazo de 10 anos para prazos de sigilo.",
            "Correta. Pela LAI, os prazos máximos são: Ultrassecreta (25 anos), Secreta (15 anos) e Reservada (5 anos).",
            "Incorreta. 25 anos é o prazo máximo para informações ULTRASSECRETAS.",
            "Incorreta. A LAI proíbe prazos perpétuos ou de 50 anos."
        ]
    },
    {
        mod: "Módulo I - Apoio Administrativo",
        topic: "Padronização de Numerais e Valores (NSCA 5-3 e MD33-M-02)",
        q: "Na redação de documentos oficiais do COMAER, conforme a NSCA 5-3, como deve ser feita a pontuação e grafia de números identificadores e valores monetários?",
        opts: [
            "Utiliza-se ponto para separar milhares em números de CPF, CEP e telefones.",
            "Em valores monetários, o símbolo da moeda antecede o número sem espaço intermediário (ex: R$1.500,00).",
            "A vírgula (,) é utilizada exclusivamente para separar a parte inteira da parte decimal, e milhares de valores numéricos comuns usam ponto (.). Números identificadores (CPF, CEP, ano) não usam ponto de milhar.",
            "Porcentagens até 10% são obrigatoriamente escritas em algarismos romanos.",
            "Ao citar regulamentos como a ICA 5-1, deve-se escrever por extenso: 'Instrução do Comando da Aeronáutica cinco traço um'."
        ],
        ans: 2,
        exp: [
            "Incorreta. A regra de separação por ponto de milhar NÃO se aplica a documentos de identificação, CPF, CEP, anos ou telefones.",
            "In
