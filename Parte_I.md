# Parte I: Estruturas Estáticas


## Vetores e Alocação Dinâmica
  - **Vetores:**
    - Também conhecidos como arrays, vetores são estruturas de dados que permitem armazenar um conjunto de valores do mesmo tipo em uma única variável.
    - Vetores reservam espaços adjacentes na memória para armazenar seus dados.
    - São acessados por meio de índice. O primeiro elemento tem o índice 0, o segundo o índice 1 e assim por diante.
    - Possuem um tamanho fixo, ou seja, seu tamanho é definido na hora em que o vetor é criado.
    - Passar um vetor como argumento para uma função em C, na verdade, você está passando um ponteiro que aponta para o endereço de memória da primeira posição do vetor.
    - Para passar um valor do vetor para uma função, a mesma deve possuir um ponteiro capaz de armazenar o endereço de memória do valor fornecido.

    - Representação de vetor:
    ![Representação de vetor](https://embarcados.com.br/wp-content/uploads/2015/12/Mem%C3%B3ria13.png)
    - Na imagem, vemos um vetor alocado na memória do computador, ocupando os espaços de memória endereçados entre 108 e 144. Bem como um ponteiro alocado no endereço 100 da memória, que armazena o endereço do primeiro índice do vetor.

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
- **Matriz:**
  - Também conhecidas como vetores bidimensionais, as matrizes são estruturas de dados que permitem armazenar um conjunto de valores do mesmo tipo em múltiplas dimensões.
  - As matrizes reservam espaços adjacentes na memória para armazenar seus dados, organizados em linhas e colunas.
  - São acessadas por meio de índices que especificam a posição de um elemento na matriz. As linhas e colunas também são indexadas a partir de 0.
  - Possuem um tamanho fixo em todas as dimensões, ou seja, suas dimensões (número de linhas e colunas) são definidas na hora em que a matriz é criada.
  - Matrizes podem ter mais de duas dimensões, tornando-as matrizes multidimensionais. A notação para acessar elementos em matrizes bidimensionais é mat[i][j], onde "i" é o índice da linha e "j" é o índice da coluna. Para matrizes tridimensionais, a notação seria mat[i][j][k], e assim por diante, dependendo do número de dimensões.


- **Exemplo de Matriz em linguagem C:**
  - Exemplo simples de declaração matriz com dimensões 3x3, para armazenar números inteiros.
```c
#include <stdio.h>

int main() {
    int matriz[3][3];

    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            matriz[i][j] = i * 4 + j + 1;
        }
    }

    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            printf("%d\t", matriz[i][j]);
        }
        printf("\n");
    }

    return 0;
}
```

## Cadeias de Caracteres (Strings)
- **Strings:**
  - Em C, as cadeias de caracteres são representadas como arrays de caracteres terminados por um caractere nulo ('\0').
  - São utilizadas para armazenar sequências de caracteres, como palavras, frases ou textos.
  - Para declarar e inicializar uma string, você pode usar a notação de vetor de caracteres, por exemplo: "char minhaString[]".
  - Também é possível declarar uma string sem especificar o tamanho e o compilador determinará o tamanho com base na string de inicialização: char outraString[] = "HelloWorld".
  - Para manipular strings, a linguagem C fornece uma biblioteca padrão chamada <string.h>, que contém funções para copiar, concatenar, comparar e muitas outras operações com strings.
  - Strings em C são arrays de caracteres, e você pode acessar caracteres individuais usando índices, por exemplo: "char primeiroChar = minhaString[0]".
  - Para comparar duas strings em C, você pode usar a função strcmp da biblioteca <string.h>, que retorna um valor inteiro indicando a igualdade ou a ordem lexicográfica das strings.
  -  É importante garantir que uma string tenha espaço suficiente para acomodar todos os caracteres, incluindo o caractere nulo, para evitar problemas de estouro de buffer.


- **Exemplo de String em linguagem C:**
  - Nesse exemplo declaramos um vetor de caracteres simples, com espaço para até 25 caracteres e o caracter nulo "\0", essa string armazena uma entrada do usuário e a imprime na tela.\
  
```c
#include <stdio.h>

int main() {
    char minhaString[25];

    printf("Digite uma frase: ");
    scanf("%25[^\n]", minhaString);

    printf("Você digitou: %s\n", minhaString);

    return 0;
}
```
## Tipos Estruturados

Tipos estruturados são usados para organizar dados complexos em programas C, permitindo que você crie representações personalizadas de objetos e suas propriedades. Eles são amplamente utilizados em programação para modelar entidades do mundo real, como pessoas, veículos, produtos, etc.

- **Estruturas (structs):**
  - Uma estrutura é uma coleção de variáveis de tipos diferentes, agrupadas sob um único nome.
  - Cada variável dentro de uma estrutura é chamada de membro ou campo.
  - Para definir uma estrutura, você usa a palavra-chave struct, seguida do nome da estrutura e a lista de membros entre chaves.
  
- **Exemplo de declaração de Struct:**
  ```c
  struct Pessoa {
        char nome[50];
        int idade;
        float altura;
    };
  ```

  - Para acessar os membros de uma estrutura, você utiliza o operador ponto (.).
- 
    ```c
    struct Pessoa pessoa1;
    pessoa1.idade = 30;
    ```

- **Unions (union):**
  - Uma union é semelhante a uma estrutura, mas todos os membros compartilham o mesmo espaço de memória.
  - Todos os membros compartilham o mesmo espaço de memória.
  - Unions são úteis quando você precisa armazenar diferentes tipos de dados em um espaço de memória compartilhado.

- **Exemplo de declaração de Union:**
  ```c
    union Dado {
        int inteiro;
        float flutuante;
        char caractere;
    };
  ```
    - Acessar membros de uma union é semelhante à estrutura, usando o operador ponto (`.``). Apenas um membro da union deve ser acessado de cada vez.
  
#### Referências Bibliográficas
1. Waldemar Celes. Renato Cerqueira. José Lucas Rangel. Introdução a Estrutura de Dados: Com Técnicas de Programação em C.
2. António Manuel Adrego da Rocha. António Rui Oliveira e Silva Borges. Estruturas de Dados e Algoritmos em C. 
=======
# Parte I: Estruturas Estáticas


## Vetores e Alocação Dinâmica
  - **Vetores:**
    - Também conhecidos como arrays, vetores são estruturas de dados que permitem armazenar um conjunto de valores do mesmo tipo em uma única variável.
    - Vetores reservam espaços adjacentes na memória para armazenar seus dados.
    - São acessados por meio de índice. O primeiro elemento tem o índice 0, o segundo o índice 1 e assim por diante.
    - Possuem um tamanho fixo, ou seja, seu tamanho é definido na hora em que o vetor é criado.
    - Passar um vetor como argumento para uma função em C, na verdade, você está passando um ponteiro que aponta para o endereço de memória da primeira posição do vetor.
    - Para passar um valor do vetor para uma função, a mesma deve possuir um ponteiro capaz de armazenar o endereço de memória do valor fornecido.

    - Representação de vetor:
      
      ![Representação de vetor](https://embarcados.com.br/wp-content/uploads/2015/12/Mem%C3%B3ria13.png)

    - Na imagem, vemos um vetor alocado na memória do computador, ocupando os espaços de memória endereçados entre 108 e 144. Bem como um ponteiro alocado no endereço 100 da memória, que armazena o endereço do primeiro índice do vetor.

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
     - Nesse exemplo o código solicita ao usuário um valor para o vetor e aloca dinâmicamente os espaços de memória.
```c
#include <stdio.h>
#include <stdlib.h>
#include <Windows.h>

int main() {
    int *vetor = NULL;
    int tamanho = 0;

    printf("Digite numeros inteiros (digite 0 para sair):\n");

    int numero;
    do {
        printf("Digite um numero: ");
        scanf("%d", &numero);

        if (numero != 0) {
            // Aloca memória dinamicamente para um novo elemento
            int *novoVetor = (int *)realloc(vetor, (tamanho + 1) * sizeof(int));

            if (novoVetor == NULL) {
                printf("Erro na alocacao de memoria.\n");
                free(vetor);
                return 1;
            }

            vetor = novoVetor;
            vetor[tamanho] = numero;
            tamanho++;
        }
    } while (numero != 0);

    printf("Valores digitados:\n");
    for (int i = 0; i < tamanho; i++) {
        printf("%d ", vetor[i]);
    }
    printf("\n");

    Sleep(5000);
    free(vetor);

    return 0;
}
```
## Matrizes
- **Matriz:**
  - Também conhecidas como vetores bidimensionais, as matrizes são estruturas de dados que permitem armazenar um conjunto de valores do mesmo tipo em múltiplas dimensões.
  - As matrizes reservam espaços adjacentes na memória para armazenar seus dados, organizados em linhas e colunas.
  - São acessadas por meio de índices que especificam a posição de um elemento na matriz. As linhas e colunas também são indexadas a partir de 0.
  - Possuem um tamanho fixo em todas as dimensões, ou seja, suas dimensões (número de linhas e colunas) são definidas na hora em que a matriz é criada.
  - Matrizes podem ter mais de duas dimensões, tornando-as matrizes multidimensionais. A notação para acessar elementos em matrizes bidimensionais é mat[i][j], onde "i" é o índice da linha e "j" é o índice da coluna. Para matrizes tridimensionais, a notação seria mat[i][j][k], e assim por diante, dependendo do número de dimensões.


- **Exemplo de Matriz em linguagem C:**
  - Exemplo simples de declaração matriz com dimensões 3x3, para armazenar números inteiros.
```c
#include <stdio.h>

int main() {
    int matriz[3][3];

    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            matriz[i][j] = i * 4 + j + 1;
        }
    }

    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            printf("%d\t", matriz[i][j]);
        }
        printf("\n");
    }

    return 0;
}
```

## Cadeias de Caracteres (Strings)
- **Strings:**
  - Em C, as cadeias de caracteres são representadas como arrays de caracteres terminados por um caractere nulo ('\0').
  - São utilizadas para armazenar sequências de caracteres, como palavras, frases ou textos.
  - Para declarar e inicializar uma string, você pode usar a notação de vetor de caracteres, por exemplo: "char minhaString[]".
  - Também é possível declarar uma string sem especificar o tamanho e o compilador determinará o tamanho com base na string de inicialização: char outraString[] = "HelloWorld".
  - Para manipular strings, a linguagem C fornece uma biblioteca padrão chamada <string.h>, que contém funções para copiar, concatenar, comparar e muitas outras operações com strings.
  - Strings em C são arrays de caracteres, e você pode acessar caracteres individuais usando índices, por exemplo: "char primeiroChar = minhaString[0]".
  - Para comparar duas strings em C, você pode usar a função strcmp da biblioteca <string.h>, que retorna um valor inteiro indicando a igualdade ou a ordem lexicográfica das strings.
  -  É importante garantir que uma string tenha espaço suficiente para acomodar todos os caracteres, incluindo o caractere nulo, para evitar problemas de estouro de buffer.


- **Exemplo de String em linguagem C:**
  - Nesse exemplo declaramos um vetor de caracteres simples, com espaço para até 25 caracteres e o caracter nulo "\0", essa string armazena uma entrada do usuário e a imprime na tela.\
  
```c
#include <stdio.h>

int main() {
    char minhaString[25];

    printf("Digite uma frase: ");
    scanf("%25[^\n]", minhaString);

    printf("Você digitou: %s\n", minhaString);

    return 0;
}
```
## Tipos Estruturados

Tipos estruturados são usados para organizar dados complexos em programas C, permitindo que você crie representações personalizadas de objetos e suas propriedades. Eles são amplamente utilizados em programação para modelar entidades do mundo real, como pessoas, veículos, produtos, etc.

- **Estruturas (structs):**
  - Uma estrutura é uma coleção de variáveis de tipos diferentes, agrupadas sob um único nome.
  - Cada variável dentro de uma estrutura é chamada de membro ou campo.
  - Para definir uma estrutura, você usa a palavra-chave struct, seguida do nome da estrutura e a lista de membros entre chaves.
  
- **Exemplo de declaração de Struct:**
  ```c
  struct Pessoa {
        char nome[50];
        int idade;
        float altura;
    };
  ```

  - Para acessar os membros de uma estrutura, você utiliza o operador ponto (.).
- 
    ```c
    struct Pessoa pessoa1;
    pessoa1.idade = 30;
    ```

- **Unions (union):**
  - Uma union é semelhante a uma estrutura, mas todos os membros compartilham o mesmo espaço de memória.
  - Todos os membros compartilham o mesmo espaço de memória.
  - Unions são úteis quando você precisa armazenar diferentes tipos de dados em um espaço de memória compartilhado.

- **Exemplo de declaração de Union:**
  ```c
    union Dado {
        int inteiro;
        float flutuante;
        char caractere;
    };
  ```
    - Acessar membros de uma union é semelhante à estrutura, usando o operador ponto (`.``). Apenas um membro da union deve ser acessado de cada vez.
  
#### Referências Bibliográficas
1. Waldemar Celes. Renato Cerqueira. José Lucas Rangel. Introdução a Estrutura de Dados: Com Técnicas de Programação em C.
2. António Manuel Adrego da Rocha. António Rui Oliveira e Silva Borges. Estruturas de Dados e Algoritmos em C. 
