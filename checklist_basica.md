# Checklist básica

- Deletar os arquivos Acessarprodutos.jar, Acessarprodutos.exe e comousar.txt, caso ainda existam
- Mover os arquivos license.txt e gplv2.txt para a pasta que de fato contem o software, caso não tenham sido movidos
- Remover eventuais pastas MACOSX e arquivo .Ds_store
- Subir todos os arquivos uma pasta cima (eliminando o primeiro nível que agora deve estar vazio, com exceção da pasta com o conteúdo de fato do software)
- Remover a pasta jars e todo seu conteúdo
- Remover os arquivos mapinha.swf, salvalocal.swf, armazenamento.swf da pasta applets
- Remover a função FlashTag nos arquivos interface.js e interface_grande.js
- Editar o arquivo index.html atualizando alguns campos da variável que contem os créditos do software pelo conteúdo abaixo:

Na variável FichaUnidade, acrescentar:

```
        {
                    titulo: 'Atualizações',
                    texto: 'Claudio Dos Santos Júnior, José Philipe Mendes De Godoy, Samuel Batista De Souza, Thais Araujo Bispo, Vinícius Andrade Santos'
				}
```

Trocar o conteúdo da FichaProjeto para:
```
  var FichaProjeto = new Array(
				{
					titulo: '- Unicamp -',
					texto: ''
				},
				{
					titulo: 'Reitor',
					texto: 'Marcelo Knobel'
				},
				{
					titulo: 'Vice-Reitor',
					texto: 'Edgar Salvadori de Decca'
				},
				{
					titulo: '- IMECC -',
					texto: ''
				},
				{
					titulo: 'Diretor',
					texto: 'Paulo R. C. Ruffino'
				},
				{
					titulo: 'Diretor associado',
					texto: 'Ricardo Miranda Martins'
				},
				{
					titulo: '- Matemática Multimídia -',
					texto: ''
				},
				{
					titulo: 'Coordenação Geral',
					texto: 'Samuel Rocha de Oliveira'
				},
				{
					titulo: 'Coordenação de Software',
					texto: 'Leonardo Barichello'
				},
				{
					titulo: 'Coordenação de Implementação',
					texto: 'Matias Costa'
				}
			);
```

