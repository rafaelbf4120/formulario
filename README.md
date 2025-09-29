<index.html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lançamento de Corridas</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap');
body {
            font-family: 'Inter', sans-serif;
            background-color: #f3f4f6;
}
        .error-border {
            border-color: #ef4444 !important;
}
        /* Style for table rows to show pointer */
        tr {
            cursor: pointer;
}
        /* Make sure modals fit on smaller screens */
        .modal-content {
            width: 95%;
max-width: 48rem; /* Equivalent to max-w-2xl */
        }
        @media (min-width: 640px) {
            .modal-content {
                width: 100%;
}
        }
    </style>
</head>
<body class="bg-gray-100 flex items-center justify-center min-h-screen p-4">
    <div id="login-page" class="bg-white p-6 md:p-8 rounded-2xl shadow-xl w-full max-w-sm border border-gray-200">
        <h1 class="text-2xl md:text-3xl font-bold text-center text-gray-800 mb-6 md:mb-8">Login</h1>
        <form id="login-form" class="space-y-4">
            <div>
                <label for="username" class="block text-sm font-medium text-gray-700">Usuário:</label>
  
              <input type="text" id="username" name="username" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
            </div>
            <div>
                <label for="password" class="block text-sm font-medium text-gray-700">Senha:</label>
                <input type="password" id="password" name="password" class="mt-1 
block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
            </div>
            <button type="submit" class="w-full px-6 py-3 bg-blue-600 text-white font-bold rounded-lg shadow-lg hover:bg-blue-700 focus:outline-none focus:ring-4 focus:ring-blue-500 focus:ring-opacity-50 transition duration-150 ease-in-out">
                Entrar
            </button>
            <p id="login-message" class="text-red-500 text-sm 
text-center mt-2 hidden">Usuário ou senha inválidos.</p>
        </form>
    </div>

    <div id="app-page" class="bg-white p-6 md:p-8 rounded-2xl shadow-xl w-full max-w-full md:max-w-5xl border border-gray-200 hidden">
        <div class="flex justify-between items-center mb-6">
            <h1 class="text-2xl md:text-3xl font-bold text-gray-800">Lançamento de Corridas</h1>
            <button id="logout-btn" class="px-4 py-2 bg-gray-300 text-gray-800 font-medium rounded-lg hover:bg-gray-400">Sair</button>
        
</div>
        
        <p id="user-id-display" class="text-sm text-transparent text-center mb-4"></p>
        
        <form id="form-corrida" class="grid grid-cols-1 md:grid-cols-2 gap-4 md:gap-6 mb-6 md:mb-8">
            
            <div>
      
          <label for="motorista" class="block text-sm font-medium text-gray-700">Motorista:</label>
                <input type="text" id="motorista" name="motorista" list="motoristas-list" onfocus="this.classList.remove('error-border')" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
                <datalist id="motoristas-list">
                                 </datalist>
            </div>

            <div>
                <label for="solicitante" class="block text-sm font-medium text-gray-700">Solicitante:</label>
              
  <input type="text" id="solicitante" name="solicitante" onfocus="this.classList.remove('error-border')" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
            </div>
            
            <div id="passageiros-campos-container" class="md:col-span-2 grid grid-cols-1 md:grid-cols-2 gap-4 md:gap-6">
                <input type="hidden" id="matricula" name="matricula">
                <input type="hidden" id="transportado" name="transportado">
            </div>

            <div class="md:col-span-2">
                <button type="button" id="add-passageiro-btn" class="w-full px-4 py-2 bg-gray-200 text-gray-800 font-medium rounded-lg hover:bg-gray-300 transition duration-150 ease-in-out">
                    + Adicionar Outro Passageiro
                </button>
            </div>

            <div>
                <label for="data" class="block text-sm font-medium text-gray-700">Data:</label>
                <input type="date" 
id="data" name="data" onfocus="this.classList.remove('error-border')" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
            </div>

            <div>
                <label for="origem" class="block text-sm font-medium text-gray-700">Origem:</label>
                <input type="text" id="origem" name="origem" onfocus="this.classList.remove('error-border')" class="mt-1 
block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
            </div>

            <div>
                <label for="destino" class="block text-sm font-medium text-gray-700">Destino:</label>
                <input type="text" id="destino" name="destino" onfocus="this.classList.remove('error-border')" class="mt-1 block w-full px-3 py-2 
bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
            </div>
            
            <div>
                <label for="partida" class="block text-sm font-medium text-gray-700">Partida:</label>
                <input type="time" 
id="partida" name="partida" onfocus="this.classList.remove('error-border')" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
            </div>

            <div>
                <label for="chegada" class="block text-sm font-medium text-gray-700">Chegada:</label>
                <input type="time" id="chegada" name="chegada" onfocus="this.classList.remove('error-border')" class="mt-1 
block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
            </div>

            <div>
                <label for="valor" class="block text-sm font-medium text-gray-700">Valor:</label>
                <div class="relative mt-1">
        
            <span class="absolute inset-y-0 left-0 flex items-center pl-3 pr-2 text-gray-400">R$</span>
                    <input type="text" id="valor" name="valor" class="block w-full px-3 py-2 pl-9 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out text-right">
                </div>
            </div>

           
 <div>
                <label for="valor-extra" class="block text-sm font-medium text-gray-700">Valor Extra:</label>
                <div class="relative mt-1">
                    <span class="absolute inset-y-0 left-0 flex items-center pl-3 pr-2 text-gray-400">R$</span>
                
    <input type="text" id="valor-extra" name="valor-extra" class="block w-full px-3 py-2 pl-9 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out text-right">
                </div>
            </div>

            <div class="md:col-span-2">
                <label 
for="observacao" class="block text-sm font-medium text-gray-700">Observação:</label>
                <textarea id="observacao" name="observacao" rows="4" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out"></textarea>
            </div>
            
            <div class="md:col-span-2 flex flex-col md:flex-row justify-between 
gap-4 mt-4">
                <button type="submit" class="w-full md:w-1/2 px-6 py-3 bg-blue-600 text-white font-bold rounded-lg shadow-lg hover:bg-blue-700 focus:outline-none focus:ring-4 focus:ring-blue-500 focus:ring-opacity-50 transition duration-150 ease-in-out">
                    Salvar Lançamento
                </button>
            </div>
        </form>

        
<hr class="my-6 md:my-8 border-gray-300">
        
        <div class="flex flex-col gap-4 mb-6">
            <h2 class="text-xl font-bold text-gray-800">Gerar Relatório CSV</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <div>
                
    <label for="start-date" class="block text-sm font-medium text-gray-700">Data de Início:</label>
                    <input type="date" id="start-date" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
                </div>
                <div>
                  
  <label for="end-date" class="block text-sm font-medium text-gray-700">Data de Fim:</label>
                    <input type="date" id="end-date" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
                </div>
            </div>
            <button type="button" id="download-csv" class="w-full px-6 py-3 bg-green-600 text-white font-bold rounded-lg shadow-lg hover:bg-green-700 
focus:outline-none focus:ring-4 focus:ring-green-500 focus:ring-opacity-50 transition duration-150 ease-in-out">
                Baixar Relatório CSV
            </button>
        </div>

        <hr class="my-6 md:my-8 border-gray-300">

        <div class="flex flex-col md:flex-row justify-center gap-4">
            <button type="button" id="open-transportados-modal" class="px-6 py-3 bg-purple-600 
text-white font-bold rounded-lg shadow-lg hover:bg-purple-700 focus:outline-none focus:ring-4 focus:ring-purple-500 focus:ring-opacity-50 transition duration-150 ease-in-out">
                Gerenciar Transportados
            </button>
            <button type="button" id="open-motoristas-modal" class="px-6 py-3 bg-indigo-600 text-white font-bold rounded-lg shadow-lg hover:bg-indigo-700 focus:outline-none focus:ring-4 focus:ring-indigo-500 focus:ring-opacity-50 transition duration-150 ease-in-out">
                Gerenciar Motoristas
            </button>
  
      </div>
    </div>

    <div id="transportados-modal" class="fixed inset-0 bg-gray-600 bg-opacity-50 hidden flex items-center justify-center p-4">
        <div class="bg-white p-6 md:p-8 rounded-2xl shadow-2xl modal-content max-h-[90vh] overflow-y-auto">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-xl md:text-2xl font-bold text-gray-800">Gerenciar Transportados</h2>
               
 <button id="close-transportados-modal" class="text-gray-500 hover:text-gray-800 text-xl font-bold">&times;</button>
            </div>

            <div class="flex flex-col md:flex-row gap-4 items-start md:items-center mb-4 md:mb-6">
                <span class="text-sm font-medium text-gray-700">Ordenar por:</span>
                <select id="sort-transportados-key" class="w-full md:w-auto border border-gray-300 rounded-lg py-1 px-2 text-sm focus:outline-none 
focus:ring-2 focus:ring-blue-500">
                    <option value="nome">Nome</option>
                    <option value="matricula">Matrícula</option>
                </select>
                <select id="sort-transportados-order" class="w-full md:w-auto border border-gray-300 rounded-lg py-1 px-2 text-sm focus:outline-none focus:ring-2 focus:ring-blue-500">
             
       <option value="asc">A-Z</option>
                    <option value="desc">Z-A</option>
                </select>
            </div>
            
            <div class="grid 
grid-cols-1 md:grid-cols-3 gap-4 items-end mb-6">
                <div>
                    <label for="new-matricula" class="block text-sm font-medium text-gray-700">Nova Matrícula:</label>
                    <input type="text" id="new-matricula" class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500">
                </div>
   
             <div>
                    <label for="new-nome" class="block text-sm font-medium text-gray-700">Novo Transportado:</label>
                    <input type="text" id="new-nome" class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500">
                </div>
          
      <button type="button" id="add-transportado" class="px-6 py-2 bg-purple-600 text-white font-bold rounded-lg shadow-lg hover:bg-purple-700 focus:outline-none focus:ring-4 focus:ring-purple-500 focus:ring-opacity-50 transition duration-150 ease-in-out">
                    Adicionar
                </button>
            </div>

            <div class="overflow-x-auto 
rounded-lg shadow-md border border-gray-200">
                <table class="min-w-full table-auto" id="transportados-table">
                    <thead class="bg-gray-50">
                        <tr>
                            <th scope="col" class="p-4 text-left text-xs 
font-medium text-gray-500 uppercase tracking-wider">
                                <input type="checkbox" id="selectAllTransportados" class="rounded-sm">
                            </th>
                            <th scope="col" class="px-6 py-3 text-left text-xs 
font-medium text-gray-500 uppercase tracking-wider w-1/4">Matrícula</th>
                            <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider w-3/4">Nome</th>
                        </tr>
                    </thead>
              
      <tbody class="bg-white divide-y divide-gray-200">
                        </tbody>
                </table>
            </div>
          
  <div class="flex justify-end mt-4">
                <button type="button" id="delete-selected-transportados" class="px-4 py-2 bg-red-600 text-white font-bold rounded-lg shadow-lg hover:bg-red-700">
                    Excluir Selecionados
                </button>
            </div>
        </div>
    </div>

    <div id="motoristas-modal" class="fixed inset-0 bg-gray-600 bg-opacity-50 hidden flex items-center justify-center p-4">
        <div class="bg-white p-6 md:p-8 rounded-2xl shadow-2xl modal-content max-h-[90vh] overflow-y-auto">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-xl md:text-2xl font-bold text-gray-800">Gerenciar Motoristas</h2>
                <button id="close-motoristas-modal" class="text-gray-500 hover:text-gray-800 text-xl font-bold">&times;</button>
            
</div>
            
            <div class="flex flex-col md:flex-row gap-4 items-start md:items-center mb-4 md:mb-6">
                <span class="text-sm font-medium text-gray-700">Ordenar por:</span>
                <select id="sort-motoristas-order" class="w-full md:w-auto border border-gray-300 rounded-lg py-1 px-2 text-sm focus:outline-none focus:ring-2 focus:ring-blue-500">
     
               <option value="asc">A-Z</option>
                    <option value="desc">Z-A</option>
                </select>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 items-end 
mb-6">
                <div>
                    <label for="new-motorista-nome" class="block text-sm font-medium text-gray-700">Novo Motorista:</label>
                    <input type="text" id="new-motorista-nome" class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500">
                </div>
       
         <button type="button" id="add-motorista" class="px-6 py-2 bg-indigo-600 text-white font-bold rounded-lg shadow-lg hover:bg-indigo-700 focus:outline-none focus:ring-4 focus:ring-indigo-500 focus:ring-opacity-50 transition duration-150 ease-in-out">
                    Adicionar
                </button>
            </div>

             <div class="overflow-x-auto rounded-lg shadow-md border border-gray-200">
                <table class="min-w-full table-auto" id="motoristas-table">
                    <thead class="bg-gray-50">
                        <tr>
                            <th scope="col" 
class="p-4 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                                <input type="checkbox" id="selectAllMotoristas" class="rounded-sm">
                            </th>
                            <th scope="col" class="px-6 
py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider w-full">Nome</th>
                        </tr>
                    </thead>
                    <tbody class="bg-white divide-y divide-gray-200">
                        </tbody>
                </table>
            </div>
            <div class="flex justify-end mt-4">
                <button type="button" id="delete-selected-motoristas" class="px-4 py-2 bg-red-600 text-white font-bold rounded-lg shadow-lg hover:bg-red-700">
    
                Excluir Selecionados
                </button>
            </div>
        </div>
    </div>

    <div id="message-modal" class="fixed inset-0 bg-gray-600 bg-opacity-50 hidden flex items-center justify-center">
        <div class="bg-white p-6 rounded-lg shadow-2xl max-w-sm w-full">
    
        <h2 class="text-xl font-bold mb-4">Aviso</h2>
            <p id="message-content" class="text-gray-700 mb-4"></p>
            <div class="flex justify-end">
                <button id="close-modal" class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700">OK</button>
            </div>
        </div>
    </div>

    <script type="module">
        
import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
import { getFirestore, addDoc, deleteDoc, onSnapshot, collection, doc, query, where, getDocs, setLogLevel } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";
// Firebase Config - Substitua com a sua própria configuração
        const firebaseConfig = {
            apiKey: "AIzaSyDmqvcKtIsga4ZQWNDg4_2k493dqMQCDVg",
            authDomain: "teste-ebf38.firebaseapp.com",
            projectId: "teste-ebf38",
            storageBucket: "teste-ebf38.firebasestorage.app",
            messagingSenderId: "741884776297",
            appId: "1:741884776297:web:a23450b4909581a1b237f8",
  
          measurementId: "G-2MD5CFD51E"
        };
// Inicializa o Firebase
        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);
const auth = getAuth(app);
        setLogLevel('debug');

        const globalAppId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
        let globalUserId = null;
// Elementos do DOM
        const loginForm = document.getElementById('login-form');
        const loginPage = document.getElementById('login-page');
const appPage = document.getElementById('app-page');
        const loginMessage = document.getElementById('login-message');
        const userIdDisplay = document.getElementById('user-id-display');
        const logoutButton = document.getElementById('logout-btn');

        // Campos do formulário original (mantidos por compatibilidade com CSV/Backend)
        const matriculaInputHidden = document.getElementById('matricula'); 
        const transportadoInputHidden = document.getElementById('transportado');

        // Novos elementos para múltiplos passageiros
        const passageirosContainer = document.getElementById('passageiros-campos-container');
        const addPassageiroBtn = document.getElementById('add-passageiro-btn');

        const valorInput = document.getElementById('valor');
        const valorExtraInput = document.getElementById('valor-extra');
// Lista de usuários e senhas (pode ser expandida)
        const users = [
            { username: 'admin', password: 'rafael22' },
            { username: 'gerente', password: 'senha123' }
        ];
let transportadosData = [];
        let motoristasData = [];
        
        // Mapeamentos para preenchimento automático
let matriculaToNome = {};
        let nomeToMatricula = {};
        
        // Contador para campos dinâmicos de passageiros
        let passageiroCount = 0;

        // Função para criar os campos de Matrícula e Nome
        function createPassageiroInput(index, isRequired = true) {
            const fieldset = document.createElement('div');
            fieldset.className = 'passageiro-row grid grid-cols-1 md:grid-cols-2 gap-4 md:gap-6';
            fieldset.id = `passageiro-row-${index}`;
            fieldset.innerHTML = `
                <div>
                    <label for="matricula-${index}" class="block text-sm font-medium text-gray-700">Matrícula (P${index + 1}):</label>
                    <input type="text" id="matricula-${index}" name="matriculas[]" list="transportados-matricula-list"
                        onfocus="this.classList.remove('error-border')" data-index="${index}" data-type="matricula"
                        class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
                </div>

                <div class="flex items-end">
                    <div class="flex-grow">
                        <label for="transportado-${index}" class="block text-sm font-medium text-gray-700">Transportado (P${index + 1}):</label>
                        <input type="text" id="transportado-${index}" name="transportados[]" list="transportados-nome-list"
                            onfocus="this.classList.remove('error-border')" data-index="${index}" data-type="nome"
                            class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
                    </div>
                    ${!isRequired ? `<button type="button" class="ml-2 px-3 py-2 bg-red-500 text-white font-bold rounded-lg shadow-md hover:bg-red-600 remove-passageiro-btn" data-index="${index}">-</button>` : ''}
                </div>
            `;
            
            // Adicionar listeners para o preenchimento automático no blur
            const matriculaInput = fieldset.querySelector(`#matricula-${index}`);
            const nomeInput = fieldset.querySelector(`#transportado-${index}`);
            
            matriculaInput.addEventListener('blur', () => handleAutofillDynamic(matriculaInput, nomeInput, 'matricula'));
            nomeInput.addEventListener('blur', () => handleAutofillDynamic(nomeInput, matriculaInput, 'nome'));
            
            return fieldset;
        }

        function handleAutofillDynamic(sourceInput, targetInput, sourceType) {
            const value = sourceInput.value.trim();
            if (value === '') return;
            
            let targetValue = '';
            
            if (sourceType === 'matricula') {
                targetValue = matriculaToNome[value];
            } else if (sourceType === 'nome') {
                targetValue = nomeToMatricula[value.toLowerCase()];
            }
            
            if (targetValue) {
                targetInput.value = targetValue;
                targetInput.classList.remove('error-border');
            } else {
                targetInput.value = '';
                // Não mostra aviso para não ser invasivo durante a digitação
            }
        }
        
        function addPassageiroRow(isRequired = false) {
            const newRow = createPassageiroInput(passageiroCount, isRequired);
            passageirosContainer.appendChild(newRow);
            
            if (!isRequired) {
                newRow.querySelector('.remove-passageiro-btn').addEventListener('click', function() {
                    newRow.remove();
                    // Garante que o contador não volte, apenas que os índices fiquem corretos no POST
                });
            }
            passageiroCount++;
        }

        // Adiciona os event listeners após o carregamento da página
        window.onload = () => {
             // Inicializa o primeiro passageiro (obrigatório)
             addPassageiroRow(true);

             // Evento para adicionar mais passageiros
             addPassageiroBtn.addEventListener('click', () => addPassageiroRow(false));

             // Vincula os eventos blur (ao sair do campo) para a lógica de preenchimento automático
            
            // Adiciona event listeners para os campos de valores
            valorInput.addEventListener('input', () => formatCurrencyInput(valorInput));
valorExtraInput.addEventListener('input', () => formatCurrencyInput(valorExtraInput));

            valorInput.addEventListener('focus', () => { if (valorInput.value === '0,00') valorInput.value = ''; });
valorExtraInput.addEventListener('focus', () => { if (valorExtraInput.value === '0,00') valorExtraInput.value = ''; });
valorInput.addEventListener('blur', () => { if (valorInput.value === '') valorInput.value = '0,00'; });
valorExtraInput.addEventListener('blur', () => { if (valorExtraInput.value === '') valorExtraInput.value = '0,00'; });
onAuthStateChanged(auth, async (user) => {
                if (user) {
                    globalUserId = user.uid;
                    userIdDisplay.innerText = `ID do Usuário: ${globalUserId}`;
                    // Sincroniza os dados do Firestore
      
              startFirestoreListeners();
                } else {
                    // Oculta a página principal se o usuário não estiver autenticado
                    loginPage.classList.remove('hidden');
                  
  appPage.classList.add('hidden');
                }
            });
// O login anônimo é para acesso ao Firestore, independente do seu formulário
            signInAnonymously(auth).catch((error) => {
                console.error("Erro ao fazer login anônimo:", error);
            });
};

        // Autenticação de Login
        loginForm.addEventListener('submit', function(event) {
            event.preventDefault();
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;

            const foundUser = users.find(user => user.username === username && user.password === password);

            if (foundUser) {
       
         loginPage.classList.add('hidden');
                appPage.classList.remove('hidden');
            } else {
                loginMessage.classList.remove('hidden');
            }
        });
logoutButton.addEventListener('click', () => {
            signOut(auth);
        });
// Listeners do Firestore para dados em tempo real
        function startFirestoreListeners() {
            // Listener para Transportados
            const transportadosRef = collection(db, 'artifacts', globalAppId, 'public', 'data', 'transportados');
onSnapshot(transportadosRef, (snapshot) => {
                transportadosData = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
                rebuildTransportadosLookups();
            });
// Listener para Motoristas
            const motoristasRef = collection(db, 'artifacts', globalAppId, 'public', 'data', 'motoristas');
onSnapshot(motoristasRef, (snapshot) => {
                motoristasData = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
                rebuildMotoristasLookups();
            });
}
        
        function rebuildTransportadosLookups(sortKey = 'nome', sortOrder = 'asc') {
            transportadosData.sort((a, b) => {
                let valA = a[sortKey];
                let valB = b[sortKey];

                if (sortOrder === 'asc') {
    
                return valA.localeCompare(valB, undefined, { numeric: true });
                } else {
                    return valB.localeCompare(valA, undefined, { numeric: true });
                }
            });
matriculaToNome = {};
            nomeToMatricula = {};
            transportadosData.forEach(item => {
                matriculaToNome[item.matricula] = item.nome;
                nomeToMatricula[item.nome.toLowerCase()] = item.matricula;
            });
renderTransportadosList();
        }

        function rebuildMotoristasLookups(sortOrder = 'asc') {
            motoristasData.sort((a, b) => {
                if (sortOrder === 'asc') {
                    return a.nome.localeCompare(b.nome);
                } else {
             
       return b.nome.localeCompare(a.nome);
                }
            });
renderMotoristasList();
            populateMotoristasDatalist();
        }

        // Funções para gerenciar o modal de aviso
        function showWarning(message) {
            document.getElementById('message-content').innerText = message;
document.getElementById('message-modal').classList.remove('hidden');
        }

        function hideWarning() {
            document.getElementById('message-modal').classList.add('hidden');
}
        
        // Funções para manipulação de dados e CSV
        function exportAllToCsv(dataArray) {
            if (dataArray.length === 0) {
                showWarning('Não há dados para exportar.');
return;
            }
            
            const bom = '\uFEFF';
const headers = Object.keys(dataArray[0]).map(key => key.replace(/([A-Z])/g, ' $1').replace(/^./, (str) => str.toUpperCase()));
const rows = dataArray.map(obj => headers.map(header => {
                const key = header.replace(/\s/g, '').replace(/^./, (str) => str.toLowerCase());
                let value = obj[key] || '';
                if (key === 'valor' || key === 'valorExtra') {
                    value = `R$ ${value.toFixed(2).replace('.', ',')}`;
 
               }
                return `"${value.toString().replace(/"/g, '""')}"`;
            }).join(';'));
            const csvContent = `${headers.join(';')}\n${rows.join('\n')}`;
            const blob = new Blob([bom + csvContent], { type: 'text/csv;charset=utf-8;' });
            const url = URL.createObjectURL(blob);
   
         const link = document.createElement('a');
            link.setAttribute('href', url);
            const now = new Date();
            const dateString = `${now.getFullYear()}-${(now.getMonth() + 1).toString().padStart(2, '0')}-${now.getDate().toString().padStart(2, '0')}_${now.getHours().toString().padStart(2, '0')}-${now.getMinutes().toString().padStart(2, '0')}-${now.getSeconds().toString().padStart(2, '0')}`;
link.setAttribute('download', `lancamentos_de_corridas_${dateString}.csv`);
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            showWarning('Relatório CSV baixado com sucesso!');
}

        // Funções de renderização de listas
        function renderTransportadosList() {
            const tableBody = document.querySelector('#transportados-table tbody');
tableBody.innerHTML = '';
            transportadosData.forEach((item, index) => {
                const row = document.createElement('tr');
                row.className = 'bg-white hover:bg-gray-50 transition-colors duration-100';
                row.dataset.id = item.id;
                row.innerHTML = `
                  
  <td class="p-4"><input type="checkbox" data-id="${item.id}" class="transportado-checkbox rounded-sm"></td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${item.matricula}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${item.nome}</td>
                `;
                tableBody.appendChild(row);
           
 });
            populateTransportadosDatalist();
        }
        
        function renderMotoristasList() {
            const tableBody = document.querySelector('#motoristas-table tbody');
tableBody.innerHTML = '';
            motoristasData.forEach((item, index) => {
                const row = document.createElement('tr');
                row.className = 'bg-white hover:bg-gray-50 transition-colors duration-100';
                row.dataset.id = item.id;
                row.innerHTML = `
                  
  <td class="p-4"><input type="checkbox" data-id="${item.id}" class="motorista-checkbox rounded-sm"></td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${item.nome}</td>
                `;
                tableBody.appendChild(row);
            });
populateMotoristasDatalist();
        }

        function populateTransportadosDatalist() {
            // O datalist existe apenas uma vez no HTML
            const matriculaDatalist = document.querySelector('#transportados-matricula-list') || document.createElement('datalist');
            matriculaDatalist.id = 'transportados-matricula-list';
            if (!document.querySelector('#transportados-matricula-list')) {
                document.body.appendChild(matriculaDatalist); // Adiciona se não existir
            }

            const nomeDatalist = document.querySelector('#transportados-nome-list') || document.createElement('datalist');
            nomeDatalist.id = 'transportados-nome-list';
            if (!document.querySelector('#transportados-nome-list')) {
                document.body.appendChild(nomeDatalist); // Adiciona se não existir
            }
            
            matriculaDatalist.innerHTML = '';
            nomeDatalist.innerHTML = '';
transportadosData.forEach(item => {
                const matriculaOption = document.createElement('option');
                matriculaOption.value = item.matricula;
                matriculaDatalist.appendChild(matriculaOption);
                
                const nomeOption = document.createElement('option');
          
      nomeOption.value = item.nome;
                nomeDatalist.appendChild(nomeOption);
            });
}

        function populateMotoristasDatalist() {
            const motoristaDatalist = document.getElementById('motoristas-list');
motoristaDatalist.innerHTML = '';
            motoristasData.forEach(item => {
                const option = document.createElement('option');
                option.value = item.nome;
                motoristaDatalist.appendChild(option);
            });
}

        // Funções de gerenciamento de dados
        document.getElementById('add-transportado').addEventListener('click', async function() {
            const newMatriculaInput = document.getElementById('new-matricula');
            const newNomeInput = document.getElementById('new-nome');
            const newMatricula = newMatriculaInput.value.trim();
            const newNome = newNomeInput.value.trim();

            if (newMatricula && newNome) 
{
                const existing = transportadosData.find(item => item.matricula === newMatricula || item.nome.toLowerCase() === newNome.toLowerCase());
                if (existing) {
                    showWarning('A matrícula ou o nome já existe.');
                } else {
           
         const transportadosRef = collection(db, 'artifacts', globalAppId, 'public', 'data', 'transportados');
                    await addDoc(transportadosRef, { matricula: newMatricula, nome: newNome });
                    newMatriculaInput.value = '';
newNomeInput.value = '';
                    showWarning('Transportado adicionado com sucesso!');
                }
            } else {
                showWarning('Por favor, preencha a matrícula e o nome.');
}
        });

        document.getElementById('delete-selected-transportados').addEventListener('click', async function() {
            const checkboxes = document.querySelectorAll('#transportados-table .transportado-checkbox:checked');
            if (checkboxes.length === 0) {
                showWarning('Selecione pelo menos um transportado para excluir.');
                return;
            }
      
      const promises = Array.from(checkboxes).map(cb => {
                const transportadoDocRef = doc(db, 'artifacts', globalAppId, 'public', 'data', 'transportados', cb.dataset.id);
                return deleteDoc(transportadoDocRef);
            });
            await Promise.all(promises);
            showWarning(`${checkboxes.length} transportados excluídos com sucesso!`);
      
  });

        document.getElementById('add-motorista').addEventListener('click', async function() {
            const newNomeInput = document.getElementById('new-motorista-nome');
            const newNome = newNomeInput.value.trim();

            if (newNome) {
                const existing = motoristasData.find(item => item.nome.toLowerCase() === newNome.toLowerCase());
                if (existing) {
         
           showWarning('O nome do motorista já existe.');
                } else {
                    const motoristasRef = collection(db, 'artifacts', globalAppId, 'public', 'data', 'motoristas');
                    await addDoc(motoristasRef, { nome: newNome });
             
       newNomeInput.value = '';
                    showWarning('Motorista adicionado com sucesso!');
                }
            } else {
                showWarning('Por favor, preencha o nome do motorista.');
            }
    
    });

        document.getElementById('delete-selected-motoristas').addEventListener('click', async function() {
            const checkboxes = document.querySelectorAll('#motoristas-table .motorista-checkbox:checked');
            if (checkboxes.length === 0) {
                showWarning('Selecione pelo menos um motorista para excluir.');
                return;
            }
          
  const promises = Array.from(checkboxes).map(cb => {
                const motoristaDocRef = doc(db, 'artifacts', globalAppId, 'public', 'data', 'motoristas', cb.dataset.id);
                return deleteDoc(motoristaDocRef);
            });
            await Promise.all(promises);
            showWarning(`${checkboxes.length} motoristas excluídos com sucesso!`);
        });
// Funções de formatação de moeda
        function formatCurrencyInput(input) {
            let value = input.value.replace(/\D/g, '');
// Remove todos os caracteres não numéricos
            if (value === '') {
                return;
}
            
            value = value.padStart(3, '0');
// Garante pelo menos 3 dígitos (ex: '1' vira '001')
            
            const integerPart = value.slice(0, -2);
const decimalPart = value.slice(-2);
            
            const formattedInteger = parseInt(integerPart, 10).toLocaleString('pt-BR');
            input.value = `${formattedInteger},${decimalPart}`;
}
        
        // Conversor de valor formatado para número puro
        function parseCurrencyValue(value) {
            return parseFloat(value.replace(/\./g, '').replace(',', '.'));
}

        // Evento de envio do formulário
        document.getElementById('form-corrida').addEventListener('submit', async function(event) {
            event.preventDefault();

            const form = event.target;
            const requiredFields = [
                'motorista', 'solicitante', 'data',
  'origem', 'partida', 'destino', 'chegada',
                'valor'
            ];
            
            // Coleta de dados dos campos dinâmicos de passageiros
            const matriculasInputs = document.querySelectorAll('#passageiros-campos-container input[name="matriculas[]"]');
            const transportadosInputs = document.querySelectorAll('#passageiros-campos-container input[name="transportados[]"]');

            const passageirosData = [];
            let isFormValid = true;
            let hasPrimaryPassageiro = false;

            // 1. Validação dos campos únicos obrigatórios
            for (const field of requiredFields) {
                const input = form[field];
                
if (input.value.trim() === '') {
                    isFormValid = false;
                    input.classList.add('error-border');
                } else {
                    input.classList.remove('error-border');
                
}
            }
            
            // 2. Coleta e validação dos passageiros (o primeiro é obrigatório)
            for (let i = 0; i < matriculasInputs.length; i++) {
                const matriculaInput = matriculasInputs[i];
                const nomeInput = transportadosInputs[i];

                const matricula = matriculaInput.value.trim();
                const nome = nomeInput.value.trim();
                
                // Limpa bordas de erro a cada submissão
                matriculaInput.classList.remove('error-border');
                nomeInput.classList.remove('error-border');
                
                // Se o par tiver dados preenchidos
                if (matricula !== '' && nome !== '') {
                    passageirosData.push({ matricula: matricula, nome: nome });
                    if (i === 0) {
                        hasPrimaryPassageiro = true;
                    }
                } 
                // Se apenas um dos campos estiver preenchido (erro)
                else if (matricula !== '' || nome !== '') {
                    isFormValid = false;
                    if (matricula === '') matriculaInput.classList.add('error-border');
                    if (nome === '') nomeInput.classList.add('error-border');
                }
            }
            
            // Valida se o primeiro passageiro (que preenche os campos do CSV) está preenchido
            if (!passageirosData[0]) {
                isFormValid = false;
                // Adiciona a borda de erro nos campos do primeiro passageiro se estiverem vazios
                if (matriculasInputs[0]) matriculasInputs[0].classList.add('error-border');
                if (transportadosInputs[0]) transportadosInputs[0].classList.add('error-border');
            }


            if (!isFormValid) {
                showWarning('Por favor, preencha todos os campos obrigatórios e verifique os dados dos passageiros (Matrícula e Nome são obrigatórios para cada passageiro).');
                return;
            }

            // Preenche os campos hidden com o primeiro passageiro para compatibilidade com o backend/CSV
            matriculaInputHidden.value = passageirosData[0].matricula;
            transportadoInputHidden.value = passageirosData[0].nome;

            // Cria o campo de passageiros extras (se houver mais de um)
            const passageirosExtras = passageirosData.length > 1 ? passageirosData.slice(1) : null;

            const newEntry = {
         
       motorista: form['motorista'].value,
                matricula: form['matricula'].value, // Primeiro passageiro (para compatibilidade CSV)
                transportado: form['transportado'].value, // Primeiro passageiro (para compatibilidade CSV)
                passageiros_extras: passageirosExtras, // Novo campo para passageiros adicionais
                solicitante: form['solicitante'].value,
                data: form['data'].value,
                origem: form['origem'].value,
       
         partida: form['partida'].value,
                destino: form['destino'].value,
                chegada: form['chegada'].value,
                valor: parseCurrencyValue(form['valor'].value),
                valorExtra: form['valor-extra'].value ?
parseCurrencyValue(form['valor-extra'].value) : null,
                observacao: form['observacao'].value
            };
const lancamentosRef = collection(db, 'artifacts', globalAppId, 'public', 'data', 'lancamentos');
            await addDoc(lancamentosRef, newEntry);

            showWarning('Lançamento salvo com sucesso!');
            form.reset();
            document.getElementById('valor').value = '0,00';
document.getElementById('valor-extra').value = '0,00';
            
            // Limpa e reinicializa os campos de passageiros
            passageirosContainer.innerHTML = '';
            passageiroCount = 0;
            addPassageiroRow(true); // Adiciona o primeiro de volta
        });

        // Evento de navegação com a tecla "Enter"
        const inputs = document.querySelectorAll('#form-corrida input:not([readonly]), #form-corrida textarea');
inputs.forEach(input => {
            input.addEventListener('keydown', function(event) {
                if (event.key === 'Enter') {
                    event.preventDefault();

                    const currentInputIndex = Array.from(inputs).indexOf(this);
                    let 
nextInput = null;

                    for (let i = currentInputIndex + 1; i < inputs.length; i++) {
                        if (inputs[i].value.trim() === '') {
                            nextInput = inputs[i];
         
                   break;
                        }
                    }

                    if (!nextInput) {
               
         for (let i = 0; i < inputs.length; i++) {
                             if (inputs[i].value.trim() === '') {
                                 nextInput = inputs[i];
              
                   break;
                             }
                        }
                    }

        
            if (nextInput) {
                        nextInput.focus();
}
                }
            });
});

        // Evento do botão de download
document.getElementById('download-csv').addEventListener('click', async function() {
    const startDate = document.getElementById('start-date').value;
    const endDate = document.getElementById('end-date').value;

    if (startDate && endDate && new Date(startDate) > new Date(endDate)) {
        showWarning('A data de início não pode ser posterior à data de fim.');
        return;
    }

    const lancamentosRef = collection(db, 'artifacts', globalAppId, 'public', 'data', 'lancamentos');

    // Monta filtros
    let filtros = [];
    if (startDate) filtros.push(where('data', 
'>=', startDate));
    if (endDate) filtros.push(where('data', '<=', endDate));

    // Monta query final
    let q = filtros.length > 0 ? query(lancamentosRef, ...filtros) : lancamentosRef;

    // Busca os dados
    try {
        const snapshot = await getDocs(q);
        const allData = snapshot.docs.map(doc => doc.data());

        console.log("Dados recebidos do Firestore:", allData);
// <-- pra debug

        if (allData.length === 0) {
            showWarning('Nenhum dado encontrado para este período.');
return;
        }

        // Gerar CSV normalmente
        const bom = '\uFEFF';
        
        // Ajusta cabeçalhos para incluir dados de passageiros extras de forma simples (se houver)
        let allHeaders = new Set();
        allData.forEach(obj => {
            Object.keys(obj).forEach(key => allHeaders.add(key));
        });
        
        // Remove passageiros_extras temporariamente para reprocessamento
        allHeaders.delete('passageiros_extras'); 

        let finalHeaders = Array.from(allHeaders);
        
        // Se houver passageiros extras, adiciona colunas dinâmicas para eles
        let maxPassageirosExtras = 0;
        allData.forEach(obj => {
            if (obj.passageiros_extras && Array.isArray(obj.passageiros_extras)) {
                maxPassageirosExtras = Math.max(maxPassageirosExtras, obj.passageiros_extras.length);
            }
        });

        for (let i = 0; i < maxPassageirosExtras; i++) {
            finalHeaders.push(`matricula_extra_${i+1}`);
            finalHeaders.push(`transportado_extra_${i+1}`);
        }
        
        // Coloca a observação por último
        const obsIndex = finalHeaders.indexOf('observacao');
        if (obsIndex > -1) {
            finalHeaders.splice(obsIndex, 1);
            finalHeaders.push('observacao');
        }

const headers = finalHeaders;
        const rows = allData.map(obj => headers.map(key => {
            let value = obj[key] ?? '';
            
            // Trata as colunas de passageiros extras
            if (key.startsWith('matricula_extra_') || key.startsWith('transportado_extra_')) {
                const parts = key.split('_');
                const index = parseInt(parts[2]) - 1; // index 0, 1, 2...
                const type = parts[0]; // matricula ou transportado
                
                if (obj.passageiros_extras && obj.passageiros_extras[index]) {
                    value = obj.passageiros_extras[index][type];
                } else {
                    value = '';
                }
            }

            if (key === 'valor' || key === 'valorExtra') {
                value = `R$ ${parseFloat(value).toFixed(2).replace('.', ',')}`;
            }
            return `"${value.toString().replace(/"/g, '""')}"`;
      
  }).join(';'));

        const csvContent = `${headers.join(';')}\n${rows.join('\n')}`;
        const blob = new Blob([bom + csvContent], { type: 'text/csv;charset=utf-8;' });
        const url = URL.createObjectURL(blob);
        const link = document.createElement('a');
        link.href = url;

        const now = new Date();
        const dateString = `${now.getFullYear()}-${(now.getMonth() + 1).toString().padStart(2, '0')}-${now.getDate().toString().padStart(2, '0')}_${now.getHours().toString().padStart(2, '0')}-${now.getMinutes().toString().padStart(2, '0')}-${now.getSeconds().toString().padStart(2, '0')}`;
       
 link.download = `lancamentos_de_corridas_${dateString}.csv`;

        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);

        showWarning('Relatório CSV baixado com sucesso!');
} catch (err) {
        console.error("Erro ao buscar dados:", err);
showWarning('Erro ao gerar relatório. Veja o console para mais detalhes.');
    }
});
// Evento para fechar o modal de aviso
        document.getElementById('close-modal').addEventListener('click', function() {
            hideWarning();
        });
// Eventos para abrir e fechar os modais
        document.getElementById('open-transportados-modal').addEventListener('click', function() {
            document.getElementById('transportados-modal').classList.remove('hidden');
        });
document.getElementById('close-transportados-modal').addEventListener('click', function() {
            document.getElementById('transportados-modal').classList.add('hidden');
            document.getElementById('selectAllTransportados').checked = false;
            document.querySelectorAll('.transportado-checkbox').forEach(cb => cb.checked = false);
        });
document.getElementById('open-motoristas-modal').addEventListener('click', function() {
            document.getElementById('motoristas-modal').classList.remove('hidden');
        });
document.getElementById('close-motoristas-modal').addEventListener('click', function() {
            document.getElementById('motoristas-modal').classList.add('hidden');
            document.getElementById('selectAllMotoristas').checked = false;
            document.querySelectorAll('.motorista-checkbox').forEach(cb => cb.checked = false);
        });
// Eventos para alteração de ordenação
        document.getElementById('sort-transportados-key').addEventListener('change', function() {
            const sortKey = this.value;
            const sortOrder = document.getElementById('sort-transportados-order').value;
            rebuildTransportadosLookups(sortKey, sortOrder);
        });
document.getElementById('sort-transportados-order').addEventListener('change', function() {
            const sortKey = document.getElementById('sort-transportados-key').value;
            const sortOrder = this.value;
            rebuildTransportadosLookups(sortKey, sortOrder);
        });
document.getElementById('sort-motoristas-order').addEventListener('change', function() {
            const sortOrder = this.value;
            rebuildMotoristasLookups(sortOrder);
        });
// Adiciona event listeners para os checkboxes de seleção
        document.getElementById('transportados-table').addEventListener('change', function(event) {
            if (event.target.id === 'selectAllTransportados') {
                const checkboxes = document.querySelectorAll('.transportado-checkbox');
                checkboxes.forEach(checkbox => checkbox.checked = event.target.checked);
            }
        });
document.getElementById('motoristas-table').addEventListener('change', function(event) {
            if (event.target.id === 'selectAllMotoristas') {
                const checkboxes = document.querySelectorAll('.motorista-checkbox');
                checkboxes.forEach(checkbox => checkbox.checked = event.target.checked);
            }
        });
// Evento para selecionar a linha clicando em qualquer lugar da tabela
        document.getElementById('transportados-table').addEventListener('click', function(event) {
            const row = event.target.closest('tr');
            if (row) {
                const checkbox = row.querySelector('.transportado-checkbox');
                if (checkbox && event.target !== checkbox) {
         
           checkbox.checked = !checkbox.checked;
                }
            }
        });
document.getElementById('motoristas-table').addEventListener('click', function(event) {
            const row = event.target.closest('tr');
            if (row) {
                const checkbox = row.querySelector('.motorista-checkbox');
                if (checkbox && event.target !== checkbox) {
                    checkbox.checked = !checkbox.checked;
      
          }
            }
        });
</script>
</body>
</html>
