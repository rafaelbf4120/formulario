<!DOCTYPE html>
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
        tr {
            cursor: pointer;
        }
        .modal-content {
            width: 95%;
            max-width: 48rem; /* Equivalent to max-w-2xl */
        }
        @media (min-width: 640px) {
            .modal-content {
                width: 100%;
            }
        }
        .modal-lg {
            max-width: 80rem; /* max-w-6xl */
        }
        .modal-title {
            text-align: center;
            flex-grow: 1;
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
                <input type="password" id="password" name="password" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
            </div>
            <button type="submit" class="w-full px-6 py-3 bg-blue-600 text-white font-bold rounded-lg shadow-lg hover:bg-blue-700 focus:outline-none focus:ring-4 focus:ring-blue-500 focus:ring-opacity-50 transition duration-150 ease-in-out">
                Entrar
            </button>
            <p id="login-message" class="text-red-500 text-sm text-center mt-2 hidden">Usuário ou senha inválidos.</p>
        </form>
    </div>

    <div id="app-page" class="bg-white p-6 md:p-8 rounded-2xl shadow-xl w-full max-w-full md:max-w-5xl border border-gray-200 hidden">
        <div class="flex justify-between items-center mb-6 relative">
            <h1 class="text-2xl md:text-3xl font-bold text-gray-800 modal-title">Lançamento de Corridas</h1>
            <button id="logout-btn" class="absolute top-0 right-0 px-4 py-2 bg-gray-300 text-gray-800 font-medium rounded-lg hover:bg-gray-400">Sair</button>
        </div>
        
        <p id="user-id-display" class="text-sm text-transparent text-center mb-4"></p>
        
        <form id="form-corrida" class="space-y-6">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <div>
                    <label for="motorista" class="block text-sm font-medium text-gray-700">Motorista:</label>
                    <input type="text" id="motorista" name="motorista" list="motoristas-list" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
                    <datalist id="motoristas-list"></datalist>
                </div>
                <div>
                    <label for="solicitante" class="block text-sm font-medium text-gray-700">Solicitante:</label>
                    <input type="text" id="solicitante" name="solicitante" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
                </div>
                <div>
                    <label for="data" class="block text-sm font-medium text-gray-700">Data:</label>
                    <input type="date" id="data" name="data" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
                </div>
                <div>
                    <label for="origem" class="block text-sm font-medium text-gray-700">Origem Principal:</label>
                    <input type="text" id="origem" name="origem" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
                </div>
            </div>

            <hr>
            <h3 class="text-lg font-semibold text-gray-700 text-center">Passageiros</h3>
            <div id="passageiros-campos-container" class="space-y-4"></div>
            <button type="button" id="add-passageiro-btn" class="w-full px-4 py-2 bg-gray-200 text-gray-800 font-medium rounded-lg hover:bg-gray-300">
                + Adicionar Passageiro
            </button>
            
            <hr>
            <h3 class="text-lg font-semibold text-gray-700 text-center">Trajetos</h3>
            <div id="destinos-container" class="space-y-4"></div>
            <button type="button" id="add-destino-btn" class="w-full px-4 py-2 bg-blue-200 text-blue-800 font-medium rounded-lg hover:bg-blue-300">
                + Adicionar Destino / Parada
            </button>
            
            <hr>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <div>
                    <label for="valor" class="block text-sm font-medium text-gray-700">Valor Total:</label>
                    <div class="relative mt-1">
                        <span class="absolute inset-y-0 left-0 flex items-center pl-3 pr-2 text-gray-400">R$</span>
                        <input type="text" id="valor" name="valor" class="block w-full px-3 py-2 pl-9 bg-gray-50 border border-gray-300 rounded-lg text-right">
                    </div>
                </div>
                <div>
                    <label for="valor-extra" class="block text-sm font-medium text-gray-700">Valor Extra Total:</label>
                    <div class="relative mt-1">
                        <span class="absolute inset-y-0 left-0 flex items-center pl-3 pr-2 text-gray-400">R$</span>
                        <input type="text" id="valor-extra" name="valor-extra" class="block w-full px-3 py-2 pl-9 bg-gray-50 border border-gray-300 rounded-lg text-right">
                    </div>
                </div>
                <div class="md:col-span-2">
                    <label for="observacao" class="block text-sm font-medium text-gray-700">Observação:</label>
                    <textarea id="observacao" name="observacao" rows="4" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg"></textarea>
                </div>
            </div>
            
            <div class="flex justify-center mt-4">
                <button type="submit" class="w-full md:w-1/2 px-6 py-3 bg-blue-600 text-white font-bold rounded-lg shadow-lg hover:bg-blue-700">
                    Salvar Lançamento
                </button>
            </div>
        </form>

        <hr class="my-6 md:my-8 border-gray-300">
        
        </div>
    
    <script type="module">
        // IMPORTAÇÕES
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, addDoc, deleteDoc, onSnapshot, collection, doc, query, where, getDocs, updateDoc, serverTimestamp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";
        
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
        const APP_ID = 'default-app-id';

        // VARIÁVEIS GLOBAIS
        let globalUserId = null;
        let currentUser = { username: null, isAdmin: false };
        let transportadosData = [], motoristasData = [], lancamentosData = [];
        let matriculaToNome = {}, nomeToMatricula = {};

        // ELEMENTOS DOM
        const loginPage = document.getElementById('login-page');
        const appPage = document.getElementById('app-page');
        const loginForm = document.getElementById('login-form');
        const logoutButton = document.getElementById('logout-btn');
        const motoristaInput = document.getElementById('motorista');
        const passageirosContainer = document.getElementById('passageiros-campos-container');
        const addPassageiroBtn = document.getElementById('add-passageiro-btn');
        const destinosContainer = document.getElementById('destinos-container');
        const addDestinoBtn = document.getElementById('add-destino-btn');

        // ==========================================================
        // AQUI ESTÁ A SEÇÃO PARA ADICIONAR USUÁRIOS
        // ==========================================================
        const users = [
            { username: 'admin', password: 'rafael22' },
            { username: 'gerente', password: 'senha123' },
            { username: 'motorista1', password: 'senha123' }
        ];
        const motoristaUsers = {
            'admin': { nome: 'Administrador Principal', is_admin: true, is_motorista_fixo: false },
            'gerente': { nome: 'Gerente Operacional', is_admin: true, is_motorista_fixo: false },
            'motorista1': { nome: 'João da Silva', is_admin: false, is_motorista_fixo: true },
        };
        // ==========================================================

        // FUNÇÕES UTILITÁRIAS
        const showWarning = (message) => { /* ... */ };
        // ... (resto das funções utilitárias que você já tem)

        // LÓGICA DE LOGIN
        loginForm.addEventListener('submit', (event) => {
            event.preventDefault();
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            const foundUser = users.find(u => u.username === username && u.password === password);
            if (foundUser) {
                loginPage.classList.add('hidden');
                appPage.classList.remove('hidden');
                setupUIForUser(username);
            } else {
                document.getElementById('login-message').classList.remove('hidden');
            }
        });

        function setupUIForUser(username) {
            const userData = motoristaUsers[username];
            currentUser = { username, isAdmin: userData?.is_admin || false };
            
            // ... (resto da lógica para bloquear campo de motorista, etc.)
        }

        // LISTENERS DO FIRESTORE
        function startFirestoreListeners() { /* ... */ }

        // LÓGICA DE AUTOFILL
        // ... (código de autofill existente)

        // --- LÓGICA DO FORMULÁRIO PRINCIPAL ---

        // Gerenciamento de Passageiros
        function createPassageiroInput(index) {
            const fieldset = document.createElement('div');
            fieldset.className = 'passageiro-row grid grid-cols-1 md:grid-cols-3 gap-4 items-end';
            fieldset.innerHTML = `
                <div>
                    <label class="block text-sm font-medium text-gray-700">Matrícula (P${index + 1}):</label>
                    <input type="text" name="matriculas[]" list="transportados-matricula-list" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
                </div>
                <div class="md:col-span-2 flex items-end">
                    <div class="flex-grow">
                        <label class="block text-sm font-medium text-gray-700">Nome Transportado (P${index + 1}):</label>
                        <input type="text" name="transportados[]" list="transportados-nome-list" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
                    </div>
                    ${index > 0 ? `<button type="button" class="ml-2 px-3 py-2 bg-red-500 text-white font-bold rounded-lg hover:bg-red-600 remove-passageiro-btn">-</button>` : ''}
                </div>`;
            return fieldset;
        }

        function addPassageiroRow() {
            const index = passageirosContainer.children.length;
            passageirosContainer.appendChild(createPassageiroInput(index));
        }

        addPassageiroBtn.addEventListener('click', addPassageiroRow);
        passageirosContainer.addEventListener('click', (e) => {
            if (e.target.classList.contains('remove-passageiro-btn')) {
                e.target.closest('.passageiro-row').remove();
                // Re-numera os labels
                Array.from(passageirosContainer.children).forEach((row, index) => {
                    row.querySelector('label[for^="matricula"]').textContent = `Matrícula (P${index + 1}):`;
                    row.querySelector('label[for^="transportado"]').textContent = `Nome Transportado (P${index + 1}):`;
                });
            }
        });

        // Gerenciamento de Destinos
        function createDestinoInput(index) {
            const fieldset = document.createElement('div');
            fieldset.className = 'destino-row border-t pt-4';
            fieldset.innerHTML = `
                <div class="flex justify-between items-center mb-2">
                    <h3 class="text-md font-semibold text-gray-600">Trajeto / Parada ${index + 1}</h3>
                    ${index > 0 ? `<button type="button" class="px-3 py-1 bg-red-500 text-white font-bold rounded-lg text-sm hover:bg-red-600 remove-destino-btn">- Remover</button>` : ''}
                </div>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                    <div>
                        <label class="block text-sm font-medium text-gray-700">Partida:</label>
                        <input type="time" name="partidas[]" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
                    </div>
                    <div class="md:col-span-2">
                        <label class="block text-sm font-medium text-gray-700">Destino:</label>
                        <input type="text" name="destinos[]" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700">Chegada:</label>
                        <input type="time" name="chegadas[]" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
                    </div>
                </div>`;
            return fieldset;
        }

        function addDestinoRow() {
            const index = destinosContainer.children.length;
            destinosContainer.appendChild(createDestinoInput(index));
        }

        addDestinoBtn.addEventListener('click', addDestinoRow);
        destinosContainer.addEventListener('click', (e) => {
            if (e.target.classList.contains('remove-destino-btn')) {
                e.target.closest('.destino-row').remove();
                Array.from(destinosContainer.children).forEach((row, index) => {
                    row.querySelector('h3').textContent = `Trajeto / Parada ${index + 1}`;
                });
            }
        });

        // Submissão do Formulário Principal
        document.getElementById('form-corrida').addEventListener('submit', async (event) => {
            event.preventDefault();
            // ... (código de submissão completo que já implementamos)
        });

        // --- MODAIS E SUAS LÓGICAS ---
        // ... (todo o código dos modais de Gerenciar e Editar que já implementamos)

        // --- INICIALIZAÇÃO ---
        window.onload = () => {
            // ... (código de inicialização que já implementamos)
            addPassageiroRow();
            addDestinoRow();
        };

    </script>
</body>
</html>
