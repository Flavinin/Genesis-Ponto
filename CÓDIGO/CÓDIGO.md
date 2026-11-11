
#include <stdio.h>
#include <string.h>
#include <time.h>

#define MAX 1000

typedef struct {
    int matricula;
    char nome[50];
} Funcionario;

typedef struct {
    int matricula, tipo;
    time_t horario;
} Registro;

Funcionario funcionarios[MAX];
Registro registros[MAX];
int nf = 0, nr = 0;

char *tipos[] = {
    "Entrada", "Saida intervalo",
    "Retorno intervalo", "Saida final"
};

// Busca funcionario pela matricula
int buscar(int mat) {
    for (int i = 0; i < nf; i++)
        if (funcionarios[i].matricula == mat)
            return i;
    return -1;
}

// Salva os dados em arquivos
void salvar() {
    FILE *f = fopen("funcionarios.txt", "w");
    if (f) {
        for (int i = 0; i < nf; i++)
            fprintf(f, "%d;%s\n",
                    funcionarios[i].matricula,
                    funcionarios[i].nome);
        fclose(f);
    }

    f = fopen("registros.txt", "w");
    if (f) {
        for (int i = 0; i < nr; i++)
            fprintf(f, "%d;%d;%lld\n",
                    registros[i].matricula,
                    registros[i].tipo,
                    (long long)registros[i].horario);
        fclose(f);
    }
}

// Carrega os dados salvos
void carregar() {
    FILE *f = fopen("funcionarios.txt", "r");
    if (f) {
        while (nf < MAX &&
               fscanf(f, "%d;%49[^\n]\n",
                      &funcionarios[nf].matricula,
                      funcionarios[nf].nome) == 2)
            nf++;
        fclose(f);
    }

    f = fopen("registros.txt", "r");
    if (f) {
        long long t;
        int mat, tipo;
        while (nr < MAX &&
               fscanf(f, "%d;%d;%lld\n",
                      &mat, &tipo, &t) == 3) {
            if (tipo < 1 || tipo > 4) continue;
            registros[nr++] = (Registro){mat, tipo, (time_t)t};
        }
        fclose(f);
    }
}

// RF01 - Cadastrar funcionario
void cadastrar() {
    if (nf >= MAX) return;

    Funcionario f;
    printf("Matricula: ");
    if (scanf("%d", &f.matricula) != 1) return;

    if (f.matricula <= 0 || buscar(f.matricula) != -1) {
        printf("Matricula invalida ou existente!\n");
        return;
    }

    printf("Nome: ");
    if (scanf(" %49[^\n]", f.nome) != 1) return;

    funcionarios[nf++] = f;
    salvar();
    printf("Funcionario cadastrado!\n");
}

// RF02 - Listar funcionarios
void listar() {
    for (int i = 0; i < nf; i++)
        printf("%d - %s\n",
               funcionarios[i].matricula,
               funcionarios[i].nome);

    if (!nf) printf("Nenhum funcionario cadastrado.\n");
}

// RF03, RF04 e RF05 - Registrar ponto
void registrar() {
    int mat, tipo;
    time_t agora = time(NULL);

    if (nr >= MAX) {
        printf("Limite de registros atingido!\n");
        return;
    }

    printf("Matricula: ");
    if (scanf("%d", &mat) != 1) return;

    if (buscar(mat) == -1) {
        printf("Funcionario nao encontrado!\n");
        return;
    }

    printf("1-Entrada  2-Saida intervalo\n");
    printf("3-Retorno intervalo  4-Saida final\n");
    printf("Opcao: ");
    if (scanf("%d", &tipo) != 1) return;

    if (tipo < 1 || tipo > 4) {
        printf("Opcao invalida!\n");
        return;
    }

    // Verifica a sequencia no dia atual
    int ultimo = 0;
    struct tm hoje = *localtime(&agora);

    for (int i = 0; i < nr; i++) {
        struct tm d = *localtime(&registros[i].horario);

        if (registros[i].matricula == mat &&
            d.tm_year == hoje.tm_year &&
            d.tm_yday == hoje.tm_yday) {
            if (registros[i].tipo > ultimo)
                ultimo = registros[i].tipo;
        }
    }

    if (tipo != ultimo + 1) {
        printf("Registro fora de sequencia!\n");
        return;
    }

    registros[nr++] = (Registro){mat, tipo, agora};
    salvar();
    printf("Ponto registrado: %s\n", tipos[tipo - 1]);
}

// RF06 e RF07 - Historico, horas e frequencia
void consultar(int opcao) {
    int mat;
    printf("Matricula: ");
    if (scanf("%d", &mat) != 1) return;

    if (buscar(mat) == -1) {
        printf("Funcionario nao encontrado!\n");
        return;
    }

    int dias = 0, atrasos = 0;
    double horas = 0, extras = 0;

    for (int i = 0; i < nr; i++) {
        if (registros[i].matricula != mat) continue;

        struct tm d = *localtime(&registros[i].horario);

        if (opcao == 4)
            printf("%s - %02d/%02d/%04d %02d:%02d\n",
                   tipos[registros[i].tipo - 1],
                   d.tm_mday, d.tm_mon + 1,
                   d.tm_year + 1900,
                   d.tm_hour, d.tm_min);

        // Calcula apenas dias com os quatro pontos
        if (registros[i].tipo != 1) continue;

        time_t t[4] = {registros[i].horario, 0, 0, 0};
        int cont[4] = {1, 0, 0, 0};

        for (int j = 0; j < nr; j++) {
            if (i == j || registros[j].matricula != mat)
                continue;

            struct tm x = *localtime(&registros[j].horario);

            if (x.tm_year == d.tm_year &&
                x.tm_yday == d.tm_yday) {
                int k = registros[j].tipo - 1;
                cont[k]++;
                t[k] = registros[j].horario;
            }
        }

        if (cont[0] != 1 || cont[1] != 1 ||
            cont[2] != 1 || cont[3] != 1 ||
            t[0] >= t[1] || t[1] >= t[2] ||
            t[2] >= t[3]) continue;

        double h = (difftime(t[1], t[0]) +
                    difftime(t[3], t[2])) / 3600.0;

        horas += h;
        dias++;

        if (h > 8) extras += h - 8;

        int entrada = d.tm_hour * 60 + d.tm_min;
        if (entrada > 540) atrasos++;
    }

    if (opcao == 5 || opcao == 6) {
        printf("\nDias trabalhados: %d\n", dias);
        printf("Horas trabalhadas: %.2f h\n", horas);
    }

    if (opcao == 6) {
        printf("Dias com atraso: %d\n", atrasos);
        printf("Horas extras: %.2f h\n", extras);
    }
}

// MENU PRINCIPAL
int main() {
    int op = -1;
    carregar();

    do {
        printf("\n===== GENESIS PONTO =====\n");
        printf("1 - Cadastrar funcionario\n");
        printf("2 - Listar funcionarios\n");
        printf("3 - Registrar ponto\n");
        printf("4 - Consultar historico\n");
        printf("5 - Calcular horas trabalhadas\n");
        printf("6 - Resumo de frequencia\n");
        printf("0 - Sair\n");
        printf("Opcao: ");

        if (scanf("%d", &op) != 1) {
            while (getchar() != '\n');
            op = -1;
            continue;
        }

        switch (op) {
            case 1: cadastrar(); break;
            case 2: listar(); break;
            case 3: registrar(); break;
            case 4: consultar(4); break;
            case 5: consultar(5); break;
            case 6: consultar(6); break;
            case 0: printf("Encerrando...\n"); break;
            default: printf("Opcao invalida!\n");
        }
    } while (op != 0);

    return 0;
}
