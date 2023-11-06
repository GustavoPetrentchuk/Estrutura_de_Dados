# Parte II: Listas, Pilhas e Filas.

## Tipos Abstratos de Dados: 
- **Módulos e Compilação em Separado:**
  - Uma forma de organizar e agrupar funcionalidades relacionadas em um programa em arquivos separados, onde cada arquivo é denominado um Módulo.
  - Em C, os módulos são implementados usando arquivos de cabeçalho (.h) para declarações e arquivos de código (.c) para a implementação.
  - Módulos facilitam a reutilização de código em diferentes partes do programa, uma vez que as funcionalidades podem ser compartilhadas em vários arquivos.
  - Mudanças em um módulo geralmente não afetam o restante do programa, o que torna a manutenção mais gerenciável.
  - A compilação em separado é o processo de compilar módulos individualmente antes de ligá-los em um programa executável.
  - Você não precisa recompilar todos os módulos sempre que um único módulo é modificado. Apenas o módulo modificado é recompilado, economizando tempo.
  - No processo de compilação em separado, cada módulo é compilado em um arquivo de objeto separado (.o ou .obj). Em seguida, esses arquivos de objeto são vinculados juntos para criar o executável final.
  
-  **TADs:**
   -  Um Tipo Abstrato de Dados (TAD) é uma abstração que descreve uma coleção de valores e um conjunto de operações que podem ser realizadas nesses valores.
   -  TADs são uma maneira de encapsular os detalhes de implementação de uma estrutura de dados, permitindo que os usuários a utilizem sem conhecer esses detalhes.
   -  Classes em linguagens orientadas a objetos frequentemente são usadas para implementar TADs.
- Características:
     - Encapsulamento: Os detalhes de implementação do TAD são ocultados do usuário.
     - Interface: O TAD define um conjunto de operações que podem ser realizadas nos valores do TAD.
     - Abstração: O usuário se concentra no que o TAD faz, não em como é implementado.
     - Reutilização: TADs facilitam a reutilização de código e modularidade.

- **Exemplo de TAD em linguagem C:**
  - Nesse exemplo de código, a estrutura interna do tabuleira é escondida dos usuários através do encapsulamento, e as funções são fornecidas para a manipulação do tabuleiro. Dessa forma, o usuário pode acessar e interagir com o tabuleiro sem ter acesso direto a estrutura interna do TAD.

```C
#include <stdio.h>
#include <stdlib.h>

typedef struct TabuleiroImpl Tabuleiro;

Tabuleiro* criarTabuleiro();

char acessarEspaco(Tabuleiro* tabuleiro, int linha, int coluna);

void liberarTabuleiro(Tabuleiro* tabuleiro);

struct TabuleiroImpl {
    char board[3][3];
};

Tabuleiro* criarTabuleiro() {
    Tabuleiro* novoTabuleiro = (Tabuleiro*)malloc(sizeof(Tabuleiro));
    if (novoTabuleiro != NULL) {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                novoTabuleiro->board[i][j] = ' ';
            }
        }
    }
    return novoTabuleiro;
}

char acessarEspaco(Tabuleiro* tabuleiro, int linha, int coluna) {
    if (tabuleiro != NULL && linha >= 0 && linha < 3 && coluna >= 0 && coluna < 3) {
        return tabuleiro->board[linha][coluna];
    } else {
        return '\0';
    }
}

void liberarTabuleiro(Tabuleiro* tabuleiro) {
    if (tabuleiro != NULL) {
        free(tabuleiro);
    }
}
```

## Listas:
  - **Listas Encadeadas:**
    - Uma lista encadeada é uma estrutura de dados linear composta por nós, onde cada nó armazena um valor e um ponteiro para o próximo nó na lista.
    - A principal característica é a alocação dinâmica de memória para nós, o que permite uma flexibilidade no tamanho da lista.
    - As listas encadeadas podem ser usadas para criar listas de tamanho variável.
  
- **Exemplo de implementação em C:**

    ```C
    #include <stdio.h>
    #include <stdlib.h>

    struct Node {
        int data;
        struct Node* next;
    };

    typedef struct Node Node;

    Node* criarNode(int data) {
        Node* newNode = (Node*)malloc(sizeof(Node));
        newNode->data = data;
        newNode->next = NULL;
        return newNode;
    }

    int main() {
        Node* head = criarNode(1);
        head->next = criarNode(2);
        head->next->next = criarNode(3);

        Node* current = head;
        while (current != NULL) {
            printf("%d -> ", current->data);
            current = current->next;
        }
        printf("NULL\n");

        return 0;
    }
    ```
  - **Implementação Recursiva:**
    - A recursão pode ser usada para percorrer ou realizar operações em listas encadeadas. A cada chamada recursiva, você pode avançar para o próximo nó da lista.
    - Um exemplo de recursão em uma lista encadeada é imprimir todos os elementos da lista de forma recursiva.
  
  - **Listas Circulares:**
    - Uma lista circular é uma variação de lista encadeada em que o último nó da lista aponta de volta para o primeiro nó, formando um ciclo.
    - Pode ser útil para implementar estruturas de dados cíclicas ou para criar uma fila circular.

  - **Exemplo de implementação em C:**
    ```C
    #include <stdio.h>
    #include <stdlib.h>

    struct Node {
        int data;
        struct Node* next;
    };

    typedef struct Node Node;

    Node* criarNode(int data) {
        Node* newNode = (Node*)malloc(sizeof(Node));
        newNode->data = data;
        newNode->next = newNode;
        return newNode;
    }

    int main() {
        Node* head = criarNode(1);
        head->next = criarNode(2);
        head->next->next = criarNode(3);

        Node* current = head;
        do {
            printf("%d -> ", current->data);
            current = current->next;
        } while (current != head);
        printf("...\n");

        return 0;
    }

    ```

  - **Listas Duplamente Encadeadas:**
    - Uma lista duplamente encadeada é uma lista em que cada nó possui uma referência tanto para o próximo nó quanto para o nó anterior na lista.
    - Permite percorrer a lista nos dois sentidos, avançando ou retrocedendo.
    - Facilita a remoção de elementos da lista sem a necessidade de percorrer a lista a partir do início.

  - **Exemplo de implementação em C:**
    ```C
    #include <stdio.h>
    #include <stdlib.h>

    struct Node {
        int data;
        struct Node* next;
        struct Node* prev;
    };

    typedef struct Node Node;

    Node* criarNode(int data) {
        Node* newNode = (Node*)malloc(sizeof(Node));
        newNode->data = data;
        newNode->next = NULL;
        newNode->prev = NULL;
        return newNode;
    }

    int main() {
        Node* head = criarNode(1);
        Node* second = criarNode(2);
        Node* third = criarNode(3);

        head->next = second;
        second->prev = head;
        second->next = third;
        third->prev = second;

        Node* current = head;
        while (current != NULL) {
            printf("%d -> ", current->data);
            current = current->next;
        }
        printf("NULL\n");

        return 0;
    }
    ```

  - **Listas de Tipos Estruturados:**
    - Em vez de armazenar apenas valores simples em nós de lista, você pode armazenar tipos de dados estruturados, como structs, em cada nó.
    - Listas de tipos estruturados são frequentemente usadas para criar estruturas de dados complexas, como listas de contatos, listas de tarefas, etc.
    - Cada nó contém uma estrutura que pode conter vários campos de dados.

  - **Exemplo de implementação em C:**
    ```C
    #include <stdio.h>
    #include <stdlib.h>

    struct Pessoa {
        char nome[50];
        int idade;
    };

    typedef struct Pessoa Pessoa;

    struct Node {
        Pessoa data;
        struct Node* next;
    };

    typedef struct Node Node;

    Node* criarNode(Pessoa data) {
        Node* newNode = (Node*)malloc(sizeof(Node));
        newNode->data = data;
        newNode->next = NULL;
        return newNode;
    }

    int main() {
        Pessoa pessoa1 = {"Gustavo", 24};
        Pessoa pessoa2 = {"Lucas", 30};
        Pessoa pessoa3 = {"Aldir", 35};

        Node* head = criarNode(pessoa1);
        head->next = criarNode(pessoa2);
        head->next->next = criarNode(pessoa3);

        Node* current = head;
        while (current != NULL) {
            printf("Nome: %s, Idade: %d\n", current->data.nome, current->data.idade);
            current = current->next;
        }

        return 0;
    }
    ```

## Pilhas:
- **Pilha:**
  - Uma pilha é uma estrutura de dados linear que segue o princípio "último a entrar, primeiro a sair" (LIFO - Last-In-First-Out).
  - As operações em uma pilha ocorrem apenas na extremidade superior, onde os elementos são inseridos e removidos.
  - A interface do tipo pilha define as operações disponíveis para interagir com uma pilha. As principais operações realizadas em pilhas:
     * Push: Adiciona um elemento à pilha.
     * Pop: Remove e retorna o elemento do topo da pilha.
     * Top: Retorna o elemento no topo da pilha sem removê-lo.
     * Empty: Verifica se a pilha está vazia.

- **Implementação de Pilha com Vetor:**
    - Uma pilha implementada com vetor utiliza um array para armazenar os elementos da pilha, E mantém um índice que aponta para o topo da pilha.
    - É uma forma de acessar rapidamente aos elementos da pilha.
    - Possui um tamanho fixo, podendo ser redimensionado manualmente.
    - Pode resultar em estouro de pilha se o tamanho máximo for atingido.

  - **Exemplo de implementação em C:**
    ```C
    #include <stdio.h>
    #include <stdlib.h>

    #define MAX_SIZE 10

    struct Pilha {
        int items[MAX_SIZE];
        int top;
    };

    typedef struct Pilha Pilha;

    Pilha criarPilha() {
        Pilha pilha;
        pilha.top = -1;
        return pilha;
    }

    int estaVazia(Pilha* pilha) {
        return pilha->top == -1;
    }

    int estaCheia(Pilha* pilha) {
        return pilha->top == MAX_SIZE - 1;
    }

    void empilhar(Pilha* pilha, int valor) {
        if (!estaCheia(pilha)) {
            pilha->items[++pilha->top] = valor;
        } else {
            printf("Erro: a pilha está cheia, %d.\n", valor);
        }
    }

    int desempilhar(Pilha* pilha) {
        if (!estaVazia(pilha)) {
            return pilha->items[pilha->top--];
        } else {
            printf("Erro: a pilha está vazia.\n");
            return -1;
        }
    }

    int topo(Pilha* pilha) {
        if (!estaVazia(pilha)) {
            return pilha->items[pilha->top];
        } else {
            printf("Erro: a pilha está vazia.\n");
            return -1;
        }
    }

    int main() {
        Pilha pilha = criarPilha();

        empilhar(&pilha, 1);
        empilhar(&pilha, 2);
        empilhar(&pilha, 3);

        printf("Topo da pilha: %d\n", topo(&pilha));

        printf("Desempilhando: %d\n", desempilhar(&pilha));
        printf("Topo da pilha: %d\n", topo(&pilha));

        return 0;
    }
  ```

- **Implementação de Pilha com Lista Encadeada:**
    - Uma pilha implementada com lista encadeada usa nós para representar os elementos da pilha. O nó no topo da pilha é a cabeça da lista.
    - Possui tamanho dinâmico, e sem riscos de estouro da pilha.
    - Acesso não tão rápido quanto em uma implementação de vetor.
    - Usa mais memória devido aos nós.

  - **Exemplo de implementação em C:**
    ```C
    #include <stdio.h>
    #include <stdlib.h>

    struct Node {
        int data;
        struct Node* next;
    };

    typedef struct Node Node;

    struct Pilha {
        Node* top;
    };

    typedef struct Pilha Pilha;

    Pilha criarPilha() {
        Pilha pilha;
        pilha.top = NULL;
        return pilha;
    }

    int estaVazia(Pilha* pilha) {
        return pilha->top == NULL;
    }

    void empilhar(Pilha* pilha, int valor) {
        Node* newNode = (Node*)malloc(sizeof(Node));
        newNode->data = valor;
        newNode->next = pilha->top;
        pilha->top = newNode;
    }

    int desempilhar(Pilha* pilha) {
        if (!estaVazia(pilha)) {
            Node* temp = pilha->top;
            int valor = temp->data;
            pilha->top = temp->next;
            free(temp);
            return valor;
        } else {
            printf("Erro: a pilha está vazia.\n");
            return -1;
        }
    }

    int topo(Pilha* pilha) {
        if (!estaVazia(pilha)) {
            return pilha->top->data;
        } else {
            printf("Erro: a pilha está vazia.\n");
            return -1;
        }
    }

    int main() {
        Pilha pilha = criarPilha();

        empilhar(&pilha, 1);
        empilhar(&pilha, 2);
        empilhar(&pilha, 3);

        printf("Topo da pilha: %d\n", topo(&pilha));

        printf("Desempilhando: %d\n", desempilhar(&pilha));
        printf("Topo da pilha: %d\n", topo(&pilha));

        return 0;
    }
  ```  

## Filas:
- **Fila:**
    - Uma fila é uma estrutura de dados linear que segue o princípio "primeiro a entrar, primeiro a sair" (FIFO - First-In-First-Out).
    - Elementos são adicionados à fila na extremidade de trás e removidos na extremidade da frente.
    - As operações ocorrem em ambas as extremidades da fila.
    - A interface do tipo fila define as operações disponíveis para interagir com uma fila. Ela é composta por funções que permitem enfileirar, desenfileirar, consultar o elemento da frente e da parte de trás, e verificar se a fila está vazia.

- **Implementação de Fila com Vetor:**
  - Uma fila implementada com vetor utiliza um array para armazenar os elementos da fila.
  - Mantém dois índices, um para a frente e outro para a parte de trás, controlando onde os elementos são inseridos e removidos.
  - Possui acesso rápido às operações de enfileirar e desenfileirar.
  - Tamanho fixo. Pode resultar em estouro de fila se o tamanho máximo for atingido.

  ```C
    #include <stdio.h>
    #include <stdlib.h>

    #define MAX_SIZE 10

    struct Lista {
        int items[MAX_SIZE];
        int tamanho;
    };

    typedef struct Lista Lista;

    Lista criarLista() {
        Lista lista;
        lista.tamanho = 0;
        return lista;
    }

    int estaVazia(Lista* lista) {
        return lista->tamanho == 0;
    }

    int estaCheia(Lista* lista) {
        return lista->tamanho == MAX_SIZE;
    }

    void inserir(Lista* lista, int valor) {
        if (!estaCheia(lista)) {
            lista->items[lista->tamanho] = valor;
            lista->tamanho++;
        } else {
            printf("Erro: a lista está cheia, %d.\n", valor);
        }
    }

    void remover(Lista* lista, int indice) {
        if (indice >= 0 && indice < lista->tamanho) {
            for (int i = indice; i < lista->tamanho - 1; i++) {
                lista->items[i] = lista->items[i + 1];
            }
            lista->tamanho--;
        } else {
            printf("Erro: índice fora dos limites.\n");
        }
    }

    int consultar(Lista* lista, int indice) {
        if (indice >= 0 && indice < lista->tamanho) {
            return lista->items[indice];
        } else {
            printf("Erro: índice fora dos limites.\n");
            return -1;
        }
    }

    int main() {
        Lista lista = criarLista();

        inserir(&lista, 1);
        inserir(&lista, 2);
        inserir(&lista, 3);

        printf("Elemento na posição 1: %d\n", consultar(&lista, 1));

        remover(&lista, 0);

        printf("Elemento na posição 0 após remoção: %d\n", consultar(&lista, 0));

        return 0;
    }
  ```

- **Implementação de Fila com Lista Encadeada:**
  - Uma fila implementada com lista encadeada usa nós para representar os elementos da fila. Mantém referências para o nó da frente e o nó de trás da fila.
  - Tamanho dinâmico. Não há preocupações com estouro de fila.
  - O acesso às operações pode ser mais lento do que em uma implementação de vetor.
  - Usa mais memória devido aos nós.
  
- **Implementação de Fila Dupla:**
  - Uma fila dupla, permite a inserção e remoção de elementos em ambas as extremidades (frente e trás) da fila.
  ![Representação de fila dupla](https://www.mundojs.com.br/wp-content/uploads/2018/02/insertion-and-deletion-in-a-deque.jpg)

- **Fila Dupla com Lista Encadeada:**
  - Uma fila dupla implementada com lista encadeada é semelhante à fila com lista encadeada, mas permite a inserção e remoção de elementos tanto na frente quanto na parte de trás
  - Acesso às operações pode ser mais lento do que em outras estruturas para certas operações.

  ```C
    #include <stdio.h>
    #include <stdlib.h>

    struct Node {
        int data;
        struct Node* next;
        struct Node* prev;
    };

    typedef struct Node Node;

    struct FilaDupla {
        Node* frente;
        Node* tras;
    };

    typedef struct FilaDupla FilaDupla;

    FilaDupla criarFilaDupla() {
        FilaDupla fila;
        fila.frente = NULL;
        fila.tras = NULL;
        return fila;
    }

    int estaVazia(FilaDupla* fila) {
        return (fila->frente == NULL && fila->tras == NULL);
    }

    void enfileirarFrente(FilaDupla* fila, int valor) {
        Node* newNode = (Node*)malloc(sizeof(Node));
        newNode->data = valor;
        newNode->next = NULL;
        newNode->prev = NULL;

        if (estaVazia(fila)) {
            fila->frente = newNode;
            fila->tras = newNode;
        } else {
            newNode->next = fila->frente;
            fila->frente->prev = newNode;
            fila->frente = newNode;
        }
    }

    void enfileirarTras(FilaDupla* fila, int valor) {
        Node* newNode = (Node*)malloc(sizeof(Node));
        newNode->data = valor;
        newNode->next = NULL;
        newNode->prev = NULL;

        if (estaVazia(fila)) {
            fila->frente = newNode;
            fila->tras = newNode;
        } else {
            newNode->prev = fila->tras;
            fila->tras->next = newNode;
            fila->tras = newNode;
        }
    }

    int desenfileirarFrente(FilaDupla* fila) {
        if (!estaVazia(fila)) {
            Node* temp = fila->frente;
            int valor = temp->data;
            if (fila->frente == fila->tras) {
                fila->frente = NULL;
                fila->tras = NULL;
            } else {
                fila->frente = fila->frente->next;
                fila->frente->prev = NULL;
            }
            free(temp);
            return valor;
        } else {
            printf("Erro: a fila dupla está vazia.\n");
            return -1;
        }
    }

    int desenfileirarTras(FilaDupla* fila) {
        if (!estaVazia(fila)) {
            Node* temp = fila->tras;
            int valor = temp->data;
            if (fila->frente == fila->tras) {
                fila->frente = NULL;
                fila->tras = NULL;
            } else {
                fila->tras = fila->tras->prev;
                fila->tras->next = NULL;
            }
            free(temp);
            return valor;
        } else {
            printf("Erro: a fila dupla está vazia.\n");
            return -1;
        }
    }

    int main() {
        FilaDupla fila = criarFilaDupla();

        enfileirarFrente(&fila, 1);
        enfileirarFrente(&fila, 2);
        enfileirarTras(&fila, 3);

        printf("Desenfileirando da frente: %d\n", desenfileirarFrente(&fila));
        printf("Desenfileirando da parte de trás: %d\n", desenfileirarTras(&fila));

        return 0;
    }
  ```

#### Referências Bibliográficas
1. Waldemar Celes. Renato Cerqueira. José Lucas Rangel. Introdução a Estrutura de Dados: Com Técnicas de Programação em C.
2. António Manuel Adrego da Rocha. António Rui Oliveira e Silva Borges. Estruturas de Dados e Algoritmos em C.