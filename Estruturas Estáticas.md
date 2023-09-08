# Parte I: Estruturas Estáticas


## Vetores e Alocação Dinâmica
  - **Vetores:**
    - Também conhecidos como arrays, vetores são estruturas de dados que permitem armazenar um conjunto de valores do mesmo tipo em uma única variável.
    - Vetores reservam espaços adjacentes na memória para armazenar seus dados.
    - São acessados por meio de índice. O primeiro elemento tem o índice 0, o segundo o índice 1 e assim por diante.
    - Possuem um tamanho fixo, ou seja, seu tamanho é definido na hora em que o vetor é criado.
    - Passar um vetor como argumento para uma função em C, na verdade, você está passando um ponteiro que aponta para o endereço de memória da primeira posição do vetor.
    - Para passar um valor do vetor para uma função, a mesma deve possuir um ponteiro capaz de armazenar o endereço de memória do valor fornecido.

  - **Exemplo de vetor em linguagem C:**
    - Nesse código, usuário insere o tamanho fixo do vetor e, em seguida, insira os valores para preenchê-lo. Após isso o vetor é passado como parâmetro para a função que incrementa seus valores com base no índice.
```c
#include <stdio.h>

void incrementarComIndice(int vetor[], int tamanho) {
    for (int i = 0; i < tamanho; i++) {
        vetor[i] += i;
    }
}

int main() {
    int tamanho;

    printf("Digite o tamanho do vetor: ");
    scanf("%d", &tamanho);

    int vetor[tamanho];

    printf("Digite os valores do vetor:\n");
    for (int i = 0; i < tamanho; i++) {
        printf("Valor %d: ", i+1);
        scanf("%d", &vetor[i]);
    }

    incrementarComIndice(vetor, tamanho);

    printf("Valores incrementados com base no índice:\n");
    for (int i = 0; i < tamanho; i++) {
        printf("%d ", vetor[i]);
    }
    printf("\n");

    return 0;
}
```  
**Alocação Dinâmica:**
    - Recurso que permite um programa alocar e liberar memória durante sua execução, em vez de alocar memória de maneira estática no início.
    - Em geral, o uso de alocação dinâmica é reservado para casos específicos aonde não se tem conhecimento do tamanho necessário para alocação do vetor.
    - Em linguagem C, as funções malloc, calloc, realloc e free são usadas para alocar e liberar memória dinamicamente.
    - A alocação dinâmica requer um cuidadoso gerenciamento de memória para evitar vazamentos ou acesso indevido à memória.


  - **Exemplo alocação dinâmica com vetor em linguagem C:**
     - Similar ao exemplo anterior com vetor, esse código solicita ao usuário um valor para o tamanho do vetor e aloca dinâmicamente os espaços de memória para o mesmo.
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int tamanho;

    printf("Digite o tamanho do vetor: ");
    scanf("%d", &tamanho);

    // Aloca dinamicamente memória para o vetor com base no tamanho fornecido pelo usuário
    int *vetor = (int *)malloc(tamanho * sizeof(int));

    if (vetor == NULL) {
        printf("Erro na alocação de memória.\n");
        return 1; // Saída com erro
    }

    printf("Digite os valores para cada índice do vetor:\n");
    for (int i = 0; i < tamanho; i++) {
        printf("Valor %d: ", i);
        scanf("%d", &vetor[i]);
    }

    printf("Valores do vetor:\n");
    for (int i = 0; i < tamanho; i++) {
        printf("%d ", vetor[i]);
    }
    printf("\n");

    free(vetor);

    return 0;
}
```
## Matrizes

## Cadeias de Caracteres

## Tipos Estruturados


#### Referências Bibliográficas
1. Waldemar Celes. Renato Cerqueira. José Lucas Rangel. Introdução a Estrutura de Dados: Com Técnicas de Programação em C.
2. António Manuel Adrego da Rocha. António Rui Oliveira e Silva Borges. Estruturas de Dados e Algoritmos em C. 
