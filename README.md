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
        
        <form id="form-corrida" class="grid grid-cols-1 md:grid-cols-2 gap-4 md:gap-6 mb-6 md:mb-8">
            <div>
                <label for="motorista" class="block text-sm font-medium text-gray-700">Motorista:</label>
                <input type="text" id="motorista" name="motorista" list="motoristas-list" onfocus="this.classList.remove('error-border')" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
                <datalist id="motoristas-list"></datalist>
            </div>
            <div>
                <label for="solicitante" class="block text-sm font-medium text-gray-700">Solicitante:</label>
                <input type="text" id="solicitante" name="solicitante" onfocus="this.classList.remove('error-border')" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
            </div>
            <div id="passageiros-campos-container" class="md:col-span-2 grid grid-cols-1 md:grid-cols-2 gap-4 md:gap-6"></div>
            <div class="md:col-span-2">
                <button type="button" id="add-passageiro-btn" class="w-full px-4 py-2 bg-gray-200 text-gray-800 font-medium rounded-lg hover:bg-gray-300 transition duration-150 ease-in-out">
                    + Adicionar Outro Passageiro
                </button>
            </div>
            <div>
                <label for="data" class="block text-sm font-medium text-gray-700">Data:</label>
                <input type="date" id="data" name="data" onfocus="this.classList.remove('error-border')" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
            </div>
            <div>
                <label for="origem" class="block text-sm font-medium text-gray-700">Origem:</label>
                <input type="text" id="origem" name="origem" onfocus="this.classList.remove('error-border')" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
            </div>
            <div>
                <label for="destino" class="block text-sm font-medium text-gray-700">Destino:</label>
                <input type="text" id="destino" name="destino" onfocus="this.classList.remove('error-border')" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
            </div>
            <div>
                <label for="partida" class="block text-sm font-medium text-gray-700">Partida:</label>
                <input type="time" id="partida" name="partida" onfocus="this.classList.remove('error-border')" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
            </div>
            <div>
                <label for="chegada" class="block text-sm font-medium text-gray-700">Chegada:</label>
                <input type="time" id="chegada" name="chegada" onfocus="this.classList.remove('error-border')" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
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
                <label for="observacao" class="block text-sm font-medium text-gray-700">Observação:</label>
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
            <h2 class="text-xl font-bold text-gray-800 text-center">Gerar Relatório CSV</h2>
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
            <button type="button" id="download-csv" class="w-full px-6 py-3 bg-green-600 text-white font-bold rounded-lg shadow-lg hover:bg-green-700 focus:outline-none focus:ring-4 focus:ring-green-500 focus:ring-opacity-50 transition duration-150 ease-in-out">
                Baixar Relatório CSV
            </button>
        </div>

        <hr class="my-6 md:my-8 border-gray-300">

        <div class="flex flex-col md:flex-row justify-center gap-4">
            <button type="button" id="open-lancamentos-modal" class="px-6 py-3 bg-teal-600 text-white font-bold rounded-lg shadow-lg hover:bg-teal-700 focus:outline-none focus:ring-4 focus:ring-teal-500 focus:ring-opacity-50 transition duration-150 ease-in-out">
                Gerenciar Lançamentos
            </button>
            <button type="button" id="open-transportados-modal" class="px-6 py-3 bg-purple-600 text-white font-bold rounded-lg shadow-lg hover:bg-purple-700 focus:outline-none focus:ring-4 focus:ring-purple-500 focus:ring-opacity-50 transition duration-150 ease-in-out">
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
                <h2 class="text-xl md:text-2xl font-bold text-gray-800 modal-title">Gerenciar Transportados</h2>
                <button id="close-transportados-modal" class="text-gray-500 hover:text-gray-800 text-xl font-bold">&times;</button>
            </div>
            <div class="flex flex-col md:flex-row gap-4 items-start md:items-center mb-4 md:mb-6">
                <span class="text-sm font-medium text-gray-700">Ordenar por:</span>
                <select id="sort-transportados-key" class="w-full md:w-auto border border-gray-300 rounded-lg py-1 px-2 text-sm focus:outline-none focus:ring-2 focus:ring-blue-500">
                    <option value="nome">Nome</option>
                    <option value="matricula">Matrícula</option>
                </select>
                <select id="sort-transportados-order" class="w-full md:w-auto border border-gray-300 rounded-lg py-1 px-2 text-sm focus:outline-none focus:ring-2 focus:ring-blue-500">
                    <option value="asc">A-Z</option>
                    <option value="desc">Z-A</option>
                </select>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4 items-end mb-6">
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
            <div class="overflow-x-auto rounded-lg shadow-md border border-gray-200">
                <table class="min-w-full table-auto" id="transportados-table">
                    <thead class="bg-gray-50">
                        <tr>
                            <th scope="col" class="p-4 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                                <input type="checkbox" id="selectAllTransportados" class="rounded-sm">
                            </th>
                            <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider w-1/4">Matrícula</th>
                            <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider w-3/4">Nome</th>
                        </tr>
                    </thead>
                    <tbody class="bg-white divide-y divide-gray-200"></tbody>
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
                <h2 class="text-xl md:text-2xl font-bold text-gray-800 modal-title">Gerenciar Motoristas</h2>
                <button id="close-motoristas-modal" class="text-gray-500 hover:text-gray-800 text-xl font-bold">&times;</button>
            </div>
            <div class="flex flex-col md:flex-row gap-4 items-start md:items-center mb-4 md:mb-6">
                <span class="text-sm font-medium text-gray-700">Ordenar por:</span>
                <select id="sort-motoristas-order" class="w-full md:w-auto border border-gray-300 rounded-lg py-1 px-2 text-sm focus:outline-none focus:ring-2 focus:ring-blue-500">
                    <option value="asc">A-Z</option>
                    <option value="desc">Z-A</option>
                </select>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 items-end mb-6">
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
                            <th scope="col" class="p-4 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                                <input type="checkbox" id="selectAllMotoristas" class="rounded-sm">
                            </th>
                            <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider w-full">Nome</th>
                        </tr>
                    </thead>
                    <tbody class="bg-white divide-y divide-gray-200"></tbody>
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
        <div class="bg-white p-6 md:p-8 rounded-2xl shadow-2xl modal-content modal-lg max-h-[90vh] flex flex-col">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-xl md:text-2xl font-bold text-gray-800 modal-title">Gerenciar Lançamentos</h2>
                <button id="close-lancamentos-modal" class="text-gray-500 hover:text-gray-800 text-xl font-bold">&times;</button>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-4">
                <div>
                    <label for="filter-start-date" class="block text-sm font-medium text-gray-700">De:</label>
                    <input type="date" id="filter-start-date" class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-lg">
                </div>
                <div>
                    <label for="filter-end-date" class="block text-sm font-medium text-gray-700">Até:</label>
                    <input type="date" id="filter-end-date" class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-lg">
                </div>
                <div class="flex items-end">
                    <button id="apply-filter-btn" class="w-full px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700">Filtrar</button>
                </div>
            </div>
            <div class="overflow-y-auto flex-grow">
                <table class="min-w-full table-auto" id="lancamentos-table">
                    <thead class="bg-gray-50 sticky top-0">
                        <tr>
                            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Data</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Motorista</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Transportado</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Origem</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Destino</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Valor</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Ações</th>
                        </tr>
                    </thead>
                    <tbody class="bg-white divide-y divide-gray-200"></tbody>
                </table>
            </div>
        </div>
    </div>

    <div id="edit-lancamento-modal" class="fixed inset-0 bg-gray-800 bg-opacity-75 hidden flex items-center justify-center p-4 z-50">
      <div class="bg-white p-6 md:p-8 rounded-2xl shadow-2xl modal-content max-h-[90vh] overflow-y-auto">
        <div class="flex justify-between items-center mb-4">
          <h2 class="text-xl md:text-2xl font-bold text-gray-800 modal-title">Editar Lançamento</h2>
          <button id="close-edit-lancamento-modal" class="text-gray-500 hover:text-gray-800 text-xl font-bold">&times;</button>
        </div>
        <form id="edit-lancamento-form" class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <input type="hidden" id="edit-lancamento-id">
          <div class="md:col-span-2">
            <label for="edit-motorista" class="block text-sm font-medium text-gray-700">Motorista:</label>
            <input type="text" id="edit-motorista" list="motoristas-list" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
          </div>
          <div>
            <label for="edit-matricula" class="block text-sm font-medium text-gray-700">Matrícula:</label>
            <input type="text" id="edit-matricula" list="transportados-matricula-list" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
          </div>
          <div>
            <label for="edit-transportado" class="block text-sm font-medium text-gray-700">Transportado:</label>
            <input type="text" id="edit-transportado" list="transportados-nome-list" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
          </div>
          <div class="md:col-span-2">
            <label for="edit-data" class="block text-sm font-medium text-gray-700">Data:</label>
            <input type="date" id="edit-data" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
          </div>
          <div>
            <label for="edit-origem" class="block text-sm font-medium text-gray-700">Origem:</label>
            <input type="text" id="edit-origem" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
          </div>
           <div>
            <label for="edit-destino" class="block text-sm font-medium text-gray-700">Destino:</label>
            <input type="text" id="edit-destino" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
          </div>
          <div>
            <label for="edit-valor" class="block text-sm font-medium text-gray-700">Valor:</label>
            <input type="text" id="edit-valor" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg text-right">
          </div>
          <div>
            <label for="edit-valor-extra" class="block text-sm font-medium text-gray-700">Valor Extra:</label>
            <input type="text" id="edit-valor-extra" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg text-right">
          </div>
          <hr class="md:col-span-2 my-2">
          <div class="md:col-span-2 text-center text-sm font-medium text-gray-500">Passageiro Extra (Opcional)</div>
           <div>
            <label for="edit-matricula-extra" class="block text-sm font-medium text-gray-700">Matrícula Passageiro Extra:</label>
            <input type="text" id="edit-matricula-extra" list="transportados-matricula-list" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
          </div>
          <div>
            <label for="edit-transportado-extra" class="block text-sm font-medium text-gray-700">Nome Passageiro Extra:</label>
            <input type="text" id="edit-transportado-extra" list="transportados-nome-list" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
          </div>
          <div class="md:col-span-2">
            <label for="edit-observacao" class="block text-sm font-medium text-gray-700">Observação:</label>
            <textarea id="edit-observacao" rows="3" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg"></textarea>
          </div>
          <div id="admin-obs-container" class="md:col-span-2 hidden">
            <label for="edit-observacao-admin" class="block text-sm font-medium text-gray-700">Observação do Administrador:</label>
            <textarea id="edit-observacao-admin" rows="3" class="mt-1 block w-full px-3 py-2 bg-yellow-50 border border-gray-300 rounded-lg"></textarea>
          </div>
          <div class="md:col-span-2 flex justify-end gap-4 mt-6">
            <button type="button" id="cancel-edit-btn" class="px-4 py-2 bg-gray-300 text-gray-800 rounded-lg hover:bg-gray-400">Cancelar</button>
            <button type="submit" class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700">Salvar Alterações</button>
          </div>
        </form>
      </div>
    </div>
    
    <div id="message-modal" class="fixed inset-0 bg-gray-600 bg-opacity-50 hidden flex items-center justify-center">
        <div class="bg-white p-6 rounded-lg shadow-2xl max-w-sm w-full">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-xl font-bold text-gray-800 modal-title">Aviso</h2>
            </div>
            <p id="message-content" class="text-gray-700 mb-4 text-center"></p>
            <div class="flex justify-end">
                <button id="close-modal" class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700">OK</button>
            </div>
        </div>
    </div>

    <script type="module">
        // --- IMPORTAÇÕES E CONFIGURAÇÃO FIREBASE ---
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, addDoc, deleteDoc, onSnapshot, collection, doc, query, where, getDocs, updateDoc, serverTimestamp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

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

        // --- VARIÁVEIS GLOBAIS ---
        let globalUserId = null;
        let currentUser = { username: null, isAdmin: false };
        let transportadosData = [], motoristasData = [], lancamentosData = [];
        let matriculaToNome = {}, nomeToMatricula = {};

        // --- ELEMENTOS DOM ---
        const loginPage = document.getElementById('login-page');
        const appPage = document.getElementById('app-page');
        const loginForm = document.getElementById('login-form');
        const logoutButton = document.getElementById('logout-btn');
        const passageirosContainer = document.getElementById('passageiros-campos-container');
        const addPassageiroBtn = document.getElementById('add-passageiro-btn');
        const motoristaInput = document.getElementById('motorista');
        const valorInput = document.getElementById('valor');
        const valorExtraInput = document.getElementById('valor-extra');

        // --- FUNÇÕES UTILITÁRIAS ---
        const showWarning = (message) => {
            document.getElementById('message-content').innerText = message;
            document.getElementById('message-modal').classList.remove('hidden');
        };
        const hideWarning = () => document.getElementById('message-modal').classList.add('hidden');
        
        const formatCurrency = (value) => {
            if (isNaN(value) || value === null) return '0,00';
            const BRL = new Intl.NumberFormat('pt-BR', { style: 'currency', currency: 'BRL' });
            return BRL.format(value).replace('R$', '').trim();
        };
        const parseCurrency = (value) => {
            if (typeof value !== 'string' || value.trim() === '') return 0;
            return parseFloat(value.replace(/\./g, '').replace(',', '.')) || 0;
        };
        const formatCurrencyInputEvent = (event) => {
            let input = event.target;
            let value = input.value.replace(/\D/g, '');
            if (value === '') { input.value = ''; return; }
            value = (parseInt(value, 10) / 100);
            input.value = formatCurrency(value);
        };
        
        // --- LÓGICA DE LOGIN E AUTENTICAÇÃO ---
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

        logoutButton.addEventListener('click', () => signOut(auth).then(() => window.location.reload()));
        
        function setupUIForUser(username) {
            const userData = motoristaUsers[username];
            currentUser = { username, isAdmin: userData?.is_admin || false };
            
            document.getElementById('open-motoristas-modal').style.display = currentUser.isAdmin ? 'block' : 'none';

            if (userData?.is_motorista_fixo) {
                motoristaInput.value = userData.nome;
                motoristaInput.readOnly = true;
                motoristaInput.classList.add('bg-gray-200');
            } else {
                motoristaInput.readOnly = false;
                motoristaInput.classList.remove('bg-gray-200');
                motoristaInput.value = userData?.nome || '';
            }
        }
        
        // --- LISTENERS DO FIRESTORE ---
        function startFirestoreListeners() {
            const basePath = collection(db, 'artifacts', APP_ID, 'public', 'data');
            onSnapshot(collection(basePath, 'transportados'), (snapshot) => {
                transportadosData = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
                rebuildTransportadosLookups();
            });
            onSnapshot(collection(basePath, 'motoristas'), (snapshot) => {
                motoristasData = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
                populateMotoristasDatalist();
            });
            onSnapshot(query(collection(basePath, 'lancamentos')), (snapshot) => {
                lancamentosData = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
                if (!document.getElementById('lancamentos-modal').classList.contains('hidden')) {
                    renderLancamentosList();
                }
            });
        }
        
        function rebuildTransportadosLookups() {
            matriculaToNome = {};
            nomeToMatricula = {};
            transportadosData.forEach(item => {
                if (item.matricula) matriculaToNome[item.matricula] = item.nome;
                if (item.nome) nomeToMatricula[item.nome.toLowerCase()] = item.matricula;
            });
            populateTransportadosDatalist();
        }

        function populateDatalist(datalistId, data, valueField) {
            const datalist = document.getElementById(datalistId) || document.createElement('datalist');
            datalist.id = datalistId;
            if (!document.body.contains(datalist)) document.body.appendChild(datalist);
            datalist.innerHTML = data.map(item => `<option value="${item[valueField]}">`).join('');
        }

        function populateTransportadosDatalist() {
            populateDatalist('transportados-matricula-list', transportadosData, 'matricula');
            populateDatalist('transportados-nome-list', transportadosData, 'nome');
        }
        function populateMotoristasDatalist() {
            populateDatalist('motoristas-list', motoristasData, 'nome');
        }

        // --- LÓGICA DO FORMULÁRIO PRINCIPAL ---
        function handleAutofill(sourceInput, targetInput, sourceType) {
            const value = sourceInput.value.trim();
            if (value !== '') {
                let targetValue = '';
                if (sourceType === 'matricula') targetValue = matriculaToNome[value];
                else if (sourceType === 'nome') targetValue = nomeToMatricula[value.toLowerCase()];
                targetInput.value = targetValue || '';
            } else {
                targetInput.value = '';
            }
        }

        passageirosContainer.addEventListener('blur', (event) => {
            const input = event.target;
            const row = input.closest('.passageiro-row');
            if (!row || !input.name) return;

            const matriculaInput = row.querySelector('input[name="matriculas[]"]');
            const nomeInput = row.querySelector('input[name="transportados[]"]');
            if (input === matriculaInput) handleAutofill(matriculaInput, nomeInput, 'matricula');
            if (input === nomeInput) handleAutofill(nomeInput, matriculaInput, 'nome');
        }, true);
        
        function createPassageiroInput(index, isRequired = true) {
            const fieldset = document.createElement('div');
            fieldset.className = 'passageiro-row grid grid-cols-1 md:grid-cols-2 gap-4 md:gap-6';
            fieldset.innerHTML = `
                <div>
                    <label class="block text-sm font-medium text-gray-700">Matrícula (P${index + 1}):</label>
                    <input type="text" name="matriculas[]" list="transportados-matricula-list" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
                </div>
                <div class="flex items-end">
                    <div class="flex-grow">
                        <label class="block text-sm font-medium text-gray-700">Transportado (P${index + 1}):</label>
                        <input type="text" name="transportados[]" list="transportados-nome-list" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
                    </div>
                    ${!isRequired ? `<button type="button" class="ml-2 px-3 py-2 bg-red-500 text-white font-bold rounded-lg hover:bg-red-600 remove-passageiro-btn">-</button>` : ''}
                </div>`;
            return fieldset;
        }

        function addPassageiroRow(isRequired = false) {
            const index = passageirosContainer.children.length;
            const newRow = createPassageiroInput(index, isRequired);
            passageirosContainer.appendChild(newRow);
        }
        
        addPassageiroBtn.addEventListener('click', () => addPassageiroRow(false));
        passageirosContainer.addEventListener('click', (e) => {
            if (e.target.classList.contains('remove-passageiro-btn')) {
                e.target.closest('.passageiro-row').remove();
            }
        });

        document.getElementById('form-corrida').addEventListener('submit', async (event) => {
            event.preventDefault();
            const form = event.target;
            
            const passageirosInputs = Array.from(passageirosContainer.querySelectorAll('.passageiro-row'));
            const passageirosData = passageirosInputs.map(row => ({
                matricula: row.querySelector('input[name="matriculas[]"]').value.trim(),
                nome: row.querySelector('input[name="transportados[]"]').value.trim()
            })).filter(p => p.matricula && p.nome);

            if (passageirosData.length === 0) {
                showWarning('É necessário preencher pelo menos um passageiro com matrícula e nome.');
                return;
            }

            const newEntry = {
                userId: globalUserId,
                createdBy: currentUser.username,
                motorista: form['motorista'].value,
                matricula: passageirosData[0].matricula, 
                transportado: passageirosData[0].nome, 
                passageiros_extras: passageirosData.length > 1 ? passageirosData.slice(1) : null,
                solicitante: form['solicitante'].value,
                data: form['data'].value,
                origem: form['origem'].value,
                partida: form['partida'].value,
                destino: form['destino'].value,
                chegada: form['chegada'].value,
                valor: parseCurrency(form['valor'].value),
                valorExtra: parseCurrency(form['valor-extra'].value),
                observacao: form['observacao'].value,
                createdAt: serverTimestamp()
            };

            const lancamentosRef = collection(db, 'artifacts', APP_ID, 'public', 'data', 'lancamentos');
            await addDoc(lancamentosRef, newEntry);
            showWarning('Lançamento salvo com sucesso!');
            form.reset();
            valorInput.value = '';
            valorExtraInput.value = '';
            passageirosContainer.innerHTML = '';
            addPassageiroRow(true);
        });

        // --- LÓGICA DO MODAL DE LANÇAMENTOS ---
        document.getElementById('open-lancamentos-modal').addEventListener('click', () => {
            renderLancamentosList();
            document.getElementById('lancamentos-modal').classList.remove('hidden');
        });
        document.getElementById('close-lancamentos-modal').addEventListener('click', () => document.getElementById('lancamentos-modal').classList.add('hidden'));
        document.getElementById('apply-filter-btn').addEventListener('click', renderLancamentosList);

        function renderLancamentosList() {
            const tableBody = document.querySelector('#lancamentos-table tbody');
            const startDate = document.getElementById('filter-start-date').value;
            const endDate = document.getElementById('filter-end-date').value;

            let dataToShow = lancamentosData;
            if (!currentUser.isAdmin) dataToShow = dataToShow.filter(lanc => lanc.userId === globalUserId);
            if (startDate) dataToShow = dataToShow.filter(lanc => lanc.data >= startDate);
            if (endDate) dataToShow = dataToShow.filter(lanc => lanc.data <= endDate);
            
            dataToShow.sort((a, b) => new Date(b.data) - new Date(a.data));
            
            tableBody.innerHTML = dataToShow.length === 0 ? '<tr><td colspan="7" class="text-center p-4">Nenhum lançamento encontrado.</td></tr>' :
                dataToShow.map(item => `
                    <tr class="bg-white hover:bg-gray-50">
                        <td class="px-6 py-4 text-sm whitespace-nowrap">${item.data}</td>
                        <td class="px-6 py-4 text-sm whitespace-nowrap">${item.motorista}</td>
                        <td class="px-6 py-4 text-sm whitespace-nowrap">${item.transportado}</td>
                        <td class="px-6 py-4 text-sm whitespace-nowrap">${item.origem}</td>
                        <td class="px-6 py-4 text-sm whitespace-nowrap">${item.destino}</td>
                        <td class="px-6 py-4 text-sm whitespace-nowrap">R$ ${formatCurrency(item.valor)}</td>
                        <td class="px-6 py-4"><button data-id="${item.id}" class="edit-lancamento-btn text-blue-600 hover:text-blue-900"><svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 pointer-events-none" viewBox="0 0 20 20" fill="currentColor"><path d="M17.414 2.586a2 2 0 00-2.828 0L7 10.172V13h2.828l7.586-7.586a2 2 0 000-2.828z" /><path fill-rule="evenodd" d="M2 6a2 2 0 012-2h4a1 1 0 010 2H4v10h10v-4a1 1 0 112 0v4a2 2 0 01-2 2H4a2 2 0 01-2-2V6z" clip-rule="evenodd" /></svg></button></td>
                    </tr>`).join('');
        }

        // --- LÓGICA DO MODAL DE EDIÇÃO ---
        document.getElementById('lancamentos-table').addEventListener('click', (event) => {
            const btn = event.target.closest('.edit-lancamento-btn');
            if (btn) openEditLancamentoModal(btn.dataset.id);
        });

        function openEditLancamentoModal(id) {
            const lancamento = lancamentosData.find(l => l.id === id);
            if (!lancamento) return;
            
            const form = document.getElementById('edit-lancamento-form');
            form.reset();

            form.querySelector('#edit-lancamento-id').value = id;
            form.querySelector('#edit-motorista').value = lancamento.motorista;
            form.querySelector('#edit-matricula').value = lancamento.matricula;
            form.querySelector('#edit-transportado').value = lancamento.transportado;
            form.querySelector('#edit-data').value = lancamento.data;
            form.querySelector('#edit-origem').value = lancamento.origem;
            form.querySelector('#edit-destino').value = lancamento.destino;
            form.querySelector('#edit-valor').value = formatCurrency(lancamento.valor);
            form.querySelector('#edit-valor-extra').value = formatCurrency(lancamento.valorExtra);
            form.querySelector('#edit-observacao').value = lancamento.observacao || '';
            form.querySelector('#edit-observacao-admin').value = lancamento.observacaoAdmin || '';
            
            const extra = lancamento.passageiros_extras?.[0];
            form.querySelector('#edit-matricula-extra').value = extra?.matricula || '';
            form.querySelector('#edit-transportado-extra').value = extra?.nome || '';
            
            const motoristaInput = form.querySelector('#edit-motorista');
            const adminObsContainer = document.getElementById('admin-obs-container');
            motoristaInput.readOnly = !currentUser.isAdmin;
            motoristaInput.classList.toggle('bg-gray-200', !currentUser.isAdmin);
            adminObsContainer.classList.toggle('hidden', !currentUser.isAdmin);
            
            document.getElementById('edit-lancamento-modal').classList.remove('hidden');
        }

        ['edit-matricula', 'edit-transportado', 'edit-matricula-extra', 'edit-transportado-extra'].forEach(id => {
            const el = document.getElementById(id);
            el.addEventListener('blur', (e) => {
                const isMatricula = e.target.id.includes('matricula');
                const targetId = isMatricula ? e.target.id.replace('matricula', 'transportado') : e.target.id.replace('transportado', 'matricula');
                handleAutofill(e.target, document.getElementById(targetId), isMatricula ? 'matricula' : 'nome');
            });
        });

        const closeEditModal = () => document.getElementById('edit-lancamento-modal').classList.add('hidden');
        document.getElementById('close-edit-lancamento-modal').addEventListener('click', closeEditModal);
        document.getElementById('cancel-edit-btn').addEventListener('click', closeEditModal);
        
        document.getElementById('edit-lancamento-form').addEventListener('submit', async (event) => {
            event.preventDefault();
            const form = event.target;
            const id = form.querySelector('#edit-lancamento-id').value;
            
            const extraMatricula = form.querySelector('#edit-matricula-extra').value.trim();
            const extraNome = form.querySelector('#edit-transportado-extra').value.trim();
            
            let obs = form.querySelector('#edit-observacao').value;
            let adminObs = form.querySelector('#edit-observacao-admin').value;

            if (currentUser.isAdmin) {
                if (!adminObs.includes('(editado por admin)')) adminObs = `${adminObs} (editado por admin)`.trim();
            } else {
                 if (!obs.includes('(editado)')) obs = `${obs} (editado)`.trim();
            }
            
            const updatedData = {
                motorista: form.querySelector('#edit-motorista').value,
                matricula: form.querySelector('#edit-matricula').value,
                transportado: form.querySelector('#edit-transportado').value,
                data: form.querySelector('#edit-data').value,
                origem: form.querySelector('#edit-origem').value,
                destino: form.querySelector('#edit-destino').value,
                valor: parseCurrency(form.querySelector('#edit-valor').value),
                valorExtra: parseCurrency(form.querySelector('#edit-valor-extra').value),
                passageiros_extras: (extraMatricula && extraNome) ? [{ matricula: extraMatricula, nome: extraNome }] : null,
                observacao: obs,
                observacaoAdmin: adminObs
            };
            
            const docRef = doc(db, 'artifacts', APP_ID, 'public', 'data', 'lancamentos', id);
            await updateDoc(docRef, updatedData);
            
            showWarning('Lançamento atualizado!');
            closeEditModal();
        });
        
        // --- CRUD MODAIS ANTIGOS (TRANSPORTADOS, MOTORISTAS) ---
        document.getElementById('open-transportados-modal').addEventListener('click', () => document.getElementById('transportados-modal').classList.remove('hidden'));
        document.getElementById('close-transportados-modal').addEventListener('click', () => document.getElementById('transportados-modal').classList.add('hidden'));
        document.getElementById('open-motoristas-modal').addEventListener('click', () => document.getElementById('motoristas-modal').classList.remove('hidden'));
        document.getElementById('close-motoristas-modal').addEventListener('click', () => document.getElementById('motoristas-modal').classList.add('hidden'));

        // ... (restante do código para gerenciar motoristas e transportados)

        // --- INICIALIZAÇÃO ---
        window.onload = () => {
            onAuthStateChanged(auth, async (user) => {
                if (user) {
                    globalUserId = user.uid;
                    startFirestoreListeners();
                } else {
                    signInAnonymously(auth).catch(console.error);
                }
            });
            document.getElementById('close-modal').addEventListener('click', hideWarning);
            addPassageiroRow(true);
            [valorInput, valorExtraInput, document.getElementById('edit-valor'), document.getElementById('edit-valor-extra')].forEach(input => {
                input.addEventListener('input', formatCurrencyInputEvent);
                input.addEventListener('focus', () => { if (parseCurrency(input.value) === 0) input.value = ''; });
                input.addEventListener('blur', () => { if (input.value.trim() === '') input.value = formatCurrency(0); });
            });
        };
    </script>
</body>
</html>
