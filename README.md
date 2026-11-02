<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simulado Interativo AAP - CFC e CESD (COMAER)</title>
    <style>
        :root {
            --primary: #003366;
            --primary-dark: #002244;
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
            max-width: 900px;
            margin: 0 auto;
        }

        header {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            padding: 30px 20px;
            border-radius: 12px;
            text-align: center;
            box-shadow: 0 4px 15px rgba(0,0,0,0.15);
            margin-bottom: 25px;
        }

        header h1 {
            font-size: 1.8rem;
            margin-bottom: 8px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        header p {
            font-size: 1rem;
            opacity: 0.9;
        }

        .stats-bar {
            background-color: var(--card-bg);
            padding: 15px 25px;
            border-radius: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.06);
            font-weight: 600;
        }

        .progress-container {
            width: 100%;
            background-color: #e9ecef;
            height: 10px;
            border-radius: 5px;
            margin-top: 8px;
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
            padding: 25px;
            margin-bottom: 25px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.08);
            border-left: 6px solid var(--primary);
        }

        .module-tag {
            display: inline-block;
            background-color: #e6f0fa;
            color: var(--primary);
            font-size: 0.8rem;
            font-weight: bold;
            padding: 4px 10px;
            border-radius: 20px;
            margin-bottom: 12px;
            text-transform: uppercase;
        }

        .question-title {
            font-size: 1.15rem;
            font-weight: 600;
            color: var(--text-dark);
            margin-bottom: 18px;
        }

        .options-list {
            list-style: none;
        }

        .option-item {
            border: 2px solid var(--neutral-border);
            border-radius: 8px;
            padding: 14px 18px;
            margin-bottom: 12px;
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
            width: 28px;
            height: 28px;
            background-color: var(--light-bg);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 12px;
            flex-shrink: 0;
            font-size: 0.9rem;
            color: var(--primary);
        }

        .option-text {
            flex-grow: 1;
            font-size: 0.98rem;
            padding-top: 2px;
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
            margin-top: 20px;
            padding: 18px;
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
            font-size: 1.05rem;
        }

        .explanation-title.correct {
            color: var(--correct-border);
        }

        .explanation-title.incorrect {
            color: var(--incorrect-border);
        }

        .explanation-item {
            margin-bottom: 8px;
            font-size: 0.92rem;
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
            header { padding: 20px 15px; }
            header h1 { font-size: 1.3rem; }
            .question-card { padding: 18px; }
            .option-item { padding: 10px 12px; }
        }
    </style>
</head>
<body>

<div class="container">
    <header>
        <h1>Simulado Especialidade AAP (Apoio)</h1>
        <p>Curso de Formação de Cabos (CFC) e Especialização de Soldados (CESD) - COMAER</p>
    </header>

    <div class="stats-bar" id="statsBar">
        <div>
            Questão: <span id="currentQNum">1</span> / <span id="totalQNum">15</span>
        </div>
        <div>
            Acertos: <span id="scoreNum" style="color: var(--correct-border);">0</span>
        </div>
    </div>
    
    <div style="margin-bottom: 20px;">
        <div class="progress-container">
            <div class="progress-bar" id="progressBar"></div>
        </div>
    </div>

    <div id="quizContainer">
        <!-- As questões serão renderizadas via JavaScript -->
    </div>

    <div class="summary-card" id="summaryCard">
        <h2>Simulado Concluído!</h2>
        <p>Você completou todas as questões do simulado de Apoio Administrativo, Logística, Manutenção e Saúde.</p>
        <div class="score-display" id="finalScore">0 / 0</div>
        <p id="performanceMsg"></p>
        <button class="btn-reset" onclick="resetQuiz()">Reiniciar Simulado</button>
    </div>
</div>

<script>
const quizData = [
    // ---------------------- MÓDULO I ----------------------
    {
        module: "Módulo I - Apoio Administrativo",
        topic: "Hardware e Memórias",
        question: "Um militar da especialidade AAP necessita identificar os componentes de hardware do microcomputador da seção. Em relação à classificação funcional da memória RAM (Random Access Memory), assinale a alternativa correta:",
        options: [
            { text: "Trata-se de uma memória não volátil e permanente, cujas rotinas de inicialização (como BIOS/UEFI e POST) são gravadas pelo fabricante.", letter: "A" },
            { text: "É uma memória volátil de acesso aleatório que abriga temporariamente dados de programas em processamento ativo, sendo limpa ao desligar o equipamento.", letter: "B" },
            { text: "Trata-se de um dispositivo secundário de massa baseado em armazenamento magnético em discos rígidos (HDD).", letter: "C" },
            { text: "Consiste em uma memória secundária em estado sólido baseada em chips flash com interface NVMe.", letter: "D" },
            { text: "É uma periférico exclusivo de saída destinado à transferência eletrostática de pigmento seco (toner) para o papel.", letter: "E" }
        ],
        correctIndex: 1,
        rationales: [
            "Incorreta. Esta descrição refere-se à memória ROM (Read-Only Memory), que retém os dados permanentemente.",
            "Correta. A memória RAM é volátil, de escrita e leitura de acesso aleatório, e perde todo o seu conteúdo quando a alimentação elétrica da máquina é interrompida.",
            "Incorreta. Os discos rígidos (HDD) são dispositivos de armazenamento secundário não voláteis.",
            "Incorreta. Trata-se da definição de unidades SSD (Solid State Drive), que não perdem dados sem energia.",
            "Incorreta. Esta é a definição de uma impressora a laser (periférico de saída de hardware)."
        ]
    },
    {
        module: "Módulo I - Apoio Administrativo",
        topic: "Redação Oficial - Pronomes de Tratamento",
        question: "Com base no Decreto Federal nº 9.758/2019 e nas normas de Redação Oficial do Comando da Aeronáutica (NSCA 5-3), qual é a forma de tratamento adequada a ser empregada nas comunicações oficiais dirigidas a agentes públicos federais (servidores civis e militares de qualquer posto ou graduação)?",
        options: [
            { text: "Vossa Excelência, para oficiais-generais e diretores de organizações militares.", letter: "A" },
            { text: "Vossa Senhoria, para oficiais superiores e graduados encarregados de seção.", letter: "B" },
            { text: "Ilustríssimo, para servidores civis com título formal de pós-graduação ou doutorado.", letter: "C" },
            { text: "Senhor ou Senhora, sendo este o único pronome de tratamento aceito no âmbito da administração pública federal.", letter: "D" },
            { text: "Doutor, sempre que o destinatário exercer funções privativas na área da saúde ou jurídica.", letter: "E" }
        ],
        correctIndex: 3,
        rationales: [
            "Incorreta. O Decreto nº 9.758/2019 vedou o uso do tratamento 'Vossa Excelência' no âmbito do Poder Executivo federal.",
            "Incorreta. A forma 'Vossa Senhoria' foi expressamente abolida nas comunicações com agentes públicos federais pelo Decreto nº 9.758/2019.",
            "Incorreta. O uso de 'Ilustríssimo' é vedado e contrário às normas vigentes de desburocratização da Redação Oficial.",
            "Correta. O Decreto nº 9.758/2019 e a NSCA 5-3 determinam que 'Senhor' ou 'Senhora' é o único pronome de tratamento empregado na comunicação oral e escrita com agentes públicos federais.",
            "Incorreta. O título 'Doutor' refere-se exclusivamente a quem obteve grau acadêmico de doutorado, não devendo ser usado como pronome de tratamento administrativo."
        ]
    },
    {
        module: "Módulo I - Apoio Administrativo",
        topic: "Documentos Oficiais e SIGADAER",
        question: "Na estrutura burocrática do Comando da Aeronáutica, assinale a alternativa correta acerca dos tipos de documentos oficiais e sua tramitação no SIGADAER:",
        options: [
            { text: "O Ofício Interno é empregado para comunicação entre organizações militares distintas e pode ser enviado como Ofício Circular ao Comandante da Aeronáutica.", letter: "A" },
            { text: "O Despacho Decisório é a comunicação externa direcionada a entidades públicas e privadas estranhas ao COMAER.", letter: "B" },
            { text: "O Ofício Particular trata de assuntos de interesse pessoal do signatário, sem numeração sequencial do setor (s/n), devendo figurar a graduação/posto e especialidade por extenso no preâmbulo e na assinatura.", letter: "C" },
            { text: "Os documentos emitidos em Difusão Geral (DIFRAL) são os únicos autorizados a inaugurar processos administrativos em múltiplos destinatários simultaneamente.", letter: "D" },
            { text: "A ementa é o campo que substitui o timbre com as Armas Nacionais na parte superior do expediente oficial.", letter: "E" }
        ],
        correctIndex: 2,
        rationales: [
            "Incorreta. O Ofício Interno é usado para comunicação entre setores da MESMA Organização Militar; o Ofício Circular não pode ser endereçado ao Comandante da Aeronáutica.",
            "Incorreta. O Despacho Decisório formaliza decisões internas de autoridades competentes em requerimentos ou processos administrativos.",
            "Correta. O Ofício Particular trata de interesses pessoais (ex: comunicação de concurso), não usa número do setor ('s/n') e substitui a função pelo posto/graduação, quadro e especialidade no preâmbulo e assinatura.",
            "Incorreta. Ofícios de Difusão Geral (DIFRAL) e Ofícios Circulares NÃO podem inaugurar processos administrativos para preservar a unicidade documental.",
            "Incorreta. A ementa é a síntese do assunto do documento (com referências e anexos), enquanto o Timbre é o cabeçalho superior com as Armas Nacionais."
        ]
    },

    // ---------------------- MÓDULO II ----------------------
    {
        module: "Módulo II - Logística, Manutenção e Eletricidade",
        topic: "Terminologia SILOMS",
        question: "No âmbito do Sistema Integrado de Logística de Material e de Serviços (SILOMS), como é classificado o ato excepcional autorizado pelo Oficial de Manutenção para a retirada de uma peça de um equipamento baixado visando à instalação em outro equipamento para pronto apronto?",
        options: [
            { text: "Implantação de Suprimento", letter: "A" },
            { text: "Canibalização ou Transferência", letter: "B" },
            { text: "Revisão Geral (Overhaul)", letter: "C" },
            { text: "Baixa por Alienação de Consumo", letter: "D" },
            { text: "Inspeção Preditiva de Pátio", letter: "E" }
        ],
        correctIndex: 1,
        rationales: [
            "Incorreta. Implantar refere-se a cadastrar pela primeira vez os dados de um item no SILOMS.",
            "Correta. Conforme a tabela de terminologia do SILOMS, canibalização ou transferência é a retirada autorizada de peça de um equipamento baixado para pronto apronto de outro.",
            "Incorreta. Overhaul (Revisão Geral) é a desmontagem completa, inspeção e reconstrução do conjunto segundo limites de fábrica.",
            "Incorreta. Trata-se de descarte de material que perde a utilidade, não de remanejamento para voo.",
            "Incorreta. Inspeção preditiva refere-se ao monitoramento contínuo de parâmetros como análise de óleo e vibração."
        ]
    },
    {
        module: "Módulo II - Logística, Manutenção e Eletricidade",
        topic: "Ferramental Manual e Segurança",
        question: "Durante a execução de manutenção mecânica no pátio ou hangar, o militar especialista de apoio deve cumprir regras fundamentais no uso de ferramentas manuais. Sobre este assunto, assinale a opção correta:",
        options: [
            { text: "É recomendado empurrar a chave de boca/combinada no sentido oposto ao corpo para obter maior torque mecânico.", letter: "A" },
            { text: "O torquímetro deve ser utilizado prioritariamente para o desaperto rápido de parafusos com alto grau de emperramento.", letter: "B" },
            { text: "Os alicates convencionais universais são indicados para o aperto de porcas estriadas e conexões de tubulações aeronáuticas.", letter: "C" },
            { text: "A chave ajustável (inglesa) deve ser girada sempre em direção ao mordente móvel para colocar a força no mordente fixo.", letter: "D" },
            { text: "Macetes com cabeça de aço forjado devem ser usados sobre revestimentos de ligas leves para evitar centelhamento.", letter: "E" }
        ],
        correctIndex: 3,
        rationales: [
            "Incorreta. O militar deve sempre PUXAR a chave em sua direção (jamais empurrá-la) para evitar lesões corporais caso o mordente escape.",
            "Incorreta. É expressamente proibido usar o torquímetro como alavanca de afrouxamento; ele é um instrumento de precisão de torque.",
            "Incorreta. Na aviação, é vedado o uso de alicates universais para apertar porcas estriadas ou conexões hidráulicas.",
            "Correta. A chave ajustável deve ser tracionada/girada na direção do mordente móvel, fazendo com que a força principal incida sobre o mordente fixo.",
            "Incorreta. Em ligas leves e áreas de inflamáveis, utilizam-se macetes plásticos, de borracha ou bronze; martelos de aço forjado são de uso em oficina geral e deformam superfícies leves."
        ]
    },
    {
        module: "Módulo II - Logística, Manutenção e Eletricidade",
        topic: "Eletricidade Básica - Lei de Ohm e Efeito Joule",
        question: "Considere um circuito elétrico resistivo alimentado por uma fonte de tensão contínua de $24\\text{ V}$ operando com uma resistência interna de $6\\ \\Omega$. Com base na Lei de Ohm ($I = V / R$) e na equação da potência ($P = V \\times I$), quais são, respectivamente, o valor da corrente elétrica e a potência dissipada por Efeito Joule?",
        options: [
            { text: "2 A e 48 W.", letter: "A" },
            { text: "4 A e 96 W.", letter: "B" },
            { text: "144 A e 24 W.", letter: "C" },
            { text: "4 A e 24 W.", letter: "D" },
            { text: "0,25 A e 6 W.", letter: "E" }
        ],
        correctIndex: 1,
        rationales: [
            "Incorreta. Calculou erroneamente a corrente como 24/12 em vez de 24/6.",
            "Correta. Aplicando a Lei de Ohm: $I = 24 / 6 = 4\\text{ A}$. Calculando a potência: $P = 24 \\times 4 = 96\\text{ W}$.",
            "Incorreta. Multiplicou os valores de tensão e resistência incorretamente.",
            "Incorreta. Acertou a corrente (4 A), mas errou o cálculo da potência ($24 \\times 4 = 96\\text{ W}$, não 24 W).",
            "Incorreta. Inverteu a divisão da Lei de Ohm ($6 / 24 = 0,25\\text{ A}$)."
        ]
    },

    // ---------------------- MÓDULO III ----------------------
    {
        module: "Módulo III - Manutenção de Veículos, Pintura e Logística",
        topic: "Procedimentos Automotivos - Jump-Start",
        question: "Durante o procedimento emergencial de partida assistida com bateria auxiliar (jump-start) em uma viatura militar socorrida, a última conexão do cabo negativo (preto) deve ser realizada obrigatoriamente em:",
        options: [
            { text: "No polo positivo da bateria descarregada da viatura socorrida.", letter: "A" },
            { text: "Diretamente no polo negativo da bateria descarregada da viatura socorrida.", letter: "B" },
            { text: "Em um ponto sólido de massa metálica não pintada do bloco do motor da viatura socorrida.", letter: "C" },
            { text: "No polo positivo da bateria doadora em funcionamento.", letter: "D" },
            { text: "No terminal central do alternador do veículo doador.", letter: "E" }
        ],
        correctIndex: 2,
        rationales: [
            "Incorreta. Conectar o cabo negativo ao polo positivo causaria um curto-circuito grave.",
            "Incorreta. Nunca se deve conectar diretamente ao polo negativo da bateria descarregada para evitar fagulhas próximas a gases de hidrogênio inflamáveis emitidos pela bateria.",
            "Correta. A conexão final do cabo negativo deve ser feita na massa metálica (chassi/bloco do motor) distante da bateria socorrida, minimizando o risco de ignição de gases inflamáveis.",
            "Incorreta. O cabo negativo jamais deve ser ligado a polos positivos.",
            "Incorreta. Conexões no alternador podem danificar a centralina e os circuitos eletrônicos do veículo."
        ]
    },
    {
        module: "Módulo III - Manutenção de Veículos, Pintura e Logística",
        topic: "Corrosão e Reações Eletroquímicas",
        question: "Para que se estabeleça uma célula galvânica elementar de corrosão eletroquímica em uma estrutura metálica, é indispensável a presença simultânea de quatro elementos fundamentais. Assinale a opção que apresenta esses quatro elementos:",
        options: [
            { text: "Área Anódica, Área Catódica, Condutor Metálico e Eletrólito.", letter: "A" },
            { text: "Área Anódica, Desgaste Abrasivo, Tinta Epóxi e Eletrólito.", letter: "B" },
            { text: "Área Catódica, Radiação Ultravioleta, Condutor Cerâmico e Vácuo.", letter: "C" },
            { text: "Erosão Mecânica, Umidade Relativa, Ácido Sulfúrico e Anodo de Sacrifício.", letter: "D" },
            { text: "Cátodo, Anodo, Película Airless e Corrente Alternada.", letter: "E" }
        ],
        correctIndex: 0,
        rationales: [
            "Correta. A pilha ou célula de corrosão eletroquímica necessita obrigatoriamente de: Ânodo (onde ocorre oxidação), Cátodo (onde ocorre redução), Condutor metálico (passagem de elétrons) e Eletrólito (meio condutor iônico).",
            "Incorreta. Desgaste abrasivo é fenômeno de erosão mecânica, não elemento constitutivo da célula galvânica.",
            "Incorreta. Cerâmicas são isolantes elétricos e o vácuo impede a presença de eletrólito.",
            "Incorreta. Confunde erosão (desgaste mecânico) com os componentes eletroquímicos fundamentais.",
            "Incorreta. Airless é um método de pintura por pulverização e corrente alternada não é elemento da pilha."
        ]
    },
    {
        module: "Módulo III - Manutenção de Veículos, Pintura e Logística",
        topic: "Publicações Técnicas do SISMA e Etiquetas",
        question: "No âmbito do SISMA e do Centro de Distribuição e Controle de Peças (CDCP), o material inspecionado que se encontra formalmente condenado, irrecuperável ou inservível deve receber a identificação por meio de qual etiqueta de conformidade?",
        options: [
            { text: "Etiqueta Verde (Material Perfeito).", letter: "A" },
            { text: "Etiqueta Amarela (Material Avariado / Recuperável).", letter: "B" },
            { text: "Etiqueta Azul (Material Sobressalente em Trânsito).", letter: "C" },
            { text: "Etiqueta Vermelha (Material Condenado).", letter: "D" },
            { text: "Etiqueta Branca (Material SSS de Exibição).", letter: "E" }
        ],
        correctIndex: 3,
        rationales: [
            "Incorreta. A Etiqueta Verde atesta material revisado e em perfeitas condições de uso operacional.",
            "Incorreta. A Etiqueta Amarela indica material avariado que exige reparo, revisão ou intervenção corretiva.",
            "Incorreta. Esta classificação de cor não existe no padrão de conformidade do SISMA exibido no manual.",
            "Correta. A Etiqueta Vermelha identifica material formalmente condenado, irrecuperável ou inservível, devendo ser separado para alienação ou destruição.",
            "Incorreta. Não existe etiqueta branca para este propósito no padrão de conformidade logístico do SISMA."
        ]
    },

    // ---------------------- MÓDULO IV ----------------------
    {
        module: "Módulo IV - Saúde, Biossegurança e Ética",
        topic: "Classificação de Spaulding de Artigos Hospitalares",
        question: "De acordo com a Classificação de Spaulding adotada nas normas de biossegurança hospitalar, os materiais que entram em contato direto com tecidos estéreis ou com o sistema vascular do paciente são definidos como:",
        options: [
            { text: "Artigos Não Críticos, exigindo apenas limpeza ou desinfecção de baixo nível.", letter: "A" },
            { text: "Artigos Semicríticos, exigindo desinfecção de alto nível com glutaraldeído.", letter: "B" },
            { text: "Artigos Críticos, exigindo compulsoriamente o processo de esterilização.", letter: "C" },
            { text: "Artigos Infectantes de Grupo D, descartáveis em sacos pretos.", letter: "D" },
            { text: "Artigos Sanitários Comuns, submetidos apenas à lavagem com água e sabão.", letter: "E" }
        ],
        correctIndex: 2,
        rationales: [
            "Incorreta. Artigos não críticos entram em contato apenas com pele intacta (ex: manguito de pressão).",
            "Incorreta. Artigos semicríticos entram em contato com mucosas íntegras ou pele não íntegra (ex: inaladores).",
            "Correta. Artigos críticos entram em tecido estéril ou sistema vascular (bisturis, agulhas, pinças) e exigem esterilização obrigatória.",
            "Incorreta. Mistura a classificação de artigos com a classificação de resíduos da RDC 222/2018 (Grupo D = comum).",
            "Incorreta. A lavagem simples não garante a eliminação microbiana exigida para tecidos estéreis."
        ]
    },
    {
        module: "Módulo IV - Saúde, Biossegurança e Ética",
        topic: "Gerenciamento de Resíduos (RDC 222/2018)",
        question: "Conforme a Resolução RDC nº 222/2018 da ANVISA, sobre o descarte de resíduos perfurocortantes (Grupo E), como lâminas de bisturi e agulhas hipodérmicas, assinale a afirmativa correta:",
        options: [
            { text: "Devem ser descartados em sacos plásticos brancos leitosos identificados com o símbolo de risco biológico até a borda superior.", letter: "A" },
            { text: "Podem ser esvaziados manualmente para reutilização do recipiente rígido após autoclavagem rápida.", letter: "B" },
            { text: "As agulhas utilizadas devem ser obrigatoriamente reencapadas antes de seu descarte na caixa de resíduos.", letter: "C" },
            { text: "Devem ser recolhidos em recipientes rígidos e estanques (tipo Descarpack), interrompendo-se o descarte ao atingir 3/4 da capacidade (linha pontilhada).", letter: "D" },
            { text: "Classificam-se como Grupo D (resíduos comuns) devendo ser descartados em sacos cinzas ou pretos.", letter: "E" }
        ],
        correctIndex: 3,
        rationales: [
            "Incorreta. Sacos brancos leitosos são destinados aos resíduos infectantes não perfurocortantes (Grupo A).",
            "Incorreta. É expressamente proibido esvaziar, reaproveitar ou reutilizar recipientes de perfurocortantes.",
            "Incorreta. O reencape manual de agulhas usadas é estritamente proibido pelas normas de biossegurança por alto risco de acidente.",
            "Correta. O Grupo E (perfurocortantes) deve ser descartado em caixas rígidas amarelas até o limite de 3/4 da capacidade (linha pontilhada de segurança).",
            "Incorreta. Grupo D é composto por resíduos comuns assemelhados ao lixo domiciliar."
        ]
    },
    {
        module: "Módulo IV - Saúde, Biossegurança e Ética",
        topic: "Sinais Vitais (SV) - Valores de Referência",
        question: "A sigla técnica padronizada nos serviços de saúde para referenciar os parâmetros corporais que expressam a homeostase fisiológica é SV (Sinais Vitais). Em relação aos valores fisiológicos normais de repouso em um adulto hígido, assinale a opção correta:",
        options: [
            { text: "Frequência Cardíaca (FC) normocárdica: 12 a 20 batimentos por minuto.", letter: "A" },
            { text: "Frequência Respiratória (FR) eupneica: 60 a 100 incursões respiratórias por minuto.", letter: "B" },
            { text: "Temperatura Axilar normotérmica: 35,5 °C a 37,2 °C.", letter: "C" },
            { text: "Pressão Arterial Sistêmica normotensa: Sistólica ≥ 140 mmHg e Diastólica ≥ 90 mmHg.", letter: "D" },
            { text: "A terminologia padronizada de saúde para checagem corporal de pulso e pressão é SST.", letter: "E" }
        ],
        correctIndex: 2,
        rationales: [
            "Incorreta. 12 a 20 é a Frequência RESPIRATÓRIA (FR) por minuto, não cardíaca.",
            "Incorreta. 60 a 100 é a Frequência CARDÍACA (FC) por minuto, não respiratória.",
            "Correta. A faixa normotérmica fisiológica axilar em adultos compreende de 35,5 °C a 37,2 °C.",
            "Incorreta. Valores de PA ≥ 140/90 mmHg indicam HIPERTENSÃO; o padrão normotenso é sistólica ≤ 120 mmHg e diastólica ≤ 80 mmHg.",
            "Incorreta. O uso da sigla SST (Saúde e Segurança do Trabalho) é incorreto para designar parâmetros corporais (Sinais Vitais é SV)."
        ]
    },
    {
        module: "Módulo IV - Saúde, Biossegurança e Ética",
        topic: "Atendimento Pré-Hospitalar - Diretrizes RCP (AHA)",
        question: "De acordo com a diretriz atualizada da American Heart Association (AHA) para Reanimação Cardiopulmonar (RCP) em adultos, qual é a frequência e profundidade corretas para a realização das compressões torácicas de alta qualidade?",
        options: [
            { text: "Frequência fixa de 80 compressões por minuto e profundidade de 2 a 3 cm.", letter: "A" },
            { text: "Frequência contínua de 100 a 120 compressões por minuto e profundidade entre 5 e 6 cm.", letter: "B" },
            { text: "Frequência de 140 a 160 compressões por minuto e profundidade mínima de 8 cm.", letter: "C" },
            { text: "Frequência de 60 compressões por minuto intercaladas com 5 ventilações profundas.", letter: "D" },
            { text: "Frequência variável dependendo do peso da vítima, mantendo o tórax sempre pressionado sem retorno.", letter: "E" }
        ],
        correctIndex: 1,
        rationales: [
            "Incorreta. Frequência muito baixa e profundidade insuficiente para gerar débito cardíaco eficaz.",
            "Correta. A diretriz AHA preconiza a taxa de 100 a 120 compressões por minuto com profundidade de 5 a 6 cm, garantindo o retorno total do tórax.",
            "Incorreta. Frequência acima de 120 cpm prejudica o enchimento ventricular e profundidade de 8 cm causa traumas graves desnecessários.",
            "Incorreta. A relação padronizada é 30:2 com taxa de compressão entre 100 e 120 cpm.",
            "Incorreta. É fundamental permitir o retorno elástico completo do tórax após cada compressão."
        ]
    },
    {
        module: "Módulo IV - Saúde, Biossegurança e Ética",
        topic: "Atendimento Pré-Hospitalar - Ferimentos Específicos",
        question: "No atendimento pré-hospitalar de uma vítima que apresenta um ferimento torácico aspirativo (pneumotórax aberto), qual é o procedimento de emergência padronizado para a curativo de primeira resposta?",
        options: [
            { text: "Remover imediatamente qualquer corpo estranho e vedar completamente com torniquete tático.", letter: "A" },
            { text: "Realizar a inserção de compressas secas para dentro da cavidade torácica empurrando o pulmão.", letter: "B" },
            { text: "Aplicar o curativo de três pontas (oclusivo selado em três bordas, deixando uma ponta livre como válvula).", letter: "C" },
            { text: "Tracionar as costelas fraturadas para fora e cobrir com pomada aquecida.", letter: "D" },
            { text: "Realizar lavagem abundante com álcool 70% e manter o paciente em decúbito ventral.", letter: "E" }
        ],
        correctIndex: 2,
        rationales: [
            "Incorreta. Objetos encravados não devem ser removidos no APH e torniquetes são aplicados exclusivamente em membros.",
            "Incorreta. Nunca se deve introduzir materiais para dentro de cavidades corporais atingidas.",
            "Correta. O curativo de três pontas atua como válvula unidirecional: impede a entrada do ar ambiente durante a inspiração e permite a saída do ar durante a expiração.",
            "Incorreta. Tracionar estruturas ósseas agrava lesões vasculares e pulmonares.",
            "Incorreta. Álcool 70% não deve ser aplicado em feridas abertas profundas e decúbito ventral dificulta a mecânica respiratória."
        ]
    },
    {
        module: "Módulo IV - Saúde, Biossegurança e Ética",
        topic: "Ética Profissional - Clauss Möller",
        question: "Segundo a conceituação das Três Virtudes do trabalho profissional de Clauss Möller, apresentada no módulo de Ética da apostila militar, assinale a opção que define corretamente a virtude da INICIATIVA:",
        options: [
            { text: "É o comprometimento inegociável do militar com o resultado de seus atos e omissões, zelando pelo patrimônio sob sua custódia.", letter: "A" },
            { text: "É a fidelidade moral expressa para com a Força Aérea Brasileira, seus superiores e pares, mantendo o sigilo funcional.", letter: "B" },
            { text: "É a capacidade de antever demandas funcionais e agir de modo produtivo e oportuno sem a necessidade de ordem externa formal, respeitando os limites regulamentares.", letter: "C" },
            { text: "É a subserviência cega a ordens ilegais acompanhada do cumprimento estrito de horários de formatura.", letter: "D" },
            { text: "É o hábito de executar manutenções de alta complexidade em circuitos de alta tensão sem possuir a certificação técnica formal.", letter: "E" }
        ],
        correctIndex: 2,
        rationales: [
            "Incorreta. Esta é a definição exata da virtude da RESPONSABILIDADE.",
            "Incorreta. Esta é a definição exata da virtude da LEALDADE.",
            "Correta. A INICIATIVA consiste em agir preventivamente e com oportunidade diante de necessidades da organização, sem depender de comandos constantes, dentro da legalidade.",
            "Incorreta. A lealdade e ética militar repelem a subserviência cega a ilegalidades.",
            "Incorreta. Intervir em sistemas complexos sem qualificação violaria a prudência e a ressalva de escopo da apostila."
        ]
    }
];

let userAnswers = new Array(quizData.length).fill(null);
let score = 0;

function renderQuiz() {
    const quizContainer = document.getElementById('quizContainer');
    document.getElementById('totalQNum').innerText = quizData.length;

    quizData.forEach((q, qIndex) => {
        const card = document.createElement('div');
        card.className = 'question-card';
        card.id = `q-card-${qIndex}`;

        let optionsHTML = '';
        q.options.forEach((opt, optIndex) => {
            optionsHTML += `
                <li class="option-item" id="opt-${qIndex}-${optIndex}" onclick="selectOption(${qIndex}, ${optIndex})">
                    <div class="option-letter">${opt.letter}</div>
                    <div class="option-text">${opt.text}</div>
                </li>
            `;
        });

        card.innerHTML = `
            <span class="module-tag">${q.module} &bull; ${q.topic}</span>
            <div class="question-title">${qIndex + 1}. ${q.question}</div>
            <ul class="options-list">
                ${optionsHTML}
            </ul>
            <div class="explanation-box" id="exp-${qIndex}">
                <div class="explanation-title" id="exp-title-${qIndex}"></div>
                <div id="exp-details-${qIndex}"></div>
            </div>
        `;

        quizContainer.appendChild(card);
    });
}

function selectOption(qIndex, optIndex) {
    if (userAnswers[qIndex] !== null) return; // Impede alterar resposta

    userAnswers[qIndex] = optIndex;
    const q = quizData[qIndex];
    const isCorrect = (optIndex === q.correctIndex);

    if (isCorrect) score++;

    // Atualizar barra de progresso e score
    const answeredCount = userAnswers.filter(a => a !== null).length;
    document.getElementById('scoreNum').innerText = score;
    document.getElementById('currentQNum').innerText = Math.min(answeredCount + 1, quizData.length);
    document.getElementById('progressBar').style.width = `${(answeredCount / quizData.length) * 100}%`;

    // Renderizar estado visual das opções
    q.options.forEach((_, i) => {
        const optEl = document.getElementById(`opt-${qIndex}-${i}`);
        optEl.classList.add('disabled');

        if (i === q.correctIndex) {
            optEl.classList.add('show-correct');
            if (i === optIndex) {
                optEl.classList.add('selected-correct');
            }
        } else if (i === optIndex && !isCorrect) {
            optEl.classList.add('selected-incorrect');
        }
    });

    // Exibir Caixa de Explicação Detalhada
    const expBox = document.getElementById(`exp-${qIndex}`);
    const expTitle = document.getElementById(`exp-title-${qIndex}`);
    const expDetails = document.getElementById(`exp-details-${qIndex}`);

    expBox.style.display = 'block';

    if (isCorrect) {
        expTitle.className = 'explanation-title correct';
        expTitle.innerHTML = '✔ RESPOSTA CORRETA!';
    } else {
        expTitle.className = 'explanation-title incorrect';
        expTitle.innerHTML = `✖ RESPOSTA INCORRETA. A alternativa correta é a letra (${q.options[q.correctIndex].letter}).`;
    }

    let detailsHTML = '';
    q.options.forEach((opt, i) => {
        const isThisCorrect = (i === q.correctIndex);
        const expClass = isThisCorrect ? 'explanation-item is-correct-exp' : 'explanation-item';
        detailsHTML += `
            <div class="${expClass}">
                <strong>Alternativa (${opt.letter}):</strong> ${q.rationales[i]}
            </div>
        `;
    });

    expDetails.innerHTML = detailsHTML;

    // Verificar se respondeu todas
    if (answeredCount === quizData.length) {
        showFinalSummary();
    }
}

function showFinalSummary() {
    document.getElementById('statsBar').style.display = 'none';
    const summaryCard = document.getElementById('summaryCard');
    const finalScore = document.getElementById('finalScore');
    const performanceMsg = document.getElementById('performanceMsg');

    finalScore.innerText = `${score} / ${quizData.length}`;
    const percentage = (score / quizData.length) * 100;

    if (percentage >= 80) {
        performanceMsg.innerText = "Excelente desempenho! Você demonstrou alto domínio dos tópicos da Apostila AAP do CFC/CESD.";
    } else if (percentage >= 60) {
        performanceMsg.innerText = "Bom resultado! Continue revisando os módulos com atenção para consolidar a matéria.";
    } else {
        performanceMsg.innerText = "Recomendamos reforçar a leitura dos quatro módulos da Apostila Técnica antes do exame.";
    }

    summaryCard.style.display = 'block';
    summaryCard.scrollIntoView({ behavior: 'smooth' });
}

function resetQuiz() {
    userAnswers = new Array(quizData.length).fill(null);
    score = 0;
    document.getElementById('quizContainer').innerHTML = '';
    document.getElementById('summaryCard').style.display = 'none';
    document.getElementById('statsBar').style.display = 'flex';
    document.getElementById('scoreNum').innerText = '0';
    document.getElementById('currentQNum').innerText = '1';
    document.getElementById('progressBar').style.width = '0%';
    renderQuiz();
    window.scrollTo({ top: 0, behavior: 'smooth' });
}

// Inicializar simulado ao carregar
window.onload = renderQuiz;
</script>

</body>
</html>
```eof

### Resumo dos Recursos Incluídos no Simulado:

1. **Cobertura Completa do Conteúdo**:
   - **Módulo I (Apoio Administrativo):** Hardware, memórias (RAM x ROM), Decreto nº 9.758/2019 (pronomes de tratamento), Redação Oficial (NSCA 5-3), tipos de Ofícios e Despachos e SIGADAER.
   - **Módulo II (Logística, Manutenção e Eletricidade):** SILOMS, terminologia técnica (*Canibalização*, *Implantar*, etc.), segurança no uso de ferramentas manuais, Lei de Ohm e Efeito Joule.
   - **Módulo III (Manutenção de Veículos, Pintura e Logística):** Procedimentos de *Jump-Start* e segurança com baterias, Célula Galvânica de corrosão, Publicações do SISMA (OT/DT/PA) e Etiquetas de Conformidade (Verde, Amarela e Vermelha).
   - **Módulo IV (Saúde, Biossegurança e Ética):** Classificação de Spaulding (Artigos Críticos), RDC 222/2018 (Perfurocortantes - Grupo E e preenchimento de 3/4), Sinais Vitais (SV) e parâmetros normais, RCP conforme Diretrizes AHA (100-120 cpm, 5-6 cm), Curativo de 3 Pontas e as Três Virtudes de Clauss Möller.

2. **Interatividade e Gabarito Comentado**:
   - Alternativas de **A até E**.
   - **Explicações imediatas e detalhadas** de todas as opções (corretas e incorretas) após a seleção da alternativa.
   - Barra de progresso dinâmica e contagem automática de acertos.

Bons estudos e excelente preparação para o CFC/CESD!
