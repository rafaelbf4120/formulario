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
        /* Custom style for larger modal */
        .modal-lg {
            max-width: 80rem;
/* max-w-6xl */
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
                <input type="password" id="password" name="password" class="mt-1 block w-full px-3 py-2 bg-gray-50 border 
border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out">
            </div>
            <button type="submit" class="w-full px-6 py-3 bg-blue-600 text-white font-bold rounded-lg shadow-lg hover:bg-blue-700 focus:outline-none focus:ring-4 focus:ring-blue-500 focus:ring-opacity-50 transition duration-150 ease-in-out">
                Entrar
            </button>
            <p id="login-message" class="text-red-500 text-sm text-center mt-2 hidden">Usuário ou senha inválidos.</p>
 
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
            
            <div 
id="passageiros-campos-container" class="md:col-span-2 grid grid-cols-1 md:grid-cols-2 gap-4 md:gap-6">
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
                <input type="text" id="origem" name="origem" onfocus="this.classList.remove('error-border')" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition 
duration-150 ease-in-out">
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
                <label 
for="valor" class="block text-sm font-medium text-gray-700">Valor:</label>
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
                <label for="observacao" class="block 
text-sm font-medium text-gray-700">Observação:</label>
                <textarea id="observacao" name="observacao" rows="4" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-150 ease-in-out"></textarea>
            </div>
            
            <div class="md:col-span-2 flex justify-center mt-4">
                <button type="submit" class="w-full md:w-1/2 px-6 py-3 
bg-blue-600 text-white font-bold rounded-lg shadow-lg hover:bg-blue-700 focus:outline-none focus:ring-4 focus:ring-blue-500 focus:ring-opacity-50 transition duration-150 ease-in-out">
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
                <h2 class="text-xl md:text-2xl font-bold text-gray-800">Gerenciar Transportados</h2>
     
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
                    <label 
for="new-nome" class="block text-sm font-medium text-gray-700">Novo Transportado:</label>
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
                <button id="close-motoristas-modal" class="text-gray-500 
hover:text-gray-800 text-xl font-bold">&times;</button>
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
   
     <div class="bg-white p-6 md:p-8 rounded-2xl shadow-2xl modal-content modal-lg max-h-[90vh] flex flex-col">
            <div class="flex justify-between items-center mb-4 relative">
                <div class="flex-grow flex justify-center">
                    <h2 class="text-xl md:text-2xl font-bold text-gray-800">Gerenciar Lançamentos</h2>
                </div>
                <button id="close-lancamentos-modal" class="absolute top-0 right-0 text-gray-500 hover:text-gray-800 text-xl font-bold">&times;</button>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-4">
                <div>
                    <label for="filter-start-date" class="block text-sm font-medium text-gray-700">De:</label>
                    <input type="date" id="filter-start-date" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
                </div>
                <div>
                    <label for="filter-end-date" class="block text-sm font-medium text-gray-700">Até:</label>
                    <input type="date" id="filter-end-date" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
                </div>
                <div class="flex items-end">
                    <button id="filter-lancamentos-btn" class="w-full px-4 py-2 bg-blue-600 text-white font-bold rounded-lg hover:bg-blue-700">Filtrar</button>
                </div>
            </div>

            <div class="overflow-y-auto flex-grow">
 
               <table class="min-w-full table-auto" id="lancamentos-table">
                    <thead class="bg-gray-50 sticky top-0">
                        <tr>
                            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 
uppercase tracking-wider">Data</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Motorista</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Transportado</th>
                           
 <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Origem</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Destino</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Valor</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Status</th>
                   
         <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Ações</th>
                        </tr>
                    </thead>
                    <tbody class="bg-white divide-y divide-gray-200">
                
        </tbody>
                </table>
            </div>
        </div>
    </div>
    
    <div id="edit-lancamento-modal" class="fixed inset-0 bg-gray-800 bg-opacity-75 hidden flex items-center justify-center p-4 z-50">
      <div class="bg-white p-6 md:p-8 rounded-2xl shadow-2xl modal-content max-h-[90vh] overflow-y-auto">
        <div class="flex justify-between items-center mb-4 relative">
            <div class="flex-grow flex justify-center">
       
   <h2 class="text-xl md:text-2xl font-bold text-gray-800">Editar Lançamento</h2>
            </div>
          <button id="close-edit-lancamento-modal" class="absolute top-0 right-0 text-gray-500 hover:text-gray-800 text-xl font-bold">&times;</button>
        </div>
        <form id="edit-lancamento-form" class="space-y-4">
          <input type="hidden" id="edit-lancamento-id">
          
          <div>
            <label for="edit-motorista" class="block text-sm font-medium text-gray-700">Motorista:</label>
            <input type="text" id="edit-motorista" list="motoristas-list" class="mt-1 block w-full px-3 py-2 
bg-gray-50 border border-gray-300 rounded-lg">
          </div>

          <div>
            <label for="edit-data" class="block text-sm 
font-medium text-gray-700">Data:</label>
            <input type="date" id="edit-data" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
          </div>

          <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            <div>
              <label for="edit-matricula" class="block text-sm font-medium text-gray-700">Matrícula (P1):</label>
              <input type="text" id="edit-matricula" name="edit-matriculas[]" list="transportados-matricula-list" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
            </div>
            <div>
              <label for="edit-transportado" class="block text-sm font-medium text-gray-700">Transportado (P1):</label>
              <input type="text" id="edit-transportado" name="edit-transportados[]" list="transportados-nome-list" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
            </div>
          </div>
          
          <div id="edit-passageiros-extras-container" class="space-y-4">
          </div>

          <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
              <div>
                <label for="edit-origem" class="block text-sm font-medium text-gray-700">Origem:</label>
                <input type="text" id="edit-origem" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
              </div>
      
     <div>
                <label for="edit-destino" class="block text-sm font-medium text-gray-700">Destino:</label>
                <input type="text" id="edit-destino" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
              </div>
          </div>
          
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            <div>
              <label for="edit-valor" class="block text-sm font-medium text-gray-700">Valor:</label>
              <div class="relative mt-1">
                <span class="absolute inset-y-0 left-0 flex items-center pl-3 pr-2 text-gray-400">R$</span>
                <input type="text" id="edit-valor" class="block w-full px-3 py-2 pl-9 bg-gray-50 border border-gray-300 rounded-lg text-right">
              </div>
            </div>
            <div>
              <label for="edit-valor-extra" class="block text-sm font-medium text-gray-700">Valor Extra:</label>
              <div class="relative mt-1">
                <span class="absolute inset-y-0 left-0 flex items-center pl-3 pr-2 text-gray-400">R$</span>
                <input type="text" id="edit-valor-extra" class="block w-full px-3 py-2 pl-9 bg-gray-50 border border-gray-300 rounded-lg text-right">
              </div>
            </div>
          </div>

          <div>
            <label for="edit-observacao" class="block text-sm font-medium text-gray-700">Observação:</label>
            <textarea id="edit-observacao" rows="3" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg"></textarea>
          </div>
          
          <div class="flex justify-end gap-4 mt-6">
            <button type="button" id="cancel-edit-btn" class="px-4 py-2 bg-gray-300 text-gray-800 rounded-lg hover:bg-gray-400">Cancelar</button>
            <button type="submit" class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700">Salvar Alterações</button>
          </div>
        </form>
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

        const globalAppId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
let globalUserId = null;
        let currentUser = {
            username: null,
            isAdmin: false,
        };
// ELEMENTOS DOM
        const loginForm = document.getElementById('login-form');
        const loginPage = document.getElementById('login-page');
const appPage = document.getElementById('app-page');
        const loginMessage = document.getElementById('login-message');
        const userIdDisplay = document.getElementById('user-id-display');
        const logoutButton = document.getElementById('logout-btn');
        const motoristaInput = document.getElementById('motorista');
const openMotoristasBtn = document.getElementById('open-motoristas-modal');
        const passageirosContainer = document.getElementById('passageiros-campos-container');
        const addPassageiroBtn = document.getElementById('add-passageiro-btn');
        const valorInput = document.getElementById('valor');
        const valorExtraInput = document.getElementById('valor-extra');
// === CONFIGURAÇÃO DE USUÁRIOS ===
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
let transportadosData = [];
        let motoristasData = [];
        let lancamentosData = [];
        let matriculaToNome = {};
        let nomeToMatricula = {};
// === FUNÇÕES DE VALIDAÇÃO E INTERFACE ===

        function showWarning(message) {
            document.getElementById('message-content').innerText = message;
document.getElementById('message-modal').classList.remove('hidden');
        }

        function hideWarning() {
            document.getElementById('message-modal').classList.add('hidden');
}
        
        function setMotoristaReadOnly(username) {
            const userData = motoristaUsers[username];
currentUser.username = username;
            currentUser.isAdmin = userData ? userData.is_admin : false;
if (userData && userData.is_admin) {
                openMotoristasBtn.classList.remove('hidden');
} else {
                openMotoristasBtn.classList.add('hidden');
}
            
            if (userData && userData.is_motorista_fixo) {
                motoristaInput.value = userData.nome;
motoristaInput.setAttribute('readonly', 'readonly');
                motoristaInput.classList.add('bg-gray-200');
            } else {
                motoristaInput.removeAttribute('readonly');
motoristaInput.classList.remove('bg-gray-200');
                 if (userData) {
                     motoristaInput.value = userData.nome;
} else {
                     motoristaInput.value = '';
}
            }
        }

        function checkPassageiroDuplicidade(sourceInput) {
            const rows = document.querySelectorAll('#passageiros-campos-container .passageiro-row');
const row = sourceInput.closest('.passageiro-row');
            const currentMatriculaInput = row.querySelector('input[name="matriculas[]"]');
            const currentNomeInput = row.querySelector('input[name="transportados[]"]');
            const currentMatricula = currentMatriculaInput.value.trim();
            const currentNome = currentNomeInput.value.trim();
if (currentMatricula === '' || currentNome === '') {
                currentMatriculaInput.classList.remove('error-border');
currentNomeInput.classList.remove('error-border');
                return false; 
            }

            const currentKey = `${currentMatricula}_${currentNome.toLowerCase()}`;
let isDuplicated = false;

            rows.forEach(r => {
                r.querySelector('input[name="matriculas[]"]').classList.remove('error-border');
                r.querySelector('input[name="transportados[]"]').classList.remove('error-border');
            });
rows.forEach(rowToCheck => {
                const rowMatricula = rowToCheck.querySelector('input[name="matriculas[]"]').value.trim();
                const rowNome = rowToCheck.querySelector('input[name="transportados[]"]').value.trim();
                const rowKey = `${rowMatricula}_${rowNome.toLowerCase()}`;
                const isSameRow = (rowToCheck === row);

                if (rowKey === currentKey 
&& !isSameRow) {
                    isDuplicated = true;
                    rowToCheck.querySelector('input[name="matriculas[]"]').classList.add('error-border');
                    rowToCheck.querySelector('input[name="transportados[]"]').classList.add('error-border');
                }
            });
if (isDuplicated) {
                currentMatriculaInput.classList.add('error-border');
                currentNomeInput.classList.add('error-border');
showWarning(`Passageiro duplicado encontrado: Matrícula ${currentMatricula} e Nome ${currentNome}.`);
            }

            return isDuplicated;
}

        function handleAutofillDynamic(sourceInput, targetInput, sourceType) {
            const value = sourceInput.value.trim();
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
                targetInput.value = '';
}

            setTimeout(() => checkPassageiroDuplicidade(sourceInput), 50);
}

        function updatePassageiroLabels() {
            const rows = document.querySelectorAll('#passageiros-campos-container .passageiro-row');
rows.forEach((row, index) => {
                const pNum = index + 1;
                const matriculaLabel = row.querySelector(`label[for^="matricula-"]`);
                const transportadoLabel = row.querySelector(`label[for^="transportado-"]`);
                
                if(matriculaLabel) matriculaLabel.textContent = `Matrícula (P${pNum}):`;
  
              if(transportadoLabel) transportadoLabel.textContent = `Transportado (P${pNum}):`;
                
                const removeBtn = row.querySelector('.remove-passageiro-btn');
                if (removeBtn) {
                    removeBtn.onclick = () => {
     
                   row.remove();
                        updatePassageiroLabels();
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
                    ${!isRequired ?
`<button type="button" class="ml-2 px-3 py-2 bg-red-500 text-white font-bold rounded-lg shadow-md hover:bg-red-600 remove-passageiro-btn">-</button>` : ''}
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

        window.onload = () => {
            function bindPassageiroListeners() {
                passageirosContainer.addEventListener('blur', (event) => {
                    const input = event.target;
                    if (input.matches('input[name="matriculas[]"]') || input.matches('input[name="transportados[]"]')) {
 
                       const row = input.closest('.passageiro-row');
                        const matriculaInput = row.querySelector('input[name="matriculas[]"]');
                        const nomeInput = row.querySelector('input[name="transportados[]"]');
                    
    if (input.name === 'matriculas[]') {
                            handleAutofillDynamic(matriculaInput, nomeInput, 'matricula');
                        } else if (input.name === 'transportados[]') {
                            handleAutofillDynamic(nomeInput, matriculaInput, 'nome');
  
                      }
                    }
                }, true);
}

            addPassageiroRow(true);
            bindPassageiroListeners();
            addPassageiroBtn.addEventListener('click', () => addPassageiroRow(false));
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
                    startFirestoreListeners();
           
     } else {
                    loginPage.classList.remove('hidden');
                    appPage.classList.add('hidden');
                }
            });
signInAnonymously(auth).catch((error) => console.error("Erro no login anônimo:", error));
        };

        loginForm.addEventListener('submit', function(event) {
            event.preventDefault();
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            const foundUser = users.find(user => user.username === username && user.password === password);
            if (foundUser) {
           
     loginPage.classList.add('hidden');
                appPage.classList.remove('hidden');
                setMotoristaReadOnly(username);
            } else {
                loginMessage.classList.remove('hidden');
            }
        });
logoutButton.addEventListener('click', () => {
            signOut(auth).then(() => {
                 window.location.reload();
            });
        });
function startFirestoreListeners() {
            const transportadosRef = collection(db, 'artifacts', globalAppId, 'public', 'data', 'transportados');
onSnapshot(transportadosRef, (snapshot) => {
                transportadosData = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
                rebuildTransportadosLookups();
            });
const motoristasRef = collection(db, 'artifacts', globalAppId, 'public', 'data', 'motoristas');
            onSnapshot(motoristasRef, (snapshot) => {
                motoristasData = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
                rebuildMotoristasLookups();
            });
const lancamentosRef = collection(db, 'artifacts', globalAppId, 'public', 'data', 'lancamentos');
            onSnapshot(lancamentosRef, (snapshot) => {
                lancamentosData = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
            });
}
        
        function rebuildTransportadosLookups(sortKey = 'nome', sortOrder = 'asc') {
            transportadosData.sort((a, b) => {
                let valA = a[sortKey] || '';
                let valB = b[sortKey] || '';
                return sortOrder === 'asc' 
? valA.localeCompare(valB, undefined, { numeric: true }) : valB.localeCompare(valA, undefined, { numeric: true });
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
            motoristasData.sort((a, b) => sortOrder === 'asc' ? a.nome.localeCompare(b.nome) : b.nome.localeCompare(a.nome));
renderMotoristasList();
            populateMotoristasDatalist();
        }
        
        function formatCurrencyInput(input) {
            if (!input) return;
            let value = input.value.replace(/\D/g, '');
if (value === '') {
                input.value = '0,00';
                return;
            }
            value = value.padStart(3, '0');
            const integerPart = value.slice(0, -2);
            const decimalPart = value.slice(-2);
const formattedInteger = parseInt(integerPart, 10).toLocaleString('pt-BR');
            input.value = `${formattedInteger},${decimalPart}`;
        }
        
        function parseCurrencyValue(value) {
            if (typeof value !== 'string' || value.trim() === '') return 0;
            return parseFloat(value.replace(/\./g, '').replace(',', '.'));
}

        document.getElementById('form-corrida').addEventListener('submit', async function(event) {
            event.preventDefault();
            const form = event.target;
            const requiredFields = ['motorista', 'solicitante', 'data', 'origem', 'partida', 'destino', 'chegada', 'valor'];
            const matriculasInputs = document.querySelectorAll('#passageiros-campos-container input[name="matriculas[]"]');
            const transportadosInputs = document.querySelectorAll('#passageiros-campos-container input[name="transportados[]"]');
        
    const passageirosData = [];
            let isFormValid = true;
            const passageirosSet = new Set();
            
            requiredFields.forEach(field => {
                const input = form[field];
                if 
(input.value.trim() === '') {
                    isFormValid = false;
                    input.classList.add('error-border');
                } else {
                    input.classList.remove('error-border');
}
            });
for (let i = 0; i < matriculasInputs.length; i++) {
                const matriculaInput = matriculasInputs[i];
const nomeInput = transportadosInputs[i];
                const matricula = matriculaInput.value.trim();
                const nome = nomeInput.value.trim();
                
                matriculaInput.classList.remove('error-border');
                nomeInput.classList.remove('error-border');
if (matricula !== '' && nome !== '') {
                    const key = `${matricula}_${nome.toLowerCase()}`;
if (passageirosSet.has(key)) {
                        isFormValid = false;
matriculaInput.classList.add('error-border');
                        nomeInput.classList.add('error-border');
                        showWarning(`Passageiro duplicado: ${nome}.`);
                        return;
                    }
                    passageirosSet.add(key);
passageirosData.push({ matricula: matricula, nome: nome });
                } else if (matricula !== '' || nome !== '') {
                    isFormValid = false;
if (matricula === '') matriculaInput.classList.add('error-border');
                    if (nome === '') nomeInput.classList.add('error-border');
}
            }
            
            if (passageirosData.length === 0) {
                isFormValid = false;
if (matriculasInputs[0]) matriculasInputs[0].classList.add('error-border');
                if (transportadosInputs[0]) transportadosInputs[0].classList.add('error-border');
            }

            if (!isFormValid) {
                showWarning('Preencha todos os campos obrigatórios.');
return;
            }

            const newEntry = {
                userId: globalUserId,
                createdBy: currentUser.username,
                motorista: form['motorista'].value,
                matricula: passageirosData[0].matricula,
                
transportado: passageirosData[0].nome,
                passageiros_extras: passageirosData.length > 1 ?
passageirosData.slice(1) : [],
                solicitante: form['solicitante'].value,
                data: form['data'].value,
                origem: form['origem'].value,
                partida: form['partida'].value,
                destino: form['destino'].value,
             
   chegada: form['chegada'].value,
                valor: parseCurrencyValue(form['valor'].value),
                valorExtra: form['valor-extra'].value ?
parseCurrencyValue(form['valor-extra'].value) : 0,
                observacao: form['observacao'].value,
                createdAt: serverTimestamp()
            };
const lancamentosRef = collection(db, 'artifacts', globalAppId, 'public', 'data', 'lancamentos');
            await addDoc(lancamentosRef, newEntry);

            showWarning('Lançamento salvo com sucesso!');
            form.reset();
            document.getElementById('valor').value = '0,00';
document.getElementById('valor-extra').value = '0,00';
            passageirosContainer.innerHTML = '';
            addPassageiroRow(true);
        });

        document.getElementById('download-csv').addEventListener('click', async function() {
            const startDate = document.getElementById('start-date').value;
            const endDate = document.getElementById('end-date').value;

            if (startDate && endDate && new Date(startDate) > new Date(endDate)) {
                showWarning('A data de início não pode ser posterior à data de fim.');
          
      return;
            }

            let dataToDownload = lancamentosData;
            // Filtra por data
            if (startDate || endDate) {
                dataToDownload = dataToDownload.filter(item => {
                
    const itemDate = new Date(item.data);
                    const start = startDate ? new Date(startDate) : null;
                    const end = endDate ? new Date(endDate) : null;
                    if(start && itemDate < start) return false;
          
          if(end && itemDate > end) return false;
                    return true;
});
            }

            // Filtra por usuário se não for admin
            if (!currentUser.isAdmin) {
                dataToDownload = dataToDownload.filter(item => item.userId === globalUserId);
}
            
            if (dataToDownload.length === 0) {
                showWarning('Nenhum dado encontrado para este período/permissão.');
return;
            }
            
            const bom = '\uFEFF';
const headers = ['data', 'motorista', 'transportado', 'matricula', 'origem', 'destino', 'valor'];
            const rows = dataToDownload.map(obj => headers.map(key => `"${obj[key] ?? ''}"`).join(';')).join('\n');
const csvContent = `${headers.join(';')}\n${rows}`;
            const blob = new Blob([bom + csvContent], { type: 'text/csv;charset=utf-8;' });
            const url = URL.createObjectURL(blob);
const link = document.createElement('a');
            link.href = url;
            link.download = `lancamentos_${new Date().toISOString().split('T')[0]}.csv`;
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        });
// --- LÓGICA DO MODAL DE LANÇAMENTOS ---
        
        document.getElementById('open-lancamentos-modal').addEventListener('click', () => {
            document.getElementById('filter-start-date').value = '';
            document.getElementById('filter-end-date').value = '';
            renderLancamentosList();
            document.getElementById('lancamentos-modal').classList.remove('hidden');
        });
document.getElementById('close-lancamentos-modal').addEventListener('click', () => {
            document.getElementById('lancamentos-modal').classList.add('hidden');
        });
        document.getElementById('filter-lancamentos-btn').addEventListener('click', renderLancamentosList);

function renderLancamentosList() {
            const tableBody = document.querySelector('#lancamentos-table tbody');
tableBody.innerHTML = '';
            
            let dataToShow = lancamentosData;

            if (!currentUser.isAdmin) {
                dataToShow = lancamentosData.filter(lanc => lanc.userId === globalUserId);
}

            const startDate = document.getElementById('filter-start-date').value;
            const endDate = document.getElementById('filter-end-date').value;

            if (startDate || endDate) {
                dataToShow = dataToShow.filter(item => {
                    if (!item.data) return false;
                    const itemDate = new Date(item.data + "T00:00:00"); // Treat date as local timezone
                    const start = startDate ? new Date(startDate + "T00:00:00") : null;
                    const end = endDate ? new Date(endDate + "T00:00:00") : null;
                    if (start && itemDate < start) return false;
                    if (end && itemDate > end) return false;
                    return true;
                });
            }
            
            dataToShow.sort((a,b) => new Date(b.data) - new Date(a.data));

if(dataToShow.length === 0){
                tableBody.innerHTML = '<tr><td colspan="8" class="text-center p-4">Nenhum lançamento encontrado.</td></tr>';
return;
            }
            
            dataToShow.forEach(item => {
                const row = document.createElement('tr');
                row.className = 'bg-white hover:bg-gray-50';
                const statusText = item.editedBy ? `<span class="text-xs text-gray-500">Editado por ${item.editedBy}</span>` : '';
                row.innerHTML = `
                 
   <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${item.data}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${item.motorista}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${item.transportado}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${item.origem}</td>
                 
   <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${item.destino}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">R$ ${(item.valor || 0).toFixed(2).replace('.',',')}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${statusText}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                        <button data-id="${item.id}" class="edit-lancamento-btn text-blue-600 hover:text-blue-900">
             
               <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor"><path d="M17.414 2.586a2 2 0 00-2.828 0L7 10.172V13h2.828l7.586-7.586a2 2 0 000-2.828z" /><path fill-rule="evenodd" d="M2 6a2 2 0 012-2h4a1 1 0 010 2H4v10h10v-4a1 1 0 112 0v4a2 2 0 01-2 2H4a2 2 0 01-2-2V6z" clip-rule="evenodd" /></svg>
                        </button>
                   
 </td>
                `;
                tableBody.appendChild(row);
            });
}
        
        document.getElementById('lancamentos-table').addEventListener('click', function(event) {
            const editButton = event.target.closest('.edit-lancamento-btn');
            if (editButton) {
                const lancamentoId = editButton.dataset.id;
                openEditLancamentoModal(lancamentoId);
  
          }
        });
function openEditLancamentoModal(id) {
            const lancamento = lancamentosData.find(l => l.id === id);
if (!lancamento) return;
            
            document.getElementById('edit-lancamento-id').value = id;
            document.getElementById('edit-data').value = lancamento.data;
            document.getElementById('edit-origem').value = lancamento.origem;
document.getElementById('edit-destino').value = lancamento.destino;
            document.getElementById('edit-observacao').value = lancamento.observacao || '';
            
            const motoristaInput = document.getElementById('edit-motorista');
            motoristaInput.value = lancamento.motorista;
            if (!currentUser.isAdmin) {
                motoristaInput.setAttribute('readonly', 'readonly');
                motoristaInput.classList.add('bg-gray-200');
            } else {
                motoristaInput.removeAttribute('readonly');
                motoristaInput.classList.remove('bg-gray-200');
            }

            document.getElementById('edit-matricula').value = lancamento.matricula || '';
            document.getElementById('edit-transportado').value = lancamento.transportado || '';
            
            const valorInput = document.getElementById('edit-valor');
            valorInput.value = (lancamento.valor || 0).toFixed(2).replace('.', ',');
            formatCurrencyInput(valorInput);

            const valorExtraInput = document.getElementById('edit-valor-extra');
            valorExtraInput.value = (lancamento.valorExtra || 0).toFixed(2).replace('.', ',');
            formatCurrencyInput(valorExtraInput);
            
            const extrasContainer = document.getElementById('edit-passageiros-extras-container');
            extrasContainer.innerHTML = '';
            if (lancamento.passageiros_extras && lancamento.passageiros_extras.length > 0) {
                lancamento.passageiros_extras.forEach((p, index) => {
                    const pNum = index + 2;
                    const fieldset = document.createElement('div');
                    fieldset.className = 'grid grid-cols-1 md:grid-cols-2 gap-4';
                    fieldset.innerHTML = `
                        <div>
                            <label class="block text-sm font-medium text-gray-700">Matrícula (P${pNum}):</label>
                            <input type="text" name="edit-matriculas[]" list="transportados-matricula-list" value="${p.matricula}" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700">Transportado (P${pNum}):</label>
                            <input type="text" name="edit-transportados[]" list="transportados-nome-list" value="${p.nome}" class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-lg">
                        </div>`;
                    extrasContainer.appendChild(fieldset);
                });
            }

            document.getElementById('edit-lancamento-modal').classList.remove('hidden');
        }

        function setupEditModalAutofill() {
            const modal = document.getElementById('edit-lancamento-modal');
            modal.addEventListener('blur', (event) => {
                const input = event.target;
                const parentDiv = input.closest('.grid');
                if (!parentDiv) return;

                const matriculaInput = parentDiv.querySelector('input[name="edit-matriculas[]"]');
                const nomeInput = parentDiv.querySelector('input[name="edit-transportados[]"]');

                if (matriculaInput && nomeInput) {
                    if (input === matriculaInput) {
                        handleAutofillDynamic(matriculaInput, nomeInput, 'matricula');
                    } else if (input === nomeInput) {
                        handleAutofillDynamic(nomeInput, matriculaInput, 'nome');
                    }
                }
            }, true);
            const valorEditInput = document.getElementById('edit-valor');
            const valorExtraEditInput = document.getElementById('edit-valor-extra');
            valorEditInput.addEventListener('input', () => formatCurrencyInput(valorEditInput));
            valorExtraEditInput.addEventListener('input', () => formatCurrencyInput(valorExtraEditInput));
        }
        setupEditModalAutofill();
        
        document.getElementById('close-edit-lancamento-modal').addEventListener('click', () => {
            document.getElementById('edit-lancamento-modal').classList.add('hidden');
        });
document.getElementById('cancel-edit-btn').addEventListener('click', () => {
            document.getElementById('edit-lancamento-modal').classList.add('hidden');
        });
document.getElementById('edit-lancamento-form').addEventListener('submit', async function(event) {
            event.preventDefault();
            const id = document.getElementById('edit-lancamento-id').value;
            
            const matriculasExtras = Array.from(document.querySelectorAll('#edit-passageiros-extras-container input[name="edit-matriculas[]"]')).map(input => input.value.trim());
            const nomesExtras = Array.from(document.querySelectorAll('#edit-passageiros-extras-container input[name="edit-transportados[]"]')).map(input => input.value.trim());
            const passageirosExtras = matriculasExtras.map((matricula, i) => ({
                matricula: matricula,
                nome: nomesExtras[i]
            })).filter(p => p.matricula && p.nome);

            const updatedData = {
                motorista: document.getElementById('edit-motorista').value,
                data: document.getElementById('edit-data').value,
                matricula: document.getElementById('edit-matricula').value,
                transportado: document.getElementById('edit-transportado').value,
                passageiros_extras: passageirosExtras,
                origem: document.getElementById('edit-origem').value,
                destino: document.getElementById('edit-destino').value,
                valor: parseCurrencyValue(document.getElementById('edit-valor').value),
                valorExtra: parseCurrencyValue(document.getElementById('edit-valor-extra').value),
                observacao: document.getElementById('edit-observacao').value,
                editedBy: currentUser.username,
                editedAt: serverTimestamp()
            };
            
            const docRef = doc(db, 'artifacts', 
globalAppId, 'public', 'data', 'lancamentos', id);
            await updateDoc(docRef, updatedData);
            
            showWarning('Lançamento atualizado com sucesso!');
document.getElementById('edit-lancamento-modal').classList.add('hidden');
            renderLancamentosList();
        });
// --- Funções CRUD e Renderização dos Modais Antigos ---
        function renderTransportadosList() {
            const tableBody = document.querySelector('#transportados-table tbody');
tableBody.innerHTML = '';
            transportadosData.forEach(item => {
                const row = document.createElement('tr');
                row.className = 'bg-white hover:bg-gray-50';
                row.innerHTML = `
                    <td class="p-4"><input type="checkbox" data-id="${item.id}" class="transportado-checkbox rounded-sm"></td>
              
      <td class="px-6 py-4">${item.matricula}</td>
                    <td class="px-6 py-4">${item.nome}</td>
                `;
                tableBody.appendChild(row);
            });
populateTransportadosDatalist();
        }
        
        function renderMotoristasList() {
            const tableBody = document.querySelector('#motoristas-table tbody');
tableBody.innerHTML = '';
            motoristasData.forEach(item => {
                const row = document.createElement('tr');
                row.className = 'bg-white hover:bg-gray-50';
                row.innerHTML = `
                    <td class="p-4"><input type="checkbox" data-id="${item.id}" class="motorista-checkbox rounded-sm"></td>
              
      <td class="px-6 py-4">${item.nome}</td>
                `;
                tableBody.appendChild(row);
            });
}
        
        function populateTransportadosDatalist() {
            const matriculaDatalist = document.querySelector('#transportados-matricula-list') ||
document.createElement('datalist');
            matriculaDatalist.id = 'transportados-matricula-list';
            const nomeDatalist = document.querySelector('#transportados-nome-list') || document.createElement('datalist');
            nomeDatalist.id = 'transportados-nome-list';
            if (!document.body.contains(matriculaDatalist)) document.body.appendChild(matriculaDatalist);
            if (!document.body.contains(nomeDatalist)) document.body.appendChild(nomeDatalist);
matriculaDatalist.innerHTML = '';
            nomeDatalist.innerHTML = '';
            transportadosData.forEach(item => {
                matriculaDatalist.innerHTML += `<option value="${item.matricula}">`;
                nomeDatalist.innerHTML += `<option value="${item.nome}">`;
            });
}
        
        function populateMotoristasDatalist() {
            const datalist = document.getElementById('motoristas-list');
datalist.innerHTML = '';
            motoristasData.forEach(item => datalist.innerHTML += `<option value="${item.nome}">`);
        }
        
        document.getElementById('add-transportado').addEventListener('click', async () => {
            const newMatricula = document.getElementById('new-matricula').value.trim();
            const newNome = document.getElementById('new-nome').value.trim();
            if (newMatricula && newNome) {
                const existing = transportadosData.find(item => item.matricula === newMatricula || 
item.nome.toLowerCase() === newNome.toLowerCase());
                if (existing) {
                    showWarning('Matrícula ou nome já existe.');
                } else {
                    await addDoc(collection(db, 'artifacts', globalAppId, 'public', 'data', 'transportados'), { matricula: newMatricula, nome: newNome });
      
              document.getElementById('new-matricula').value = '';
                    document.getElementById('new-nome').value = '';
                    showWarning('Transportado adicionado.');
                }
            } else {
           
     showWarning('Preencha matrícula e nome.');
            }
        });
document.getElementById('delete-selected-transportados').addEventListener('click', async () => {
            const checkboxes = document.querySelectorAll('#transportados-table .transportado-checkbox:checked');
            if (checkboxes.length === 0) {
                showWarning('Selecione ao menos um transportado.');
                return;
            }
            const promises = Array.from(checkboxes).map(cb 
=> deleteDoc(doc(db, 'artifacts', globalAppId, 'public', 'data', 'transportados', cb.dataset.id)));
            await Promise.all(promises);
            showWarning(`${checkboxes.length} transportados excluídos.`);
        });
document.getElementById('add-motorista').addEventListener('click', async () => {
            const newNome = document.getElementById('new-motorista-nome').value.trim();
            if (newNome) {
                if (motoristasData.find(item => item.nome.toLowerCase() === newNome.toLowerCase())) {
                    showWarning('Motorista já existe.');
                } else {
     
               await addDoc(collection(db, 'artifacts', globalAppId, 'public', 'data', 'motoristas'), { nome: newNome });
                    document.getElementById('new-motorista-nome').value = '';
                    showWarning('Motorista adicionado.');
                }
            } else {
  
              showWarning('Preencha o nome do motorista.');
            }
        });
document.getElementById('delete-selected-motoristas').addEventListener('click', async () => {
            const checkboxes = document.querySelectorAll('#motoristas-table .motorista-checkbox:checked');
            if (checkboxes.length === 0) {
                showWarning('Selecione ao menos um motorista.');
                return;
            }
            const promises = Array.from(checkboxes).map(cb 
=> deleteDoc(doc(db, 'artifacts', globalAppId, 'public', 'data', 'motoristas', cb.dataset.id)));
            await Promise.all(promises);
            showWarning(`${checkboxes.length} motoristas excluídos.`);
        });
// --- Eventos de UI restantes ---
        document.getElementById('close-modal').addEventListener('click', hideWarning);
        document.getElementById('open-transportados-modal').addEventListener('click', () => document.getElementById('transportados-modal').classList.remove('hidden'));
document.getElementById('close-transportados-modal').addEventListener('click', () => document.getElementById('transportados-modal').classList.add('hidden'));
        document.getElementById('open-motoristas-modal').addEventListener('click', () => document.getElementById('motoristas-modal').classList.remove('hidden'));
        document.getElementById('close-motoristas-modal').addEventListener('click', () => document.getElementById('motoristas-modal').classList.add('hidden'));
document.getElementById('sort-transportados-key').addEventListener('change', function() {
            rebuildTransportadosLookups(this.value, document.getElementById('sort-transportados-order').value);
        });
document.getElementById('sort-transportados-order').addEventListener('change', function() {
            rebuildTransportadosLookups(document.getElementById('sort-transportados-key').value, this.value);
        });
document.getElementById('sort-motoristas-order').addEventListener('change', function() {
            rebuildMotoristasLookups(this.value);
        });
</script>
</body>
</html>
