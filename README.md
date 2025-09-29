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
block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
            </div>
            <button type="submit" class="w-full px-6 py-3 bg-blue-600 text-white font-bold rounded-lg shadow-lg hover:bg-blue-700 focus:outline-none focus:ring-4 focus:ring-blue-500 focus:ring-opacity-50 transition duration-150 ease-in-out">
                Entrar
            </button>
            <p id="login-message" class="text-red-500 text-sm 
text-center mt-2 hidden">Usuário ou senha inválidos.</p>
        </form>
    </div>

    <div id="app-page" class="bg-white p-6 md:p-8 rounded-2xl shadow-xl w-full max-w-full md:max-w-5xl border border-gray-200 hidden">
        <div class="flex justify-between items-center mb-6 relative">
            <div class="flex-grow flex justify-center">
                <h1 class="text-2xl md:text-3xl font-bold text-gray-800">Lançamento de Corridas</h1>
            </div>
            <button id="logout-btn" class="absolute top-0 right-0 px-4 py-2 bg-gray-300 text-gray-800 font-medium rounded-lg hover:bg-gray-400">Sair</button>
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
            
            <div class="md:col-span-2 flex justify-center mt-4">
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
            <button type="button" id="open-lancamentos-modal" class="px-6 py-3 bg-red-600 text-white font-bold rounded-lg shadow-lg hover:bg-red-700 focus:outline-none focus:ring-4 focus:ring-red-500 focus:ring-opacity-50 transition duration-150 ease-in-out">
                Gerenciar Lançamentos
            </button>
            <button type="button" id="open-transportados-modal" class="px-6 py-3 bg-purple-600 
text-white font-bold rounded-lg shadow-lg hover:bg-purple-700 focus:outline-none focus:ring-4 focus:ring-purple-500 focus:ring-opacity-50 transition duration-150 ease-in-out">
                Gerenciar Transportados
            </button>
            <button type="button" id="open-motoristas-modal" class="px-6 py-3 bg-indigo-600 text-white font-bold rounded-lg shadow-lg hover:bg-indigo-700 focus:outline-none focus:ring-4 focus:ring-indigo-500 focus:ring-opacity-50 transition duration-150 ease-in-out hidden">
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

    <div id="lancamentos-modal" class="fixed inset-0 bg-gray-600 bg-opacity-50 hidden flex items-center justify-center p-4">
        <div class="bg-white p-6 md:p-8 rounded-2xl shadow-2xl modal-content max-h-[90vh] overflow-y-auto">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-xl md:text-2xl font-bold text-gray-800">Gerenciar Lançamentos</h2>
                <button id="close-lancamentos-modal" class="text-gray-500 hover:text-gray-800 text-xl font-bold">&times;</button>
            </div>
            <p id="lancamentos-modal-filter-info" class="text-sm text-gray-600 mb-4"></p>

            <div class="overflow-x-auto rounded-lg shadow-md border border-gray-200">
                <table class="min-w-full table-auto" id="lancamentos-table">
                    <thead class="bg-gray-50">
                        <tr>
                            <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Data</th>
                            <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Motorista</th>
                            <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Destino</th>
                            <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Valor</th>
                        </tr>
                    </thead>
                    <tbody class="bg-white divide-y divide-gray-200">
                        </tbody>
                </table>
            </div>
            <div class="flex justify-end mt-4">
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
        // IMPORTAÇÕES
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, addDoc, deleteDoc, onSnapshot, collection, doc, query, where, getDocs, setLogLevel } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";
        
        // CONFIGURAÇÃO FIREBASE
        const firebaseConfig = {
            apiKey: "AIzaSyDmqvcKtIsga4ZQWNDg4_2k493dqMQCDVg",
            authDomain: "teste-ebf38.firebaseapp.com",
            projectId: "teste-ebf38",
            storageBucket: "teste-ebf38.firebasestorage.app",
            messagingSenderId: "741884776297",
            appId: "1:741884776297:web:a23450b4909581a1b237f8",
            measurementId: "G-2MD5CFD51E"
        };
        
        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);
        const auth = getAuth(app);
        setLogLevel('debug');

        const globalAppId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
        let globalUserId = null;

        // ESTADO GLOBAL DO USUÁRIO LOGADO
        let currentUserData = null; 

        // ELEMENTOS DOM
        const loginForm = document.getElementById('login-form');
        const loginPage = document.getElementById('login-page');
        const appPage = document.getElementById('app-page');
        const loginMessage = document.getElementById('login-message');
        const userIdDisplay = document.getElementById('user-id-display');
        const logoutButton = document.getElementById('logout-btn');
        const motoristaInput = document.getElementById('motorista'); 
        const openMotoristasBtn = document.getElementById('open-motoristas-modal'); 
        const openLancamentosBtn = document.getElementById('open-lancamentos-modal');

        const matriculaInputHidden = document.getElementById('matricula'); 
        const transportadoInputHidden = document.getElementById('transportado');

        const passageirosContainer = document.getElementById('passageiros-campos-container');
        const addPassageiroBtn = document.getElementById('add-passageiro-btn');

        const valorInput = document.getElementById('valor');
        const valorExtraInput = document.getElementById('valor-extra');
        const downloadCsvBtn = document.getElementById('download-csv');
        
        // === CONFIGURAÇÃO DE USUÁRIOS ===
        const users = [
            { username: 'admin', password: 'rafael22' },
            { username: 'gerente', password: 'senha123' },
            { username: 'motorista1', password: 'senha123' }
        ];
        
        // Mapeamento de usuários para nome de motorista fixo e permissão
        const motoristaUsers = {
            'admin': { nome: 'Administrador Principal', is_admin: true, is_motorista_fixo: false }, 
            'gerente': { nome: 'Gerente Operacional', is_admin: true, is_motorista_fixo: false }, 
            
            // MOTORISTA COMUM: Tem NOME FIXO
            'motorista1': { nome: 'João da Silva', is_admin: false, is_motorista_fixo: true }, 
        };

        let transportadosData = [];
        let motoristasData = [];
        let lancamentosData = [];
        
        let matriculaToNome = {};
        let nomeToMatricula = {};

        // === FUNÇÕES DE PERMISSÃO E UI ===

        function showWarning(message) {
            document.getElementById('message-content').innerText = message;
            document.getElementById('message-modal').classList.remove('hidden');
        }

        function hideWarning() {
            document.getElementById('message-modal').classList.add('hidden');
        }
        
        function setMotoristaReadOnly(username) {
            const userData = motoristaUsers[username];
            
            // ATUALIZA ESTADO GLOBAL
            currentUserData = userData; 

            // 1. Gerencia a visibilidade dos botões de administração
            if (userData && userData.is_admin) {
                openMotoristasBtn.classList.remove('hidden');
                downloadCsvBtn.classList.remove('hidden');
            } else {
                openMotoristasBtn.classList.add('hidden');
                downloadCsvBtn.classList.add('hidden'); // Oculta CSV para não-admins
            }
            openLancamentosBtn.classList.remove('hidden'); // Todos podem gerenciar lançamentos (filtrados)

            
            // 2. Lógica para preencher/bloquear o campo Motorista
            if (userData && userData.is_motorista_fixo) {
                // Se for um motorista fixo: BLOQUEIA E PREENCHE
                motoristaInput.value = userData.nome;
                
                // Torna o campo somente leitura e altera estilo
                motoristaInput.setAttribute('readonly', 'readonly');
                motoristaInput.classList.remove('bg-gray-50');
                motoristaInput.classList.add('bg-gray-200'); 
            } else {
                // Se for Admin, Gerente ou outro usuário sem nome fixo: DEIXA EDITÁVEL
                motoristaInput.removeAttribute('readonly');
                motoristaInput.classList.remove('bg-gray-200');
                motoristaInput.classList.add('bg-gray-50');
                
                // Pré-preenche com o nome de usuário (útil para admins/gerentes)
                if (userData) {
                     motoristaInput.value = userData.nome;
                } else {
                     motoristaInput.value = '';
                }
            }
        }


        // Função para checar duplicidade na tela (em tempo real)
        function checkPassageiroDuplicidade(sourceInput) {
            const rows = document.querySelectorAll('#passageiros-campos-container .passageiro-row');
            
            // Localiza os campos na linha atual
            const row = sourceInput.closest('.passageiro-row');
            const currentMatriculaInput = row.querySelector('input[name="matriculas[]"]');
            const currentNomeInput = row.querySelector('input[name="transportados[]"]');

            const currentMatricula = currentMatriculaInput.value.trim();
            const currentNome = currentNomeInput.value.trim();

            if (currentMatricula === '' || currentNome === '') {
                // Remove borda se a linha está incompleta
                currentMatriculaInput.classList.remove('error-border');
                currentNomeInput.classList.remove('error-border');
                return false; 
            }

            const currentKey = `${currentMatricula}_${currentNome.toLowerCase()}`;
            let isDuplicated = false;

            // Limpa bordas de todas as linhas que podem ter sido corrigidas (preventivamente)
            rows.forEach(r => {
                r.querySelector('input[name="matriculas[]"]').classList.remove('error-border');
                r.querySelector('input[name="transportados[]"]').classList.remove('error-border');
            });


            rows.forEach(rowToCheck => {
                const rowMatricula = rowToCheck.querySelector('input[name="matriculas[]"]').value.trim();
                const rowNome = rowToCheck.querySelector('input[name="transportados[]"]').value.trim();

                const rowKey = `${rowMatricula}_${rowNome.toLowerCase()}`;

                // Verifica se é a mesma linha de entrada para ignorar a si mesma
                const isSameRow = (rowToCheck === row);

                if (rowKey === currentKey && !isSameRow) {
                    isDuplicated = true;
                    // Aplica borda de erro também na linha duplicada
                    rowToCheck.querySelector('input[name="matriculas[]"]').classList.add('error-border');
                    rowToCheck.querySelector('input[name="transportados[]"]').classList.add('error-border');
                }
            });

            if (isDuplicated) {
                // Aplica borda de erro nos campos duplicados que acabaram de ser preenchidos
                currentMatriculaInput.classList.add('error-border');
                currentNomeInput.classList.add('error-border');
                showWarning(`Passageiro duplicado encontrado: Matrícula ${currentMatricula} e Nome ${currentNome}. Por favor, remova ou edite a duplicidade.`);
            }

            return isDuplicated;
        }

        // Função de preenchimento automático DINÂMICA com checagem de duplicidade
        function handleAutofillDynamic(sourceInput, targetInput, sourceType) {
            const value = sourceInput.value.trim();
            
            // 1. Lógica de Autofill
            if (value !== '') {
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
                }
            } else {
                // Se o campo for limpo, limpa o campo oposto para evitar dados parciais
                targetInput.value = '';
            }

            // 2. Lógica de Validação Imediata (Duplicidade)
            setTimeout(() => {
                // Checa a duplicidade no elemento que está sendo focado (o sourceInput)
                checkPassageiroDuplicidade(sourceInput);
            }, 50); 
        }

        // Função para reordenar a numeração (P1, P2, P3...) após remoção ou adição
        function updatePassageiroLabels() {
            const rows = document.querySelectorAll('#passageiros-campos-container .passageiro-row');
            rows.forEach((row, index) => {
                const pNum = index + 1;
                
                // Atualiza os labels
                const matriculaLabel = row.querySelector(`label[for^="matricula-"]`);
                const transportadoLabel = row.querySelector(`label[for^="transportado-"]`);
                
                if(matriculaLabel) matriculaLabel.textContent = `Matrícula (P${pNum}):`;
                if(transportadoLabel) transportadoLabel.textContent = `Transportado (P${pNum}):`;
                
                // Atualiza o listener de remoção
                const removeBtn = row.querySelector('.remove-passageiro-btn');
                if (removeBtn) {
                    removeBtn.onclick = () => {
                        row.remove();
                        updatePassageiroLabels(); // Chama recursivamente para reordenar o restante
                    };
                }
            });
        }

        function createPassageiroInput(index, isRequired = true) {
            const fieldset = document.createElement('div');
            fieldset.className = 'passageiro-row grid grid-cols-1 md:grid-cols-2 gap-4 md:gap-6';
            fieldset.dataset.index = index; 
            fieldset.innerHTML = `
                <div>
                    <label for="matricula-${index}" class="block text-sm font-medium text-gray-700">Matrícula (P${index + 1}):</label>
                    <input type="text" id="matricula-${index}" name="matriculas[]" list="transportados-matricula-list"
                        onfocus="this.classList.remove('error-border')"
                        class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
                </div>

                <div class="flex items-end">
                    <div class="flex-grow">
                        <label for="transportado-${index}" class="block text-sm font-medium text-gray-700">Transportado (P${index + 1}):</label>
                        <input type="text" id="transportado-${index}" name="transportados[]" list="transportados-nome-list"
                            onfocus="this.classList.remove('error-border')"
                            class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
                    </div>
                    ${!isRequired ? `<button type="button" class="ml-2 px-3 py-2 bg-red-500 text-white font-bold rounded-lg shadow-md hover:bg-red-600 remove-passageiro-btn">-</button>` : ''}
                </div>
            `;
            
            return fieldset;
        }

        function addPassageiroRow(isRequired = false) {
            const newIndex = Date.now(); 
            const newRow = createPassageiroInput(newIndex, isRequired);
            passageirosContainer.appendChild(newRow);
            
            updatePassageiroLabels(); 
        }

        // NOVO: LÓGICA DE GERENCIAR LANÇAMENTOS
        
        function renderLancamentosList() {
            const tableBody = document.querySelector('#lancamentos-table tbody');
            const filterInfo = document.getElementById('lancamentos-modal-filter-info');
            tableBody.innerHTML = '';

            let dataToDisplay = lancamentosData;
            
            // FILTRAGEM DE PERMISSÃO
            if (currentUserData && !currentUserData.is_admin) {
                const motoristaNome = currentUserData.nome;
                dataToDisplay = lancamentosData.filter(l => l.motorista === motoristaNome);
                filterInfo.textContent = `Visualizando apenas seus lançamentos como "${motoristaNome}".`;
            } else {
                filterInfo.textContent = `Visualizando todos os lançamentos.`;
            }
            
            if (dataToDisplay.length === 0) {
                tableBody.innerHTML = '<tr><td colspan="4" class="p-4 text-center text-gray-500">Nenhum lançamento encontrado.</td></tr>';
                return;
            }

            dataToDisplay.forEach(item => {
                const row = document.createElement('tr');
                row.className = 'bg-white hover:bg-gray-100 transition-colors duration-100';
                row.dataset.id = item.id;
                
                // Formatação simples para a tabela de gerenciamento
                const formattedDate = item.data.split('-').reverse().join('/');
                const formattedValue = `R$ ${item.valor ? item.valor.toFixed(2).replace('.', ',') : '0,00'}`;
                
                row.innerHTML = `
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${formattedDate}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${item.motorista}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${item.destino}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${formattedValue}</td>
                `;
                tableBody.appendChild(row);
            });
        }
        
        // ... (Funções de CRUD de modais) ...

        // Evento de envio do formulário (Lógica para Múltiplos Passageiros, Duplicidade e Validação)
        document.getElementById('form-corrida').addEventListener('submit', async function(event) {
            event.preventDefault();

            const form = event.target;
            const requiredFields = [
                'motorista', 'solicitante', 'data',
                'origem', 'partida', 'destino', 'chegada',
                'valor'
            ];
            
            const matriculasInputs = document.querySelectorAll('#passageiros-campos-container input[name="matriculas[]"]');
            const transportadosInputs = document.querySelectorAll('#passageiros-campos-container input[name="transportados[]"]');

            const passageirosData = [];
            let isFormValid = true;
            
            // Conjunto para verificar duplicidade: { 'matricula_nome' }
            const passageirosSet = new Set();
            let hasError = false; 

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
            
            // 2. Coleta, validação e verificação de duplicidade dos passageiros
            for (let i = 0; i < matriculasInputs.length; i++) {
                const matriculaInput = matriculasInputs[i];
                const nomeInput = transportadosInputs[i];

                const matricula = matriculaInput.value.trim();
                const nome = nomeInput.value.trim();
                
                matriculaInput.classList.remove('error-border');
                nomeInput.classList.remove('error-border');
                
                // Se o par tiver dados preenchidos
                if (matricula !== '' && nome !== '') {
                    const key = `${matricula}_${nome.toLowerCase()}`;
                    
                    if (passageirosSet.has(key)) {
                        isFormValid = false;
                        hasError = true;
                        matriculaInput.classList.add('error-border');
                        nomeInput.classList.add('error-border');
                        showWarning(`Passageiro duplicado encontrado: Matrícula ${matricula} e Nome ${nome}. Por favor, remova ou edite a duplicidade.`);
                        return;
                    }
                    
                    passageirosSet.add(key);
                    passageirosData.push({ matricula: matricula, nome: nome });
                } 
                // Se apenas um dos campos estiver preenchido (erro de campo obrigatório)
                else if (matricula !== '' || nome !== '') {
                    isFormValid = false;
                    hasError = true;
                    if (matricula === '') matriculaInput.classList.add('error-border');
                    if (nome === '') nomeInput.classList.add('error-border');
                }
            }
            
            // 3. Valida se pelo menos um passageiro (o primeiro) está preenchido
            if (!passageirosData[0]) {
                isFormValid = false;
                hasError = true;
                if (matriculasInputs[0]) matriculasInputs[0].classList.add('error-border');
                if (transportadosInputs[0]) transportadosInputs[0].classList.add('error-border');
            }


            if (!isFormValid) {
                if (!hasError || !document.getElementById('message-modal').classList.contains('hidden')) { 
                    showWarning('Por favor, preencha todos os campos obrigatórios e verifique os dados dos passageiros (Matrícula e Nome são obrigatórios para pelo menos 1 passageiro).');
                }
                return;
            }

            // Preenche os campos hidden com o primeiro passageiro para compatibilidade com o backend/CSV
            matriculaInputHidden.value = passageirosData[0].matricula;
            transportadoInputHidden.value = passageirosData[0].nome;

            // Cria o campo de passageiros extras (se houver mais de um)
            const passageirosExtras = passageirosData.length > 1 ? passageirosData.slice(1) : null;

            const newEntry = {
                motorista: form['motorista'].value,
                matricula: form['matricula'].value, 
                transportado: form['transportado'].value, 
                passageiros_extras: passageirosExtras, 
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
            addPassageiroRow(true); // Adiciona o primeiro de volta
        });

        // Evento do botão de download - CORRIGIDO PARA ORDENAR E TRATAR ERROS
        document.getElementById('download-csv').addEventListener('click', async function() {
            // Verifica se é admin antes de prosseguir (redundante, mas seguro)
            if (!currentUserData || !currentUserData.is_admin) {
                 showWarning('Acesso negado. Apenas administradores podem baixar o relatório CSV.');
                 return;
            }

            const startDate = document.getElementById('start-date').value;
            const endDate = document.getElementById('end-date').value;

            if (startDate && endDate && new Date(startDate) > new Date(endDate)) {
                showWarning('A data de início não pode ser posterior à data de fim.');
                return;
            }

            const lancamentosRef = collection(db, 'artifacts', globalAppId, 'public', 'data', 'lancamentos');

            let filtros = [];
            if (startDate) filtros.push(where('data', '>=', startDate));
            if (endDate) filtros.push(where('data', '<=', endDate));

            let q = filtros.length > 0 ? query(lancamentosRef, ...filtros) : lancamentosRef;

            try {
                const snapshot = await getDocs(q);
                const allData = snapshot.docs.map(doc => doc.data());

                if (allData.length === 0) {
                    showWarning('Nenhum dado encontrado para este período.');
                    return;
                }

                const bom = '\uFEFF';
                
                // 1. Define a lista de todas as chaves únicas no Firestore
                let allKeys = new Set();
                allData.forEach(obj => {
                    Object.keys(obj).forEach(key => allKeys.add(key));
                });
                
                // 2. Define a Ordem Desejada para as colunas principais
                const orderedKeys = [
                    'motorista', 'solicitante', 
                    'matricula', 'transportado', 
                    'data', 'origem', 'destino', 
                    'partida', 'chegada', 
                    'valor', 'valorExtra', 'observacao'
                ];

                let finalHeaders = [];
                let maxPassageirosExtras = 0;
                
                // 3. Determina o máximo de extras para saber quantas colunas dinâmicas criar
                allData.forEach(obj => {
                    if (obj.passageiros_extras && Array.isArray(obj.passageiros_extras)) {
                        maxPassageirosExtras = Math.max(maxPassageirosExtras, obj.passageiros_extras.length);
                    }
                });

                // 4. Constrói o cabeçalho final na ordem correta
                orderedKeys.forEach(key => {
                    if (allKeys.has(key)) {
                        finalHeaders.push(key);
                    }
                    
                    // Se for o campo 'transportado', insere os pares extras logo após ele
                    if (key === 'transportado') {
                        for (let i = 0; i < maxPassageirosExtras; i++) {
                            finalHeaders.push(`matricula_extra_${i+1}`);
                            finalHeaders.push(`transportado_extra_${i+1}`);
                        }
                    }
                });
                
                // Garante que 'passageiros_extras' não vá para o cabeçalho, mas sim as colunas que acabamos de criar
                finalHeaders = finalHeaders.filter(header => header !== 'passageiros_extras');


                // 5. Mapeamento dos Dados
                const headers = finalHeaders;
                const rows = allData.map(obj => headers.map(key => {
                    let value = obj[key] ?? '';
                    
                    if (key.startsWith('matricula_extra_') || key.startsWith('transportado_extra_')) {
                        const parts = key.split('_');
                        const index = parseInt(parts[2]) - 1; 
                        const type = parts[0] === 'matricula' ? 'matricula' : 'nome'; 
                        
                        if (obj.passageiros_extras && obj.passageiros_extras[index]) {
                            value = obj.passageiros_extras[index][type] ?? ''; 
                        } else {
                            value = '';
                        }
                    }

                    if (key === 'valor' || key === 'valorExtra') {
                        let numValue = parseFloat(value);
                        value = isNaN(numValue) || numValue === 0 ? '' : `R$ ${numValue.toFixed(2).replace('.', ',')}`;
                    }
                    
                    return `"${String(value).replace(/"/g, '""')}"`;
      
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

        // Funções de renderização de modais (simplificadas)
        function renderTransportadosList() { /* ... */ }
        function renderMotoristasList() { /* ... */ }
        function populateTransportadosDatalist() { /* ... */ }
        function populateMotoristasDatalist() { /* ... */ }
        
        document.getElementById('add-transportado').addEventListener('click', async function() { /* ... */ });
        document.getElementById('delete-selected-transportados').addEventListener('click', async function() { /* ... */ });
        document.getElementById('add-motorista').addEventListener('click', async function() { /* ... */ });
        document.getElementById('delete-selected-motoristas').addEventListener('click', async function() { /* ... */ });
        
        document.getElementById('close-modal').addEventListener('click', function() { hideWarning(); });
        document.getElementById('open-transportados-modal').addEventListener('click', function() { document.getElementById('transportados-modal').classList.remove('hidden'); });
        document.getElementById('close-transportados-modal').addEventListener('click', function() { document.getElementById('transportados-modal').classList.add('hidden'); });
        document.getElementById('open-motoristas-modal').addEventListener('click', function() { document.getElementById('motoristas-modal').classList.remove('hidden'); });
        document.getElementById('close-motoristas-modal').addEventListener('click', function() { document.getElementById('motoristas-modal').classList.add('hidden'); });
        
        // Eventos do modal de Lançamentos
        document.getElementById('open-lancamentos-modal').addEventListener('click', function() {
            renderLancamentosList(); // Carrega os dados na abertura
            document.getElementById('lancamentos-modal').classList.remove('hidden');
        });
        document.getElementById('close-lancamentos-modal').addEventListener('click', function() {
            document.getElementById('lancamentos-modal').classList.add('hidden');
        });

        document.getElementById('sort-transportados-key').addEventListener('change', function() { /* ... */ });
        document.getElementById('sort-transportados-order').addEventListener('change', function() { /* ... */ });
        document.getElementById('sort-motoristas-order').addEventListener('change', function() { /* ... */ });
        document.getElementById('transportados-table').addEventListener('change', function(event) { /* ... */ });
        document.getElementById('motoristas-table').addEventListener('change', function(event) { /* ... */ });
        document.getElementById('transportados-table').addEventListener('click', function(event) { /* ... */ });
        document.getElementById('motoristas-table').addEventListener('click', function(event) { /* ... */ });
    </script>
</body>
</html>
