# Previsão do overall - EA FC 27

Trabalho de Machine Learning da faculdade. Quis ver se dava pra adivinhar o overall de um jogador do FC 27 olhando só os seis atributos da carta (pace, shooting, passing, dribbling, defending e physicality).

## Base de dados

Peguei a base [EA Sports FC 27 Player Ratings](https://www.kaggle.com/datasets/mikedpad/ea-sports-fc27-player-ratings) do Kaggle. Ela tem 19.789 jogadores e 60 colunas, mas usei só o `overall_rating`, os seis atributos e a `position` (pra tirar os goleiros).

## O que eu fiz

É um problema de regressão: o modelo aprende com jogadores que já têm overall e depois tenta acertar o de jogadores que ele não viu.

- Tirei os goleiros, já que o overall deles vem de outros atributos (diving, reflexes...). Ficaram 17.585 jogadores.
- Olhei a correlação dos atributos com o overall. Passing (0,75) e dribbling (0,71) foram os que mais pesaram, e pace (0,26) quase não influencia.
- Separei 80% dos dados pra treino e 20% pra teste.
- Treinei uma Regressão Linear e uma Random Forest e comparei o previsto com o real.

## Resultado

- Regressão Linear: erra em média 2,6 pontos, R² de 0,78.
- Random Forest: erra em média menos de 1 ponto (0,96), R² de 0,97.

A Random Forest ganhou com folga. A regressão usa a mesma conta pra todo jogador, só que o peso de cada atributo muda com a posição (defending conta muito pra zagueiro e quase nada pra atacante). A Random Forest consegue separar esses perfis.

Um exemplo: o Michael Olise tem 90 de overall. A regressão chutou 82 e a Random Forest chutou 89.

O ponto fraco é que os dois modelos erram mais nos jogadores com overall muito alto ou muito baixo, e a Random Forest não consegue prever valores fora da faixa que viu no treino.

## Como rodar

```bash
pip install pandas matplotlib seaborn scikit-learn
```

Abre o `analise.ipynb` no VS Code (com a extensão Jupyter) ou no Jupyter e roda todas as células. O `players.csv` tem que estar na mesma pasta.

Usei Python, pandas, matplotlib, seaborn e scikit-learn.
