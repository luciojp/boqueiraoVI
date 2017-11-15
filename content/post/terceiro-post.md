+++

date = 2014-10-13T20:07:15Z
draft = false
title = "Eh possivel observar alguma semelhanca no nivel das aguas de boqueirao no mes de junho?"

weight = 0.2

+++


<div id="vis" width=300></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/vega/3.0.7/vega.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/vega-lite/2.0.1/vega-lite.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/vega-embed/3.0.0-rc7/vega-embed.js"></script>
<script>
    const spec = {
  "$schema": "https://vega.github.io/schema/vega/v3.0.json",
  "autosize": "pad",
  "padding": 5,
  "width": 400,
  "height": 200,
  "style": "cell",
  "data": [
    {
      "name": "source_0",
      "url": "https://api.insa.gov.br/reservatorios/12172/monitoramento",
      "format": {
        "type": "json",
        "property": "volumes",
        "parse": {
          "DataInformacao": "utc:'%d/%m/%Y'",
          "VolumePercentual": "number"
        }
      },
      "transform": [
        {
          "type": "filter",
          "expr": "inrange(time(datetime(year(datum[\"DataInformacao\"]), 0, 1, 0, 0, 0, 0)), [time(datetime(1994, 0, 1, 0, 0, 0, 0)), time(datetime(2017, 0, 1, 0, 0, 0, 0))])"
        },
        {
          "type": "filter",
          "expr": "inrange(time(datetime(0, month(datum[\"DataInformacao\"]), 1, 0, 0, 0, 0)), [time(datetime(0, 5, 1, 0, 0, 0, 0)), time(datetime(0, 6, 1, 0, 0, 0, 0))])"
        },
        {
          "type": "formula",
          "as": "year_DataInformacao",
          "expr": "datetime(year(datum[\"DataInformacao\"]), 0, 1, 0, 0, 0, 0)"
        },
        {
          "type": "aggregate",
          "groupby": ["year_DataInformacao"],
          "ops": ["mean"],
          "fields": ["VolumePercentual"],
          "as": ["mean_VolumePercentual"]
        },
        {
          "type": "filter",
          "expr": "datum[\"year_DataInformacao\"] !== null && !isNaN(datum[\"year_DataInformacao\"])"
        }
      ]
    }
  ],
  "marks": [
    {
      "name": "marks",
      "type": "rect",
      "style": ["bar"],
      "from": {"data": "source_0"},
      "encode": {
        "update": {
          "xc": {"scale": "x","field": "year_DataInformacao"},
          "width": {"value": 5},
          "y": {"scale": "y","field": "mean_VolumePercentual"},
          "y2": {"scale": "y","value": 0},
          "fill": {"value": "#4c78a8"}
        }
      }
    }
  ],
  "scales": [
    {
      "name": "x",
      "type": "time",
      "domain": {"data": "source_0","field": "year_DataInformacao"},
      "range": [0,{"signal": "width"}],
      "padding": 5
    },
    {
      "name": "y",
      "type": "linear",
      "domain": {"data": "source_0","field": "mean_VolumePercentual"},
      "range": [{"signal": "height"},0],
      "nice": true,
      "zero": true
    }
  ],
  "axes": [
    {
      "title": "Anos",
      "scale": "x",
      "orient": "bottom",
      "labelFlush": true,
      "labelOverlap": true,
      "tickCount": {"signal": "ceil(width/40)"},
      "zindex": 1,
      "encode": {
        "labels": {
          "update": {
            "text": {"signal": "timeFormat(datum.value, '%Y')"}
          }
        }
      }
    },
    {
      "scale": "x",
      "orient": "bottom",
      "domain": false,
      "grid": true,
      "labels": false,
      "maxExtent": 0,
      "minExtent": 0,
      "tickCount": {"signal": "ceil(width/40)"},
      "ticks": false,
      "zindex": 0,
      "gridScale": "y"
    },
    {
      "title": "Média do volume (%)",
      "scale": "y",
      "orient": "left",
      "labelOverlap": true,
      "tickCount": {"signal": "ceil(height/40)"},
      "zindex": 1
    },
    {
      "scale": "y",
      "orient": "left",
      "domain": false,
      "grid": true,
      "labels": false,
      "maxExtent": 0,
      "minExtent": 0,
      "tickCount": {"signal": "ceil(height/40)"},
      "ticks": false,
      "zindex": 0,
      "gridScale": "x"
    }
  ],
  "config": {"axisY": {"minExtent": 30}}
};
  	vegaEmbed('#vis', spec).catch(console.warn);
</script>



Nao eh possivel observar semelhancas nos nivel da agua nos meses de junho e julho (epoca do Sao Joao) .
