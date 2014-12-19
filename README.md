-PROJECT
========
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

struct card{
    int numberi;
    char numberc;
    int suiti;
    char suitc;
};

struct card player[2];
struct card computer[2];
struct card pub[5];

int deck[52]={0};

void deal();

char findnumberc(int);

char findsuitc(int);

void sortcard();

int main(){
    int enter;
    printf("歡迎來到中正資工德州撲克\n是否進入遊戲?(1:進入，0:離開)\n");
    scanf("%d",&enter);
    if(enter){
        deal();
        system("pause");
        sortcard();
        system("pause");
    }
    return 0;
}

void deal(){
    int a,i;
    srand(time(NULL));
    for(i=0;i<2;i++){
        a=rand()%52;
        while(deck[a]){
            if(a==51)
                a=0;
            else
                a++;
        }
        deck[a]=1;
        player[i].numberi=a%13+1;
        player[i].suiti=a/13;
        player[i].numberc=findnumberc(player[i].numberi);
        player[i].suitc=findsuitc(player[i].suiti);
    }
    printf("玩家手牌為");
    for(i=0;i<2;i++)
        printf("%c%c ",player[i].numberc,player[i].suitc);
    printf("\n");

    for(i=0;i<2;i++){
        a=rand()%52;
        while(deck[a]){
            if(a==51)
                a=0;
            else
                a++;
        }
        deck[a]=1;
        computer[i].numberi=a%13+1;
        computer[i].suiti=a/13;
        computer[i].numberc=findnumberc(computer[i].numberi);
        computer[i].suitc=findsuitc(computer[i].suiti);
    }
    printf("電腦手牌為");
    for(i=0;i<2;i++)
        printf("%c%c ",computer[i].numberc,computer[i].suitc);
    printf("\n");

    for(i=0;i<5;i++){
        a=rand()%52;
        while(deck[a]){
            if(a==51)
                a=0;
            else
                a++;
        }
        deck[a]=1;
        pub[i].numberi=a%13+1;
        pub[i].suiti=a/13;
        pub[i].numberc=findnumberc(pub[i].numberi);
        pub[i].suitc=findsuitc(pub[i].suiti);
    }
    printf("公用牌為");
    for(i=0;i<5;i++)
        printf("%c%c ",pub[i].numberc,pub[i].suitc);
    printf("\n");
}

char findnumberc(int x){
    if(x==1)
        return 'A';
    if(x==2)
        return '2';
    if(x==3)
        return '3';
    if(x==4)
        return '4';
    if(x==5)
        return '5';
    if(x==6)
        return '6';
    if(x==7)
        return '7';
    if(x==8)
        return '8';
    if(x==9)
        return '9';
    if(x==10)
        return 'T';
    if(x==11)
        return 'J';
    if(x==12)
        return 'Q';
    if(x==13)
        return 'K';
}

char findsuitc(int x){
    if(x==0)
        return 'C';
    if(x==1)
        return 'D';
    if(x==2)
        return 'H';
    if(x==3)
        return 'S';
}

void sortcard(){
    int tempn,temps,i,j;
    if(player[0].numberi>player[1].numberi){
        tempn=player[0].numberi;
        player[0].numberi=player[1].numberi;
        player[1].numberi=tempn;
        temps=player[0].suiti;
        player[0].suiti=player[1].suiti;
        player[1].suiti=temps;
        for(i=0;i<2;i++){
            player[i].numberc=findnumberc(player[i].numberi);
            player[i].suitc=findsuitc(player[i].suiti);
        }
    }
    if(player[0].numberi==player[1].numberi && player[0].suiti>player[1].suiti){
        tempn=player[0].numberi;
        player[0].numberi=player[1].numberi;
        player[1].numberi=tempn;
        temps=player[0].suiti;
        player[0].suiti=player[1].suiti;
        player[1].suiti=temps;
        for(i=0;i<2;i++){
            player[i].numberc=findnumberc(player[i].numberi);
            player[i].suitc=findsuitc(player[i].suiti);
        }
    }
    printf("玩家手牌排序後為");
    for(i=0;i<2;i++)
        printf("%c%c ",player[i].numberc,player[i].suitc);
    printf("\n");

    if(computer[0].numberi>computer[1].numberi){
        tempn=computer[0].numberi;
        computer[0].numberi=computer[1].numberi;
        computer[1].numberi=tempn;
        temps=computer[0].suiti;
        computer[0].suiti=computer[1].suiti;
        computer[1].suiti=temps;
        for(i=0;i<2;i++){
            computer[i].numberc=findnumberc(computer[i].numberi);
            computer[i].suitc=findsuitc(computer[i].suiti);
        }
    }
    if(computer[0].numberi==computer[1].numberi && computer[0].suiti>computer[1].suiti){
        tempn=computer[0].numberi;
        computer[0].numberi=computer[1].numberi;
        computer[1].numberi=tempn;
        temps=computer[0].suiti;
        computer[0].suiti=computer[1].suiti;
        computer[1].suiti=temps;
        for(i=0;i<2;i++){
            computer[i].numberc=findnumberc(computer[i].numberi);
            computer[i].suitc=findsuitc(computer[i].suiti);
        }
    }
    printf("電腦手牌排序後為");
    for(i=0;i<2;i++)
        printf("%c%c ",computer[i].numberc,computer[i].suitc);
    printf("\n");

    for(i=0;i<4;i++)
        for(j=i+1;j<5;j++)
            if(pub[i].numberi>pub[j].numberi){
                tempn=pub[i].numberi;
                pub[i].numberi=pub[j].numberi;
                pub[j].numberi=tempn;
                temps=pub[i].suiti;
                pub[i].suiti=pub[j].suiti;
                pub[j].suiti=temps;
            }

    for(i=0;i<4;i++)
        for(j=i+1;j<5;j++)
            if(pub[i].numberi==pub[j].numberi && pub[i].suiti>pub[j].suiti){
                tempn=pub[i].numberi;
                pub[i].numberi=pub[j].numberi;
                pub[j].numberi=tempn;
                temps=pub[i].suiti;
                pub[i].suiti=pub[j].suiti;
                pub[j].suiti=temps;
            }

    for(i=0;i<5;i++){
        pub[i].numberc=findnumberc(pub[i].numberi);
        pub[i].suitc=findsuitc(pub[i].suiti);
    }

    printf("公用牌排序後為");
    for(i=0;i<5;i++)
        printf("%c%c ",pub[i].numberc,pub[i].suitc);
    printf("\n");
}
