# Atualizações SalvaLocal

- Adicionar nosso script 'salvaLocal.js' (disponível na pasta de arquivos necessários) na pasta scripts e inserir a tag `<script type="text/javascript" src="scripts/salvaLocal.js"></script>` logo abaixo da tag `<script type="text/javascript" src="scripts/protoaculous.js"></script>` em todos os arquivos que o chamam.

- Verificar como o getResp e setResp estao sendo usados (caso exista):
    - Verificar como é feita a chamada dos metodos Salva() e Pega() do $('SalvaLocal') e corrigi-lá caso necessário (trocar possivel chamada de funcao "getFlash" por "$"). 

- Remover as tags <Object> que chamam 'SalvaLocal' em todos os arquivos .html

- Colocar flash_loaded = true como default, nos arquivos de correcao (as vezes o nome pode estar de outra forma tipo flash_flag, flag_flash, etc...)

- Colocar interface_salva_local = true como default nos arquivos interface.js e interfaceGrande.js

- Testar apagatudo do mapinha para ver se o mesmo está funcionando como esperado.

- Chamar gerenciaParte() no comeco da funcao do arquivo interface.js que contém "document.observe("dom:loaded"..."