# Thread
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
#include<stdlib.h>

#define ARRSIZE 25

int fib_arr[ARRSIZE];                                     //this array is shared by threads
void *fibonacci(void *n);                            // dynamic allocation of memory

int main(int argc,char *argc1[] )
{
 int num;
 int x;
 pthread_attr_t attr;                               //declare pthread_t type variable 'tid'
if(argc !=2)
 {
  printf("Please insert one command line argument\n");
  return -1;
 }
 num=atoi(argc1[1]);                           //convert string value to integer and store to 'no'

  if(num<0)
{
  printf("To Continue please enter non-negative number\n");
 }
 else
{
  pthread_attr_init(&attr);
  pthread_t tid;                                          //thread Identifier
  pthread_create(&tid,&attr,fibonacci,num);            //create a thread
  pthread_join(tid,NULL);  
   printf(" - Programs Out put - \n");
  printf("\n");
  printf("Set of Fibonacci numbers.........\n");

   for(x=0; x<num; x++){

   printf("%d \t ",fib_arr[x]);
  }
  printf("\n");
  
 }
 return 0;
}

void *fibonacci(void *n)
{

  int x = 0;
 int y = 1;
 int fibn=0;
 int i;
 
 for(i=1; i<=n; i++){
  fib_arr[i-1]=fibn;
  fibn = x + y;
  x = y;
  y = fibn;
 } 
 pthread_exit(0);
}
