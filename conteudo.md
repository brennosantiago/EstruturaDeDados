# Resumo: Listas Dinâmicas em C

## 1️⃣ Introdução às Listas Dinâmicas

### 🔹 Definição
Uma **lista dinâmica** é uma estrutura de dados que permite armazenar elementos de forma encadeada na memória, onde cada elemento aponta para o próximo. Ela é chamada de "dinâmica" porque o tamanho da lista pode crescer ou diminuir durante a execução do programa, ao contrário das listas estáticas.

### 🔹 Listas Estáticas vs Dinâmicas

| Aspecto              | Lista Estática (Array)                   | Lista Dinâmica (Encadeada)             |
|----------------------|------------------------------------------|----------------------------------------|
| Tamanho              | Fixo, definido na compilação             | Variável, alocado em tempo de execução |
| Acesso aos elementos | Direto (índice)                          | Sequencial (percorre do início)        |
| Inserção/Remoção     | Mais custosa, exige realocação           | Mais eficiente, apenas ajusta ponteiros|
| Uso de memória       | Pode desperdiçar espaço                  | Usa somente o necessário               |

### 🔹 Vantagens das Listas Dinâmicas
- Flexibilidade de tamanho.
- Inserções e remoções eficientes.

### 🔹 Desvantagens
- Acesso sequencial (mais lento).
- Consumo de memória adicional por causa dos ponteiros.

---

## 2️⃣ Estrutura de uma Lista Dinâmica

Uma **lista encadeada simples** é composta por nós (ou *nodes*), onde cada nó contém:
- Um **dado** (ex: um `int`).
- Um **ponteiro** para o próximo nó da lista.

### Exemplo em C:

typedef struct No {
    int valor;
    struct No* proximo;
} No;

## 3️⃣ Operações Básicas

No* lista = NULL;

void inserir_inicio(No** lista, int valor) {
    No* novo = (No*) malloc(sizeof(No));
    novo->valor = valor;
    novo->proximo = *lista;
    *lista = novo;
}

void remover(No** lista, int valor) {
    No* atual = *lista;
    No* anterior = NULL;

    while (atual != NULL && atual->valor != valor) {
        anterior = atual;
        atual = atual->proximo;
    }

    if (atual == NULL) return; // Valor não encontrado

    if (anterior == NULL) {
        *lista = atual->proximo;
    } else {
        anterior->proximo = atual->proximo;
    }

    free(atual);
}

## 4️⃣ Implementação em C

#include <stdio.h>
#include <stdlib.h>

typedef struct No {
    int valor;
    struct No* proximo;
} No;

void inserir_inicio(No** lista, int valor) {
    No* novo = (No*) malloc(sizeof(No));
    novo->valor = valor;
    novo->proximo = *lista;
    *lista = novo;
}

void imprimir(No* lista) {
    while (lista != NULL) {
        printf("%d -> ", lista->valor);
        lista = lista->proximo;
    }
    printf("NULL\n");
}

int main() {
    No* lista = NULL;

    inserir_inicio(&lista, 30);
    inserir_inicio(&lista, 20);
    inserir_inicio(&lista, 10);

    imprimir(lista); // Saída: 10 -> 20 -> 30 -> NULL

    return 0;
}

## 5️⃣ Referências

FOROUZAN, Behrouz A.; GILBERG, Richard F. Estruturas de Dados em C. Cengage Learning.

CURY, Fábio. Algoritmos e Estruturas de Dados em C. Pearson.
