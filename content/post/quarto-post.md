+++
date = 2014-10-13T20:07:10Z
draft = false
title = "Lab 02 Parte 02"

weight = 1

+++

<!DOCTYPE html>
<html lang="pt-br">

<head>
  <meta charset="utf-8">
  <title>Barras simples</title>
  <script src="https://d3js.org/d3.v4.min.js"></script>
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css">
</head>

<body>
  <div class="container">
    <div class="row">
      <h2>Volume m�ximo e m�nimo do A�ude Epit�cio Pessoa, por m�s</h2>
    </div>
    <div class="row mychart" id="chart">
    </div>
  </div>

  <style>
    .mychart circle {
      fill: yellow;
    }
    .mychart circle:hover {
      fill: lemonchiffon;
    }
    .mychart text {
      font: 12px sans-serif;
      text-anchor: left;
    }
  </style>

  <script type="text/javascript">
    "use strict"
    function desenhaGrafico(dados) {
     // definicoes de altura e largura do svg e da vis dentro
      var alturaSVG = 600, larguraSVG = 2000;
      var	margin = {top: 10, right: 20, bottom:30, left: 100}, // para descolar a vis das bordas do grafico
          larguraVis = larguraSVG - margin.left - margin.right,
          alturaVis = alturaSVG - margin.top - margin.bottom;
      /*
       * Prepara onde adicionaremos a visualizacao
       */
      var grafico = d3.select('#chart') // cria elemento <svg> com um <g> dentro
        .append('svg')
          .attr('width', larguraVis + margin.left + margin.right)
          .attr('height', alturaVis + margin.top + margin.bottom)
        .append('g') // para entender o <g> v? em x03-detalhes-svg.html
          .attr('transform', 'translate(' +  margin.left + ',' + margin.top + ')');
      /*
       * As escalas
       */
      var maxAltura = d3.max(dados, (d, i) => d.noventa_percentil) + 10;
      var x = d3.scaleBand()
                .domain(dados.map(function(d) { return d.mes; }))
                .range([0,larguraVis])
                .padding(.10);
      var y = d3.scaleLinear()
                .domain([60, maxAltura])
                .range([alturaVis,0]);
      /*
       * As marcas
       */
      grafico.selectAll('g')
              .data(dados)
              .enter()
                .append('circle')
                  .attr('r', d => d.noventa_percentil)
                  .attr('cx', d => x(d.mes))
                  .attr('cy', d => y(d.noventa_percentil));
     grafico.selectAll('g')
          .data(dados)
          .enter()
          .append('circle')
          .attr('r', d => d.dez_percentil)
          .attr('cx', d => x(d.mes))
          .attr('cy', d => y(d.noventa_percentil))
          .style('fill', '#3393FF');
       /*
       * Os eixos
       */
      grafico.append("g")
              .attr("class", "x axis")
              .attr("transform", "translate(0," + alturaVis + ")")
              .call(d3.axisBottom(x)); // magica do d3: gera eixo a partir da escala
      grafico.append('g')
              .attr('transform', 'translate(0,0)')
              .call(d3.axisLeft(y))  // gera eixo a partir da escala
      grafico.append("text")
        .attr("transform", "translate(-30," + (alturaVis + margin.top)/2 + ") rotate(-90)")
        .text("Volume (%)");
    }
    var dados = "dados/boqueirao-por-mes.json";
    d3.json(dados, function(dados) {
      desenhaGrafico(dados);
    });
  </script>
</body>

</html>
