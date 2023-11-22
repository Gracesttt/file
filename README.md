# file
#include <stdio.h>
#include <string.h>

int main()
{
    unsigned int account;// account number
    char name[30],s_name[30];   // account name
    double balance; // account balance
    int choice;
    
    FILE *fp;
    
    if ( (fp=fopen("client.dat","a+") )==NULL) {
        puts ("File could not be opened ");
    }
    else{
        puts("Enter your request");
        puts("1.Search with Account Name");
        puts("2.List all account");
        puts("3.Add account");
        printf("4.End of run\n?"); 
        scanf("%d",&choice);
        
        while(choice !=4){
              fscanf(fp,"%d %s %lf",&account,name,&balance);
              switch(choice){
                  case 1:
                  double totalBalance = 0.0;
                    printf("Enter name to search:");
                    scanf("%s",s_name);
                   while(!feof(fp)){
                       if(strcmp(name,s_name)==0) {
                             printf("%-10d%-13s%7.2f\n",account,name,balance);
                             totalBalance += balance;
                       }
                        fscanf(fp,"%d %s %lf",&account,name,&balance);
                   } 
                   printf("Total Balance: %.2f\n", totalBalance);
                  break;
                  case 2:
                   while(!feof(fp)){
                        printf("All account\n");
                        printf("%-10s%-13s%7s\n","Account","Name","Balance");
                        double totalAllBalance = 0.0;
                        while(!feof(fp)){
                            printf("%-10d%-13s%7.2f\n",account,name,balance);
                            totalAllBalance += balance;
                            fscanf(fp,"%d %s %lf",&account,name,&balance);
                            
                        } 
                        printf("Total All Balance: %.2f\n", totalAllBalance);
                   }
                  break;
                  
                  case 3:
                  
                  puts("Enter the account number name balance: ");
                  puts("Enter (keyboard) EOF to end the input");
                  printf("?");
                  scanf("%d %s %lf",&account,name,&balance);
                  
                  while(!feof(stdin)){
                   fprintf(fp, "%d %s %.2f\n", account,name,balance);
                   printf("?");
                   scanf("%d %s %lf",&account,name,&balance);
                  }
                  fclose(fp);
                  break;
              }
              
        printf("?");
        scanf("%d",&choice);
        rewind(fp);              
        }
        fclose(fp);
    }

    return 0;
}
