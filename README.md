
# Hamiltonian Path Finder

## Execução
Para executar o código, abra o terminal (cmd) no diretório onde está localizado o arquivo `main.py` e utilize o comando:
```bash
python main.py
```

---

## Explicação linha a linha

Explicação Linha a Linha
1: Define a classe Grafo.

2: Construtor recebe número de vértices e flag de direcionamento.

3: Armazena n (quantidade de vértices).

4: Cria lista de adjacência como dict {vértice: lista_de_vizinhos}.

5: Guarda se o grafo é direcionado.

6: Linha em branco (organização).

7: Define método para adicionar aresta (u, v).

8: Adiciona v na lista de adjacência de u.

9: Se não direcionado, também adiciona u em v.

10: Fecha o if.

11: Linha em branco.

12: Define método que checa se é válido inserir v na posição pos do caminho.

13: Verifica se v é vizinho do último vértice adicionado (caminho[pos-1]).

14: Se não for vizinho, rejeita.

15: Linha em branco.

16: Verifica se v já foi usado no caminho (evita repetição).

17: Se repetido, rejeita.

18: Linha em branco.

19: Caso passe nas verificações, aceita.

20: Linha em branco.

21: Método recursivo auxiliar do backtracking.

22: Caso base: se já posicionou V vértices, encontrou caminho completo.

23: Retorna sucesso.

24: Linha em branco.

25: Itera por todos os vértices como possíveis candidatos para a posição atual.

26: Testa se é seguro colocar v nesta posição.

27: Coloca v no caminho (faz a escolha).

28: Linha em branco.

29: Avança recursivamente para a próxima posição.

30: Se a recursão retornar sucesso, propaga sucesso.

31: Linha em branco.

32: Backtrack: desfaz a escolha (marca posição como -1).

33: Linha em branco.

34: Se nenhum v funcionar, retorna falha para este ramo.

35: Linha em branco.

36: Método público que tenta achar caminho a partir de diferentes vértices iniciais.

37: Inicializa caminho com -1 (posição vazia).

38: Linha em branco.

39: Itera todos os possíveis vértices iniciais.

40: Fixa o vértice inicial na posição 0.

41: Linha em branco.

42: Chama o auxiliar para preencher da posição 1 em diante.

43: Se encontrar, retorna o caminho.

44: Linha em branco.

45: Se nenhum início funcionar, informa ausência de caminho no console.

46: Retorna None (falha).

47: Linha em branco.

48: Linha em branco.

49: Ponto de entrada do script (executa apenas quando rodado diretamente).

50: Cria grafo não direcionado com 5 vértices.

51: Adiciona aresta (0, 1).

52: Adiciona aresta (0, 3).

53: Adiciona aresta (1, 2).

54: Adiciona aresta (1, 3).

55: Adiciona aresta (1, 4).

56: Adiciona aresta (2, 4).

57: Adiciona aresta (3, 4).

58: Linha em branco.

59: Invoca a busca por caminho hamiltoniano.

60: Linha em branco.

61: Se caminho encontrado...

62: Imprime rótulo de sucesso.

63: Imprime a sequência de vértices formatada.

64: Caso contrário...

65: Imprime mensagem de falha.

---

## Relatório Técnico

### Classes P, NP, NP-Completo e NP-Difícil

1. **Classificação do problema:**  
   O problema do **Caminho Hamiltoniano** está na classe **NP-Completo**.

2. **Justificativa:**  
   - O problema pertence à classe NP porque uma solução pode ser verificada em tempo polinomial.  
   - É NP-Completo pois qualquer problema em NP pode ser reduzido a ele em tempo polinomial.  
   - Relaciona-se diretamente com o **Problema do Caixeiro Viajante (TSP)**, que também é NP-Completo. A diferença é que no TSP há pesos e o objetivo é minimizar o custo, enquanto no Caminho Hamiltoniano buscamos apenas a existência de um caminho que passe por todos os vértices uma única vez.

---

### Análise da complexidade assintótica de tempo

1. **Complexidade temporal:**  
   A complexidade do algoritmo é **O(n!)**, onde n é o número de vértices.

2. **Método de determinação:**  
   - Foi utilizado a **contagem de operações**.  
   - A função `encontrar_caminho_hamiltoniano_util` tenta todos os possíveis caminhos, o que gera uma árvore de recursão com ramificações de ordem fatorial, já que cada posição pode ter múltiplas possibilidades dependendo do grafo.

---

### Aplicação do Teorema Mestre

- **Aplicabilidade:**  
  Não é possível aplicar o Teorema Mestre neste caso.
  
---

### Análise dos casos de complexidade

1. **Melhor caso:**  
   - Um caminho Hamiltoniano é encontrado logo nas primeiras tentativas.  
   - Complexidade é O(n!) ( o tempo é redusido pelas podas )

2. **Caso médio:**  
   - A média das execuções em diferentes grafos gera tentativa e erro com backtracking, ainda com complexidade O(n!).

3. **Pior caso:**  
   - Não existe caminho Hamiltoniano, e o algoritmo tenta **todas as combinações possíveis**.  
   - Tempo máximo de execução: **O(n!)** ( porém neste caso o tempo é maior do que nos 2 casos anteriores ).

4. **Impacto no desempenho:**  
   - A variação entre os casos pode impactar severamente o tempo de execução. O algoritmo não possui otimizações para evitar repetir estados ou reduzir a árvore de busca.