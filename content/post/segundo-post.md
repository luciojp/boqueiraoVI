+++
charset = "UTF-8"
date = 2014-10-13T20:07:30Z
draft = false
title = "Observando o historico de boqueirao,eh possivel inferir um certo ciclo no nivel das aguas? Se sim, quando deve voltar a subir?"

weight = 0.8

+++



<div id="vis" width=300></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/vega/3.0.7/vega.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/vega-lite/2.0.1/vega-lite.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/vega-embed/3.0.0-rc7/vega-embed.js"></script>
<script>
    const spec = {
    "$schema": "https://vega.github.io/schema/vega-lite/v2.json",
    "data": {
        "url": "https://api.insa.gov.br/reservatorios/12172/monitoramento",
        "format": {
        "type": "json",
        "property": "volumes",
        "parse": {
            "DataInformacao": "utc:'%d/%m/%Y'"
                }
            }
        },

    "width": 700,
  "mark": "line",
"encoding": {
  "x": {
    "timeUnit": "yearmonth",
    "field": "DataInformacao",
    "type": "temporal",
    "axis": {"title": "Anos"}
  },
  "y": {
    "aggregate": "mean",
    "field": "VolumePercentual",
    "type": "quantitative",
    "axis": {"title": "Média do volume (%)"}
  }
}
};
  	vegaEmbed('#vis', spec).catch(console.warn);
</script>


Como nao temos informacoes de muitos anos anteriores a 1994, nao eh possivel afirmar com 
precisao se ha ou nao esse ciclo, porem, se o periodo  da ultima grande estiagem  de 1998 
a 2004 se repetir, estamos pertos do fim desta estiagem atual.
 
Outra coisa interessante a se observar eh que ha um padrao na epoca em que o acude de 
boqueirao enche rapidamente, que e do final de um ano indo pro inicio do proximo. 
Ficando intrigado com isso, fui atras e encontrei uma resposta climatica que eh ciclica,
o fenomeno 'La nina' (a crianca), que um dos seus efeitos eh na epoca de dezembro a 
fevereiro um grande aumento no volume de chuvas na regiao nordeste, explicando o rapido
enchimento do volume de boqueirao. E este fenomeno esta previsto para acontecer entre 
2018 e 2019.

