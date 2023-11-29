# Parte III: Árvores, Ordenação, Busca e Tabelas de Dispersão.

## Árvores:
- Uma árvore é uma estrutura de dados hierárquica que consiste em nós conectados.
- Cada nó em uma árvore tem um pai (exceto o nó superior, chamado de raiz) e zero ou mais filhos. 
- Os nós que não têm filhos são chamados de folhas.
- A estrutura de árvore é amplamente utilizada em ciência da computação para representar hierarquias, como a estrutura de pastas e arquivos em um sistema de arquivos.

- **Árvores binárias:**
  - Uma árvore binária é um tipo específico de árvore em que cada nó possui no máximo dois filhos, um à esquerda e outro à direita.
  - A ordem dos nós em uma árvore binária é crucial para determinar a eficiência de muitas operações, como busca e inserção.
  - Em uma árvore de busca binária, os nós são organizados de forma que os elementos menores do que o nó pai estão à esquerda, e os elementos maiores estão à direita. Isso facilita a busca eficiente de elementos na árvore.

- **Árvores com número variável de filhos:**
  - Árvores com número variável de filhos são aquelas em que cada nó pode ter um número arbitrário de filhos.
  - Um nó pode ter de 0 a n filhos.

## Ordenação:
- Ordenação é o processo de organização de um conjunto de elementos em uma ordem específica.
- O objetivo é facilitar a busca e recuperação eficiente de dados.

- **Ordenação bolha:**
  - Algoritmo de ordenação simples que percorre repetidamente a lista, compara elementos adjacentes e os troca se estiverem na ordem errada.
  - O processo é repetido até que a lista esteja ordenada. O nome "bolha" vem do fato de que os elementos menores "brotam" para o topo da lista gradualmente, assim como bolhas sobem na água.
  
```C
  #include <stdio.h>

  void bubbleSort(int arr[], int n) {
      for (int i = 0; i < n - 1; i++) {
          for (int j = 0; j < n - i - 1; j++) {
              if (arr[j] > arr[j + 1]) {
                  int temp = arr[j];
                  arr[j] = arr[j + 1];
                  arr[j + 1] = temp;
              }
          }
      }
  }

  int main() {

      int n = 5;
      int vetor[5];

      printf("Digite 5 numeros inteiros:\n");

      for (int i = 0; i < n; i++) {
          printf("Número %d: ", i + 1);
          scanf("%d", &vetor[i]);
      }

      printf("\nVetor antes da ordenacao:\n");
      for (int i = 0; i < n; i++) {
          printf("%d ", vetor[i]);
      }

      bubbleSort(vetor, n);

      printf("\nVetor apos a ordenacao bolha:\n");
      for (int i = 0; i < n; i++) {
          printf("%d ", vetor[i]);
      }

      return 0;
  }
```

- **Ordenação rápida:**
  - algoritmo onde um elemento é escolhido como pivô e a lista é particionada em duas sub-listas, uma contendo elementos menores que o pivô e outra com elementos maiores.
  - O processo é então aplicado recursivamente a ambas as sub-listas.

```C
  #include <stdio.h>

  void trocar(int *a, int *b) {
      int temp = *a;
      *a = *b;
      *b = temp;
  }

  int particionar(int arr[], int baixo, int alto) {
      int pivô = arr[alto];
      int i = (baixo - 1);

      for (int j = baixo; j <= alto - 1; j++) {
          if (arr[j] < pivô) {
              i++;
              trocar(&arr[i], &arr[j]);
          }
      }
      trocar(&arr[i + 1], &arr[alto]);
      return (i + 1);
  }

  void quicksort(int arr[], int baixo, int alto) {
      if (baixo < alto) {
          int pi = particionar(arr, baixo, alto);

          quicksort(arr, baixo, pi - 1);
          quicksort(arr, pi + 1, alto);
      }
  }

  int main() {
  
      int n = 5;

      int vetor[5];

      printf("Digite 5 números inteiros:\n");

      for (int i = 0; i < n; i++) {
          printf("Número %d: ", i + 1);
          scanf("%d", &vetor[i]);
      }

      printf("\nVetor antes da ordenação:\n");
      for (int i = 0; i < n; i++) {
          printf("%d ", vetor[i]);
      }

      quicksort(vetor, 0, n - 1);

      printf("\nVetor após a ordenação rápida:\n");
      for (int i = 0; i < n; i++) {
          printf("%d ", vetor[i]);
      }

      return 0;
  }

```

## Busca:
- **Busca em vetor:**
  - O algoritmo de busca linear, percorre o vetor elemento por elemento até encontrar o item desejado ou atingir o final do vetor. Abordagem simples, mas pode ser ineficiente para grandes conjuntos de dados.
  - O algoritmo de busca binária é uma abordagem mais eficiente, mas requer que o vetor esteja ordenado.A ideia é dividir repetidamente o vetor ao meio e comparar o valor do meio com o elemento desejado. Com base nessa comparação, a busca continua na metade relevante do vetor.

```C
  #include <stdio.h>

  int buscaBinaria(int arr[], int tamanho, int chave) {
      int inicio = 0;
      int fim = tamanho - 1;

      while (inicio <= fim) {
          int meio = inicio + (fim - inicio) / 2;

          if (arr[meio] == chave) {
              return meio;
          }

          if (arr[meio] > chave) {
              fim = meio - 1;
          }

          else {
              inicio = meio + 1;
          }
      }

      return -1;
  }

  int main() {
      int vetor[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
      int tamanho = sizeof(vetor) / sizeof(vetor[0]);
      int chave;

      printf("Digite a chave que deseja buscar: ");
      scanf("%d", &chave);

      int resultado = buscaBinaria(vetor, tamanho, chave);

      if (resultado != -1) {
          printf("Chave encontrada no índice %d.\n", resultado);
      } else {
          printf("Chave não encontrada no vetor.\n");
      }

      return 0;
  }
```


- **Árvore binária de busca:**
  - Uma Árvore Binária de Busca é uma estrutura de dados em árvore onde cada nó possui no máximo dois filhos chamados de subárvores, e para cada nó, todos os elementos na subárvore à esquerda são menores que o nó e todos os elementos na subárvore à direita são maiores.
  - A ordem dos elementos em uma árvore binária de busca permite uma busca eficiente.

  ![Representação de árvore binária de busca](https://upload.wikimedia.org/wikipedia/commons/thumb/d/da/Binary_search_tree.svg/1024px-Binary_search_tree.svg.png)


## Tabelas de Dispersão:
- **Hashtables:**
  - Uma hash table é uma estrutura de dados que permite o armazenamento e recuperação eficiente de dados, utiliza uma função de dispersão para mapear chaves para índices em uma tabela.
  - Em condições ideais, a função de dispersão distribui uniformemente as chaves pelos índices da tabela, minimizando colisões.
  - A busca, inserção e remoção de elementos podem ser realizadas em tempo constante, tornando as tabelas de dispersão extremamente eficientes.
  

- **Função de Dispersão:**
  - Responsável por transformar a chave do elemento em um índice na tabela.
  - Essa função deve distribuir as chaves de maneira uniforme para evitar colisões excessivas.
  
- **Tratamento de Colisão:**
  - Colisões ocorrem quando duas chaves diferentes são mapeadas para o mesmo índice pela função de dispersão.
  - **Encadeamento Separado:** Cada célula da tabela contém uma lista encadeada de elementos que mapeiam para o mesmo índice. Quando ocorre uma colisão, os elementos são simplesmente adicionados à lista.
  - **Endereçamento Aberto:** 
    - Sondagem Linear: Se houver uma colisão, procura-se linearmente por um próximo slot vazio.
    - Sondagem Quadrática: Similar à linear, mas a busca por um próximo slot vazio é feita de maneira quadrática (i²) em vez de linear (i).
    - Duplo Hashing: Usa uma segunda função de dispersão para calcular a próxima posição em caso de colisão.
  - **Rehashing:** Periodicamente, a tabela é aumentada de tamanho e os elementos são reorganizados. Isso ajuda a manter um fator de carga baixo e a evitar colisões excessivas.
  - **Cadeamento Coalescido:** Semelhante ao encadeamento separado, mas em vez de ter uma lista encadeada em cada célula da tabela, todos os elementos são armazenados em uma única lista global.
  - **Cuckoo Hashing:** Um método de endereçamento aberto que envolve dois arrays, e se uma posição é ocupada, o elemento existente é empurrado para o outro array.

  ```C
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>

    #define TAMANHO_TABELA 10

    struct Node {
        char chave[50];
        struct Node* proximo;
    };

    unsigned int funcaoDispersao(const char* chave) {
        unsigned int hash = 0;
        for (int i = 0; chave[i] != '\0'; i++) {
            hash += chave[i];
        }
        return hash % TAMANHO_TABELA;
    }

    struct Node* criarNo(const char* chave) {
        struct Node* novoNo = (struct Node*)malloc(sizeof(struct Node));
        strcpy(novoNo->chave, chave);
        novoNo->proximo = NULL;
        return novoNo;
    }

    void inserirChave(struct Node* tabela[], const char* chave) {
        unsigned int indice = funcaoDispersao(chave);

        struct Node* novoNo = criarNo(chave);

        if (tabela[indice] == NULL) {
            tabela[indice] = novoNo;
        } else {
            novoNo->proximo = tabela[indice];
            tabela[indice] = novoNo;
        }
    }

    int buscarChave(struct Node* tabela[], const char* chave) {
        unsigned int indice = funcaoDispersao(chave);

        struct Node* atual = tabela[indice];

        while (atual != NULL) {
            if (strcmp(atual->chave, chave) == 0) {
                return 1;
            }
            atual = atual->proximo;
        }

        return 0;
    }

    int main() {
        struct Node* tabela[TAMANHO_TABELA];
        for (int i = 0; i < TAMANHO_TABELA; i++) {
            tabela[i] = NULL;
        }

        inserirChave(tabela, "Maca");
        inserirChave(tabela, "Banana");
        inserirChave(tabela, "Laranja");
        inserirChave(tabela, "Uva");

        printf("Busca por 'Banana': %s\n", buscarChave(tabela, "Banana") ? "Encontrada" : "Não encontrada");
        printf("Busca por 'Kiwi': %s\n", buscarChave(tabela, "Kiwi") ? "Encontrada" : "Não encontrada");

        return 0;
    }
  ```

#### Referências Bibliográficas
1. Waldemar Celes. Renato Cerqueira. José Lucas Rangel. Introdução a Estrutura de Dados: Com Técnicas de Programação em C.
2. António Manuel Adrego da Rocha. António Rui Oliveira e Silva Borges. Estruturas de Dados e Algoritmos em C.