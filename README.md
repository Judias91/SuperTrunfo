# SuperTrunfo
desenvolver um programa em C que crie e gerencie dados das cartas para o jogo de Super Trunfo, com o propósito de aprimorar habilidades práticas na manipulação de variáveis, operadores e funções de entrada e saída.
#include <stdio.h>
#include <string.h>

#define MAX_CIDADES 100
#define TAM_NOME 50

typedef struct {
    int codigo;
    char nome[TAM_NOME];
    long populacao;
    float area;
    double pib;
    int pontos_turisticos;
    float densidade_populacional;
    double pib_per_capita;
} Cidade;

void cadastrarCidade(Cidade cidades[], int *numCidades) {
    if (*numCidades >= MAX_CIDADES) {
        printf("Limite de cidades atingido!\n");
        return;
    }

    Cidade novaCidade;

    printf("Codigo da cidade: ");
    scanf("%d", &novaCidade.codigo);

    printf("Nome da cidade: ");
    scanf(" %[^\n]", novaCidade.nome);

    printf("Populacao: ");
    scanf("%ld\n", &novaCidade.populacao);

    printf("Area (em km²): ");
    scanf("%f\n", &novaCidade.area);

    printf("PIB: ");
    scanf("%f\n", &novaCidade.pib);

    printf("Numero de pontos turisticos: ");
    scanf("%d\n", &novaCidade.pontos_turisticos);

    // Calcula densidade populacional e PIB per capita
    novaCidade.densidade_populacional = novaCidade.populacao / novaCidade.area;
    novaCidade.pib_per_capita = novaCidade.pib / novaCidade.populacao;

    cidades[*numCidades] = novaCidade;
    (*numCidades)++;

    printf("Cidade cadastrada com sucesso!\n");
}

void listarCidades(Cidade cidades[], int numCidades) {
    if (numCidades == 0) {
        printf("Nenhuma cidade cadastrada.\n");
        return;
    }

    printf("\nLista de Cidades Cadastradas:\n");
    for (int i = 0; i < numCidades; i++) {
        printf("\nCidade %d:\n", i + 1);
        printf("  Codigo: %d\n", cidades[i].codigo);
        printf("  Nome: %s\n", cidades[i].nome);
        printf("  Populacao: %ld\n", cidades[i].populacao);
        printf("  Area: %.2f km²\n", cidades[i].area);
        printf("  PIB: %.2lf\n", cidades[i].pib);
        printf("  Pontos Turisticos: %d\n", cidades[i].pontos_turisticos);
        printf("  Densidade Populacional: %.2f hab/km²\n", cidades[i].densidade_populacional);
        printf("  PIB per Capita: %.2lf\n", cidades[i].pib_per_capita);
    }
}

void compararCidades(Cidade cidades[], int numCidades) {
    if (numCidades < 2) {
        printf("É necessário cadastrar pelo menos duas cidades para comparar.\n");
        return;
    }

    int vencedor_densidade = 0;
    int vencedor_pib = 0;
    int vencedor_pontos_turisticos = 0;
    int vencedor_populacao = 0;
    int vencedor_area = 0;

    for (int i = 1; i < numCidades; i++) {
        // Compara densidade populacional (menor valor vence)
        if (cidades[i].densidade_populacional < cidades[vencedor_densidade].densidade_populacional) {
            vencedor_densidade = i;
        }

        // Compara PIB per capita (maior valor vence)
        if (cidades[i].pib_per_capita > cidades[vencedor_pib].pib_per_capita) {
            vencedor_pib = i;
        }

        // Compara pontos turísticos (maior valor vence)
        if (cidades[i].pontos_turisticos > cidades[vencedor_pontos_turisticos].pontos_turisticos) {
            vencedor_pontos_turisticos = i;
        }

        // Compara população (maior valor vence)
        if (cidades[i].populacao > cidades[vencedor_populacao].populacao) {
            vencedor_populacao = i;
        }

        // Compara área (maior valor vence)
        if (cidades[i].area > cidades[vencedor_area].area) {
            vencedor_area = i;
        }
    }

    printf("\nResultados da Comparacao:\n");
    printf("  - Vencedor em Densidade Populacional (menor valor): %s (%.2f hab/km²)\n",
           cidades[vencedor_densidade].nome, cidades[vencedor_densidade].densidade_populacional);
    printf("  - Vencedor em PIB per Capita (maior valor): %s (%.2lf)\n",
           cidades[vencedor_pib].nome, cidades[vencedor_pib].pib_per_capita);
    printf("  - Vencedor em Pontos Turisticos (maior valor): %s (%d)\n",
           cidades[vencedor_pontos_turisticos].nome, cidades[vencedor_pontos_turisticos].pontos_turisticos);
    printf("  - Vencedor em Populacao (maior valor): %s (%ld)\n",
           cidades[vencedor_populacao].nome, cidades[vencedor_populacao].populacao);
    printf("  - Vencedor em Area (maior valor): %s (%.2f km²)\n",
           cidades[vencedor_area].nome, cidades[vencedor_area].area);
}

int main() {
    Cidade cidades[MAX_CIDADES];
    int numCidades = 0;
    int opcao;

    do {
        printf("\nMenu:\n");
        printf("1. Cadastrar cidade\n");
        printf("2. Listar cidades\n");
        printf("3. Comparar cidades\n");
        printf("0. Sair\n");
        printf("Escolha uma opcao: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                cadastrarCidade(cidades, &numCidades);
                break;
            case 2:
                listarCidades(cidades, numCidades);
                break;
            case 3:
                compararCidades(cidades, numCidades);
                break;
            case 0:
                printf("Saindo...\n");
                break;
            default:
                printf("Opcao invalida! Tente novamente.\n");
        }
    } while (opcao != 0);

    return 0;
    }
