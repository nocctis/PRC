#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct {
    char nome [50], professor [50];
    int creditos, semestre, ano;
    double n1, n2, media;
} TDisciplina;

typedef struct {
    TDisciplina v[100];
    int qtd;
} THistorico;

void limpartela()
{
#ifdef _WIN32
   system("cls");
#else
   system("clear");
#endif
}

void LerDisciplina (TDisciplina d[]){
    printf("Digite o nome da disciplina: ");
    scanf(" %s", (*d).nome);
    printf("Digite o ano: ");
    scanf("%d", &(*d).ano);
    printf("Digite o semestre: ");
    scanf("%d", &(*d).semestre);
    printf("Digite o nome do professor: ");
    scanf("%s", (*d).professor);
    printf("Digite os creditos: ");
    scanf("%d", &(*d).creditos);
    printf("Digite a primeira nota: ");
    scanf("%lf", &(*d).n1);
    printf("Digite a segunda nota: ");
    scanf("%lf", &(*d).n2);
}

int obterindice(THistorico h, char inf[]){
    int v, i;
    v = 0;
    i = 0;
    while(!v && i < h.qtd)
        if (strcmp(h.v[i].nome, inf) == 0)
            v = 1;
        else
            i++;
    return v ? i : -1;
        
}

void MediaDisciplina (TDisciplina d[]){
    (*d).media = ((*d).n1+(*d).n2)/2;
}

void MostrarDisciplina (THistorico h, char inf[]){
    int p = obterindice(h, inf);
    printf("\nDisciplina: %s\n", h.v[p].nome);
    printf("Professor: %s\n", h.v[p].professor);
    printf("Media: %.2lf\n", h.v[p].media);
    printf("Creditos: %d\n", h.v[p].creditos);
    printf("\n");

}

void inicializar (THistorico *h){
    (*h).qtd=0;
}

void inserir(THistorico *h, TDisciplina d){
    (*h).v[(*h).qtd] = d;
    (*h).qtd++;
}


int remover(THistorico *h, char inf[]){
    int p = obterindice(*h, inf);
    if (p > -1){
        (*h).v[p] = (*h).v[(*h).qtd-1];
        (*h).qtd--;
        return 1;
    }else{
        return 0; 
    }
}

int alterar(THistorico *h, char inf[], TDisciplina d){
    int p = obterindice(*h, inf);
    if (p > -1){
        (*h).v[p] = d;
        return 1;
    }else{
        return 0;
    }
}

void listar(THistorico h){
    int i;
    printf("---------------------------\n");
    for(i=0; i<h.qtd; i++){
         printf("Semestre: %d -- Ano: %d\n", h.v[i].semestre, h.v[i].ano);
         printf("Disciplina: %s\n", h.v[i].nome);
         printf("Professor: %s\n", h.v[i].professor);
         printf("Media: %.2lf\n", h.v[i].media);
         printf("Creditos: %d\n", h.v[i].creditos);
         printf("\n");
    }
    printf("---------------------------\n");
}

int cr(THistorico *h){
    int i;
    double cr, soma, somacreditos;
    for(i=0; i<(*h).qtd; i++){
        soma = soma + (*h).v[i].media;
        somacreditos = somacreditos + (*h).v[i].creditos;
    }
    cr = soma/somacreditos;
    return cr;
}

int menu(){
    int x;
    do{
        printf("\n1 - Inserir disciplina\n");
        printf("2 - Remover disciplina\n");
        printf("3 - Alterar disciplina\n");
        printf("4 - Mostrar os dados de uma disciplina\n");
        printf("5 - Listar disciplinas\n");
        printf("6 - Mostrar historico\n");
        printf("7 - Sair\n");
        printf("\nDigite uma opcao: ");
        scanf("%d", &x);
    } while (x < 1 || x > 7);
    limpartela();
    return x;
}

int main(){
    TDisciplina disciplina;
    THistorico historico;
    int a, fim = 0;
    char aux [10];
    inicializar(&historico);
    while(!fim){
        switch(menu()){
            case 1:
              LerDisciplina(&disciplina);
              MediaDisciplina(&disciplina);
              inserir(&historico, disciplina);
              printf("\nDisciplina inserida!\n");
              system("pause");
              break;
            case 2:
              printf("Informe a disciplina a ser removida: ");
              scanf("%s", aux);
              if(remover(&historico, aux))
                printf("\nDisciplina removida!\n");
              else
                printf("\nDisciplina nao encontrada!\n");
              system("pause");
              break;
            case 3:
              printf("Informe a disciplina a ser alterada: ");
              scanf("%s", aux);
              LerDisciplina(&disciplina);
              if(alterar(&historico, aux, disciplina))
                printf("\nDisciplina alterada!\n");
              else
                printf("\nDisciplina nao encontrada!\n");
              system("pause");
              break;
            case 4:
              printf("Informe a disciplina que deseja mostrar: ");
              scanf("%s", aux);
              MostrarDisciplina(historico, aux);
              system("pause");
              break;
            case 5:
              listar(historico);
              system("pause");
              break;
            case 6:
              printf("--- HISTORICO ESCOLAR ---\n");
              listar(historico);
              printf("Coeficiente de rendimento: ");
              a = cr(&historico);
              printf("%d\n\n", a);
              system("pause");
              break;
            case 7:
              fim = 1;
              break;
            default:
              printf("Alternativa nao encontrada!\n\n");
              system("pause");
              break;
        }
    }
    return 0;
}
