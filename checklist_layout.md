# Checklist Layout

## Os seguintes arquivos devem ser substituidos:
* css/abertura.css
* css/abertura2.css
* css/bloco.css
* css/curiosidade_transicao.css
* css/curiosidade_transicao2.css
* css/estilo.css
* css/estilo2.css
* css/estilo_grande.css
* css/estilo_grande2.css
* css/notas.css
* css/popup.css
* script/abertura.js
* script/browser.js
* img_layout/barra-ferramentas.gif
* img_layout/logo.gif
* detect.html
* visualizar.html

## Alterações nos arquivos:

#### scripts/conteudovisualizar.js:
* Alterar `var “tipo” = "software v2.0"`
* Alterar em **var FichaTecnica**, na sessão **requisitos**, trocar o **conteudo** por esse:
`conteudo: 'Navegador moderno (Chrome 70+ ou Firefox 62+). O suporte não é garantido para dispositivos mobiles.'`
* Alterar **var sobre_projeto** para:
`var sobre_projeto = 'M³ &ndash; Matemática MultiMídia é uma coleção de materiais didáticos disponíveis em mídias digitais para o uso do professor de matemática do ensino médio no Brasil e facilitar o ensino-aprendizagem. Composta por áudios, experimentos, softwares e vídeos, a coleção foi desenvolvida, entre 2008 e 2010, por uma grande equipe de professores e estudantes da Unicamp e vários colaboradores, tendo contado com recursos do FNDE, do MEC e do MCT. Para maiores detalhes sobre a utilização da coleção M³&nbsp;&ndash;&nbsp;Matemática Multimídia, consulte o Guia do Professor. A versão 2.0 foi lançada em 2020, como uma medida para garantir que o software tivesse suporte aos novos sistemas.'`
* Alterar **var site_projeto** para: `var site_projeto = 'http://m3.ime.unicamp.br/portal/'`

#### atividadeN_parteN.html e desafioN.html (N representa números):
* No **id="rodape"**: trocar `m3.mat.br` por `m3.ime.unicamp.br`
* No **id="ferramenta"**: comentar a linha do `link_calculadora` e `link_acessibilidade`

#### index.html:
* Dentro do *head*, insira a linha: `<link href='https://fonts.googleapis.com/css?family=Fira+Sans' rel='stylesheet'>`
* No **id="conteudo"**: trocar isso: `<h1>Titulo</h1> ` por isso: `<h1>Titulo<i>v2.0</i></h1>`
* Descomente a linha ou comente dentro do **id="fichas"**: `<a href="detect.html" style="float:right;" id="ficha_tecnica_projeto">Ver relatório de compatibilidade</a>`
* No **id="rodape"**: trocar `m3.mat.br` por `m3.ime.unicamp.br`
* Verificar se o tamanho da imagem está ok, se não, vá até **id="apresentacao"**, em `<img src="imgs/dados_apresentacao.jpg"` acrescentar `style="height: xxxpx"` (xxx representa o tamanho que deixa a imagem de forma correta)

#### introducao.html:
* No **id="rodape"**: trocar `m3.mat.br` por `m3.ime.unicamp.br`

#### mapa.html:
* No **id="rodape"**: trocar `m3.mat.br` por `m3.ime.unicamp.br`

#### detect.html:
* Escrever o nome do software na tag **<title></title>**
