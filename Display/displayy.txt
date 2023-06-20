



/* 
	LDC 16X2
    
*/

/*
	Materiais:
    1 - Resistores de 220 Ohms
    1 - Resistor de 1,5 Kilohms
    1 - Display LCD 16x02

*/
/*
	BIBLIOTECAS ARDUINO
*/
#include <LiquidCrystal.h>


/*
	DECLARAÇÃO DE VARIÁVEL
*/

// Define os pinos de controle que serão utilizados para ligar o display

#define RS 7 // Define o pino de controle RS;
#define E 6 //Define o pino de controle E;
#define D4 5 //Define o pino de controle DB4;
#define D5 4 //Define o pino de controle DB4;
#define D6 3 //Define o pino de controle DB6;
#define D7 2 //Define o pino de controle DB7;

LiquidCrystal lcd(RS, E, D4, D5,D6,D7);

//Matriz de bytes correspondente ao desenho de um coração
byte heart[8] = {
	0b00000 ,
  	0b01010 ,
  	0b11111 ,
    0b01110 ,
  	0b00100 ,
  	0b00000 ,
  	0b00000
};

void setup()
{	// seta o número de colunas e linhas do display
	lcd.begin(16 , 2);
  
  	//coração
  	lcd.createChar(1, heart);
  
  	//chama a função limpa_tela
  	limpa_tela();
}

void loop()
{
	limpa_tela();
  
  	imprime_mensagem(6 , 0 , "EU");
  
  	imprime_caracter(9 , 0 , 1);
  
  	imprime_mensagem(4 , 1 , "LIVROS");
  
  
  for(int cont = 0; cont <= 5; cont++)
  {
  	delay(500);
    
    imprime_mensagem(9,0," ");
    
    delay(500);
    
    imprime_caracter(9,0,1);
  
  }
  
  for (int posicao = 0; posicao < 4; posicao++)
{
	lcd.scrollDisplayLeft();

 	delay(200);
}



for(int posicao = 0; posicao <8; posicao++)
{ 
  lcd.scrollDisplayRight();
  delay(200);
}
  

}

void limpa_tela()
{
	lcd.clear();
}

void imprime_mensagem(int coluna, int linha, char* mensagem)
{
  //posição
	lcd.setCursor(coluna, linha);
		//envia
  lcd.print(mensagem);
}

void imprime_caracter(int coluna, int linha, byte caracter)
{

	lcd.setCursor(coluna, linha);
    
  lcd.write(caracter);

}