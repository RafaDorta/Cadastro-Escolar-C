# Cadastro-Escolar-C

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>
#include <windows.h>

///Struct dos alunos==========================================================================
typedef struct
{

    int ra;
    char nome[20] ;
    int nmrmateria[20];
    int nmraulas;
} als;

///Struct dos professores==========================================================================
typedef struct
{

    int ra;
    char nome[20];
    int nmrmateria[20];
    int mtr_reg;
} pfs;

///Struct dos cursos==========================================================================
typedef struct
{


       int cod;
        char nome_curs[30];
    
} curs;

///VOID DOS ALUNOS==========================================================================
void alunos(als es[],int *i,curs mat[],int nmr_c)
{

    int opc;
    int ra_aluno;
    int h=0;
    int cd_ver;
    int rep_v;
    int alun_n;
    int saida=0;
    int saida2 =0;
    int saida3 =1000;
    int cd_ver2;
    int verifica1;
    int repeteco=1;
    int saida4=0;
    do
    {
        system("cls");
        printf("Digite: \n1- Para registra novo aluno/a;\n2- Para adicionar um curso para um aluno/a;\n3- Para remover um curso de um aluno/a;\nR:");
        
       scanf("%d", &opc);
///REGISTRA UM NOVO ALUNO==========================================================================
       
       if(opc==1)
        {

            int a;
            a = *i;
            fflush(stdin);
            printf("\nNome:");
            gets(es[a].nome);
            do
            {
                printf("\nRA:");
                scanf("%d",&es[a].ra);
                saida4=0;

                for(int d=0; d<a; d++)
                {
                    if(es[a].ra==es[d].ra )
                    {
                        printf("Esse RA j\240 em uso,digite outro RA\n");
                        saida4=400;
                    }
                }
            }
            while(saida4==400);
            a++;
            *i=a;
            do
            {

                printf("\n\nVoc\210 deseja Cadastrar mais algum aluno/a? Sim <1>, N\306o <0>\nR:");
                scanf("%d", &verifica1);
                fflush(stdin);
                if(verifica1 == 1)
                {
                    a = *i;
                    fflush(stdin);
                    printf("\n\nNome:");
                    gets(es[a].nome);
                    do
                    {
                        printf("\nRA:");
                        scanf("%d",&es[a].ra);
                        saida4=0;
                        for(int d=0; d<a; d++)
                        {
                            if(es[a].ra==es[d].ra )
                            {
                                printf("Esse RA j\240 est\240 em uso,digite outro RA\n");
                                saida4=400;
                            }
                        }
                    }
                    while(saida4==400);
                    a++;
                    *i=a;

                }
            }
            while(verifica1 != 0);
        }
        else
        {
///ADICIONA UMA MATÉRIA PRO ALUNO===================================================
            
            if(opc==2)
            {
                int V[20];
                int b2=0;
                int ctd=0;
                int M[20];
                int k2= 0;

                printf("Cursos registrados no sistema: %d\n",nmr_c);
                printf("\n\nLista de alunos:\n");
                for(int x1=0; x1<*i; x1++)
                {
                    printf("- Nome: %10s   RA: %4.4d\n",es[x1].nome,es[x1].ra);
                }

                printf("RA do/s aluno/os (Apos adicionar todos os RAs digite 0): ");

                for(int b =0; b<*i+1; b++)
                {
                    scanf("%d,",&V[b]);
                    if(V[b]== 0000)break;
                }





                for(b2=0; b2<*i+1; b2++)
                {
                    h=0;
                    if(V[b2]== 0000) break;
                    for(int z=0; z<20; z++)
                    {
                        saida=0;
                        h++;
                        if(V[b2]==es[z].ra)
                        {
                            if(ctd == 0)
                            {
                                printf("Escolha o curso:");
                                printf("\n\n                NOME    C\340DIGO\n\n");
                                for(int l=0; l< nmr_c; l++)
                                {
                                    printf("%20s     %4.4d\n",mat[l].nome_curs,mat[l].cod);

                                }
                                printf("Digite o C\242digo do Mat\202ria/as (Apos adicionar todos os RAs digite 0): ");
                                for(int k =0; k<nmr_c+1; k++)
                                {
                                    scanf("%d,",&M[k]);

                                    if(M[k]== 0000) break;
                                }
                                ctd = 1;
                            }

                            for( int g=0 ; g<nmr_c+1 ; g++)
                            {
                                if(M[g]== 0000) break;

                                for(int l5=0; l5<nmr_c; l5++)
                                {


                                    if(M[g] == mat[l5].cod)
                                    {

                                        for(int l4=0; l4<es[z].nmraulas; l4++)
                                        {
                                            if(M[g] ==  es[z].nmrmateria[l4])
                                            {

                                                printf("\n\nAluno/a %s j\240 cadastrado/a para essa disciplina!!",es[z].nome);
                                                saida =1000;

                                            }
                                        }

                                        if(saida != 1000)
                                        {
                                            es[z].nmrmateria[es[z].nmraulas]= mat[l5].cod;
                                            printf("\n\nAluno/a %s registrado/a na Mat\202ria %s!",es[z].nome,mat[l5].nome_curs);
                                            es[z].nmraulas++;
                                        }



                                    }
                                }

                            }
                            break;
                        }
                        else
                        {
                            if(h==20)
                                printf("\nOp\207\306o n\306o encontrada...");

                        }
                    }
                }
            }
            else
            {
///RETIRA UMA MATÉRIA PRO ALUNO===================================================
                
                if(opc==3)
                {
                    int V2[20];
                    int M[20];
                    int verifica2;
                    int rmv;
                    int ctd =0;
                    printf("\n\nLista de alunos:\n");
                    for(int x1=0; x1<*i; x1++)
                    {
                        printf("- Nome: %10s   RA: %4.4d\n",es[x1].nome,es[x1].ra);
                    }


                    printf("RA do/s aluno/os (Apos adicionar todos os RAs digite 0): ");

                    for(int b =0; b<*i+1; b++)
                    {
                        scanf("%d,",&V2[b]);
                        if(V2[b]== 0000)break;
                    }
                    for(int b2=0; b2<*i+1; b2++)
                    {
                        if(V2[b2]== 0000) {saida3 = 100; break;}
                        for(int z=0; z<20; z++)
                        {
                            saida3 == 1000;
                            if(V2[b2]==es[z].ra)
                            {
                                if(ctd == 0)
                                {
                                    printf("Escolha o curso que deseja remover:");
                                    printf("\n\n                NOME    C\340DIGO\n\n");
                                    for(int l=0; l< nmr_c; l++)
                                    {
                                        printf("%20s     %4.4d\n",mat[l].nome_curs,mat[l].cod);

                                    }

                                    printf("Digite o C\242digo do Mat\202ria/as(Apos adicionar todos os RAs digite 0): ");
                                    for(int k =0; k<nmr_c+1; k++)
                                    {
                                        scanf("%d,",&M[k]);

                                        if(M[k]== 0000) break;
                                    }


                                    ctd = 1;
                                }


                                for( int g=0 ; g<nmr_c+1 ; g++)
                                {
                                    if(M[g]== 0000){ break;
                                    saida3 = 100;

                                    }



                                    if(es[z].nmraulas == 0)
                                    {
                                        printf("\nEsse RA %4.4d nao tem Materias",V2[b2]);
                                        saida3 = 100;
                                    }

                                    for(int i2=0; i2<es[z].nmraulas; i2++)
                                    {
                                        if(M[g] == es[z].nmrmateria[i2])
                                        {
                                            for(int p = 0; p< es[z].nmraulas - i2; p++)
                                            {

                                                es[z].nmrmateria[i2 + p] = es[z].nmrmateria[i2 + 1 + p];
                                            }
                                            es[z].nmraulas--;
                                            printf("\n\nMat\202ria retirada da grade de %s!!!\n",es[z].nome );
                                            saida3 == 100;

                                        }

                                    }
                                }
                            }
                        }
                    }


                    if(saida3 == 1000)
                        printf("\nOp\207\306o n\306o encontrada...");

                }
            }
        }
        fflush(stdin);
        printf("\n\nDeseja realizar mais alguma a\207\306o em alunos? Sim <1>, N\306o <0>\nR:");
        scanf("%d",&repeteco);


    }
    while(repeteco==1);
};


///VOID QUE CUIDA DO REGISTRO DOS CURSOS========================================================================================================================================================================

void curso(curs mat[],pfs prof[],int *nmr_c)
{

    int sim;
    int saida=0;
    int saida4=0;

    printf("Cursos registrados no sistema: %d\n",*nmr_c);
    printf("Para registrar um curso, digite <1> para sair digite <0>\nR: ");
    scanf("%d",&sim);
    fflush(stdin);
    int j=*nmr_c;

    if(sim==1)
    {
        do
        {
            printf("\nDigite os dados do curso: \n");
            printf("\nNome:");
            gets(mat[j].nome_curs);
            do
            {
                printf("\nC\242digo:");
                scanf("%d",&mat[j].cod);
                saida4=0;

                for(int d=0; d<j; d++)
                {
                    if(mat[j].cod==mat[d].cod )
                    {
                        printf("Esse CODIGO j\240 em uso,digite outro CODIGO\n");
                        saida4=400;
                    }
                }
            }
            while(saida4==400);
            j++;
            *nmr_c = j;
            printf("Deseja Registrar mais algum curso? Sim <1>, N\306o <0>\nR:");
            scanf("%d",&saida);
            fflush(stdin);
        }
        while(saida == 1);
    }
    else
    {

    }
};

///VOID QUE CUIDA DOS PROFESSORES ========================================================================================================================================================================

void professores(pfs prof[],curs mat[],int *nmr_c, int *nmr_p)
{
    
    int ra_prof;
    int saida=0;
    int i = *nmr_p;
    int h=0;
    int again=1;
    int opc_prof;
    int cd_ver;
    int repeteco2=1;
    int saida4=0;
    do
    {
        system("cls");
        printf("Digite:\n1- Deseja registrar um novo professor/a;\n2- Deseja adicionar um professor/a a um curso;\n3- Deseja retirar um professor/a de um curso;\nR:");
        scanf("%d",&opc_prof);
        fflush(stdin);
///REGISTRA UM PROFESSOR=============================================================
        
        if(opc_prof==1)
        {
            printf("\nNome:");
            gets(prof[i].nome);

            do
            {
                printf("\nRA:");
                scanf("%d",&prof[i].ra);
                saida4=0;

                for(int d=0; d<i; d++)
                {
                    if(prof[i].ra==prof[d].ra )
                    {
                        printf("Esse RA j\240 em uso,digite outro RA\n");
                        saida4=400;
                    }
                }
            }
            while(saida4==400);



            i++;
            *nmr_p =i;
            printf("\nDeseja registrar outro professor/a? Sim <1>, N\306o <0>\nR: ");
            scanf("%d",&again);

            while(again==1)
            {

                fflush(stdin);


                printf("\nNome:");
                gets(prof[i].nome);

                do
                {
                    printf("\nRA:");
                    scanf("%d",&prof[i].ra);
                    saida4=0;

                    for(int d=0; d<i; d++)
                    {
                        if(prof[i].ra==prof[d].ra )
                        {
                            printf("Esse RA j\240 em uso,digite outro RA\n");
                            saida4=400;
                        }
                    }
                }
                while(saida4==400);
                i++;
                *nmr_p =i;

                printf("\nDeseja registrar outro professor/a? Sim <1>, N\306o <0>\nR: ");
                scanf("%d",&again);
            }



        }
        else
        {
///ADICIONA UM PROFESSOR A UM CURSO=============================================================
           
           if(opc_prof==2)
            {
                int ctd =0;
                int V[20];
                int M[20];
                printf("Cursos registrados no sistema: %d \n",nmr_c);
                printf("\n\nLista de professores:\n");
                for(int x2=0; x2<*nmr_p; x2++)
                {
                    printf("- Nome: %10s   RA: %4.4d\n",prof[x2].nome,prof[x2].ra);
                }
                printf("RA do/s Professor/es (Apos adicionar todos os RAs digite 0): ");

                for(int b =0; b<i+1; b++)
                {
                    scanf("%d,",&V[b]);
                    if(V[b]== 0000)break;
                }





                for(int b2=0; b2<i+1; b2++)
                {
                    h=0;
                    if(V[b2]== 0000) break;
                    for(int z=0; z<20; z++)
                    {
                        saida = 0;
                        h++;
                        if(V[b2]==prof[z].ra)
                        {

                            if(ctd == 0)
                            {
                                printf("Escolha o curso:");
                                printf("\n\n                NOME    C\340DIGO\n\n");
                                for(int l=0; l< nmr_c; l++)
                                {
                                    printf("%20s     %4.4d\n",mat[l].nome_curs,mat[l].cod);

                                }
                                printf("Digite o C\242digo do Mat\202ria/as (Apos adicionar todos os RAs digite 0): ");
                                for(int k =0; k<nmr_c+1; k++)
                                {
                                    scanf("%d,",&M[k]);

                                    if(M[k]== 0000) break;
                                }
                                ctd = 1;
                            }

                            for( int g=0 ; g<nmr_c+1 ; g++)
                            {
                                if(M[g]== 0000) break;



                                for(int l2=0; l2< nmr_c; l2++)
                                {

                                    if(M[g] ==mat[l2].cod)
                                    {

                                        for(int l4=0; l4<prof[z].mtr_reg; l4++)
                                        {
                                            if(M[g] ==  prof[z].nmrmateria[l4])
                                            {
                                                printf("\n\nProfessor/a j\240 cadastrado/a para essa disciplina!!");
                                                saida =1000;

                                            }
                                        }

                                        if(saida!=1000)
                                        {
                                            prof[z].nmrmateria[ prof[z].mtr_reg] = M[g];
                                            printf("\n\n Professor/a %s registrado/a como professor/a de %s!\n",prof[z].nome,mat[l2].nome_curs);
                                            prof[z].mtr_reg++;
                                        }

                                    }

                                }


                            }
                            break;
                        }
                        else
                        {
                            if(h==20)
                                printf("\nOp\207\306o n\306o encontrada...");

                        }
                    }
                }


            }
            else
            {
///RETIRA UM PROFESSOR A UM CURSO=============================================================
                
                if(opc_prof==3)
                {
                    int ctd =0;
                    system("cls");
                    int retirar, rmv;
                    int V2[20];
                    int saida3 = 0;
                    int ver_prof;
                    int M[20];
                    printf("\n\nLista de professores:\n");
                    for(int x2=0; x2<*nmr_p; x2++)
                    {
                        printf("- Nome: %10s   RA: %4.4d\n",prof[x2].nome,prof[x2].ra);
                    }

                    printf("RA do/s aluno/os (Apos adicionar todos os RAs digite 0): ");

                    for(int b =0; b<i+1; b++)
                    {
                        scanf("%d,",&V2[b]);
                        if(V2[b]== 0000)break;
                    }

                    for(int b2=0; b2< i+1; b2++)
                    {
                        if(V2[b2]== 0000) break;
                        for(int t=0; t<20; t++)
                        {

                            saida3 == 0;
                            if(V2[b2]==prof[t].ra)
                            {

                                if(ctd == 0)
                                {
                                    printf("Escolha o curso que deseja remover:");
                                    printf("\n\n                NOME    C\340DIGO\n\n");
                                    for(int l=0; l< nmr_c; l++)
                                    {
                                        printf("%20s     %4.4d\n",mat[l].nome_curs,mat[l].cod);

                                    }
                                    printf("Digite o C\242digo do Mat\202ria/as(Apos adicionar todos os RAs digite 0): ");
                                    for(int k =0; k<nmr_c+1; k++)
                                    {
                                        scanf("%d,",&M[k]);

                                        if(M[k]== 0000) break;
                                    }
                                    ctd = 1;
                                }

                                for( int g=0 ; g<nmr_c+1 ; g++)
                                {
                                    if(M[g]== 0000) break;


                                    if(prof[t].mtr_reg == 0)
                                    {
                                        printf("\n\nEsse RA %4.4d nao esta cadastrado com professor da Materia",V2[b2]);
                                    }


                                    for(int u=0; u<prof[t].mtr_reg; u++)
                                    {
                                        if(M[g]==prof[t].nmrmateria[u])
                                        {
                                            for(int p = 0; p< prof[t].mtr_reg - u; p++)
                                            {

                                                prof[t].nmrmateria[u + p] = prof[t].nmrmateria[u + 1 + p];
                                            }
                                            prof[t].mtr_reg--;
                                            printf("\n\nA mat\202ria  foi retirada do professor/a %s",prof[t].nome);
                                            saida3 = 10;
                                        }

                                    }
                                }
                            }
                        }
                    }


                }
            }
        }
        fflush(stdin);
        printf("\n\nDeseja realizar mais alguma a\207\306o em PROFESSORES? Sim <1>, N\306o <0>\nR:");
        scanf("%d",&repeteco2);


    }
    while(repeteco2==1);

};

///IMPRIME O NOME DOS ALUNOS RA E MATERIAS QUE ESTÃO EM UMA TABELINHA ==========================================================================

void imprimir(pfs prof[],als es[],int nmr_a,curs mat[],int nmr_c,int nmr_p)
{
    
    int v;
    int ra_aluno;
    int verifc ;
    int ra_prof;
    int cod;

    do
    {
        system("cls");
        printf("\nDigite:\n1- Visualizar as mat\202rias de um aluno/a;\n2- Visualizar as mat\202rias de um professor/a;\n3- Visualizar a lista de chamada de um curso;\n4- Visualizar a lista de alunos;\n5- Visualizar a lista de professores;\n6- Visualizar a lista de cursos;\n7- Sair;\nR:");
        scanf("%d", &v);
        fflush(stdin);
        if(v==1)
        {

            do
            {
                verifc = 0;
                printf("\n\nLista de alunos:\n");
                for(int x1=0; x1<nmr_a; x1++)
                {
                    printf("- Nome: %10s   RA: %4.4d\n",es[x1].nome,es[x1].ra);
                }
                printf("\nDigite o RA do aluno/a:");
                scanf("%d",&ra_aluno);
                fflush(stdin);
                for (int j = 0; j<nmr_a; j++)
                {
                    verifc++;
                    if(es[j].ra == ra_aluno)
                    {
                        verifc = 4000;
                        printf("\n\nAluno/a: %s\nMat\202rias: ", es[j].nome);
                        for(int x=0; x<es[j].nmraulas; x++)
                        {
                            for(int c=0; c<nmr_c; c++)
                            {

                                if(mat[c].cod == es[j].nmrmateria[x])
                                {
                                    printf("%s, ",mat[c].nome_curs);
                                }
                            }
                        }
                    }
                }

                if(verifc == nmr_a)
                {
                    printf("\n\nRA n\306o encontrado!");
                }
            }
            while(verifc == nmr_a);
            printf("\n");
            system("pause");
        }
        else
        {
            if(v==2)
            {

                do
                {
                    verifc = 0;
                    printf("\n\nLista de professores:\n");
                    for(int x2=0; x2<nmr_p; x2++)
                    {
                        printf("- Nome: %10s   RA: %4.4d\n",prof[x2].nome,prof[x2].ra);
                    }
                    printf("\nDigite o RA do professor/a:");
                    scanf("%d",&ra_prof);
                    fflush(stdin);
                    for (int j = 0; j<nmr_p; j++)
                    {
                        verifc++;
                        if(prof[j].ra == ra_prof)
                        {
                            verifc = 4000;
                            printf("\n\nProfessor/a: %s\nMat\202rias: ", prof[j].nome);
                            for(int x=0; x<prof[j].mtr_reg; x++)
                            {
                                for(int c=0; c<nmr_c; c++)
                                {

                                    if(mat[c].cod == prof[j].nmrmateria[x])
                                    {
                                        printf("%s, ",mat[c].nome_curs);
                                    }

                                }
                            }
                        }
                    }

                    if(verifc == nmr_p)
                    {
                        printf("\n\nRA n\306o encontrado!");
                    }
                }
                while(verifc == nmr_p);
                printf("\n");
                system("pause");
            }
            else
            {
                if(v==3)
                {
                    printf("\n\nLista de cursos:\n");
                    for(int x3=0; x3<nmr_c; x3++)
                    {
                        printf("- Nome: %10s   CODIGO: %4.4d\n",mat[x3].nome_curs,mat[x3].cod);
                    }
                    printf("Digite o c\242digo do curso: ");
                    scanf("%d", &cod);
                    fflush(stdin);
                    for(int h = 0; h<nmr_c; h++)
                    {
                        if(cod == mat[h].cod)
                        {
                            printf("\n\nMat\202ria: %s\n",mat[h].nome_curs);
                            for(int x=0; x<nmr_p; x++)
                            {
                                for(int w=0; w<nmr_c; w++)
                                {

                                    if(prof[x].nmrmateria[w] == cod)
                                    {
                                        printf("Professor/a: %s ",prof[x].nome);
                                    }
                                }
                            }
                            printf("\nAlunos: \n");
                            for(int y=0; y<nmr_a; y++)
                            {
                                for(int u=0; u<nmr_c; u++)
                                {

                                    if(es[y].nmrmateria[u] == cod)
                                    {
                                        printf("\n- %s",es[y].nome);
                                    }
                                }
                            }

                        }

                    }
                    printf("\n");
                    system("pause");
                }
                else
                {
                    if(v==7)
                    {
                        

                        return 0;

                    }
                    else
                    {
                        if(v==4)
                        {
                            printf("\n\nLista de alunos:\n");
                            for(int x1=0; x1<nmr_a; x1++)
                            {
                                printf("- Nome: %10s   RA: %4.4d\n",es[x1].nome,es[x1].ra);
                            }

                            printf("\n");
                            system("pause");

                        }
                        else
                        {
                            if(v==5)
                            {
                                printf("\n\nLista de professores:\n");
                                for(int x2=0; x2<nmr_p; x2++)
                                {
                                    printf("- Nome: %10s   RA: %4.4d\n",prof[x2].nome,prof[x2].ra);
                                }

                                printf("\n");
                                system("pause");
                            }
                            else
                            {
                                if(v==6)
                                {
                                    printf("\n\nLista de cursos:\n");
                                    for(int x3=0; x3<nmr_c; x3++)
                                    {
                                        printf("- Nome: %10s   CODIGO: %4.4d\n",mat[x3].nome_curs,mat[x3].cod);
                                    }

                                    printf("\n");
                                    system("pause");
                                }
                            }
                        }
                    }
                }
            }
        }

    }

    while(v!=7);
}
void limpa_variavel(pfs prof[], als es[])
{

    for(int x=0; x<20; x++)
    {
        prof[x].mtr_reg=0;
        es[x].nmraulas=0;
        for(int j=0; j<20; j++)
        {

            es[x].nmrmateria[j]=0;
            prof[x].nmrmateria[j]=0;
        }
    }
}
int main()
{
///CHAMA AS STRUCTS NO INT MAIN ==============================================================================================
    
    als estudantes[20];
    pfs professor[20];
    curs cur[20];
    int nmrcursos=0;
    int nmrprof = 0;
    char opc1[7] = {'a','l','u','n','o','s','\0'};
    char opc2 [7] = {'c','u','r','s','o','s','\0'};
    char opc3 [12] = {'p','r','o','f','e','s','s','o','r','e','s','\0'};
    int parar= 1;
    int nmralunos = 0;
    char escolha[12];
    int saida;
    limpa_variavel(professor,estudantes);
    do{
  ///MENU INICIAL DO PROGRAMA ========================================================================================================
    
    do{
            system("cls");
    printf("\n\t\tBem vindo ao cadastro da Puc!\nO que voce deseja: \n1- Matricular ou Cadastrar;\n2- Visualizar as Altera\207\344es;\n3- Sair;\nR: ");
    scanf("%d", &saida);
    fflush(stdin);
    }while(saida < 0 && saida >4);




    if(saida == 1){

    do
    {
        parar=0;
        system("cls");
///MENU SECUNDARIO DO PROGRAMA ========================================================================================================
        
        printf("\n\t\tBem vindo ao cadastro da Puc!\nO que voce deseja Cadastrar/Matricular? (alunos, professores ou cursos)\nR: ");
        gets(escolha);

        if (strcmp(escolha,opc1) == 0)
        {
            alunos(estudantes,&nmralunos,cur, nmrcursos);
        }
        else
        {
            if (strcmp(escolha,opc2) == 0)
            {
                curso(cur,professor,&nmrcursos);
            }
            else
            {
                if (strcmp(escolha,opc3) == 0)
                {
                    professores(professor,cur,nmrcursos,&nmrprof);
                }
                else
                {
                    printf("\nOp\207\306o n\306o encontrada...");
                }
            }
        }
        printf("\n\n\n\nDeseja Inserir mais algum dado? Sim <1>, N\306o <0>\nR:");
        scanf("%d", &parar);
        fflush(stdin);
        system("cls");
    }while(parar!= 0);}
    else{
        if(saida == 2){imprimir(professor,estudantes,nmralunos,cur,nmrcursos,nmrprof);}
        else{
            printf("\n\n\n        OBRIGADO POR UTILIZAR O PROGRAMA!!!\n\n\n");
            return 0;
        }
    }

    } while(saida != 3);
    return 0;

}
