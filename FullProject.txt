#include <stdio.h>
#include <stdlib.h>
#include <time.h>

float metrii,b,pt_tije=0.0,cl=0.0;

int main()
{

    afisare(&metrii,&b);


}


void numar_tije (float *x,float *y, float *rez )
{
    *rez=*x+*y;
}


void cheltuiala (float *x,float *y, float *rez_cost)
{
    *rez_cost=*x+*y;
}


void tija_ramasa (float *x,float *y,float *rest)
{
    *rest=*x-*y;
}

void afisare ()
{
    int i,pret,bucata=2;
    float tije_vandute,rez,rez_cost,cost,cost_total,a;
    char decizie3,decizie2,decizie;
    srand(time(NULL));
    metrii=rand()%100;
    printf("\n\nTja are lungimea de %.0f metrii\n",metrii);
    printf("\n\n        Numar de bucati :");
    printf("                Pret     :\n");
    for(i=1;i<=metrii;i++)
    {
        pret=bucata*i;
        printf("\n");
        printf(i<=1 ? "        Pentru %d metru :                %d lei\n" : "        Pentru %d metrii :                %d lei\n",i,pret);
    }

        printf("\n\nCati metrii doriti sa cumparati din tija ? : \n");
        b = (float)rand()/RAND_MAX;
        printf("%.1f metrii",b);
        if (b<=metrii)
        prelucrare_1();
       else
        if(b>metrii)
        prelucrare_2();


}

void prelucrare_1()
{
    float tije_vandute=0.0,rez,cost_total=0.0,cost,rez_cost,bucata=2.0,rest;
    numar_tije(&tije_vandute,&b,&rez);
     pt_tije=pt_tije+rez;
    tija_ramasa(&metrii,&b,&rest);
    cost=b*bucata;
    printf(b==1 ? "\nAti selectat un metru\n" : "\nAti selectat %.1f metrii\n",b);
    printf("\nCostul este %.2f lei \n",cost);
    cheltuiala(&cost_total,&cost,&rez_cost);
    cl=cl+rez_cost;
    if (rest>0)
        prelucrare_3();


}

void prelucrare_2()
{
    char decizie3;
    float cost,bucata=2.0,cost_total,rez_cost,tije_vandute,rez;
    printf("\n\nNe pare rau,dar nu avem suficienti metrii din tija\n");
    printf("\n\nDar va putem oferi restul de %.0f metrii\n",metrii);
    printf("\n\nDoriti sa cumparati? [Y/N]:");
    scanf("%s",&decizie3);
    decizie_trei();
    if(decizie3=='Y')
            {
                cost=metrii*bucata;
                printf("\n\nAti cumparat toti metrii din tija!\n");
                printf("\n\nVa costa %.2f lei\n",cost);
                cheltuiala(&cost_total,&cost,&rez_cost);
                numar_tije(&tije_vandute,&metrii,&rez);
                printf("\n\n\nInventarul obtinut prin vanzarea a %.1f metrii din tija este de %.2f lei\n",rez,rez_cost);
            }
                else
                {
                printf("\n\n\nInventarul obtinut prin vanzarea a %.1f metrii din tija este de %.2f lei\n",rez,rez_cost);
                }
}

void prelucrare_3()
{
    char decizie,decizie2;
    float cost,bucata=2.0,rez,rez_cost,rest;
    tija_ramasa(&metrii,&b,&rest);
    printf(rest==1 ? "\nMai este valabil un metru din tija" : "\nMai sunt valabili %.1f metrii din tija\n",rest);
    printf("\n\nMai doriti sa cumparati ? [Y/N] :");
    scanf("%s",&decizie);
    decizie_unu();
     while(decizie=='Y' && rest>0)
        {

                printf("\nCati metrii mai doriti ? : ");
                b = (float)rand()/RAND_MAX;
                if(b<=rest && rest>0 && decizie=='Y')
                {
                    tija_ramasa(&rest,&b,&rest);
                    cost=bucata*b ;
                    printf(b==1 ? "\n\nAti mai comandat un metru" : "\n\nAti mai comandat %.1f metrii\n",b);
                    printf("\nVa mai costa inca %.2f lei\n",cost);
                    numar_tije(&rez,&b,&rez);
                    cheltuiala(&rez_cost,&cost,&rez_cost);
                    printf(rest==1 ? "\nMai este valabil un metru" : "\nMai sunt valabili %.1f metrii din tija\n",rest);
                    printf("\nMai doriti metrii din tija ? [Y/N] :");
                    scanf("%s",&decizie);
                }
                else
                    if(b>rest)
                {
                    printf("\nNe pare rau,nu mai avem suficienti metrii \n");
                    if(rest>0)
                    {
                        printf(rest==1 ? "\nDar va mai putem oferi un metru din tija ramasa\n" : "\nDar va mai putem oferi restul de %.1f metrii din tija\n",rest);
                        printf(rest==1 ? "\nDoriti sa  cumparati ? [Y/N] :" : "Doriti sa  cumparati ? : [Y/N] :");
                        scanf("%s",&decizie2);
                        decizie_doi();
                        if(decizie2=='Y')
                        {
                            cost=rest*bucata;
                            printf(rest==1 ? "\nAti mai cumparat un metru" : "\nAti mai cumparat %.1f metrii\n",rest);
                            printf("\nVa mai costa %.2f lei\n",cost);
                            numar_tije(&rez,&b,&rez);
                            cheltuiala(&rez_cost,&cost,&rez_cost);
                            printf("\n\n\nInventarul obtinut prin vanzarea a %.1f metrii din tija este de %.2f lei\n",rez,rez_cost);
                        }
                        else
                            printf("\n\n\nInventarul obtinut prin vanzarea a %.1f metrii din tija este de %.2f lei\n",rez,rez_cost);
                    }
                }
        }printf("\n\n\nInventarul obtinut prin vanzarea a %.1f metrii din tija este de %.2f lei\n",rez+pt_tije,rez_cost+cl);


}




void decizie_trei ()
{
    char decizie3;
     switch(decizie3)
            {
            case 'Y' : break;
            case 'N' : break;
            }
}

void decizie_unu ()
{
    char decizie;
    switch(decizie)
        {
            case 'Y' : break;
            case 'N' : break;
        }
}


void decizie_doi ()
{
    char decizie2;
     switch(decizie2)
                        {
                            case 'Y' : break;
                            case 'N' : break;
                        }
}




