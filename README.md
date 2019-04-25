# os-project
#include<stdio.h>
#include<string.h>
#include<conio.h>
int main()
{
	int TS,PROCESSID[10],NEED[10],WTIME[10],TURNARTIME[10],i,j,n,n1;
    int BURSTTIME[10],flag[10],TOTALTAT=0.0,TWT=0.0;
    float AVGWTIME=0,AVGTAT=0;
    printf("Enter NO of Processes \n");
    scanf("%d",&n);
    n1=n; 
    printf("\nEnter the Time-slice \n");
    scanf("%d",&TS);
    for(i=1;i<=n;i++)
{
    		printf("\nEnter the process ID for %d :" ,i);
    		scanf("%d",&PROCESSID[i]);
            printf("\nEnter the Burst Time for the process:");
            scanf("%d",&BURSTTIME[i]);
            NEED[i]=BURSTTIME[i];
        }
for(i=1;i<=n;i++)
   {
    flag[i]=1;
    WTIME[i]=0;
    }
while(n!=0){
for(i=1;i<=n;i++)
{
if(NEED[i]>=TS){
for(j=1;j<=n;j++)       
{
 if((i!=j)&&(flag[i]==1)&&(NEED[j]!=0))	  
WTIME[j]+=TS;
} 
NEED[i]-=TS;      
 if(NEED[i]==0)
{
flag[i]=0;
n--;
}
}    
else  
{
for(j=1;j<=n;j++)
{
if((i!=j)&&(flag[i]==1)&&(NEED[j]!=0))	  
WTIME[j]+=NEED[i];
}
NEED[i]=0;
n--;
flag[i]=0;
}}
}
for(i=1;i<=n1;i++)
{
TURNARTIME[i]=WTIME[i]+BURSTTIME[i];
TWT=TWT+WTIME[i];
TOTALTAT=TOTALTAT+TURNARTIME[i];
}
for(i=1;i<=n1;i++)
{
AVGWTIME=(float)TWT/n1;
AVGTAT=(float)TOTALTAT/n1;	
}
printf("\n ROUND ROBIN SCHEDULING ALGORITHM \n");
printf("\n\n Process\tProcess ID\tBurstTime\tWaiting Time\tTurnaroundTime \n ");
for(i=1;i<=n1;i++)
{
printf("\n %5d\t\t%5d \t\t %5d \t\t %5d \t\t %5d \n", i,PROCESSID[i],BURSTTIME[i],WTIME[i],TURNARTIME[i]);
}
printf("\n The average Waiting Time= %f",AVGWTIME);
printf("\n The average Turn around Time= %f",AVGTAT);
getch();
}         
