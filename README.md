/*
name  main.c
creat time: 20161029
brief intruction: test of swa simulation 
mcu stm32f103rct6
by warpgate_hzk
e-mail: warpgate_hzk@foxmail.com
good luck
*/
#include "stm32f10x.h"
#include "delay.h"
#include "usart.h"
u8 t=0;
int main (void ){
	GPIO_InitTypeDef GPIO_InitStructure;
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOD,ENABLE);
	GPIO_InitStructure.GPIO_Pin = GPIO_Pin_2;
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOD,&GPIO_InitStructure);
	GPIO_SetBits(GPIOD,GPIO_Pin_2);
	
	delay_init();
	NVIC_PriorityGroupConfig(NVIC_PriorityGroup_2);		//NVIC 提供中断控制器
	uart_init(9600);
	while (1){
		GPIO_ResetBits(GPIOD,GPIO_Pin_2);
		printf("t:%d\n",t);	
		delay_ms(500);
		GPIO_SetBits(GPIOD,GPIO_Pin_2);
		delay_ms(500);
		t++;
		
	}
}


