<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lançamento de Corridas</title>
    <!-- Tailwind CSS CDN -->
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
    <!-- Firebase SDKs -->
    <script type="module">
      import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
      import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
      import { getFirestore, doc, getDoc, addDoc, setDoc, updateDoc, deleteDoc, onSnapshot, collection, query, where, addDoc, getDocs, setLogLevel } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

      // Firebase Config - SUBSTITUA PELA SUA CONFIGURAÇÃO
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
      setLogLevel('debug'); // Ativa logs do Firestore

      // Variáveis globais para serem usadas no script
      window.db = db;
      window.auth = auth;
      window.onAuthStateChanged = onAuthStateChanged;
      window.signInAnonymously = signInAnonymously;
      window.signInWithCustomToken = signInWithCustomToken;
      window.signOut = signOut;
      window.addDoc = addDoc;
      window.collection = collection;
      window.onSnapshot = onSnapshot;
      window.doc = doc;
      window.deleteDoc = deleteDoc;
      window.query = query;
      window.orderBy = orderBy;
      window.where = where;
      window.crypto = crypto;
      window.setDoc = setDoc;

      window.globalUserId = null;
      window.globalAppId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
      window.globalInitialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;
    </script>
    <script type="module">
        import { getFirestore, collection, onSnapshot, addDoc, doc, deleteDoc, query } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";
        import { getAuth, onAuthStateChanged, signInWithCustomToken, signInAnonymously } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        
        // Autenticação
        const loginForm = document.getElementById('login-form');
        const loginPage = document.getElementById('login-page');
        const appPage = document.getElementById('app-page');
        const loginMessage = document.getElementById('login-message');
        const userIdDisplay = document.getElementById('user-id-display');
        const logoutButton = document.getElementById('logout-btn');

        // Lista de usuários e senhas
        const users = [
            { username: 'admin', password: 'rafael22' },
            { username: 'gerente', password: 'senha123' }
        ];

        let transportadosData = [];
        let motoristasData = [];

        // Inicializa o app e Firestore
        const db = getFirestore();
        const auth = getAuth();
        let appInitialized = false;

        function initializeApp() {
            if (appInitialized) return;
            
            // Login Anônimo ou com token
            onAuthStateChanged(auth, async (user) => {
                if (user) {
                    window.globalUserId = user.uid;
                    userIdDisplay.innerText = `ID do Usuário: ${window.globalUserId}`;
                    loginPage.classList.add('hidden');
                    appPage.classList.remove('hidden');
                    
                    // Inicia listeners para as coleções
                    startFirestoreListeners();
                } else {
                    window.globalUserId = null;
                    loginPage.classList.remove('hidden');
                    appPage.classList.add('hidden');
                }
            });
            
            if (window.globalInitialAuthToken) {
                signInWithCustomToken(auth, window.globalInitialAuthToken).catch((error) => {
                    console.error("Erro ao fazer login com token customizado:", error);
                    signInAnonymously(auth);
                });
            } else {
                signInAnonymously(auth);
            }
            appInitialized = true;
        }

        // Listener para os dados do Firestore
        function startFirestoreListeners() {
            // Listener para Transportados
            const transportadosRef = collection(db, 'artifacts', window.globalAppId, 'public', 'data', 'transportados');
            onSnapshot(transportadosRef, (snapshot) => {
                transportadosData = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
                rebuildTransportadosLookups();
            });

            // Listener para Motoristas
            const motoristasRef = collection(db, 'artifacts', window.globalAppId, 'public', 'data', 'motoristas');
            onSnapshot(motoristasRef, (snapshot) => {
                motoristasData = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
                rebuildMotoristasLookups();
            });
        }
        
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

        let matriculaToNome = {};
        let nomeToMatricula = {};

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

        // Funções de preenchimento automático para transportados
        function autofillTransportado() {
            const matriculaInput = document.getElementById('matricula');
            const transportadoInput = document.getElementById('transportado');
            const matricula = matriculaInput.value.trim();
            const nome = matriculaToNome[matricula];

            if (matricula === '') {
                transportadoInput.value = '';
            } else if (nome) {
                transportadoInput.value = nome;
            } else {
                transportadoInput.value = '';
                showWarning('Matrícula não encontrada.');
            }
        }

        function autofillMatricula() {
            const matriculaInput = document.getElementById('matricula');
            const transportadoInput = document.getElementById('transportado');
            const nome = transportadoInput.value.trim().toLowerCase();
            const matricula = nomeToMatricula[nome];

            if (nome === '') {
                matriculaInput.value = '';
            } else if (matricula) {
                matriculaInput.value = matricula;
            } else {
                matriculaInput.value = '';
                showWarning('Nome não encontrado.');
            }
        }
        
        // Validação do motorista
        function validateMotorista() {
            const motoristaInput = document.getElementById('motorista');
            const nome = motoristaInput.value.trim();
            const found = motoristasData.some(item => item.nome === nome);
            if (nome !== '' && !found) {
                showWarning('Motorista não encontrado na lista.');
            }
        }

        // Funções para manipulação de dados e CSV
        function exportAllToCsv(dataArray) {
            if (dataArray.length === 0) {
                showWarning('Não há dados para exportar.');
                return;
            }
            
            // Add UTF-8 BOM to fix special characters in Excel
            const bom = '\uFEFF'; 

            const keys = Object.keys(dataArray[0]);
            
            const headers = keys.map(key => {
                return key.replace(/([A-Z])/g, ' $1').replace(/^./, (str) => str.toUpperCase());
            });

            const rows = dataArray.map(obj => {
                return keys.map(key => `"${(obj[key] || '').toString().replace(/"/g, '""')}"`).join(';');
            });
            
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
        }

        function populateMotoristasDatalist() {
            const datalist = document.getElementById('motoristas-list');
            datalist.innerHTML = '';
            motoristasData.forEach(item => {
                const option = document.createElement('option');
                option.value = item.nome;
                datalist.appendChild(option);
            });
        }

        // Funções de gerenciamento de dados
        document.getElementById('add-transportado').addEventListener('click', async function() {
            const newMatriculaInput = document.getElementById('new-matricula');
            const newNomeInput = document.getElementById('new-nome');
            const newMatricula = newMatriculaInput.value.trim();
            const newNome = newNomeInput.value.trim();

            if (newMatricula && newNome) {
                const existing = transportadosData.find(item => item.matricula === newMatricula || item.nome.toLowerCase() === newNome.toLowerCase());
                if (existing) {
                    showWarning('A matrícula ou o nome já existe.');
                } else {
                    const transportadosRef = collection(db, 'artifacts', window.globalAppId, 'public', 'data', 'transportados');
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
                const transportadoDocRef = doc(db, 'artifacts', window.globalAppId, 'public', 'data', 'transportados', cb.dataset.id);
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
                    const motoristasRef = collection(db, 'artifacts', window.globalAppId, 'public', 'data', 'motoristas');
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
                const motoristaDocRef = doc(db, 'artifacts', window.globalAppId, 'public', 'data', 'motoristas', cb.dataset.id);
                return deleteDoc(motoristaDocRef);
            });
            await Promise.all(promises);
            showWarning(`${checkboxes.length} motoristas excluídos com sucesso!`);
        });
        
        // Funções de formatação de moeda
        function formatCurrencyInput(input) {
            let value = input.value.replace(/\D/g, ''); // Remove todos os caracteres não numéricos
            if (value === '') {
                input.value = '';
                return;
            }
            
            value = value.padStart(3, '0'); // Garante pelo menos 3 dígitos (ex: '1' vira '001')
            
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
                'motorista', 'matricula', 'transportado', 'solicitante', 'data',
                'origem', 'partida', 'destino', 'chegada',
                'valor'
            ];

            let isFormValid = true;
            for (const field of requiredFields) {
                const input = form[field];
                if (input.value.trim() === '') {
                    isFormValid = false;
                    input.classList.add('error-border');
                } else {
                    input.classList.remove('error-border');
                }
            }

            if (!isFormValid) {
                showWarning('Por favor, preencha todos os campos obrigatórios.');
                return;
            }

            const newEntry = {
                motorista: form['motorista'].value,
                matricula: form['matricula'].value,
                transportado: form['transportado'].value,
                solicitante: form['solicitante'].value,
                data: form['data'].value,
                origem: form['origem'].value,
                partida: form['partida'].value,
                destino: form['destino'].value,
                chegada: form['chegada'].value,
                valor: parseCurrencyValue(form['valor'].value),
                valorExtra: form['valor-extra'].value ? parseCurrencyValue(form['valor-extra'].value) : null,
                observacao: form['observacao'].value
            };

            const lancamentosRef = collection(db, 'artifacts', window.globalAppId, 'public', 'data', 'lancamentos');
            await addDoc(lancamentosRef, newEntry);

            showWarning('Lançamento salvo com sucesso!');
            form.reset();
            document.getElementById('valor').value = '0,00';
            document.getElementById('valor-extra').value = '0,00';
        });

        // Evento de navegação com a tecla "Enter"
        const inputs = document.querySelectorAll('#form-corrida input:not([readonly]), #form-corrida textarea');
        inputs.forEach(input => {
            input.addEventListener('keydown', function(event) {
                if (event.key === 'Enter') {
                    event.preventDefault();

                    const currentInputIndex = Array.from(inputs).indexOf(this);
                    let nextInput = null;

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
            const lancamentosRef = collection(db, 'artifacts', window.globalAppId, 'public', 'data', 'lancamentos');
            const snapshot = await getDocs(lancamentosRef);
            const allData = snapshot.docs.map(doc => doc.data());

            exportAllToCsv(allData);
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

        window.onload = initializeApp;
    </script>

</body>
</html>
