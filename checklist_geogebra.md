# Conversão Applet Geogebra

1) Inserir no header do arquivo HTML (se não existir):

```
        <meta name=viewport content="width=device-width,initial-scale=1">  
        <script src="https://www.geogebra.org/apps/deployggb.js"></script>
```
    
2) No arquivo HTML antigo, vai ter uma tag de applet da seguinte forma:

```
    <applet name="ggbApplet" code="geogebra.GeoGebraApplet" codebase="./" archive="jars/geogebra.jar" width="519" height="380" MAYSCRIPT>
        <param name="filename" value="applets/grafico_seno.ggb" />
        <param name="framePossible" value="false" />
        <param name="showResetIcon" value="false" />
        <param name="enableRightClick" value="false" />
        <param name="showMenuBar" value="false" />
        <param name="showToolBar" value="false" />
        <param name="showToolBarHelp" value="false" />
        <param name="showAlgebraInput" value="false" />
        <param name="scriptable" value="true" />
        <param name="enableShiftDragZoom" value="false" />
    </applet>
```

Possivelmente com valores diferentes, ou alguns a mais ou a menos. Usando https://wiki.geogebra.org/en/Reference:GeoGebra_App_Parameters como referência, verificar se os params existem na documentação atual do geogebra. Neste exemplo, tanto "scriptable" como "framePossible" não existem, então vamos remove-los.

Sempre adicionar a opção "useBrowserForJS" com o valor True. Isso faz com o que o geogebra chame a função ggbOnInit dos nossos arquivos quando é inicializado, que era o comportamento esperado na época.

Com isso, convertemos a tag <applet> anterior para a nova forma de chamar o geogebra. Ela deve ser substituida, neste exemplo, por:

```
            <div id="ggbApplet"></div> 
                <script>  
                    var ggbApp = new GGBApplet({"appName": "classic", 
                    "width": 519, "height": 380, 
                    "filename": "applets/blablabla.ggb",
                    "showResetIcon": false,
                    "enableRightClick": false,
                    "showMenuBar": false,
                    "showToolBar": false,
                    "showToolBarHelp": false,
                    "showAlgebraInput": false,
                    "enableShiftDragZoom": false,
                    "useBrowserForJS": true                
                    }, true);
                    window.addEventListener("load", function() { 
                    ggbApp.inject('ggbApplet');
                    });
                </script>
```

Manter a propriedadfes "appName" sempre como "classic".

Manter as demais <divs> presentes como id="borda_applet", etc, pois são usadas pelo script de interface.

Com isso, alguns softwares já podem funcionar sem problemas. A maioria utiliza document.ggbApplet para enviar comandos para o applet do geogebra, como este exemplo:

```
	var applet = document.ggbApplet;
	var anguloSaida = applet.getValueString('γ');	//pega o valor do angulo escolhido pelo usuario. "γ = 27°"
```

Se tiver alguma diferença no nome "ggbApplet" talvez alguns ajustes sejam necessários.

Caso apareçam erros/problemas, a documentação atual da API do Geogebra esta em: https://wiki.geogebra.org/en/Reference:GeoGebra_Apps_API.
