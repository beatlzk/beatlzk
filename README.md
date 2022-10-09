- 今天是2022年十月九号
开始学习51单片机的部分基础实验，依据从b站江科大视频所学
本次使用的是STC89C52 用于制作点亮 闪烁LED 以及LED的流水化（可简易改变间隔时间）
第一：先了解单片机的结构以及各部件的用途
第二：点亮LED       
#include <REGX52.H>//定义单片机的一种头文件


void main()
{
P2=0xEE;//P2=xx 是指单片机上部件的位置 0x是c语言  EE是二进制转十六进制以及位置
		
}//主函数
第三：闪烁
#include <REGX52.H>
#include<INTRINS.H>//定义_nop_()
void Delay500ms()		//@11.0592MHz
{
	unsigned char i, j, k;

	_nop_();
	i = 4;
	j = 129;
	k = 119;
	do
	{
		do
		{
			while (--k);
		} while (--j);
	} while (--i);
}
//通过stc考录软件自带的软件延时所copy的代码
void main()
{
	
	while(1)
	{
	P2=0xFE;
	Delay500ms();	
	P2=0xFF;
	Delay500ms();	//由上方所copy的代码所定义并赋予意义，Delay延时
  }//    while循环           
}
第四流水灯（由一unsigned int xms定义）

#include <REGX52.H>

void Delay1ms(unsigned int xms)		//@11.0592MHz
{
	unsigned char i, j;
  while(xms)
	{
	i = 2;
	j = 199;
	do
	{
		while (--j);
	} while (--i);
		xms--;
	}
	//定义xms 使其为一个正整数
}
void main()
{
		P2=0xFE;//1111 1110
		Delay1ms(100);//括号内数字可更改
		P2=0xFD;//1111 1101
	  Delay1ms(100);
		P2=0xFB;//1111 1011
		Delay1ms(100);
		P2=0xF7;//1111 0111
		Delay1ms(100);
		P2=0xEE;//1110 1111
		Delay1ms(100);
		P2=0xDF;//1101 1111
		Delay1ms(100);
		P2=0xBE;//1011 1111
		Delay1ms(100);
		P2=0x7F;//0111 1111
		Delay1ms(100);
}//同理如第三点


<!---
beatlzk/beatlzk is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
