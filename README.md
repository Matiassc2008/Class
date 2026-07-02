#include <stdio.h>

/* =========================================================================
   NOME: [O seu nome aqui]
   NÚMERO: [O seu número de aluno aqui]
   ========================================================================= */

// Função para validar a quantidade total de monstros (M) entre 1 e 54 inclusivo.
// Retorna 1 se for válido, 0 caso contrário.
int validarQuantidade(int m) {
    if (m >= 1 && m <= 54) {
        return 1;
    }
    return 0;
}

// Função para validar o peso de cada monstro entre 3 e 10000 inclusivo.
// Retorna 1 se for válido, 0 caso contrário.
int validarPeso(int peso) {
    if (peso >= 3 && peso <= 10000) {
        return 1;
    }
    return 0;
}

// Função para contar quantos monstros são da categoria "Fofinho" (peso <= 6)
int contarFofinhos(int pesos[], int m) {
    int contagem = 0;
    for (int i = 0; i < m; i++) {
        if (pesos[i] <= 6) {
            contagem++;
        }
    }
    return contagem;
}

// Função para determinar o menor peso entre os monstros, EXCLUINDO os "Fofinhos"
// Retorna o menor peso encontrado, ou -1 se não houver monstros válidos para esta contagem.
int determinarMenorPeso(int pesos[], int m) {
    int menor = -1;
    
    for (int i = 0; i < m; i++) {
        // Ignora monstros fofinhos (peso menor ou igual a 6)
        if (pesos[i] > 6) {
            // Se for o primeiro peso válido encontrado ou se for menor que o anterior armazenado
            if (menor == -1 || pesos[i] < menor) {
                menor = pesos[i];
            }
        }
    }
    return menor;
}

int main() {
    // Declaração de variáveis locais exigidas
    int m = 0;
    int pesos[54]; // Array para guardar os pesos (capacidade máxima de 54 conforme enunciado)
    int fofinhosContagem = 0;
    int menorPesoNaoFofinho = 0;

    // Leitura da quantidade de monstros com validação
    do {
        printf("Quantidade de monstros avistados: ");
        scanf("%d", &m);
        if (!validarQuantidade(m)) {
            printf("Valor invalido!\n");
        }
    } while (!validarQuantidade(m));

    printf("Pesos dos monstros:\n");
    // Leitura dos pesos dos M monstros
    for (int i = 0; i < m; i++) {
        int pesoTemp;
        do {
            scanf("%d", &pesoTemp);
            if (!validarPeso(pesoTemp)) {
                printf("Valor invalido!\n");
            }
        } while (!validarPeso(pesoTemp));
        
        // Guarda o peso validado no array
        pesos[i] = pesoTemp;
    }

    printf("\n");

    // Processamento e escrita das categorias de cada monstro
    for (int i = 0; i < m; i++) {
        int p = pesos[i];
        
        // Verifica as categorias conforme a tabela (ignorando os fofinhos no output)
        if (p <= 6) {
            // "excepto para os monstros 'fofinhos'... porque são 'fofinhos'" -> Não imprime nada
            continue;
        } else if (p > 6 && p < 60) {
            printf("Kaiju %d: Categoria A\n", i + 1);
        } else if (p >= 60 && p < 160) {
            printf("Kaiju %d: Categoria B\n", i + 1);
        } else if (p >= 160) {
            printf("Kaiju %d: Categoria C\n", i + 1);
        }
    }

    printf("\n");

    // Chamada das funções de processamento de dados do array
    fofinhosContagem = contarFofinhos(pesos, m);
    menorPesoNaoFofinho = determinarMenorPeso(pesos, m);

    // Outputs finais requeridos
    printf("Monstros fofinhos: %d.\n", fofinhosContagem);
    
    if (menorPesoNaoFofinho != -1) {
        printf("Monstro com menor peso: %d toneladas.\n", menorPesoNaoFofinho);
    } else {
        printf("Monstro com menor peso: Nao existem monstros na categoria (excluindo fofinhos).\n");
    }

    return 0;
}
