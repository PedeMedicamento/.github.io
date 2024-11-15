<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de Dose de Medicamentos</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: url('https://zellosaude.app/wp-content/uploads/2021/03/medicamentos-2.jpg') no-repeat center center fixed;
            background-size: cover;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            position: relative;
        }

        .container {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            background: rgba(255, 255, 255, 0.8);
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
            width: 100%;
            max-width: 400px;
        }

        .title {
            font-size: 30px;
            font-weight: bold;
            text-transform: uppercase;
            color: black;
            margin-bottom: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .title img {
            height: 30px;
            margin-right: 10px;
        }

        .input-group {
            margin-bottom: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            width: 100%;
        }

        input[type="number"], input[type="text"], input[type="password"] {
            width: 50%;
            padding: 10px;
            font-size: 16px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

        .button {
            padding: 10px;
            background-color: green;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin-top: 20px;
        }

        .result-box {
            background-color: white;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            width: 100%;
            margin-top: 20px;
        }

        .button-container {
            margin-top: 10px;
            display: flex;
            justify-content: space-between;
            width: 100%;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.5);
            justify-content: center;
            align-items: center;
            z-index: 10000;
        }

        .modal-content {
            background-color: white;
            padding: 20px;
            border-radius: 5px;
            max-width: 400px;
            width: 80%;
            text-align: center;
        }

        .close {
            padding: 10px;
            background-color: red;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        .impressao {
            display: none;
            padding: 20px;
            border: 1px solid #ccc;
            width: 80%;
            margin: 0 auto;
            text-align: center;
        }

        .mensagem {
            font-size: 16px;
            color: #008000;
            margin-top: 10px;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1 class="title">
            <img src="https://seeklogo.com/images/M/medicina-logo-886CC8F59D-seeklogo.com.png" alt="Logo Medicina">
            Calculadora de Doses de Medicamentos
        </h1>

        <!-- Novo bloco para Doença -->
        <div class="input-group">
            <label for="doenca">Doença:</label>
            <select id="doenca">
                <option value="Febre">Febre</option>
                <option value="Dor de cabeça">Dor de cabeça</option>
                <option value="Inflamação nas vias respiratórias
">Inflamação nas vias respiratórias
</option>
                <option value="Otite média">Otite média</option>
                <option value="Pneumonia bacteriana">Pneumonia bacteriana</option>
                <option value="Dor abdominal">Dor abdominal</option>
		<option value="Rinite alérgica">Rinite alérgica</option>
		<option value="Dor abdominal">Dor abdominal</option>
		<option value="Conjuntivite alérgica">Conjuntivite alérgica</option>
		<option value="Asma">Asma</option>
		<option value="Bronquite obstrutiva">Bronquite obstrutiva</option>
		<option value="Desidratação">Desidratação</option>
		<option value="Limpeza nasal em resfriados">Limpeza nasal em resfriados</option>
		<option value="Urticária">Urticária</option>
		<option value="Infecção urinária">Infecção urinária</option>
		<option value="Infecção de pele">Infecção de pele</option>
		<option value="Náuseas">Náuseas</option>
		<option value="Vômitos pós-cirúrgicos">Vômitos pós-cirúrgicos</option>
                <option value="outros">Outros</option>
            </select>
        </div>

        <!-- Novo campo de seleção para Medicamento -->
        <div class="input-group">
            <label for="medicamento">Medicamento:</label>
            <select id="medicamento" onchange="atualizarDose()">
                <option value="outros">Outros</option>
                <option value="paracetamol">Paracetamol</option>
                <option value="ibuprofeno">Ibuprofeno</option>
                <option value="amoxicilina">Amoxicilina (antibiótico)</option>
                <option value="dipirona">Dipirona (antitérmico e analgésico)</option>
                <option value="clorfeniramina">Clorfeniramina (antialérgico)</option>
                <option value="salbutamol">Salbutamol (broncodilatador)</option>
                <option value="soro">Soro fisiológico (hidratação e limpeza nasal)</option>
                <option value="loratadina">Loratadina (antialérgico)</option>
                <option value="cefalexina">Cefalexina (antibiótico)</option>
                <option value="metoclopramida">Metoclopramida (antiemético)</option>
            </select>
        </div>

        <div class="input-group">
            <label for="peso">Peso (kg):</label>
            <input type="number" id="peso" placeholder="Digite o peso">
        </div>

        <div class="input-group">
            <label for="dose">Dose (mg/kg):</label>
            <input type="number" id="dose" placeholder="Digite a dose">
        </div>

        <div class="input-group">
            <label for="frequencia">Frequência (h):</label>
            <select id="frequencia">
                <option value="12">12h</option>
                <option value="8">8h</option>
                <option value="6">6h</option>
                <option value="4">4h</option>
                <option value="3">3h</option>
                <option value="2">2h</option>
                <option value="1">1h</option>
            </select>
        </div>

        <button class="button" onclick="calcularDose()">Calcular</button>

        <div class="result-box" id="resultado">
            <p id="doseResultado"></p>
            <p id="dosePorAplicacao"></p>
            <p id="doseDiaria"></p>
            <p id="doseMaxima"></p> <!-- Novo campo para Dose máxima -->
            <p id="mensagem"></p> <!-- Novo campo para a mensagem de "Qualquer idade" -->
        </div>

        <div class="button-container">
            <button class="button" onclick="showAviso()">Aviso</button>
            <button class="button" onclick="imprimirResultado()">Imprimir</button>
        </div>
    </div>

    <!-- Modal -->
    <div class="modal" id="modal">
        <div class="modal-content">
            <h3>Aviso</h3>
            <p>Por favor, insira os dados corretamente antes de calcular a dose.</p>
            <button class="close" onclick="closeModal()">Fechar</button>
        </div>
    </div>

    <div class="impressao" id="impressao">
        <h3>Resultado do Cálculo</h3>
        <p><strong>Dose por aplicação: </strong><span id="impressao-dose-aplicacao"></span></p>
        <p><strong>Dose diária total: </strong><span id="impressao-dose-diaria"></span></p>
        <p><strong>Dose máxima (60mg/kg): </strong><span id="impressao-dose-maxima"></span></p>
        <button class="button" onclick="window.print()">Imprimir</button>
    </div>

    <script>
        function atualizarDose() {
            var medicamento = document.getElementById("medicamento").value;
            var doseInput = document.getElementById("dose");
            var frequenciaInput = document.getElementById("frequencia");

            // Definir a dose e a frequência automaticamente com base no medicamento
            if (medicamento === 'outros') {
                doseInput.removeAttribute("readonly");
                frequenciaInput.removeAttribute("readonly");
                doseInput.value = '';
                frequenciaInput.value = '';
            } else {
                switch (medicamento) {
                    case 'paracetamol':
                        doseInput.value = 15;
                        frequenciaInput.value = "8";
                        break;
                    case 'ibuprofeno':
                        doseInput.value = 10;
                        frequenciaInput.value = "6";
                        break;
                    case 'amoxicilina':
                        doseInput.value = 25;
                        frequenciaInput.value = "8";
                        break;
                    case 'dipirona':
                        doseInput.value = 10;
                        frequenciaInput.value = "6";
                        break;
                    case 'clorfeniramina':
                        doseInput.value = 4;
                        frequenciaInput.value = "8";
                        break;
                    case 'salbutamol':
                        doseInput.value = 10;
                        frequenciaInput.value = "6";
                        break;
                    case 'soro':
                        doseInput.value = 100;
                        frequenciaInput.value = "Quando necessário";
                        break;
                    case 'loratadina':
                        doseInput.value = 10;
                        frequenciaInput.value = "1";
                        break;
                    case 'cefalexina':
                        doseInput.value = 25;
                        frequenciaInput.value = "12";
                        break;
                    case 'metoclopramida':
                        doseInput.value = 0.2;
                        frequenciaInput.value = "8";
                        break;
                    default:
                        doseInput.value = '';
                        frequenciaInput.value = '';
                        break;
                }

                doseInput.setAttribute("readonly", true);
                frequenciaInput.setAttribute("readonly", true);
            }
        }

        function calcularDose() {
            var peso = parseFloat(document.getElementById("peso").value);
            var dose = parseFloat(document.getElementById("dose").value);
            var frequencia = parseInt(document.getElementById("frequencia").value);

            if (frequencia === "Quando necessário") {
                frequencia = 1; // Quando necessário, considerar como 1 aplicação para facilitar o cálculo
            }

            var dosePorAplicacao = (dose * peso) / frequencia;
            var doseDiaria = dosePorAplicacao * frequencia; 
            var doseMaxima = 60 * peso;

            // Mostrar resultado
            document.getElementById("doseResultado").innerText = "Dose por aplicação: " + dosePorAplicacao.toFixed(2) + " mg";
            document.getElementById("dosePorAplicacao").innerText = "Dose diária total: " + doseDiaria.toFixed(2) + " mg";
            document.getElementById("doseMaxima").innerText = "Dose máxima: " + doseMaxima.toFixed(2) + " mg";

            // Verificar dose máxima
            if (dosePorAplicacao > doseMaxima) {
                document.getElementById("mensagem").innerText = "A dose por aplicação excede a dose máxima recomendada para este medicamento!";
            } else {
                document.getElementById("mensagem").innerText = "Dose recomendada dentro dos limites.";
            }
        }

        function showAviso() {
            var modal = document.getElementById("modal");
            modal.style.display = "flex";
        }

        function closeModal() {
            var modal = document.getElementById("modal");
            modal.style.display = "none";
        }

        function imprimirResultado() {
            var resultadoBox = document.getElementById("resultado");
            var impressaoBox = document.getElementById("impressao");

            impressaoBox.style.display = "block";

            document.getElementById("impressao-dose-aplicacao").innerText = document.getElementById("doseResultado").innerText;
            document.getElementById("impressao-dose-diaria").innerText = document.getElementById("dosePorAplicacao").innerText;
            document.getElementById("impressao-dose-maxima").innerText = document.getElementById("doseMaxima").innerText;
        }
    </script>


</body>
</html>
