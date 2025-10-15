
# Hamiltonian Path Finder

## Execução
Para executar o código, abra o terminal (cmd) no diretório onde está localizado o arquivo `main.py` e utilize o comando:
```bash
python main.py
```

---

## Explicação linha a linha

Explicação Linha a Linha
**`class Grafo:`**
- Define a classe principal que representa um grafo

**`def __init__(self, vertices, direcionado=False):`**
- Método construtor que inicializa o grafo

**`self.V = vertices`**
- Armazena o número total de vértices

**`self.grafo = {v: [] for v in range(vertices)}`**
- Cria um dicionário onde cada vértice tem uma lista vazia de vizinhos

**`self.direcionado = direcionado`**
- Define se o grafo é direcionado ou não

## Método adicionar_aresta

**`def adicionar_aresta(self, u, v):`**
- Método para adicionar uma aresta entre dois vértices

**`self.grafo[u].append(v)`**
- Adiciona o vértice v à lista de adjacência de u

**`if not self.direcionado:`**
- Verifica se o grafo não é direcionado

**`self.grafo[v].append(u)`**
- Se não for direcionado, adiciona u à lista de v (bidirecional)

## Método eh_seguro

**`def eh_seguro(self, v, pos, caminho):`**
- Verifica se é seguro adicionar um vértice ao caminho

**`if v not in self.grafo[caminho[pos-1]]:`**
- Checa se v é adjacente ao último vértice adicionado

**`return False`**
- Retorna falso se não for adjacente

**`if v in caminho:`**
- Verifica se o vértice já está no caminho

**`return False`**
- Retorna falso se o vértice já foi visitado

**`return True`**
- Retorna verdadeiro se passar em todas as verificações

## Método encontrar_caminho_hamiltoniano_util

**`def encontrar_caminho_hamiltoniano_util(self, caminho, pos):`**
- Método recursivo auxiliar para backtracking

**`if pos == self.V:`**
- Caso base: verifica se todos os vértices foram visitados

**`return True`**
- Retorna verdadeiro quando o caminho está completo

**`for v in range(self.V):`**
- Itera por todos os vértices possíveis

**`if self.eh_seguro(v, pos, caminho):`**
- Verifica se o vértice pode ser adicionado

**`caminho[pos] = v`**
- Adiciona o vértice ao caminho

**`if self.encontrar_caminho_hamiltoniano_util(caminho, pos+1):`**
- Chamada recursiva para a próxima posição

**`return True`**
- Propaga o sucesso da recursão

**`caminho[pos] = -1`**
- Backtracking: remove o vértice se não levar à solução

**`return False`**
- Retorna falso se nenhum vértice funcionar

## Método encontrar_caminho_hamiltoniano

**`def encontrar_caminho_hamiltoniano(self):`**
- Método principal para encontrar o caminho hamiltoniano

**`caminho = [-1] * self.V`**
- Inicializa o caminho com valores -1 (não visitado)

**`for inicio in range(self.V):`**
- Tenta cada vértice como ponto de partida

**`caminho[0] = inicio`**
- Define o vértice inicial

**`if self.encontrar_caminho_hamiltoniano_util(caminho, 1):`**
- Chama o método auxiliar começando da posição 1

**`return caminho`**
- Retorna o caminho encontrado

**`print("Não existe caminho hamiltoniano")`**
- Mensagem de falha (caractere corrompido no original)

**`return None`**
- Retorna None se não encontrar caminho

## Bloco Principal

**`if __name__ == "__main__":`**
- Garante que o código só executa quando o arquivo é rodado diretamente

**`g = Grafo(5, direcionado=False)`**
- Cria um grafo não direcionado com 5 vértices

**`g.adicionar_aresta(0, 1)`** até **`g.adicionar_aresta(3, 4)`**
- Adiciona as arestas que formam o grafo

**`caminho = g.encontrar_caminho_hamiltoniano()`**
- Executa a busca pelo caminho hamiltoniano

**`if caminho:`**
- Verifica se um caminho foi encontrado

**`print("Caminho Hamiltoniano encontrado:")`**
- Mensagem de sucesso

**`print(" => ".join(map(str, caminho)))`**
- Formata e exibe o caminho encontrado

**`else:`**
- Caso nenhum caminho seja encontrado

**`print("Nenhum caminho hamiltoniano encontrado")`**
- Mensagem de falha final

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
