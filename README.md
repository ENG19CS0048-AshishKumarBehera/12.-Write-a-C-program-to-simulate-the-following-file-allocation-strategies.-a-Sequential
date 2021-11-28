# 12.-Write-a-C-program-to-simulate-the-following-file-allocation-strategies.-a-Sequential
#include<stdio.h>
#define FALSE 0
#define TRUE 1
int allocateSequentially(int startingPosition, int allocationLength, int 
maximumSize, int block[])
{
/*------------------------------------------------------------------------------
----------- */
 // initializations
int isPossible = TRUE;
int i; //loopvar
/*------------------------------------------------------------------------------
----------- */
 //checking whether already occupied
 if(startingPosition + allocationLength > maximumSize + 1)
 {
 return FALSE;
 }
 for(i=startingPosition-1; i<startingPosition+allocationLength-1; i++)
 {
 if(block[i] == TRUE)
 {
 isPossible = FALSE;
 return FALSE;
 }
 }
 /*----------------------------------------------------------------------------------
------- */
 //allocate
 for(i=startingPosition-1; i<startingPosition+allocationLength-1; i++)
 {
 block[i] = TRUE;
 }
 return TRUE;
}
int main()
{
/*------------------------------------------------------------------------------
----------- */
 // initializations
 int allocationLength, startingPosition, maximumSize;
 int i, j; //loop var
 int inputChoice;
 /*----------------------------------------------------------------------------------
------- */
 // input
 printf("\n\n\t\t Sequential File Allocation Method Demonstration\n\t\t 
---------- ---- ---------- ------");
 printf("\n\n\t Enter the maximum size available : ");
 scanf("%d", &maximumSize);
 /*----------------------------------------------------------------------------------
------- */
 // initialisation
 int block[maximumSize];
 for(i=0; i<maximumSize; i++)
 {
 block[i] = FALSE;
 }
 /*----------------------------------------------------------------------------------
------- */
 //execute till user wants to exit
 while(1)
 {
 printf("\n\n\t\t MENU : \n\n\t\t 1. Allocate \n\n\t\t 2. Exit \n\n\t\t 
Choice : ");
 scanf("%d", &inputChoice);
 if(inputChoice == 2)
 {
 return 0;
 }
 printf("\n\n\t Enter the starting address : ");
 scanf("%d", &startingPosition);
 printf("\n\n\t Enter the length of the block : ");
 scanf("%d", &allocationLength);
 if(allocateSequentially(startingPosition, allocationLength, 
maximumSize, block) == TRUE)
 {
 printf("\n\n\t Successfully Allocated!");
 }
 else
 {
 printf("\n\n\t Space cannot be allocated!");
 }
 } }
b) Indexed
#include <stdio.h>
#include <conio.h>
#include <stdlib.h>
int files[50], indexBlock[50], indBlock, n;
void recurse1();
void recurse2();
void recurse1(){
 printf("Enter the index block: ");
 scanf("%d", &indBlock);
 if (files[indBlock] != 1){
 printf("Enter the number of blocks and the number of files needed 
for the index %d on the disk: ", indBlock);
 scanf("%d", &n);
 }
 else{
 printf("%d is already allocated\n", indBlock);
 recurse1();
 }
 recurse2();
}
void recurse2(){
 int ch;
 int flag = 0;
 for (int i=0; i<n; i++){
 scanf("%d", &indexBlock[i]);
 if (files[indexBlock[i]] == 0)
 flag++;
 }
 if (flag == n){
 for (int j=0; j<n; j++){
 files[indexBlock[j]] = 1;
 }
 printf("Allocated\n");
 printf("File Indexed\n");
 for (int k=0; k<n; k++){
 printf("%d ------> %d : %d\n", indBlock, indexBlock[k], 
files[indexBlock[k]]);
 }
 }
 else{
 printf("File in the index is already allocated\n");
 printf("Enter another indexed file\n");
 recurse2();
 }
 printf("Do you want to enter more files?\n");
 printf("Enter 1 for Yes, Enter 0 for No: ");
 scanf("%d", &ch);
 if (ch == 1)
 recurse1();
 else
 exit(0);
 return;
}
int main()
{
 for(int i=0;i<50;i++)
 files[i]=0;
 recurse1();
 return 0
