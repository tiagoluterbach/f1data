# Previsao de Posicao Final em Corridas de F1 (Temporada 2024)

Projeto desenvolvido para a disciplina de Topicos Especiais em Engenharia de Telecomunicacoes, com o objetivo de prever a posicao final de um piloto em uma corrida de Formula 1 com base em seu desempenho na temporada e na posicao de largada (grid).

## Objetivo

Construir e comparar modelos de regressao capazes de estimar a posicao de chegada de um piloto em uma corrida, utilizando como variaveis preditoras:

- Idade do piloto
- Experiencia (anos de carreira na F1)
- Pontos atuais no campeonato
- Posicao de largada (grid)

## Dados

O dataset combina informacoes reais dos 20 pilotos da temporada 2024 (idade, anos de experiencia, pontuacao final e "tier" da equipe, com base em fontes como Autosport e F1.com) com uma simulacao de 10 corridas, gerando 200 registros. A posicao final de cada corrida e calculada a partir da posicao de largada e do desempenho do carro/piloto (pontos na temporada), com um fator de ruido aleatorio para simular a imprevisibilidade de uma corrida real.

Observacao: os dados de corrida (posicao final por corrida) sao simulados, nao sao resultados oficiais da FIA. O notebook nao consulta uma API de corridas real.

## Modelos utilizados

Foram treinados e comparados tres modelos de regressao:

| Modelo | Erro (validacao cruzada) | Erro (teste final) |
|---|---|---|
| Regressao Linear | 2.81 posicoes | 2.57 posicoes |
| KNN (k=7) | 3.04 posicoes | 2.66 posicoes |
| Random Forest | 3.24 posicoes | 2.89 posicoes |

Apos otimizacao de hiperparametros do Random Forest via GridSearchCV (testando n_estimators, max_depth e min_samples_split), o melhor resultado encontrado foi:

- Melhores parametros: max_depth=5, min_samples_split=5, n_estimators=200
- Erro do modelo otimizado: 2.63 posicoes

A analise de correlacao mostrou que pontos atuais (-0.87) e posicao de largada (+0.86) sao, de longe, as variaveis mais relevantes para prever a posicao final, muito mais do que idade ou experiencia.

## Resultados

O notebook gera um grafico comparando a posicao final real e a posicao prevista pelo modelo otimizado para os dados de teste (nunca vistos pelo modelo).

## Tecnologias utilizadas

- Python 3
- pandas / numpy
- scikit-learn (Regressao Linear, KNN, Random Forest, GridSearchCV)
- matplotlib

## Como executar

```bash
git clone <link-do-repositorio>
cd <nome-do-repositorio>
pip install -r requirements.txt
jupyter notebook trabalho3tep.ipynb
```

## Estrutura

```
.
├── trabalho3tep.ipynb   # Notebook com todo o projeto (dados, modelos, avaliacao e grafico)
├── requirements.txt
└── README.md
```

## Autor

Tiago Luterbach de Medeiros
