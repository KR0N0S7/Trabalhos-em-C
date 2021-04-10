# Controlador de Estoque :open_file_folder:

#include <stdio.h>

#include <string.h>  //usado para utilizar funções do sistema

#include <stdlib.h>

#define SIZE 100  //define uma constante



int cod[SIZE];

int estoque[SIZE]; 

char desc[SIZE][30];  

float preco[SIZE];

float frete[SIZE]; 

int op;



void cadastra_produto();

void pesquisa();

void lista();

void apaga();

void edita();

void compra();



//função para cadastro de produtos

void cadastra_produto(){

​	static int linha;

​	do{

​		printf("Entrar com o codigo do produto a ser registrado: ");

​		scanf("%d", &cod[linha]);

​		setbuf(stdin, NULL);  //limpa o buffer do teclado

​		printf("Descrever o produto registrado: ");

​		fgets(desc[linha], 30, stdin);

​		desc[linha] [strcspn(desc[linha], "\n")] = 0; 	/*ao utilizar o fgets,

​		este armazena a quebra de linha na memória, portanto, 

​		utiliza-se 'strcspn' para substituir '\n' por um valor nulo*/

​		//variável[strcspn(variável, "\n")] = 0;

​		printf("Informe o preco do produto: ");

​		scanf("%f", &preco[linha]);



​		printf("Entrar com a quantidade do produto registrado no estoque: ");

​		scanf("%d", &estoque[linha]);



​		printf("Entrar com o frete do produto registrado: ");

​		scanf("%f", &frete[linha]);



​		printf("\nDigite 1 para continuar ou outro valor para sair: ");

​		scanf("%d", &op);



​		linha++;



​	}while(op==1);



}



//função para pesquisar produto no sistema

void pesquisa(){

​	int cod_pesquisa;

​	char desc_pesquisa[30];

​	int i;

​	

do{

​	printf("\nDigite 1 para pesquisar por codigo ou 2 para pesquisar pelo nome do produto: ");

​	scanf("%d", &op);

​	switch(op){

​		case 1:{

​			printf("\nDigite o codigo do produto: ");

​			scanf("%d", &cod_pesquisa);

​			for(i=0;i<SIZE;i++){  //percorre todas as linhas de cadastro para verificar valores

​				if(cod[i]==cod_pesquisa){ 

​					printf("\nCodigo do produto: %d\nNome do produto: %s\nPreco unitario: RS%.2f\nValor do frete: RS%.2f\nQuantidade em estoque: %d\n", cod[i], desc[i], preco[i], frete[i], estoque[i]);

​				}

​			}

​			break;

​		}

​		case 2:{

​			setbuf(stdin, NULL);

​			printf("Digite o nome do produto: ");

​			fgets(desc_pesquisa, 30, stdin);

​			for(i=0;i<SIZE;i++){

​				if(strcmp(desc[i], desc_pesquisa)){ 	//strcmp, compara duas strings

​					printf("\nCodigo do produto: %d\nNome do produto: %sPreco unitario: RS%.2f\nValor do frete: RS%.2f\nQuantidade em estoque: %d\n", cod[i], desc[i], preco[i], frete[i], estoque[i]);

​				}

​			}

​			break;

​		}

​		default:{

​			printf("\nOpcao invalida.");

​			break;

​		}

​	}

​	printf("\nDigite 1 para continuar pesquisando: ");

​	scanf("%d", &op);

​	}while(op==1);



}



//função para listar produtos cadastrados

void lista(){

​	int i;

​	

​	printf("Codigo");

​	printf("\t\tNome do produto");

​	printf("\t\t\tpreco [unidade1]");

​	printf("\testoque");

​	printf("\t\tfrete\n");



​	for(i=0;i<SIZE;i++){

​		if(cod[i]>0){

​			printf("%-10d", cod[i]);

​			printf("\t%-30s", desc[i]);

​			printf("\tRS%9.2f", preco[i]);

​			printf("\t\t%-3d", estoque[i]);

​			printf("\t\tRS%5.2f\n", frete[i]);

​		}

​		else break; 	/* ao terminar os cadastros a função é terminada,
​		se não, a função percorre até as linhas finais mesmo não tendo
​		mais cadastros de produtos */

​	}

​	getch();



}



//função para apagar produtos da lista

void apaga(){

​	int cod_apaga;

​	int i;

​	

do{

​	printf("\nDigite o codigo 1 para continuar ou 2 para retornar: ");

​	scanf("%d", &op);

​	switch(op){

​		case 1:{

​			printf("\nDigite o codigo do produto a ser deletado: ");

​			scanf("%d", &cod_apaga);

​			for(i=0;i<SIZE;i++){

​				if(cod[i]==cod_apaga){

​					cod[i] = 0;

​					estoque[i] = 0;

​					//desc[i][strcspn(desc[i], "")] = 0;

​					//desc[i] = '\0';

​					preco[i] = 0;

​					frete[i] = 0;

​					printf("\nProduto deletado com sucesso.");

​				}

​			}

​			break;

​		}

​		case 2:{

​			break;

​		}

​		default:{

​			printf("\nOpcao invalida.");

​			break;

​		}

​	}

​	printf("\nDigite 1 para continuar deletando: ");

​	scanf("%d", &op);



​	}while(op==1);



}



//função para editar produtos cadastrados

void edita(){

​	int cod_edita;

​	int i;

​	

​	do{

​		printf("\nDigite o codigo 1 para continuar ou 2 para retornar: ");

​		scanf("%d", &op);

​		switch(op){

​			case 1:{

​				printf("\nDigite o codigo do produto a ser editado: ");

​				scanf("%d", &cod_edita);

​				for(i=0;i<SIZE;i++){

​					if(cod[i]==cod_edita){

​						printf("Entrar com o codigo do produto a ser registrado: ");

​						scanf("%d", &cod[i]);



​						setbuf(stdin, NULL);

​						printf("Descrever o produto registrado: ");

​						fgets(desc[i], 30, stdin);

​						desc[i][strcspn(desc[i], "\n")] = 0;



​						printf("Informe o preco do produto: ");

​						scanf("%f", &preco[i]);



​						printf("Entrar com a quantidade do produto registrado no estoque: ");

​						scanf("%d", &estoque[i]);



​						printf("Entrar com o frete do produto registrado: ");

​						scanf("%f", &frete[i]);



​						printf("\nProduto editado com sucesso.");



​					}



​				}

​				break;



​			}

​			case 2:{

​				break;



​			}

​			default:{

​				printf("\nOpcao invalida.");

​				break;

​			}



​		}

​		if(op==2) break;

​		printf("\nDigite 1 para continuar editando: ");

​		scanf("%d", &op);



​	}while(op==1);



}



//função para comprar produtos

void compra(){

​	do{

​		char nome[50], end[50];

​		int i, num, quant_compra, op;

​		float total1, total2;

​		

​		setbuf(stdin, NULL);

​		printf("Nome completo do cliente: ");

​		fgets(nome, 50, stdin);

​		nome[strcspn(nome, "\n")] = 0;

​	

​		printf("Codigo do produto desejado: ");

​		scanf("%d", &num);



​		for(i=0; i<SIZE; i++){

​			if (num==cod[i]){

​				setbuf(stdin, NULL);

​				printf("Endereco de entrega: ");

​				fgets(end, 30, stdin);

​				end[strcspn(end, "\n")] = 0;

​				printf("Quantia desejada: ");

​				scanf("%d", &quant_compra);

​					if (quant_compra<=estoque[i]){

​					estoque[i] = estoque[i] - quant_compra;

​					total1 = preco[i] * quant_compra; 

​					total2 = total1 + frete[i];

​		 

​					printf("\n-----Dados do Produto----- ");

​					printf("\nCodigo do produto: %d", cod[i]);

​					printf("\nDescricao do produto: %s", desc[i]);

​					printf("\nPreco unitario: RS%.2f", preco[i]);

​					printf("\nQuantidade atual no estoque: %d", estoque[i]);

​					printf("\nFrete do produto: RS%.2f", frete[i]);

​					printf("\n\n-----Dados dacompra----- ");

​					printf("\nNome do cliente: %s", nome);

​					printf("\nEndereco de entrega: %s", end);

​					printf("\nValor total da compra sem o frete: RS%.2f", total1);

​					printf("\nValor total da compra com o frete: RS%.2f", total2);



​					getch();



​				}

​				else

​					printf("Pedido NAO pode ser atendido");

​					getch();



​			}



​		}


​		printf("Digite 1 para continuar comprando");

​		scanf("%d", &op);



​	}while(op==1);



}



//programa principal

int main(void){

​	do{

​		system("cls");

​		printf("---------------------------------------\n");

​		printf("\tControlador de Estoques\n");

​		printf("---------------------------------------\n\n");

​		printf("-----------------Menu------------------\n");

​		printf("\t    1 - Cadastrar\n\t    2 - Pesquisar\n\t    3 - Listar\n\t    4 - Apagar\n\t    5 - Editar\n\t    6 - Comprar\n\t    7 - Sair");

​		printf("\n---------------------------------------\n");

​		printf("\nOpcao desejada: ");

​		scanf("%d", &op);

​		

​		switch(op){

​			case 1:{

​				cadastra_produto();

​				break;

​			}

​			case 2:{

​				pesquisa();

​				break;

​			}

​			case 3:{

​				lista();

​				break;

​			}

​			case 4:{

​				apaga();

​				break;

​			}

​			case 5:{

​				edita();

​				break;

​			}

​			case 6:{

​				compra();

​				break;

​			}

​			case 7:{

​				system("exit");

​				break;

​			}

​			default:{

​				printf("Opcao invalida.");

​				getch();

​				break;

​			}

​		}

​	}while(op!=7);



}

