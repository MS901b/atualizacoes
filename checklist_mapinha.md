
# Atualização Mapinha
Esse checklist substitui o applet Flash mapinha.swf por elementos SVG do HTML5 por meio do arquivo mapinha.js.

## mapinha.js
- Colocar o arquivo mapinha.js na pasta scripts
> Caso queira, no início do arquivo mapinha.js algumas constantes podem ser ajustadas.

## mapa.html
- Importar o mapinha.js no mapa.html
```
<script type="text/javascript" src="scripts/mapinha.js"></script>
```
- Remover bloco do object do flash
```
<object id="Mapinha" name="Mapinha" type="application/x-shockwave-flash" data="applets/Mapinha.swf" width="960" height="500" wmode="transparent">
							<param name="menu" value="false" />
							<param name="movie" value="applets/Mapinha.swf" />
							<param name="allowScriptAccess" value="sameDomain" />
							<param name="wmode" value="transparent">
						</object>
```
- Caso exista a função `resetar()`, passe para o proximo item, senão coloque o seguinte bloco de código (ele é necessário para que o Limpar funcione):
```
		<script type="text/javascript">
			var nomeSoft = 'XXXXXXX'; //troque pelo nome do software
			var Perguntas = $H({
				limpar: {
					conteudo: '<p>Isso irá apagar todos os dados armazenados, como respostas guardadas, para essa unidade.</p><p style="margin-top:10px;">Você tem certeza?</p>',
					layout: ['seta_cima','direita'],
					largura: 10,
					callback: resetar,
					// se o usuário clicar em 'Sim', o popup chamará a funcao funcao_pede na qual this.resultado será 'sim'
					// Veja que essa função deve estar definida, ou ser definida nesse exato momento (como no exemplo "pede2")
					respostas: [{sim: 'Sim'}, {nao: 'Não'}]
				}
			});

			function resetar() {
				if (this.resultado == 'sim') {
					$('SalvaLocal').ApagaTudo(nomeSoft);
					location.reload();
				}
			}
		</script>
```

- Na função `resetar()`, para chamadas do tipo `$('SalvaLocal').Salva(nomeSoft, 'item_x',y)` ou `$('Mapinha').Salva(nomeSoft, 'item_x',y)`, onde item é `atividade`, `transicao` ou `desafio`, x é um número e o y o estado inicial, faremos o seguinte (ignore os casos com `automacao_` ou `_parte_`):
	 * Copie essas linhas para passarmos esses estados iniciais para o estrutura.xml da pasta scripts (mais detalhes na seção sobre o estrutura.xml), caso necessário.
	 * Remova essas linhas do mapa.html.
	 * Caso, ao invés de `'SalvaLocal'` esteja `'Mapinha'`, troque por `'SalvaLocal'`.

- Colocar o seguinte bloco no mapa.html
```
	<script>
	fetch("scripts/estrutura.xml")
			.then(function(response){
			response.text().then(function(data){
				const m = new Mapinha("conteudo", nomeSoft);
				m.parseXml(data);
				m.adicionaBotoesItens();
				});
			})
			.catch(function(err){ 
			console.error('Failed retrieving information', err);
			});
	</script>
```
> Repare que na criação do Mapinha, é passado como parâmetro o id da div que receberá o SVG (no caso "conteudo"), por isso é recomendado que este bloco seja inserido após a declaração da div em questão.

##  estrutura.xml (pasta scripts)
> Há uma pasta `novas estruturas xml` em que se encontram algumas estruturas já convertidas seguindo o padrão descrito a seguir.

> O mapinha agora dispõe os itens na vertical (houve uma inversão na interpretação entre as tags `<coluna>` e `<altura>`) . Como originalmente os itens possuíam alturas negativas ou positivas (pulando a altura  = 0), é possível que algum item pareça estar deslocado (deixa vago o espaço que seria do item de altura = 0). Isso pode ser ajustado, caso haja necessidade, mudando os valores das coordenadas.

### Ligações
Originalmente, as ligações (tag `<com>`) entre os itens era feita com base na ordem em que os itens apareciam no documento. Agora deve-se usar a tag `<id>`.
- Insira dentro das tags `<item>` a tag `<id>xy</id>`, onde x deve ser substituído por uma letra (a = atividade, d = desafio, t = transição) e y por um número correspondente
- Alterar as tags `<com>` de acordo com os ids definidos no item anterior

Exemplo antes
```
<software nome="xxxxx">
	<!-- 1: 1a Atividade -->
	<item>
		<tipo>atividade</tipo>
	</item>

	<!-- 2: texto longo -->
	<item>
		<tipo>transicao</tipo>
		<ligacoes>
			<com>1</com>			
		</ligacoes>
	</item>		
	
	<!-- 3: 2a Atividade -->
	<item>
		<tipo>atividade</tipo>
		<ligacoes>
			<com>2</com>
		</ligacoes>
	</item>
</software>
```

Exemplo depois
```
<software nome="xxxxx">
	<!-- 1: 1a Atividade -->
	<item>
		<id>a1</id>
		<tipo>atividade</tipo>
	</item>

	<!-- 2: texto longo -->
	<item>
		<id>t1</id>
		<tipo>transicao</tipo>
		<ligacoes>
			<com>a1</com>			
		</ligacoes>
	</item>		
	
	<!-- 3: 2a Atividade -->
	<item>
		<id>a2</id>
		<tipo>atividade</tipo>
		<ligacoes>
			<com>t1</com>
		</ligacoes>
	</item>
</software>
```
### Estado inicial
Originalmente, o estado inicial do item era definido no mapa.html. Agora isso está na estrutura.xml.
- Colocar `<estadoinicial>y</estadoinicial>` dentro de cada `<item>`, onde y deve ser substituído pelo número correspondente ao estado inicial daquele item (copiado do mapa.html anteriormente)

| Estado |nº correspondente |
|------------|-------|
|Travado |0|
|Aberto |1|
|Iniciado |2|
|Finalizado |3|

##  Arquivos _correcao.js (pasta scripts)

### Aplicando estado "iniciado"
Caso o mapinha não esteja funcionado como esperado (sem mudar as cores), verificar os arquivos _correcao.js
- Procure por partes de código similar a seguinte (com `flash:`). Repare que o a mudança de estado (`setAtividade()`) depende do flash para funcionar.
```
Event.observe(document, 'flash:SalvaLocal', function(ev){
	setAtividade('item_x',y,false);	//Comecou a fazer a item_y
	flash_flag = 1;
	exec_init();
});
```
- Procure onde o estado do item é modificado (normalmente nas chamadas `setAtividade()` ou `setResp()`)
- Caso essas chamadas estejam apenas nas partes que usam flash, copie a chamada do `setAtividade()` (ou `setResp()`) para uma função que é executada quando a página da atividade é carregada (normalmente exec_init() ou InitOnLoad()). Assim, logo quando o usuário entrar na atividade, o estado muda para "iniciado"


### Aplicando estado "finalizado"
A mudança no estado da atividade para "finalizado" ocorre nas funções `tudoCerto()`. Caso seja decidido "travar" alguma atividade, essa função deve ser alterada para que ocorra o "destrave" da tarefa seguinte usando as funções do tipo `setAtividade()` ou `setResp()`, passando o estado "aberto".
