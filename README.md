1. Limpeza e Processamento de Dados

O primeiro passo para treinar qualquer modelo de aprendizado de máquina é preparar e limpar os dados. Os textos das avaliações continham caracteres especiais, stopwords e outros elementos que precisavam ser removidos para melhorar a performance dos modelos. O processamento envolveu as seguintes etapas:

    Remoção de caracteres especiais e símbolos: Utilizamos expressões regulares (regex) para remover caracteres que não são úteis para a análise de texto, como pontuações e símbolos.
    Tokenização: O texto foi segmentado em palavras individuais (tokens).
    Remoção de stopwords: Palavras irrelevantes, como preposições e artigos (em português), foram removidas para focar nos termos mais significativos.
    Stemização ou Lematização: Dependendo da configuração, aplicamos stemização (redução das palavras à sua raiz, como "jogando" para "jog") ou lematização (redução das palavras à sua forma base, como "jogando" para "jogar").

Esse processo resultou em um texto mais "limpo" e adequado para ser convertido em uma representação numérica utilizável por modelos de aprendizado de máquina.
2. Vetorização com TF-IDF

Após a limpeza dos textos, utilizamos a TF-IDF (Term Frequency-Inverse Document Frequency) para converter o texto em uma matriz numérica. Essa técnica atribui um peso maior a palavras que são frequentes em um documento, mas raras em outros, o que ajuda a destacar termos distintivos. Usamos o TfidfVectorizer da biblioteca Scikit-learn para gerar vetores de características, limitados a um máximo de 1000 palavras mais importantes.
3. Adição da Coluna de Fraude

O conjunto de dados tinha avaliações com classificações (número de estrelas). Com base nisso, criamos uma coluna de alvo (label), onde classificações extremas (1 ou 5 estrelas) foram consideradas como potencialmente fraudulentas, assumindo que essas avaliações poderiam estar mais suscetíveis a manipulações ou vieses.

    Fraude (1): Avaliações com 1 ou 5 estrelas.
    Não fraude (0): Avaliações entre 2 e 4 estrelas.

4. Balanceamento de Dados com SMOTE

Muitas vezes, os conjuntos de dados estão desbalanceados, ou seja, existem mais exemplos de uma classe (neste caso, não fraudulentas) do que de outra (fraudulentas). Para resolver esse problema, utilizamos o método SMOTE (Synthetic Minority Over-sampling Technique). Ele gera exemplos sintéticos da classe minoritária para aumentar sua proporção no conjunto de dados, permitindo que o modelo não seja enviesado.
5. Modelos de Aprendizado de Máquina Utilizados

Utilizamos três modelos diferentes para realizar a classificação das avaliações:
5.1 Random Forest

O Random Forest é um modelo de aprendizado de máquina baseado em múltiplas árvores de decisão. Ele funciona criando diversas árvores de decisão em subconjuntos aleatórios do conjunto de dados, e a predição final é feita por votação majoritária entre as árvores. Isso ajuda a reduzir o overfitting e melhora a generalização dos dados. É um modelo robusto e amplamente utilizado em classificação.
5.2 Regressão Logística

A Regressão Logística é um modelo estatístico usado para tarefas de classificação binária. Ele estima a probabilidade de uma observação pertencer a uma das classes (neste caso, fraude ou não fraude). A regressão logística é útil por ser interpretável e eficiente, especialmente em cenários onde a relação entre as variáveis preditoras e o alvo é linear.
5.3 Naive Bayes

O Naive Bayes é um classificador probabilístico baseado no Teorema de Bayes. Ele assume que as características são independentes, o que simplifica os cálculos e torna o algoritmo rápido e eficiente. É particularmente eficaz para classificação de textos e foi aplicado neste projeto para comparar sua performance com os outros modelos.
6. Avaliação dos Modelos

A avaliação foi feita utilizando três métricas principais: acurácia, matriz de confusão e a curva ROC.
6.1 Matriz de Confusão

A matriz de confusão mostra o número de classificações corretas e incorretas, divididas entre verdadeiros positivos, falsos positivos, verdadeiros negativos e falsos negativos. Essa visualização ajuda a entender como o modelo está performando em termos de previsões corretas e erros.
6.2 Curva ROC e AUC

A Curva ROC (Receiver Operating Characteristic) mostra a relação entre a taxa de falsos positivos e a taxa de verdadeiros positivos em diferentes thresholds de decisão. O AUC (Area Under the Curve) é a área sob essa curva e serve como uma métrica para avaliar a capacidade do modelo de distinguir entre classes. Um AUC próximo de 1 indica um bom desempenho.
7. Resultados

Cada modelo foi treinado com o conjunto de dados balanceado, e suas performances foram comparadas.

    Random Forest mostrou resultados robustos, devido à sua capacidade de lidar com dados complexos e não lineares.
    Regressão Logística foi eficiente e rápida, mas pode não ter capturado toda a complexidade dos dados devido à sua natureza linear.
    Naive Bayes foi rápido e simples, mas suas suposições de independência entre as variáveis podem ter limitado sua performance.

Para cada modelo, foram geradas a matriz de confusão e a curva ROC, permitindo uma análise visual e quantitativa de seu desempenho.
8. Visualização dos Resultados

As matrizes de confusão permitiram uma rápida inspeção de quantos casos foram corretamente ou incorretamente classificados, enquanto as curvas ROC ajudaram a comparar visualmente o desempenho dos diferentes modelos. A curva ROC mais próxima do canto superior esquerdo indicou melhores resultados.
Conclusão

Neste projeto, realizamos um fluxo completo de preparação de dados, aplicamos técnicas avançadas de balanceamento e exploramos três modelos de classificação para identificar fraudes em avaliações. O Random Forest demonstrou ser o modelo mais robusto para essa tarefa, mas as diferentes técnicas permitem ajustes conforme o comportamento e a natureza dos dados. A análise visual e quantitativa das métricas de avaliação foi essencial para determinar a melhor abordagem para resolver o problema.
