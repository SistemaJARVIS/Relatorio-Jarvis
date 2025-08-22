# Relatorio-Jarvis
Relatório de Matemática 5º Ano B e C
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Relatório de Matemática - 5º Ano B e C</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/FileSaver.js/2.0.5/FileSaver.min.js"></script>
    <style>
        :root {
            --primary-color: #1f4e79;
            --secondary-color: #2e75b6;
            --accent-color: #21a366;
            --danger-color: #ff4d4d;
            --light-color: #f0f3f8;
            --dark-color: #333;
            --table-header-bg: #2e75b6;
            --table-row-even: #f2f8ff;
            --table-row-hover: #e6f0ff;
            --border-color: #d9d9d9;
        }
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        body {
            background-color: var(--light-color);
            color: var(--dark-color);
            line-height: 1.6;
            padding: 20px;
        }
        .container {
            max-width: 1800px;
            margin: 0 auto;
            background: white;
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }
        header {
            background: var(--primary-color);
            color: white;
            padding: 20px;
            text-align: center;
        }
        header h1 {
            font-size: 24px;
            margin-bottom: 10px;
        }
        header p {
            font-size: 16px;
            opacity: 0.9;
        }
        .controls {
            padding: 15px 20px;
            background: #e6eef7;
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            justify-content: space-between;
            align-items: center;
        }
        .search-container {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .search-container input {
            padding: 8px 12px;
            border: 1px solid #ccc;
            border-radius: 4px;
            width: 250px;
        }
        .tabs {
            display: flex;
            background: #d0e0f0;
            border-bottom: 2px solid var(--secondary-color);
        }
        .tab {
            padding: 12px 20px;
            cursor: pointer;
            background: #d0e0f0;
            border: none;
            font-weight: 600;
            transition: all 0.3s;
        }
        .tab.active {
            background: var(--secondary-color);
            color: white;
        }
        .tab:hover:not(.active) {
            background: #b8d0e8;
        }
        .btn {
            padding: 10px 15px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s;
        }
        .btn-primary {
            background: var(--primary-color);
            color: white;
        }
        .btn-primary:hover {
            background: var(--secondary-color);
        }
        .btn-success {
            background: var(--accent-color);
            color: white;
        }
        .btn-success:hover {
            background: #107c41;
        }
        .btn-danger {
            background: var(--danger-color);
            color: white;
        }
        .btn-danger:hover {
            background: #e60000;
        }
        .btn-group {
            display: flex;
            gap: 10px;
        }
        .table-container {
            overflow-x: auto;
            max-height: 70vh;
        }
        table {
            width: 100%;
            border-collapse: collapse;
        }
        th, td {
            border: 1px solid var(--border-color);
            padding: 10px;
            text-align: center;
            font-size: 14px;
            vertical-align: middle; /* Centraliza verticalmente o conteúdo */
        }
        th {
            background-color: var(--table-header-bg);
            color: white;
            position: sticky;
            top: 0;
            z-index: 10;
            cursor: help;
            position: relative;
        }
        tr:nth-child(even) {
            background-color: var(--table-row-even);
        }
        tr:hover {
            background-color: var(--table-row-hover);
        }
        .student-name {
            min-width: 220px;
            text-align: left;
            font-weight: 500;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .checkbox-cell {
            width: 40px;
            text-align: center;
        }
        input[type="checkbox"] {
            transform: scale(1.2);
            cursor: pointer;
        }
        .instructions {
            padding: 15px 20px;
            background: #fff4e6;
            border-top: 1px solid #ffd8b8;
            font-size: 14px;
        }
        .instructions h3 {
            margin-bottom: 8px;
            color: #cc6600;
        }
        .instructions ul {
            padding-left: 20px;
        }
        .instructions li {
            margin-bottom: 5px;
        }
        .hidden {
            display: none;
        }
        .highlight {
            background-color: yellow;
            font-weight: bold;
        }
        /* Tooltip styles */
        .tooltip {
            position: relative;
            display: inline-block;
            border-bottom: 1px dotted white;
        }
        .tooltip .tooltiptext {
            visibility: hidden;
            width: 300px;
            background-color: #555;
            color: #fff;
            text-align: left;
            border-radius: 6px;
            padding: 10px;
            position: absolute;
            z-index: 1000;
            bottom: 125%;
            left: 50%;
            margin-left: -150px;
            opacity: 0;
            transition: opacity 0.3s;
            font-size: 12px;
            font-weight: normal;
            box-shadow: 0 2px 10px rgba(0,0,0,0.2);
        }
        .tooltip .tooltiptext::after {
            content: "";
            position: absolute;
            top: 100%;
            left: 50%;
            margin-left: -5px;
            border-width: 5px;
            border-style: solid;
            border-color: #555 transparent transparent transparent;
        }
        .tooltip:hover .tooltiptext {
            visibility: visible;
            opacity: 1;
        }
        /* Comentário styles */
        .comentario-btn {
            background-color: #4CAF50;
            color: white;
            padding: 5px 10px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 12px;
            margin-left: 10px;
            flex-shrink: 0; /* Impede o botão de encolher */
        }
        .comentario-btn:hover {
            background-color: #45a049;
        }
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
        }
        .modal-content {
            background-color: #fefefe;
            margin: 5% auto;
            padding: 20px;
            border: 1px solid #888;
            width: 80%;
            max-width: 600px;
            border-radius: 8px;
        }
        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
            cursor: pointer;
        }
        .close:hover {
            color: black;
        }
        textarea {
            width: 100%;
            height: 120px;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            resize: vertical;
            font-family: Arial, sans-serif;
        }
        .salvar-btn {
            background-color: #008CBA;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            margin-top: 10px;
        }
        .salvar-btn:hover {
            background-color: #007B9A;
        }
        @media (max-width: 1200px) {
            .controls {
                flex-direction: column;
                align-items: stretch;
            }
            .btn-group {
                width: 100%;
                justify-content: center;
                flex-wrap: wrap;
            }
            .search-container {
                width: 100%;
                justify-content: center;
            }
            .search-container input {
                width: 100%;
                max-width: 300px;
            }
        }
        @media (max-width: 768px) {
            th, td {
                padding: 6px;
                font-size: 12px;
            }
            .student-name {
                min-width: 150px;
            }
            .tab {
                padding: 8px 12px;
                font-size: 14px;
            }
            .tooltip .tooltiptext {
                width: 200px;
                margin-left: -100px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>RELATÓRIO QUINZENAL/MENSAL - 5º ANO B E C</h1>
            <p>COMPONENTE CURRICULAR - MATEMÁTICA - PROFESSOR FRANCISCO SANTOS</p>
        </header>
        <div class="controls">
            <div class="search-container">
                <input type="text" id="searchInput" placeholder="Pesquisar aluno...">
                <button class="btn btn-primary" id="searchBtn">Buscar</button>
            </div>
            <div class="btn-group">
                <button class="btn btn-primary" id="editToggle">Modo Edição</button>
                <button class="btn btn-success" id="saveBtn">Salvar Dados</button>
                <button class="btn btn-primary" id="exportExcel">Exportar Excel</button>
                <button class="btn btn-primary" id="exportPDF">Exportar PDF</button>
                <button class="btn btn-primary" id="exportWord">Exportar Word</button>
                <button class="btn btn-danger" id="resetBtn">Restaurar Original</button>
            </div>
        </div>
        <div class="tabs">
            <button class="tab active" data-tab="turmaB">5º Ano B - Francisco Santos</button>
            <button class="tab" data-tab="turmaC">5º Ano C - Francisco Santos</button>
        </div>
        <div class="table-container">
            <table id="turmaB" class="turma-table">
                <thead>
                    <tr>
                        <th>Nº</th>
                        <th>Estudante</th>
                        <th>
                            <div class="tooltip">Ler/escrever números até milhar
                                <span class="tooltiptext">
                                    <strong>Marcos de Aprendizagem:</strong><br>
                                    • Lê números naturais até a ordem das unidades de milhar<br>
                                    • Escreve números naturais até a ordem das unidades de milhar<br>
                                    • Compreende o valor posicional dos algarismos<br>
                                    • Compara números naturais usando os símbolos >, < ou =
                                </span>
                            </div>
                        </th>
                        <th>
                            <div class="tooltip">Utiliza procedimentos de cálculos
                                <span class="tooltiptext">
                                    <strong>Marcos de Aprendizagem:</strong><br>
                                    • Realiza adições com reserva<br>
                                    • Realiza subtrações com recurso<br>
                                    • Resolve problemas envolvendo as quatro operações<br>
                                    • Utiliza diferentes estratégias de cálculo mental
                                </span>
                            </div>
                        </th>
                        <th>
                            <div class="tooltip">Problemas de multiplicação
                                <span class="tooltiptext">
                                    <strong>Marcos de Aprendizagem:</strong><br>
                                    • Compreende a multiplicação como adição de parcelas iguais<br>
                                    • Resolve problemas de multiplicação com até duas cifras<br>
                                    • Utiliza a tabuada para resolver problemas<br>
                                    • Identifica situações que envolvem multiplicação
                                </span>
                            </div>
                        </th>
                        <th>
                            <div class="tooltip">Classifica figuras planas
                                <span class="tooltiptext">
                                    <strong>Marcos de Aprendizagem:</strong><br>
                                    • Identifica e classifica figuras planas (círculo, quadrado, retângulo, triângulo)<br>
                                    • Reconhece propriedades de figuras planas (número de lados e vértices)<br>
                                    • Diferenciar polígonos de não polígonos<br>
                                    • Identifica figuras planas em objetos do cotidiano
                                </span>
                            </div>
                        </th>
                        <th>
                            <div class="tooltip">Identifica unidades de medida
                                <span class="tooltiptext">
                                    <strong>Marcos de Aprendizagem:</strong><br>
                                    • Identifica unidades de medida de comprimento (metro, centímetro)<br>
                                    • Identifica unidades de medida de capacidade (litro, mililitro)<br>
                                    • Identifica unidades de medida de massa (quilograma, grama)<br>
                                    • Realiza conversões entre unidades de medida
                                </span>
                            </div>
                        </th>
                        <th>
                            <div class="tooltip">Identifica unidade de comprimento
                                <span class="tooltiptext">
                                    <strong>Marcos de Aprendizagem:</strong><br>
                                    • Compreende o conceito de comprimento<br>
                                    • Utiliza instrumentos de medida (régua, fita métrica)<br>
                                    • Estima medidas de comprimento<br>
                                    • Resolve problemas envolvendo unidades de comprimento
                                </span>
                            </div>
                        </th>
                        <th>Aluno com deficiência</th>
                        <th>Comportamento atípico</th>
                        <th>Infrequente</th>
                    </tr>
                </thead>
                <tbody>
                    <!-- Dados da Turma B serão preenchidos via JavaScript -->
                </tbody>
            </table>
            <table id="turmaC" class="turma-table hidden">
                <thead>
                    <tr>
                        <th>Nº</th>
                        <th>Estudante</th>
                        <th>
                            <div class="tooltip">Ler/escrever números até milhar
                                <span class="tooltiptext">
                                    <strong>Marcos de Aprendizagem:</strong><br>
                                    • Lê números naturais até a ordem das unidades de milhar<br>
                                    • Escreve números naturais até a ordem das unidades de milhar<br>
                                    • Compreende o valor posicional dos algarismos<br>
                                    • Compara números naturais usando os símbolos >, < ou =
                                </span>
                            </div>
                        </th>
                        <th>
                            <div class="tooltip">Utiliza procedimentos de cálculos
                                <span class="tooltiptext">
                                    <strong>Marcos de Aprendizagem:</strong><br>
                                    • Realiza adições com reserva<br>
                                    • Realiza subtrações com recurso<br>
                                    • Resolve problemas envolvendo as quatro operações<br>
                                    • Utiliza diferentes estratégias de cálculo mental
                                </span>
                            </div>
                        </th>
                        <th>
                            <div class="tooltip">Problemas de multiplicação
                                <span class="tooltiptext">
                                    <strong>Marcos de Aprendizagem:</strong><br>
                                    • Compreende a multiplicação como adição de parcelas iguais<br>
                                    • Resolve problemas de multiplicação com até duas cifras<br>
                                    • Utiliza a tabuada para resolver problemas<br>
                                    • Identifica situações que envolvem multiplicação
                                </span>
                            </div>
                        </th>
                        <th>
                            <div class="tooltip">Classifica figuras planas
                                <span class="tooltiptext">
                                    <strong>Marcos de Aprendizagem:</strong><br>
                                    • Identifica e classifica figuras planas (círculo, quadrado, retângulo, triângulo)<br>
                                    • Reconhece propriedades de figuras planas (número de lados e vértices)<br>
                                    • Diferenciar polígonos de não polígonos<br>
                                    • Identifica figuras planas em objetos do cotidiano
                                </span>
                            </div>
                        </th>
                        <th>
                            <div class="tooltip">Identifica unidades de medida
                                <span class="tooltiptext">
                                    <strong>Marcos de Aprendizagem:</strong><br>
                                    • Identifica unidades de medida de comprimento (metro, centímetro)<br>
                                    • Identifica unidades de medida de capacidade (litro, mililitro)<br>
                                    • Identifica unidades de medida de massa (quilograma, grama)<br>
                                    • Realiza conversões entre unidades de medida
                                </span>
                            </div>
                        </th>
                        <th>
                            <div class="tooltip">Identifica unidade de comprimento
                                <span class="tooltiptext">
                                    <strong>Marcos de Aprendizagem:</strong><br>
                                    • Compreende o conceito de comprimento<br>
                                    • Utiliza instrumentos de medida (régua, fita métrica)<br>
                                    • Estima medidas de comprimento<br>
                                    • Resolve problemas envolvendo unidades de comprimento
                                </span>
                            </div>
                        </th>
                        <th>Aluno com deficiência</th>
                        <th>Comportamento atípico</th>
                        <th>Infrequente</th>
                    </tr>
                </thead>
                <tbody>
                    <!-- Dados da Turma C serão preenchidos via JavaScript -->
                </tbody>
            </table>
        </div>
        <div class="instructions">
            <h3>Instruções de Uso:</h3>
            <ul>
                <li>Use as abas para alternar entre as turmas</li>
                <li>Passe o mouse sobre os nomes das competências para ver os marcos de aprendizagem</li>
                <li>Clique em <strong>"Modo Edição"</strong> para habilitar a edição dos campos</li>
                <li>Marque/desmarque os checkboxes para indicar se o aluno já desenvolveu cada habilidade</li>
                <li>Clique em <strong>"Salvar Dados"</strong> para guardar as alterações no navegador</li>
                <li>Use a caixa de pesquisa para encontrar alunos específicos</li>
                <li>Use os botões de exportação para baixar relatórios nos formatos Excel, PDF ou Word</li>
                <li><strong>"Restaurar Original"</strong> volta aos dados iniciais (cuidado: apagará suas alterações)</li>
                <li>Clique no botão <strong>"Comentário"</strong> ao lado do nome do aluno para adicionar/editar observações individuais</li>
            </ul>
        </div>
    </div>

    <!-- Modal para comentários -->
    <div id="modalComentario" class="modal">
        <div class="modal-content">
            <span class="close" onclick="fecharModal()">&times;</span>
            <h2 id="modalTitulo">Comentário para </h2>
            <textarea id="textoComentario" placeholder="Digite seu comentário sobre o desenvolvimento do aluno..."></textarea>
            <br>
            <button class="salvar-btn" onclick="salvarComentario()">Salvar Comentário</button>
        </div>
    </div>

    <script>
        // Dados corrigidos da Turma B
        const turmaBData = [
            { numero: 1, nome: 'AGHATA SOPHIA SOUSA SANTOS', habilidades: [true, true, true, true, false, false, false, false, false] },
            { numero: 2, nome: 'ALERRANDRO LENE DA SILVA SOUSA', habilidades: [true, false, false, false, false, false, false, false, false] },
            { numero: 3, nome: 'ALICIA GABRIELLY JESUS DE SOUSA', habilidades: [true, true, true, true, true, false, false, false, false] },
            { numero: 4, nome: 'ANA CAROLINA DA SILVA FERREIRA', habilidades: [true, true, true, true, false, false, false, false, false] },
            { numero: 5, nome: 'ANA SOFIA DA SILVA LIMA', habilidades: [true, true, true, true, false, false, false, false, false] },
            { numero: 6, nome: 'ANTONIO DAVID SOUSA DA SILVA ALVES', habilidades: [true, true, true, true, false, false, false, false, false] },
            { numero: 7, nome: 'ANTONIO LIMA SILVA FILHO', habilidades: [true, true, false, false, true, false, false, false, false] },
            { numero: 8, nome: 'BRENDA SOPHIA DA SILVA RODRIGUES', habilidades: [true, true, true, true, true, false, false, false, false] },
            { numero: 9, nome: 'BRUNNA ISABELLY SOUSA MAGALHAES', habilidades: [true, true, true, true, true, false, false, false, false] },
            { numero: 10, nome: 'CARLOS EDUARDO DA SILVA ALMEIDA', habilidades: [true, true, true, false, false, false, false, false, false] },
            { numero: 11, nome: 'EDUARDO FELIZARDO', habilidades: [true, true, true, false, false, false, false, false, false] },
            { numero: 12, nome: 'ENZO RAFAEL SILVA SOARES', habilidades: [true, true, true, true, true, false, false, false, false] },
            { numero: 13, nome: 'ESTER RODRIGUES DE CARVALHO', habilidades: [true, false, false, false, false, false, false, false, false] },
            { numero: 14, nome: 'GABRIEL VIEIRA DA SILVA', habilidades: [true, true, true, true, false, false, false, false, false] },
            { numero: 15, nome: 'HADASSA VITORIA ALVES DE OLIVEIRA', habilidades: [true, false, false, false, false, false, false, false, false] },
            { numero: 16, nome: 'JESUS KHAUER SILVA ARAUJO', habilidades: [true, true, true, true, true, false, false, false, false] },
            { numero: 17, nome: 'KAYLA SOPHIA DE JESUS COSTA', habilidades: [true, true, true, true, true, false, false, false, false] },
            { numero: 18, nome: 'KEVEN YAN CUNHA DO NASCIMENTO', habilidades: [true, true, true, false, false, false, false, false, false] },
            { numero: 19, nome: 'MICHELLY SOPHIA SANTOS DA SILVA', habilidades: [true, true, true, false, false, false, false, false, false] },
            { numero: 20, nome: 'MYLLENA LIMA COSTA', habilidades: [true, true, true, true, true, false, false, false, false] },
            { numero: 21, nome: 'PALLOMA SANTOS GOMES', habilidades: [true, true, true, true, false, false, false, false, false] },
            { numero: 22, nome: 'PAULO VICTOR LEONARDO DE SOUSA', habilidades: [true, true, true, true, false, false, false, false, false] },
            { numero: 23, nome: 'RAYNARA LEONARDO MORAIS SILVA', habilidades: [true, true, false, false, false, false, false, false, false] },
            { numero: 24, nome: 'RHAVYLLA ARYELLY PINHEIRO FERNANDES', habilidades: [true, true, true, true, true, false, false, false, false] },
            { numero: 25, nome: 'RHIANA SOPHIA ARAUJO GUIMARAES', habilidades: [true, true, true, false, false, false, false, false, false] },
            { numero: 26, nome: 'THAYLLA NYCOLLI PINHEIRO LIMA', habilidades: [true, true, true, true, false, false, false, false, false] },
            { numero: 27, nome: 'YZABELA ALVES PEREIRA', habilidades: [true, true, false, false, false, false, false, false, false] }
        ];
        // Dados corrigidos da Turma C
        const turmaCData = [
            { numero: 1, nome: 'ANAÍSA RIBEIRO SOUSA', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 2, nome: 'ANNA BEATRYZ LIMA DE SOUSA', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 3, nome: 'ANTONIA LARYSSA GUIMARÃES DOS SANTOS', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 4, nome: 'GABRIEL DE SÁ MEDEIROS', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 5, nome: 'GUSTAVO LIMA CARVALHEDO', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 6, nome: 'HÁVYLA BRENDHA GOMES DA SILVA', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 7, nome: 'IZABELLA RAMOS DA SILVA', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 8, nome: 'JEÚS PAÉ BATISTA SOUSA', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 9, nome: 'JOÃO LUCAS DIAS SILVER', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 10, nome: 'JUCIVAN DIAS SILVA', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 11, nome: 'LÁZARO SOUSA COÊLHO', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 12, nome: 'LUCAS SILVA LOPES DO NASCIMENTO', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 13, nome: 'MARCOS EMANUEL DE SOUSA SILVA', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 14, nome: 'MARIA CECÍLIA DE SOUSA SILVA', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 15, nome: 'MARIA ISÍS SILVA', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 16, nome: 'PAULO RICARDO DE SOUSA SILVA', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 17, nome: 'PEDRO HENRIQUE DA SILVA FEITOSA', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 18, nome: 'RITA SOPHIA BARRAGEM DA SILVA', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 19, nome: 'SAMYLLA SANTOS SILVA', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 20, nome: 'SARAH KATARYNA CARVALHO DE SOUSA', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 21, nome: 'WESLLA KAROLYNNE DA SILVA BARROS', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 22, nome: 'MARIA ESTEFANY DA SILVA FERREIRA', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 23, nome: 'YSABELLA SILVA E SOUSA', habilidades: [false, false, false, false, false, false, false, false, false] },
            { numero: 24, nome: 'MARIA LETÍCIA SANTOS RODRIGUES', habilidades: [false, false, false, false, false, false, false, false, false] }
        ];
        let currentTurmaData = {
            'turmaB': JSON.parse(JSON.stringify(turmaBData)),
            'turmaC': JSON.parse(JSON.stringify(turmaCData))
        };
        let editMode = false;
        let activeTab = 'turmaB';
        let alunoAtual = '';
        let idAlunoAtual = '';

        // Carregar dados do localStorage
        function loadData() {
            const savedData = localStorage.getItem('diagnosticosMatematica');
            if (savedData) {
                const parsedData = JSON.parse(savedData);
                if (parsedData.turmaB) currentTurmaData.turmaB = parsedData.turmaB;
                if (parsedData.turmaC) currentTurmaData.turmaC = parsedData.turmaC;
            }
            renderTable('turmaB');
            renderTable('turmaC');
        }
        // Salvar dados no localStorage
        function saveData() {
            localStorage.setItem('diagnosticosMatematica', JSON.stringify(currentTurmaData));
            alert('Dados salvos com sucesso! Eles serão mantidos mesmo após fechar o navegador.');
        }
        // Renderizar a tabela para uma turma específica
        function renderTable(turma) {
            const tbody = document.querySelector(`#${turma} tbody`);
            tbody.innerHTML = '';
            currentTurmaData[turma].forEach(student => {
                const row = document.createElement('tr');
                // Coluna Número
                let cell = document.createElement('td');
                cell.textContent = student.numero;
                row.appendChild(cell);
                // Coluna Nome
                cell = document.createElement('td');
                cell.className = 'student-name';
                if (editMode) {
                    cell.contentEditable = true;
                }
                cell.textContent = student.nome;
                cell.dataset.id = student.numero;
                cell.dataset.field = 'nome';

                // Adicionar botão de comentário
                const comentarioBtn = document.createElement('button');
                comentarioBtn.className = 'comentario-btn';
                comentarioBtn.textContent = 'Comentário';
                comentarioBtn.onclick = function () {
                    abrirComentario(`${turma}_${student.numero}`, student.nome);
                };
                cell.appendChild(comentarioBtn);

                row.appendChild(cell);
                // Colunas de habilidades (9 colunas)
                for (let i = 0; i < 9; i++) {
                    cell = document.createElement('td');
                    cell.className = 'checkbox-cell';
                    const checkbox = document.createElement('input');
                    checkbox.type = 'checkbox';
                    checkbox.checked = student.habilidades[i] || false;
                    checkbox.dataset.id = student.numero;
                    checkbox.dataset.index = i;
                    checkbox.dataset.turma = turma;
                    checkbox.disabled = !editMode;
                    // Adicionar evento para atualizar dados quando checkbox for alterado
                    checkbox.addEventListener('change', function () {
                        const id = parseInt(this.dataset.id);
                        const index = parseInt(this.dataset.index);
                        const turmaKey = this.dataset.turma;
                        const studentObj = currentTurmaData[turmaKey].find(s => s.numero === id);
                        if (studentObj) {
                            studentObj.habilidades[index] = this.checked;
                        }
                    });
                    cell.appendChild(checkbox);
                    row.appendChild(cell);
                }
                tbody.appendChild(row);
            });
        }
        // Alternar modo de edição
        function toggleEditMode() {
            editMode = !editMode;
            document.getElementById('editToggle').textContent = editMode ? 'Sair do Modo Edição' : 'Modo Edição';
            renderTable('turmaB');
            renderTable('turmaC');
        }
        // Exportar para Excel
        function exportToExcel() {
            const dataToExport = [];
            dataToExport.push(['RELATÓRIO QUINZENAL/MENSAL - 5º ANO B E C']);
            dataToExport.push(['COMPONENTE CURRICULAR - MATEMÁTICA - PROFESSOR FRANCISCO SANTOS']);
            dataToExport.push([]);
            // Turma B
            dataToExport.push(['TURMA B']);
            dataToExport.push([
                'Nº', 'Estudante', 'Ler/escrever números até milhar',
                'Utiliza procedimentos de cálculos', 'Problemas de multiplicação',
                'Classifica figuras planas', 'Identifica unidades de medida',
                'Identifica unidade de comprimento', 'Aluno com deficiência',
                'Comportamento atípico', 'Infrequente', 'Comentários'
            ]);
            currentTurmaData.turmaB.forEach(student => {
                 const comentarioKey = `comentario_turmaB_${student.numero}`;
                 const comentario = localStorage.getItem(comentarioKey) || '';
                dataToExport.push([
                    student.numero,
                    student.nome,
                    student.habilidades[0] ? 'X' : '',
                    student.habilidades[1] ? 'X' : '',
                    student.habilidades[2] ? 'X' : '',
                    student.habilidades[3] ? 'X' : '',
                    student.habilidades[4] ? 'X' : '',
                    student.habilidades[5] ? 'X' : '',
                    student.habilidades[6] ? 'X' : '',
                    student.habilidades[7] ? 'X' : '',
                    student.habilidades[8] ? 'X' : '',
                    comentario
                ]);
            });
            dataToExport.push([]);
            // Turma C
            dataToExport.push(['TURMA C']);
            dataToExport.push([
                'Nº', 'Estudante', 'Ler/escrever números até milhar',
                'Utiliza procedimentos de cálculos', 'Problemas de multiplicação',
                'Classifica figuras planas', 'Identifica unidades de medida',
                'Identifica unidade de comprimento', 'Aluno com deficiência',
                'Comportamento atípico', 'Infrequente', 'Comentários'
            ]);
            currentTurmaData.turmaC.forEach(student => {
                 const comentarioKey = `comentario_turmaC_${student.numero}`;
                 const comentario = localStorage.getItem(comentarioKey) || '';
                dataToExport.push([
                    student.numero,
                    student.nome,
                    student.habilidades[0] ? 'X' : '',
                    student.habilidades[1] ? 'X' : '',
                    student.habilidades[2] ? 'X' : '',
                    student.habilidades[3] ? 'X' : '',
                    student.habilidades[4] ? 'X' : '',
                    student.habilidades[5] ? 'X' : '',
                    student.habilidades[6] ? 'X' : '',
                    student.habilidades[7] ? 'X' : '',
                    student.habilidades[8] ? 'X' : '',
                    comentario
                ]);
            });
            // Criar planilha
            const worksheet = XLSX.utils.aoa_to_sheet(dataToExport);
            const workbook = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(workbook, worksheet, 'Relatório Matemática');
            // Exportar
            XLSX.writeFile(workbook, 'relatorio_matematica_5ano.xlsx');
        }
        // Exportar para PDF - NOVO LAYOUT MELHORADO
        function exportToPDF() {
            const { jsPDF } = window.jspdf;
            const doc = new jsPDF('landscape'); // Paisagem

            const pageWidth = doc.internal.pageSize.width;
            const pageHeight = doc.internal.pageSize.height;
            const margin = 10;
            const tableStartX = margin;
            let y = margin + 10; // Começa um pouco abaixo do topo

            // Cores
            const headerColor = [31, 78, 121]; // --primary-color
            const tableHeaderColor = [46, 117, 182]; // --table-header-bg
            const rowEvenColor = [242, 248, 255]; // --table-row-even
            const textColor = [0, 0, 0];
            const lineColor = [217, 217, 217]; // --border-color

            // Título do Documento
            doc.setFontSize(18);
            doc.setTextColor(...headerColor);
            doc.text('RELATÓRIO QUINZENAL/MENSAL - 5º ANO B E C', pageWidth / 2, y, { align: 'center' });
            y += 8;
            doc.setFontSize(12);
            doc.setTextColor(...textColor);
            doc.text('COMPONENTE CURRICULAR - MATEMÁTICA - PROFESSOR FRANCISCO SANTOS', pageWidth / 2, y, { align: 'center' });
            y += 15;

            // Função para desenhar uma tabela
            function drawTable(turmaData, turmaNome) {
                // Título da Turma
                doc.setFontSize(14);
                doc.setTextColor(...tableHeaderColor);
                doc.text(turmaNome, tableStartX, y);
                y += 10;

                // Definir larguras das colunas
                const colWidths = [
                    10,  // Nº
                    45,  // Estudante
                    15,  // Ler
                    15,  // Cálc
                    15,  // Mult
                    15,  // Fig
                    15,  // Med
                    15,  // Comp
                    15,  // Def
                    15,  // Comp
                    15,  // Inf
                    60   // Comentários
                ];
                const totalTableWidth = colWidths.reduce((a, b) => a + b, 0);
                const startX = (pageWidth - totalTableWidth) / 2; // Centraliza a tabela

                const rowHeight = 10;
                const headerHeight = 10;

                // Cabeçalhos da Tabela
                doc.setFontSize(8);
                doc.setTextColor(255, 255, 255);
                doc.setFillColor(...tableHeaderColor);

                let currentX = startX;
                const headers = ['Nº', 'Estudante', 'Ler', 'Cálc', 'Mult', 'Fig', 'Med', 'Comp', 'Def', 'Comp', 'Inf', 'Comentários'];
                headers.forEach((header, i) => {
                    doc.setFillColor(...tableHeaderColor);
                    doc.rect(currentX, y - headerHeight, colWidths[i], headerHeight, 'F');
                    doc.text(header, currentX + colWidths[i] / 2, y - headerHeight / 2 + 2, { align: 'center' });
                    currentX += colWidths[i];
                });

                y += 2; // Pequeno espaço após cabeçalho

                // Dados dos Alunos
                doc.setFontSize(7);
                doc.setTextColor(...textColor);

                turmaData.forEach((student, index) => {
                    // Verifica se precisa de nova página
                    if (y + rowHeight > pageHeight - margin) {
                        doc.addPage();
                        y = margin;
                         // Re-desenha cabeçalhos na nova página
                        doc.setFontSize(8);
                        doc.setTextColor(255, 255, 255);
                        doc.setFillColor(...tableHeaderColor);
                        currentX = startX;
                        headers.forEach((header, i) => {
                            doc.setFillColor(...tableHeaderColor);
                            doc.rect(currentX, y, colWidths[i], headerHeight, 'F');
                            doc.text(header, currentX + colWidths[i] / 2, y + headerHeight / 2 + 2, { align: 'center' });
                            currentX += colWidths[i];
                        });
                        y += headerHeight + 2;
                        doc.setFontSize(7);
                        doc.setTextColor(...textColor);
                    }

                    // Cor de fundo da linha
                    if (index % 2 === 0) {
                        doc.setFillColor(...rowEvenColor);
                    } else {
                        doc.setFillColor(255, 255, 255);
                    }
                    doc.rect(startX, y, totalTableWidth, rowHeight, 'F');

                    // Borda da linha
                    doc.setDrawColor(...lineColor);
                    doc.rect(startX, y, totalTableWidth, rowHeight);

                    // Dados da linha
                    const comentarioKey = `comentario_${turmaNome.includes('B') ? 'turmaB' : 'turmaC'}_${student.numero}`;
                    const comentario = localStorage.getItem(comentarioKey) || '';

                    const rowData = [
                        student.numero.toString(),
                        student.nome,
                        student.habilidades[0] ? 'X' : '',
                        student.habilidades[1] ? 'X' : '',
                        student.habilidades[2] ? 'X' : '',
                        student.habilidades[3] ? 'X' : '',
                        student.habilidades[4] ? 'X' : '',
                        student.habilidades[5] ? 'X' : '',
                        student.habilidades[6] ? 'X' : '',
                        student.habilidades[7] ? 'X' : '',
                        student.habilidades[8] ? 'X' : '',
                        comentario
                    ];

                    currentX = startX;
                    rowData.forEach((data, i) => {
                        let align = 'center';
                        let textX = currentX + colWidths[i] / 2;
                        if (i === 1 || i === 11) { // Nome ou Comentário
                            align = 'left';
                            textX = currentX + 2;
                        }
                        doc.text(data, textX, y + rowHeight / 2 + 2, { align: align, maxWidth: colWidths[i] - (align === 'left' ? 4 : 0) });
                        currentX += colWidths[i];
                    });

                    y += rowHeight;
                });

                y += 10; // Espaço após a tabela da turma
            }

            // Desenhar Tabelas
            drawTable(currentTurmaData.turmaB, 'TURMA B - Francisco Santos');
            drawTable(currentTurmaData.turmaC, 'TURMA C - Francisco Santos');

            doc.save('relatorio_matematica_5ano.pdf');
        }
        // Exportar para Word
        function exportToWord() {
             let htmlContent = `
                <html xmlns:o="urn:schemas-microsoft-com:office:office" xmlns:w="urn:schemas-microsoft-com:office:word" xmlns="http://www.w3.org/TR/REC-html40">
                <head>
                    <meta charset="UTF-8">
                    <title>RELATÓRIO QUINZENAL/MENSAL - 5º ANO B E C</title>
                    <!--[if gte mso 9]>
                    <xml>
                        <w:WordDocument>
                            <w:View>Print</w:View>
                            <w:Zoom>100</w:Zoom>
                            <w:DoNotOptimizeForBrowser/>
                            <w:Orientation>LandScape</w:Orientation>
                        </w:WordDocument>
                    </xml>
                    <![endif]-->
                    <style>
                        @page {
                            size: A4 landscape;
                            margin: 1cm;
                        }
                        body {
                            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
                            margin: 1cm;
                            background-color: #f0f3f8;
                        }
                        .container {
                            background: white;
                            border-radius: 10px;
                            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
                            overflow: hidden;
                            padding: 20px;
                        }
                        header {
                            background: #1f4e79;
                            color: white;
                            padding: 15px;
                            text-align: center;
                            border-radius: 5px;
                        }
                        header h1 {
                            font-size: 18pt;
                            margin-bottom: 8px;
                        }
                        header p {
                            font-size: 12pt;
                            opacity: 0.9;
                        }
                        h2 {
                            font-size: 14pt;
                            color: #2e75b6;
                            margin: 20px 0 10px 0;
                        }
                        table {
                            width: 100%;
                            border-collapse: collapse;
                            table-layout: fixed;
                            page-break-inside: auto;
                            margin: 10px 0;
                            font-size: 9pt;
                        }
                        th, td {
                            border: 1px solid #d9d9d9;
                            padding: 6px;
                            word-wrap: break-word;
                            text-align: center;
                            vertical-align: top;
                        }
                        th {
                            background-color: #2e75b6;
                            color: white;
                        }
                        tr:nth-child(even) {
                            background-color: #f2f8ff;
                        }
                        .student-name-col { width: 120px; }
                        .skill-col { width: 35px; }
                        .comment-col { width: 150px; text-align: left; }
                        tr { page-break-inside: avoid; }
                    </style>
                </head>
                <body>
                    <div class="container">
                        <header>
                            <h1>RELATÓRIO QUINZENAL/MENSAL - 5º ANO B E C</h1>
                            <p>COMPONENTE CURRICULAR - MATEMÁTICA - PROFESSOR FRANCISCO SANTOS</p>
                        </header>
                        <br>
                        <h2>TURMA B</h2>
                        <table>
                            <tr>
                                <th>Nº</th>
                                <th class="student-name-col">Estudante</th>
                                <th class="skill-col">Ler</th>
                                <th class="skill-col">Cálc</th>
                                <th class="skill-col">Mult</th>
                                <th class="skill-col">Fig</th>
                                <th class="skill-col">Med</th>
                                <th class="skill-col">Comp</th>
                                <th class="skill-col">Def</th>
                                <th class="skill-col">Comp</th>
                                <th class="skill-col">Inf</th>
                                <th class="comment-col">Comentários</th>
                            </tr>
            `;
            currentTurmaData.turmaB.forEach(student => {
                 const comentarioKey = `comentario_turmaB_${student.numero}`;
                 const comentario = localStorage.getItem(comentarioKey) || '';
                htmlContent += `
                    <tr>
                        <td>${student.numero}</td>
                        <td>${student.nome}</td>
                        <td>${student.habilidades[0] ? 'X' : ''}</td>
                        <td>${student.habilidades[1] ? 'X' : ''}</td>
                        <td>${student.habilidades[2] ? 'X' : ''}</td>
                        <td>${student.habilidades[3] ? 'X' : ''}</td>
                        <td>${student.habilidades[4] ? 'X' : ''}</td>
                        <td>${student.habilidades[5] ? 'X' : ''}</td>
                        <td>${student.habilidades[6] ? 'X' : ''}</td>
                        <td>${student.habilidades[7] ? 'X' : ''}</td>
                        <td>${student.habilidades[8] ? 'X' : ''}</td>
                        <td>${comentario}</td>
                    </tr>
                `;
            });
            htmlContent += `
                        </table>
                        <br style="page-break-before: always;">
                        <h2>TURMA C</h2>
                        <table>
                            <tr>
                                <th>Nº</th>
                                <th class="student-name-col">Estudante</th>
                                <th class="skill-col">Ler</th>
                                <th class="skill-col">Cálc</th>
                                <th class="skill-col">Mult</th>
                                <th class="skill-col">Fig</th>
                                <th class="skill-col">Med</th>
                                <th class="skill-col">Comp</th>
                                <th class="skill-col">Def</th>
                                <th class="skill-col">Comp</th>
                                <th class="skill-col">Inf</th>
                                <th class="comment-col">Comentários</th>
                            </tr>
            `;
            currentTurmaData.turmaC.forEach(student => {
                 const comentarioKey = `comentario_turmaC_${student.numero}`;
                 const comentario = localStorage.getItem(comentarioKey) || '';
                htmlContent += `
                    <tr>
                        <td>${student.numero}</td>
                        <td>${student.nome}</td>
                        <td>${student.habilidades[0] ? 'X' : ''}</td>
                        <td>${student.habilidades[1] ? 'X' : ''}</td>
                        <td>${student.habilidades[2] ? 'X' : ''}</td>
                        <td>${student.habilidades[3] ? 'X' : ''}</td>
                        <td>${student.habilidades[4] ? 'X' : ''}</td>
                        <td>${student.habilidades[5] ? 'X' : ''}</td>
                        <td>${student.habilidades[6] ? 'X' : ''}</td>
                        <td>${student.habilidades[7] ? 'X' : ''}</td>
                        <td>${student.habilidades[8] ? 'X' : ''}</td>
                        <td>${comentario}</td>
                    </tr>
                `;
            });
            htmlContent += `
                        </table>
                    </div>
                </body>
                </html>
            `;
            const blob = new Blob([htmlContent], { type: 'application/msword' });
            saveAs(blob, 'relatorio_matematica_5ano.doc');
        }
        // Pesquisar aluno
        function searchStudent() {
            const searchTerm = document.getElementById('searchInput').value.toLowerCase();
            if (!searchTerm) return;
            document.querySelectorAll('.highlight').forEach(el => {
                el.classList.remove('highlight');
            });
            let found = false;
            document.querySelectorAll('.turma-table').forEach(table => {
                const rows = table.querySelectorAll('tbody tr');
                rows.forEach(row => {
                    const nameCell = row.querySelector('.student-name');
                    // Extrai apenas o nome, ignorando o botão
                    const nomeAluno = nameCell ? nameCell.textContent.replace('Comentário', '').trim() : '';
                    if (nomeAluno && nomeAluno.toLowerCase().includes(searchTerm)) {
                        nameCell.classList.add('highlight');
                        row.scrollIntoView({ behavior: 'smooth', block: 'center' });
                        found = true;
                        const turmaId = table.id;
                        if (turmaId !== activeTab) {
                            switchTab(turmaId);
                        }
                    }
                });
            });
            if (!found) {
                alert('Aluno não encontrado!');
            }
        }
        // Alternar entre abas
        function switchTab(tabId) {
            document.querySelectorAll('.tab').forEach(tab => {
                tab.classList.remove('active');
            });
            document.querySelector(`.tab[data-tab="${tabId}"]`).classList.add('active');
            document.querySelectorAll('.turma-table').forEach(table => {
                table.classList.add('hidden');
            });
            document.getElementById(tabId).classList.remove('hidden');
            activeTab = tabId;
        }
        // Restaurar dados originais
        function resetData() {
            if (confirm('Tem certeza que deseja restaurar os dados originais? Todas as suas alterações serão perdidas.')) {
                currentTurmaData.turmaB = JSON.parse(JSON.stringify(turmaBData));
                currentTurmaData.turmaC = JSON.parse(JSON.stringify(turmaCData));
                // Opcional: Limpar comentários também
                // Object.keys(localStorage).forEach(key => {
                //     if (key.startsWith('comentario_')) {
                //         localStorage.removeItem(key);
                //     }
                // });
                renderTable('turmaB');
                renderTable('turmaC');
                alert('Dados originais restaurados com sucesso!');
            }
        }

        // --- Funções para Comentários ---
        function abrirComentario(idAluno, nomeAluno) {
            alunoAtual = nomeAluno;
            idAlunoAtual = idAluno;
            document.getElementById('modalTitulo').innerHTML = 'Comentário para ' + nomeAluno;

            // Carregar comentário salvo (se existir)
            const comentarioSalvo = localStorage.getItem('comentario_' + idAluno);
            if (comentarioSalvo) {
                document.getElementById('textoComentario').value = comentarioSalvo;
            } else {
                document.getElementById('textoComentario').value = '';
            }

            document.getElementById('modalComentario').style.display = 'block';
        }

        function fecharModal() {
            document.getElementById('modalComentario').style.display = 'none';
        }

        function salvarComentario() {
            const comentario = document.getElementById('textoComentario').value;
            if (comentario.trim() !== '') {
                localStorage.setItem('comentario_' + idAlunoAtual, comentario);
                alert('Comentário salvo com sucesso!');
            } else {
                 // Se o campo estiver vazio, remove o comentário salvo
                localStorage.removeItem('comentario_' + idAlunoAtual);
            }
            fecharModal();
             // Re-renderiza a tabela para refletir possíveis mudanças (opcional, mas bom para UX)
             renderTable(activeTab);
        }

        // Fechar modal ao clicar fora dele
        window.onclick = function (event) {
            const modal = document.getElementById('modalComentario');
            if (event.target == modal) {
                modal.style.display = 'none';
            }
        }

        // Inicializar
        document.addEventListener('DOMContentLoaded', function () {
            loadData();
            document.getElementById('editToggle').addEventListener('click', toggleEditMode);
            document.getElementById('saveBtn').addEventListener('click', saveData);
            document.getElementById('exportExcel').addEventListener('click', exportToExcel);
            document.getElementById('exportPDF').addEventListener('click', exportToPDF);
            document.getElementById('exportWord').addEventListener('click', exportToWord);
            document.getElementById('searchBtn').addEventListener('click', searchStudent);
            document.getElementById('searchInput').addEventListener('keypress', function (e) {
                if (e.key === 'Enter') searchStudent();
            });
            document.getElementById('resetBtn').addEventListener('click', resetData);
            document.querySelectorAll('.tab').forEach(tab => {
                tab.addEventListener('click', function () {
                    const tabId = this.getAttribute('data-tab');
                    switchTab(tabId);
                });
            });
            document.addEventListener('blur', function (e) {
                if (e.target.classList.contains('student-name') && e.target.isContentEditable) {
                    const id = parseInt(e.target.dataset.id);
                    const turma = activeTab;
                    const student = currentTurmaData[turma].find(s => s.numero === id);
                    if (student) {
                        // Extrai apenas o nome, ignorando o botão
                        const nomeAtualizado = e.target.textContent.replace('Comentário', '').trim();
                        student.nome = nomeAtualizado;
                    }
                }
            }, true);
        });
    </script>
</body>
</html>
