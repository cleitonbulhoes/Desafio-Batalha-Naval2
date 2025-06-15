#include <stdio.h>

#define TAM 10       // Tamanho do tabuleiro (10x10)
#define TAM_NAVIO 3  // Tamanho fixo dos navios

// Função para inicializar o tabuleiro com 0 (água)
void inicializaTabuleiro(int tab[TAM][TAM]) {
    for (int i = 0; i < TAM; i++) {
        for (int j = 0; j < TAM; j++) {
            tab[i][j] = 0;
        }
    }
}

// Função para verificar se o navio cabe no tabuleiro e não sobrepõe outros navios
// orientacao: 'H' para horizontal, 'V' para vertical
int validaPosicao(int tab[TAM][TAM], int linha, int coluna, char orientacao) {
    if (orientacao == 'H') {
        if (coluna + TAM_NAVIO > TAM) return 0; // ultrapassa borda direita
        for (int j = coluna; j < coluna + TAM_NAVIO; j++) {
            if (tab[linha][j] == 3) return 0; // já ocupado
        }
    } else if (orientacao == 'V') {
        if (linha + TAM_NAVIO > TAM) return 0; // ultrapassa borda inferior
        for (int i = linha; i < linha + TAM_NAVIO; i++) {
            if (tab[i][coluna] == 3) return 0; // já ocupado
        }
    } else {
        return 0; // orientação inválida
    }
    return 1; // posição válida
}

// Função para posicionar o navio no tabuleiro
void posicionaNavio(int tab[TAM][TAM], int linha, int coluna, char orientacao) {
    if (orientacao == 'H') {
        for (int j = coluna; j < coluna + TAM_NAVIO; j++) {
            tab[linha][j] = 3;
        }
    } else if (orientacao == 'V') {
        for (int i = linha; i < linha + TAM_NAVIO; i++) {
            tab[i][coluna] = 3;
        }
    }
}

// Função para imprimir o tabuleiro
void imprimeTabuleiro(int tab[TAM][TAM]) {
    printf("Tabuleiro (0=água, 3=navio):\n\n");
    for (int i = 0; i < TAM; i++) {
        for (int j = 0; j < TAM; j++) {
            printf("%d ", tab[i][j]);
        }
        printf("\n");
    }
}

int main() {
    int tabuleiro[TAM][TAM];

    // Inicializa o tabuleiro com água
    inicializaTabuleiro(tabuleiro);

    // Define coordenadas iniciais dos navios (fixas, no código)
    int linhaNavio1 = 1, colunaNavio1 = 2; // navio horizontal
    int linhaNavio2 = 4, colunaNavio2 = 5; // navio vertical

    // Valida e posiciona navio horizontal
    if (validaPosicao(tabuleiro, linhaNavio1, colunaNavio1, 'H')) {
        posicionaNavio(tabuleiro, linhaNavio1, colunaNavio1, 'H');
    } else {
        printf("Erro: Não foi possível posicionar o navio horizontal nas coordenadas (%d,%d)\n", linhaNavio1, colunaNavio1);
        return 1; // encerra programa com erro
    }

    // Valida e posiciona navio vertical
    if (validaPosicao(tabuleiro, linhaNavio2, colunaNavio2, 'V')) {
        posicionaNavio(tabuleiro, linhaNavio2, colunaNavio2, 'V');
    } else {
        printf("Erro: Não foi possível posicionar o navio vertical nas coordenadas (%d,%d)\n", linhaNavio2, colunaNavio2);
        return 1; // encerra programa com erro
    }

    // Imprime o tabuleiro com os navios posicionados
    imprimeTabuleiro(tabuleiro);

    return 0;
}
