~~~assembly
;*******************************************
;Project  -DRV8—— 驱动芯片1628电磁炉参考程序
;普通按键通用四位数码管
;Chip     - highway 08 
;Crystal  - 8M  
;Programer- Ycq  
;Date     - 20130326  
;Checksum -      
;****************************
;****************************
; highway 001  define area
;****************************
;#INCLUDE "HT45R0Y.INC"
IAR0		EQU		[00H]   
R0			EQU		[00H]	;old style declaration, not recommended for use
MP0			EQU		[01H]
IAR1		EQU		[02H]
R1			EQU		[02H]	;old style declaration, not recommended for use
MP1			EQU		[03H]
ACC			EQU		[05H]
PCL			EQU		[06H]
TBLP		EQU		[07H]
TBLH		EQU		[08H]
STATUS		EQU		[0AH]

INTC0		EQU		[0BH]
TMR0		EQU		[0DH]
TMR0C		EQU		[0EH]
TMR1		EQU		[010H]
TMR1C		EQU		[011H]

PA			EQU		[012H]
PAC			EQU		[013H]
PB			EQU		[014H]
PBC			EQU		[015H]
PC			EQU		[016H]
PCC			EQU		[017H]

CTRL0		EQU		[01AH]
CMP0C		EQU		[01BH]
CMP1C		EQU		[01CH]
CMP2C		EQU		[01DH]
INTC1		EQU		[01EH]
PPGC		EQU		[020H]
PPGTA		EQU		[021H]

PPGTB		EQU		[022H]		;已取消
PPGTEX		EQU		[023H]		;已取消

ADRL		EQU		[024H]
ADRH		EQU		[025H]
ADCR		EQU		[026H]
ACSR		EQU		[027H]

CTRL1		EQU		[028H]
OPAC		EQU		[029H]
CTRL2		EQU		[02AH]

PWLT		EQU		[02BH]		;已取消

CTRL3		EQU		[02CH]
TMR2		EQU		[02DH]
TMR2C		EQU		[02EH]
CMPSC		EQU		[02FH]

;========特殊功能寄存器位标志定义区======
;///STATUS
C			EQU		[0AH].0
AC			EQU		[0AH].1
Z			EQU		[0AH].2
OV			EQU		[0AH].3
PDF			EQU		[0AH].4
TO			EQU		[0AH].5

;////INTC0
EMI			EQU		[0BH].0
EEI			EQU		[0BH].1
EC1I		EQU		[0BH].2
EC2I		EQU		[0BH].3
EIF			EQU		[0BH].4
C1F			EQU		[0BH].5
C2F			EQU		[0BH].6

;///TMR0C
T0PSC0		EQU		[0EH].0
T0PSC1		EQU		[0EH].1
T0PSC2		EQU		[0EH].2
T0E			EQU		[0EH].3
T0ON		EQU		[0EH].4
T0M0		EQU		[0EH].6
T0M1		EQU		[0EH].7

;///TMR1C
T1PSC0		EQU		[011H].0
T1PSC1		EQU		[011H].1
T1PSC2		EQU		[011H].2
T1E			EQU		[011H].3
T1ON		EQU		[011H].4
T1M0		EQU		[011H].6
T1M1		EQU		[011H].7

;///PA
PA0			EQU		[012H].0
PA1			EQU		[012H].1
PA2			EQU		[012H].2
PA3			EQU		[012H].3
PA4			EQU		[012H].4  
PA5			EQU		[012H].5
PA6			EQU		[012H].6
PA7			EQU		[012H].7

;///PAC
PAC0		EQU		[013H].0
PAC1		EQU		[013H].1
PAC2		EQU		[013H].2
PAC3		EQU		[013H].3
PAC4		EQU		[013H].4
PAC5		EQU		[013H].5
PAC6		EQU		[013H].6
PAC7		EQU		[013H].7

;///PB
PB0			EQU		[014H].0
PB1			EQU		[014H].1
PB2			EQU		[014H].2
PB3			EQU		[014H].3
PB4			EQU		[014H].4
PB5			EQU		[014H].5
PB6			EQU		[014H].6
PB7			EQU		[014H].7

;///PBC
PBC0		EQU		[015H].0
PBC1		EQU		[015H].1
PBC2		EQU		[015H].2
PBC3		EQU		[015H].3
PBC4		EQU		[015H].4
PBC5		EQU		[015H].5
PBC6		EQU		[015H].6
PBC7		EQU		[015H].7

;///PC
PC0			EQU		[016H].0
PC1			EQU		[016H].1
PC2			EQU		[016H].2
PC3			EQU		[016H].3

;///PCC
PCC0		EQU		[017H].0
PCC1		EQU		[017H].1
PCC2		EQU		[017H].2
PCC3		EQU		[017H].3

;///CTRL0
LVDC		EQU		[01AH].0		;已取消	
LVDO		EQU		[01AH].1
PSCS		EQU		[01AH].2		
OSTPC		EQU		[01AH].3
BZE			EQU		[01AH].4
BZCS		EQU		[01AH].5
TMR0ECS		EQU		[01AH].6
TMR1ECS		EQU		[01AH].7

;///CMP0C
C0COF0		EQU		[01BH].0
C0COF1		EQU		[01BH].1
C0COF2		EQU		[01BH].2
C0COF3		EQU		[01BH].3
C0COF4		EQU		[01BH].4
C0CRS		EQU		[01BH].5
C0COFM		EQU		[01BH].6
C0CMPOP		EQU		[01BH].7

;///CMP1C
C1COF0		EQU		[01CH].0
C1COF1		EQU		[01CH].1
C1COF2		EQU		[01CH].2
C1COF3		EQU		[01CH].3
C1COF4		EQU		[01CH].4
C1CRS		EQU		[01CH].5
C1COFM		EQU		[01CH].6
C1CMPOP		EQU		[01CH].7

;///CMP2C
C2COF0		EQU		[01DH].0
C2COF1		EQU		[01DH].1
C2COF2		EQU		[01DH].2
C2COF3		EQU		[01DH].3
C2COF4		EQU		[01DH].4
C2CRS		EQU		[01DH].5
C2COFM		EQU		[01DH].6
C2CMPOP		EQU		[01DH].7

;///INTC1
ET0I		EQU		[01EH].0
ET1I		EQU		[01EH].1
EADI		EQU		[01EH].2
T0F			EQU		[01EH].4
T1F			EQU		[01EH].5
ADF			EQU		[01EH].6

;///PPGC
C1RLEN		EQU		[020H].0		;已取消
PPGE0		EQU		[020H].2		;
PPGE1		EQU		[020H].3		;always 01
RLBF		EQU		[020H].4		;已取消
PSPEN		EQU		[020H].5
PRSEN		EQU		[020H].6
PST			EQU		[020H].7

;///PPGTA
PGTA0		EQU		[021H].0
PGTA1		EQU		[021H].1
PGTA2		EQU		[021H].2
PGTA3		EQU		[021H].3
PGTA4		EQU		[021H].4
PGTA5		EQU		[021H].5
PGTA6		EQU		[021H].6
PGTA7		EQU		[021H].7

;///PPGTB ;已取消
;PGTB0		EQU		[022H].0		;已取消	
;PGTB1		EQU		[022H].1		;已取消
;PGTB2		EQU		[022H].2		;已取消
;PGTB3		EQU		[022H].3		;已取消
;PGTB4		EQU		[022H].4		;已取消
;PGTB5		EQU		[022H].5		;已取消
;PGTB6		EQU		[022H].6		;已取消
;PGTB7		EQU		[022H].7		;已取消

;///PPGTEX ;已取消
;PGTA8		EQU		[023H].0		;已取消
;PGTB8		EQU		[023H].4		;已取消

;///ADRL
D0			EQU		[024H].4
D1			EQU		[024H].5
D2			EQU		[024H].6
D3			EQU		[024H].7

;///ADRH
D4			EQU		[025H].0
D5			EQU		[025H].1
D6			EQU		[025H].2
D7			EQU		[025H].3
D8			EQU		[025H].4
D9			EQU		[025H].5
D10			EQU		[025H].6
D11			EQU		[025H].7

;///ADCR
ACS0		EQU		[026H].0
ACS1		EQU		[026H].1
ACS2		EQU		[026H].2
PCR0		EQU		[026H].3
PCR1		EQU		[026H].4
PCR2		EQU		[026H].5
EOCB		EQU		[026H].6
START		EQU		[026H].7

;///ACSR
ADCS0		EQU		[027H].0
ADCS1		EQU		[027H].1

;///CTRL1
DBC0		EQU		[028H].0
DBC1		EQU		[028H].1
DBC2		EQU		[028H].2
DBC3		EQU		[028H].3
DBC4		EQU		[028H].4
DBC5		EQU		[028H].5
LLDF		EQU		[028H].6		;
LVDF		EQU		[028H].7		;
;INTS		EQU		[028H].6		;已取消	
;INTINV		EQU		[028H].7		;已取消

;///OPAC
OPAOF0		EQU		[029H].0
OPAOF1		EQU		[029H].1
OPAOF2		EQU		[029H].2
OPAOF3		EQU		[029H].3
;OPARS		EQU		[029H].4
OPAOFN		EQU		[029H].5
OPAOP		EQU		[029H].6
OPAEN		EQU		[029H].7


;///CTRL2
CVREF0		EQU		[02AH].0
CVREF1		EQU		[02AH].1
CVREF2		EQU		[02AH].2
CVREF3		EQU		[02AH].3
CVREF4		EQU		[02AH].4
CVREF5		EQU		[02AH].5
OP2AD0		EQU		[02AH].6
OPAPCTL		EQU		[02AH].7

;////CTRL3
PCKE		EQU		[02CH].0

;///TMR2C
T2PSC0		EQU		[02EH].0
T2PSC1		EQU		[02EH].1
T2PSC2		EQU		[02EH].2 
T2ON		EQU		[02EH].4
T2M0		EQU		[02EH].6
T2M1		EQU		[02EH].7

;////CMPSC
CMP0EN		EQU		[02FH].0
CMP1EN		EQU		[02FH].1
CMP2EN		EQU		[02FH].2
C0HYSON		EQU		[02FH].4
C1HYSON		EQU		[02FH].5
C2HYSON		EQU		[02FH].6

;第二点			：2016-12-3 15:21    13A升级版本，去掉该寄存器。
OPAC0		EQU			OPAC
TMR3		EQU			[32H]
TMR3C		EQU			[33H]
OPAC1		EQU			[38H]		;2016-4-15 18:19

T3M1		equ			TMR3C.7
T3M0		equ			TMR3C.6
TMR3ECS		equ			TMR3C.5
T3ON		equ			TMR3C.4
T3E			equ			TMR3C.3 
T3PSC2		equ			TMR3C.2 
T3PSC1		equ			TMR3C.1
T3PSC0		equ			TMR3C.0

T3RSEN		equ			OPAC1.7
OPAOFM		equ			OPAC1.6
OPARS		equ			OPAC1.5
;第二点结束		2016-4-20 8:49	

LASTPAGE	EQU		0F00H
;=======================================
;Circuit pin define area
;=======================================
;ppg  no define
;opo  no define
;///pa port
p_cur_op_	equ		pa.0	;op-
p_sur_		equ		pa.1
p_syn_s		equ		pa.2
p_syn_n		equ		pa.3

p_buz		equ		pa.4	;buz port
p_fan		equ		pa.4

;///pb port 
p_curad		equ		pb.0
p_igbtad	equ		pb.1
p_mainad	equ		pb.2	;check main
p_volad		equ		pb.3

;///operate display board
p_outdata	equ	    pa.5
p_uart_in	equ		pb.5
;******************************************* 
;///p3 ;no use
p_n0		equ		pc.0		;no use
p_n1		equ		pc.1
p_n2		equ		pc.2
p_n3		equ		pc.3
;=========new picture======
;///总的显示com数设置
dsp_bufnum	equ		14			;4*2
;//*******************************************************
;//实际功率选项（主板参数：R27=62K，500欧姆可调器在中间
;//谐振电容为0.27UF，线盘电感量为110U，线盘距炉面高度11~12mm 
;//不同的功率对应的目标电流，最大PWM宽度及反压保护值都不一样）
;//*******************************************************
;chk_maxpower equ    00010000b  ;(01=1250w,02=1350w,04=1450w,08=1550w,10=1650w)
;v250_1300w   equ    00000000b   ;(bit5=0时250V功率都为1300W，为1时保持不变）      
;//*********************************
;//constant  define area
;//*********************************
;//不同PWM限制宽度对应IGBT的导通时间
pwm1_max    equ     78h  ;17us
pwm2_max    equ     78h  ;17us
pwm3_max    equ     78h  ;17us
pwm4_max    equ     78h  ;17us
pwm5_max    equ     68h  ;19us
pwm6_max    equ     58h  ;21us 
pwm7_max    equ     48h  ;23us
pwm8_max    equ     38h  ;25us

;///所有火力档对应的最小PWM限制宽度约6us(48*0.125)
pwm_min		equ		0d0h 	;;最小PPG值（pwm)
pwm_on		equ		0c8h    ;脉冲启动宽度约7us(56*0.125)
pwm_off		equ		0

delay_check equ		30		;;30*60=1.8s 电流检无锅的延时检测时间

main_max	equ		0f4h	;主温度传感器(发热盘传感器)报短路A.d值
main_min	equ		02h		;主温度传感器(发热盘传感器)报开路A.d值
main_85		equ		40h
main_140	equ		095h	;烧水功能侦测干烧或者高温的起始温度判断点；
main_210    equ     0cah	;烧水功能侦测干烧或者高温的最高温度保护点；
main_270	equ		0e8h	;烧油功能侦测高温的最高温度保护点；

;/////主温度不变的持续时间程序用到的常量定义
dtemp_ganshao	equ	5		;5*256=1280ms 
dtemp_7t		equ	7		;干烧计数的次数

shui_dstart		equ	1bh*2	;温度不变计数最小值
shui_15m		equ	20		;烧水15分钟才开始侦测
shui_25m		equ 30		;烧水25分钟最长时间关机
shui_maxt		equ	0f0h	;温度不变的时间为60秒
shui_pclv28t	equ	28h		;烧水温度不变，低电压的补偿值
dtemp_shui7t	equ	7		;烧水温度不变的次数
dtemp_shui10t	equ	10		;烧水温度不变的次数
dtemp_150s		equ	150		;若拉锅，则延时150秒进行判断
;///
cur_max		equ		0c0h	;最大设定目标电流值
;///igbt temperature define area
igbt_max	equ		0f0h	;igbt温度传感器(散热器传感器)报短路A.d值
igbt_min	equ		02h		;igbt温度传感器(散热器传感器)报短路A.d值
igbt_65		equ		4fh		;igbt高温保护恢复加热温度值65度A.D值
igbt_80		equ		6ch		;igbt 80度A.D值
igbt_90		equ		7fh		;igbt 90度A.D值
igbt_110	equ		90h 	;igbt 110度A.D值
                          
;// voltage constant define area
                          
;// voltage constant define area
vol_min		equ		33h  	;低压保护值班85V对应的A.D值
vol_80		equ		36h  	;90V对应的A.D值
vol_180		equ		6Dh		;180V对应的A.D值  
vol_205		equ		79h  	;210V对应的A.D值 
vol_210		equ		80h  	;210V对应的A.D值 
vol_220		equ		86h  	;220V对应的A.D值 
vol_240		equ		93h	 	;240V对应的A.D值
vol_250     equ     9ah		;250V对应的A.D值 
vol_max		equ		0a9h 	;高压保护值275v对应的A.D值

vol_min1    equ     33h+5    ;低压保护值恢复加热对应的A.D值
vol_max1    equ     0a9h-2   ;85h-2h
vol_disguo  equ     0aBh     ;8ah  

vol220_const	equ		220	 ;220 常量的定义

;///各故障代码定义	(通讯的时候不能为零，所以代码都加了1)
er_nopan    equ     0   ;无锅
er_mainpcb  equ     0   ;线路故障
er_volmin   equ     1   ;电压过低（小于85V） 
er_volmax   equ     2   ;电压过高（大于275V）
er_mainmin  equ     3   ;炉面传感器开路（延时1分钟检测）
er_mainmax  equ     3   ;炉面传感器短路 
er_igbtmin  equ     4   ;散热片传感器开路（延时1分钟检测）
er_igbtmax  equ     4   ;散热片传感器短路
er_mainwarm equ     5   ;炉面高温（大于280度）
er_igbtwarm equ     6   ;散热片传感器过热（大于105度）
er_mainerr	equ		7  	;传感器失效保护  
er_comm		equ		9		;通迅故障      
;/////////////// 
p_200       equ     1
p_400       equ     2
p_800       equ     3
p_1000		equ		4	 
p_1300		equ		5	 	
p_1600		equ		6		
p_1800		equ		7
p_2000      equ     8	

;///总的火力档位
huoli_number  equ   8

;///间断加热占空比(周期为10s)
tiao_200w   equ     6   ;加热3s/停止7s
tiao_400w   equ     10  ;加热5s/停止5s
tiao_800w   equ     16  ;加热8s/停止2s

;///烧油功能各档炉面实际温度保护点
main_80c    equ     30h 
main_100c   equ     5bh
main_120c   equ     72h
main_160c   equ     94h
main_180c   equ     0A0h      
main_200c   equ     0b5h 
main_240c   equ     0c7h
main_270c   equ     0d0h
main_275c   equ     0d4h		;全灯六档火力用，其它模式不用

;///各档温度显示
dsp_temp1   equ     08h
dsp_temp2   equ     10h
dsp_temp3   equ     12h
dsp_temp4   equ     16h
dsp_temp5   equ     18h
dsp_temp6   equ     20h   
dsp_temp7   equ     24h
dsp_temp8   equ     27h

;///各档功率显示
dsp_power1  equ     02h 
dsp_power2  equ     06h
dsp_power3  equ     08h
dsp_power4  equ     10h
dsp_power5  equ     13h       
dsp_power6  equ     16h   
dsp_power7  equ     18h
dsp_power8  equ     20h

;//menu mode define area
m_huoguo    equ    1
m_chaocai   equ    2
m_baochao	equ    3
m_warm      equ    4
m_wenhuo	equ	   5	;wenhuo= 3 档间断加热，武火1800W加热，不能调节火力，同
						;同火锅工作过程一样，
m_soupzhou	equ    6    ;m_soup
m_zheng		equ    7
m_milk		equ    8
m_shaoshui	equ    9 
m_zhou      equ    10

m_zhufan	equ    11
m_jianchao  equ    12
m_shaokao	equ    13		;代替煎炒
m_wuhuo     equ    14

;///各功能默认火力档定3义 
h_huoguo    equ    5
h_chaocai   equ    7
h_baochao   equ    8
h_warm      equ    1
h_wenhuo	equ	   3	;wenhuo
h_soupzhou  equ    6
h_zheng     equ    6
h_milk      equ    3

h_shaoshui  equ    8
h_zhou      equ    6
h_zhufan    equ    4
h_jianchao  equ    6
h_shaokao   equ    5
h_wuhuo     equ    8

;///各功能默认工作时间定义
t_huoguo    equ    120
t_chaocai   equ    60
t_baochao   equ    60
t_warm      equ    60
t_wenhuo	equ	   120		;wenhuo
t_soupzhou  equ    120
t_zheng     equ    90
t_milk      equ    20

t_shaoshui  equ    35
t_zhou      equ    120
t_zhufan    equ    45
t_jianchao  equ    60
t_shaokao   equ    60
t_wuhuo     equ    120


;// ad convert channel
ch_cur  	equ		01100000B 	;//ad0 pb.0
ch_vol		equ		01100110B	;//ad6 pa.7
ch_main		equ		01100101B	;//ad5 pa.6
ch_igbt		equ		01100001B	;//ad1 pb.1

;=================================
;================================
;///macro define area 宏定义
;---------------------------
bit0		equ		1
bit1		equ		2
bit2		equ		4
bit3		equ		8
bit4		equ		16
bit5		equ		32
bit6		equ		64
bit7		equ		128

;================================
;For display symbol define
;================================
seg_a			equ		bit1
seg_b			equ		bit7
seg_c			equ		bit5
seg_d			equ		bit3
seg_e			equ		bit2
seg_f			equ		bit0
seg_g			equ		bit6
seg_h			equ		bit4

;//define display symbol  
sym_0		equ		(seg_a|seg_b|seg_c|seg_d|seg_e|seg_f)
sym_1		equ		(seg_b|seg_c)
sym_2		equ		(seg_a|seg_b|seg_d|seg_e|seg_g)
sym_3		equ		(seg_a|seg_b|seg_c|seg_d|seg_g)
sym_4		equ		(seg_b|seg_c|seg_f|seg_g)
sym_5		equ		(seg_a|seg_c|seg_d|seg_f|seg_g)
sym_6		equ		(seg_a|seg_c|seg_d|seg_e|seg_f|seg_g)
sym_7		equ		(seg_a|seg_b|seg_c)
sym_8		equ		(seg_a|seg_b|seg_c|seg_d|seg_e|seg_f|seg_g)
sym_9		equ		(seg_a|seg_b|seg_c|seg_d|seg_f|seg_g)
sym_a		equ		(seg_a|seg_b|seg_c|seg_e|seg_f|seg_g)
sym_b		equ		(seg_c|seg_d|seg_e|seg_f|seg_g)
sym_c		equ		(seg_a|seg_d|seg_e|seg_f)
sym_d		equ		(seg_b|seg_c|seg_d|seg_e|seg_g)
sym_e		equ		(seg_a|seg_d|seg_e|seg_f|seg_g)
sym_f		equ		(seg_a|seg_e|seg_f|seg_g)

sym_off		equ		 00h
sym_heng	equ		 seg_g
sym_char	equ		(seg_a|seg_b|seg_f|seg_g)
sym_p		equ		(seg_a|seg_b|seg_e|seg_f|seg_g)
sym_u		equ		(seg_b|seg_c|seg_d|seg_e|seg_f)
sym_n		equ		(seg_a|seg_b|seg_c|seg_e|seg_f)
;======================================
data .section 'data' 

dspbuff		equ		060h
;///display data define area    
vfd_byte0	db		?			
vfd_byte1	db	?				

;///C1
vfd_byte2	db		?				
vfd_byte3	db		?		


;///C2
vfd_byte4	db		?			
vfd_byte5	db		?			


;///C3
vfd_byte6	db		?		 	
vfd_byte7	db		?			

;///C4  
vfd_byte8	db		?			
vfd_byte9	db		?			

;///C5  
vfd_byte10	db		?			
vfd_byte11	db		?			

;////c6 
vfd_byte12	db		?			
vfd_byte13	db		?		

dspbuf0		equ		vfd_byte6
sdot0       equ     dspbuf0.4
dspbuf1		equ		vfd_byte8
sdot1       equ     dspbuf1.4
dspbuf2     equ		vfd_byte10
sdot2       equ     dspbuf2.4 
dspbuf3     equ		vfd_byte12
sdot3       equ     dspbuf3.4

;;触摸按键专用，增对对方寄存器而设定的
ledbuf0		equ		vfd_byte7
stcoulo		equ     ledbuf0.0;COM5 SEG7 L1  
stpower		equ     ledbuf0.1;COM5 SEG1 L2  
stmilk		equ     ledbuf0.2;COM5 SEG2 L3  
sthuoguo	equ     ledbuf0.3;COM5 SEG3 L4  
stbaochao	equ     ledbuf0.4;COM5 SEG4 L5  
stshaokao	equ     ledbuf0.5;COM5 SEG8 L6  
stlock		equ		ledbuf0.6;COM5 SEG5 L7  
stshijian	equ     ledbuf0.7;COM5 SEG6 L8	
                                            
ledbuf1		equ		vfd_byte9               
sttemp		equ		ledbuf1.0;COM6 SEG7 L9  
sttimer		equ     ledbuf1.1;COM6 SEG1 L10 
stsoup	    equ     ledbuf1.2;COM6 SEG2 L11 
stshaoshui	equ     ledbuf1.3;COM6 SEG3 L12 
stzheng	    equ     ledbuf1.4;COM6 SEG4 L13 
stonoff		equ     ledbuf1.5;COM6 SEG8 L14 
stzhufan	equ		ledbuf1.6;COM6 SEG5 L15 
stjianzha	equ		ledbuf1.7;COM6 SEG6 L16 

ledbuf2		equ		vfd_byte11 
st1			equ		ledbuf2.0;COM7 SEG7 L17
st2			equ		ledbuf2.1;COM7 SEG1 L18
st3			equ		ledbuf2.2;COM7 SEG2 L19
st4			equ		ledbuf2.3;COM7 SEG3 L20
st5			equ		ledbuf2.4;COM7 SEG4 L21
st6			equ		ledbuf2.5;COM7 SEG8 L22
st7			equ		ledbuf2.6;COM7 SEG5 L23
st8			equ		ledbuf2.7;COM7 SEG6 L24

;///display define end    
dispno	    db	?	 
dspparamjs  db	? 
bakdat0		db	?

key1addr	 equ	71h
;;*************************************************
;;一键通按键定义区域  keydat1
;****************************************************************
keydat1		db	?			;ic_cs
keydat2     db	?		  ;ic_dat
keydat3		db	?
keydat4		db	?
keydat5		db	?

;*******************************************************
;;触摸板按键的定义区域
keydat6		equ		keydat1
k_tmenu		equ		keydat6.0;SW8
k_tlock		equ		keydat6.1;SW7
k_tstart	equ		keydat6.2;SW6
k_tmenu2	equ		keydat6.3;SW5
k_tadd		equ		keydat6.4;SW4
k_ttimer	equ		keydat6.5;SW3
k_tcoulo	equ		keydat6.6;SW2
k_tsub		equ		keydat6.7;SW1

;*******************************************************
keyontime	db	?
heatpower   db  ?		;功率选择及250V是否只有一档火力选择寄存器；
bheat125bz  equ     heatpower.0
bheat135bz  equ     heatpower.1
bheat145bz  equ     heatpower.2 
bheat155bz  equ     heatpower.3
bheat165bz  equ     heatpower.4
b250volbz   equ     heatpower.5
b205volbz   equ     heatpower.6
	
;*******************************************
;注意，这样的定义顺序不要随意改动，在temp6后面
;放keydat1定义位置，由于最后读的一组按键存
;在keydat1 里面,这样做的目的主要为省RAM;
;1628是这样做，针对6208则可以不这样做
;*******************************************
temp0		db	?		;被除法的高位/商
tmp0_b0		equ	temp0.0	
tmp0_b1		equ	temp0.1	
tmp0_b2		equ	temp0.2	
tmp0_b3		equ	temp0.3	
tmp0_b4		equ	temp0.4	
tmp0_b5		equ	temp0.5	
tmp0_b6		equ	temp0.6	
tmp0_b7		equ	temp0.7	

temp1		db	?		;被除法的低位/商	
temp2		db	?		;除数的低位

;===暂存按键值，然后转换成按键存值////
ktmp3addr	equ	7bh		
temp3		db	?		;余数
temp4		db	?
temp5		db	?
temp6		db	?

;无符号乘除法变量
data0		equ	temp0  
data1		equ	temp1
data4		equ	temp2
to0			equ	temp3
to1			equ	temp4
count0		equ	temp5
com			equ	temp6			;除法的余数                
;///
pwmdly1sjs	db	?	;在HEAT程序中延时处理电流检测无锅计数器
pwmtiaojs	db	?	;加减PWM时调节速度计数器
jianguojs	db	?	;脉冲检锅的计数步骤

backup_acc		db	?	;中断保护暂存寄存器acc
backup_status	db	?	;中断保护暂存寄存器status
;// save current  a.d value
main_ds     equ   084h
temp_main	db	?	;主温度A.D值
tmainjs		db	?	;主温度不变(+/-1变化为不变)250ms计一次累计计数次数	
temp_igbt	db	?	;散热器A.D值
vol_in		db	?	;电压A.D值
current		db	?	;电流A.D值
adjs		db	?	
valuecur	db	?	 ;//to get actural compare current
dpanjs      db	?
	
;=====note sym==1 =======
cura		db	?			 ;电流四次递滚值寄存器A
curb		db	?			 ;电流四次递滚值寄存器B
curc		db	?			 ;电流四次递滚值寄存器C	
curd		db	?			 ;电流四次递滚值寄存器D

cur0		db	?			 ;电流采集值累加和最低位寄存器
curl		db	?			 ;电流采集累加和低位寄存器
curh		db	?			 ;电流采集累加和高位寄存器

voll		db	?			 ;电压采集累加和低位寄存器	
volh		db	?			 ;电压采集累加和高位寄存器

mainl		db	?			 ;主温度采集累加和低位寄存器
mainh		db	?		     ;主温度采集累加和高位寄存器

igbtl		db	?			 ;主温度采集累加和低位寄存器
igbt_h		db	?			 ;主温度采集累加和高位寄存器
	
init_cur	db	?			 ;电流全亮以后,初始电流值
                             ;以后采集出来的值减去此个值
                             ;以克服放大器的误差; 
;//unsigned char tobject;
errorcode	db	?	 ;// save error code

;//system time fag
flh_500ms	db	?	;;500ms闪烁计数器
;flh_second	db	?	;
;bsnd0	 	equ	flh_second.0 ;(flh_second&0x01)

beep_count0	db	?	;蜂鸣器鸣叫计数器

tiao_zong	db	?	;;间断加热周期寄存器
tiao_on		db	?	;;间断加热加热时间寄存器
tiaojs		db	?	;;间断加热计数累加器

highvoljs	db	?	;产生高压保护中断后则延时减小PPGA 
					;的计数器 25*60=1.5s disable dec ppgta
lowvoldetjs	db	?	;系统低电压连续5次则报浪涌
langyongjs	db	?	;;浪涌保护2秒后恢复加热值
buznopanjs	db	?	;;无锅加热2秒蜂鸣叫一声

debug_stage	db	?	;;调试显示代码步骤值	
dya_js		db	?	;;低压保护持续1S计数器
gya_js		db	?	;;高压保护持续1S计数器
count20msjs	db	?	;20MS计数累加器
;*******************************************************
;touch part  通讯模块寄存器
;******************************	*************************
senddelay   db     ? 
sendjs      db     ? 
send0js     db     ?
send1js     db     ?		

run_ram0	db	?
run_ram1	db	?
run_ram2	db	? 
run_ram3	db	?
run_ram4	db	?
run_ram5	db	?
run_ram6	db	?
run_ram7	db	?

;errorjs	 	   db		?		;侦测通迅故障的计数器 
phighjs  	   		db 	?		    ;高电平计数器
oldphighjs			db	?
plowjs       		db 	?			;低电平计数器
oldplowjs      		db 	?
bbitjs				db	?

uartrevbytel	 	db		?			;接收数据暂存寄数器
uartrevbyteh	 	db		?

;;触摸按键和普通按键的选择  
key_flag1 	db	?
b_touch		equ		key_flag1.0
b_menumode	equ		key_flag1.1
brecok		equ     key_flag1.2	;已经接收数据位的状态
p_status	equ     key_flag1.3	;映射接收脚的电平状态的反状态
b_secok		equ		key_flag1.4

;//_37
;//*********************************
;//bit variable define area
;//*********************************
time_flag	db	?			;各种时序变量	
bpan500ms   equ	time_flag.0	;20MS时间到标志
f_2ms	    equ	time_flag.1	;2MS时间到标志
f_2s	    equ time_flag.2	;2S时间到标志
bheat40ms   equ	time_flag.3	;系统加热40MS时间到标志
badt300ms	equ	time_flag.4	;按加/减键持续不放300MS时间到标志
bdin1min	equ	time_flag.5	;定时计数模式500ms时间到标志
byu1min     equ time_flag.6	;预约计数模式500ms时间到标志
bsnd0	 	equ	time_flag.7 ;500MS闪动标志,bit7注意,不要随意更改,由于后面的程序要用到

;//normal flag1
nor_flag1 	db	?			;系统加热标志	
berror   	equ	nor_flag1.0	;系统有错误标志
benscan     equ nor_flag1.1	;允许扫描按键标志
bpwmwen     equ	nor_flag1.2	;PPG维持不变标志
bheate		equ	nor_flag1.3	;系统允许加热标志
bheatno     equ	nor_flag1.4	;系统不能加热标志
bheatyes    equ	nor_flag1.5	;间断加热判断允许加热的标志
bendspdebug	equ	nor_flag1.6	;上电按住减小键,允许按定时键调调试代码标志
bendspall   equ	nor_flag1.7	;系统在上电全亮标示

;//normal flag2
nor_flag2	db	?
bguoon		 equ	nor_flag2.0	;系统有锅标志
bonoff       equ	nor_flag2.1	;系统开机标志
bsurge		 equ	nor_flag2.2	;系统浪涌保护标志
bkeyrls      equ	nor_flag2.3	;按键已处理标志
bwarmh     	 equ	nor_flag2.4	;IGBT高温保护标志
control_igbt equ    nor_flag2.5	;IGBT在开通状态标志
bdown3m		 equ	nor_flag2.6
bdown5m		 equ	nor_flag2.7

lockjs		db	?

nor_flag3	db	?
b_ledmode	equ		nor_flag3.0
b_fivepower	equ		nor_flag3.1
b_sixpower	equ		nor_flag3.2
bbusysts	equ		nor_flag3.3
bnochange	equ	    nor_flag3.4
;;无烟锅检测标志定义区域
nor_flag5	db	?
byanguo		equ		nor_flag5.0

yanguo_ds	equ		0c2h
dyanguojs1	db	?		;进中断次数累加器
dyanguojs2	db	?		;
dtime5sjs	db	?		;5S时间处理计数器	
dtime10sjs	db	?


;/*******************************/
;// standby clear ram variable 
;/******************************/
mode_clear		equ		0c6h		;#mode	;get mode address
yhour      	 	db	?			;预约状态小时寄存器
yminute			db	?			;预约状态分钟寄存器
tminute			db	?			;定时分钟寄存器

mode			db	?			;系统工作模式寄存器
modejs			db	?				
confirm5sjs		db	?			;确认定时/预约时间5秒计数器

;fan_counter		db	?			;关机后风扇延时1分钟停转计数器
nopanoffjsh		db	?			;无锅1分钟计数器
adt300msjs		db	?			;按加/减键持续不放300MS计数器

dsphuoli		db	?			;当前的显示火力寄存器
ledhuoli		db	?			;全指示灯用火力

heathuoli		db	?			;当前的加热火力寄存器
poweron1mjs		db	?			;系统在连续工作1分钟计数器,主要为侦测温度

;///coulom param
cou36sjsl		db	1			;电量IGBT连续加热36秒计数器
coulomjsl		db	1			;电量累加和低位计数器
coulomjsh		db	1			;电量累加和高位计数器 
seep_state		db	1			;查看电压/电量的识别寄存器
seecoulo15sjs	db	1			;查看电压/电量15秒返回原来状态计数器

com_flag1		db	?
bfan	    	equ		com_flag1.0	;系统关机后风扇转标志
bfun500ms   	equ		com_flag1.1	;系统500MS时间到寄存器
bendspguo   	equ    	com_flag1.2	;允许显示无锅标志
benfan      	equ    	com_flag1.3	;映射当前风扇状态;
bpo1m			equ		com_flag1.4	;系统当前连续加热1分钟到标志
block			equ		com_flag1.5
btemplock		equ		com_flag1.6

down15mjs		db	?

;// new mode must clear ram unit
yclear			equ		0d9h
y1mjsl			db		?	;;预约时间运行1分钟计数低位计数器
y1mjsh			db		?	;预约时间运行1分钟计数高位计数器

t1mjsl			db		?	;定时时间运行1分钟计数低位计数器
t1mjsh			db		?	;定时时间运行1分钟计数高位计数器

t_500ms			db		?	;系统500MS计数器
secjs			db		?	;系统工作秒计数器
minjs			db		?	;系统工作分钟计数器

menujs			db		?	;功能运行暂存寄存器
minutet			db		?	;设定定时时间分钟暂存寄存器

oldhuoli		db		?	;工作模式更改加热火力的寄存器
delay30sjs		db		?	;系统发生拖锅,抖锅延时75秒判断干烧
cur500ms		db		?	;系统工作时,存500MS前的工作电流,
comm_state		db		?	;;菜单运行各阶段寄存器		//run zhufan program state

dtem_ds         equ   0e6h
dtemp1			db		?	;当前主温度不变的250MS计一次的累计计数次数
							;主要用来作烧水,煮饭,干烧及其它菜单用
							;侦测用							
dganshaojs  	db		?	;系统判断发生干烧计数器
dshaoshuijs 	db		?	;系统烧水判断水开计数器

menu_flag		db		?	;
bshuiup      	equ		menu_flag.0	;当前主温度上升标志
bbaowen		 	equ		menu_flag.1	;当前菜单保温标志
bshuikai     	equ		menu_flag.2	;水开标志
bigbtwarm       equ     menu_flag.3	;IGBT加热状态标志
bganshao     	equ    	menu_flag.4	;系统干烧标志
bautomenu    	equ    	menu_flag.5	;当前功能是否为不可调节火力功能
btempsts     	equ    	menu_flag.6	;当前功能为烧油功能
bdiscursurge	equ		menu_flag.7	;不允许侦测电流突变浪涌标志
									;调火力时要延时6秒侦测电流浪涌									
flh_flag		db	?				;定时,预约设置标志
bflash	   		equ		flh_flag.0	;当前功能为设置定时/预约
bflhdin	    	equ		flh_flag.1	;当前功能为设置定时标志
bflhyu      	equ		flh_flag.2	;当前功能为设置预约标志
bfastadd    	equ		flh_flag.3	;当前可以快速加标志
bfastsub		equ		flh_flag.4	;当前可以快速减标志
bsettimests 	equ		flh_flag.5	;当前状态已经按下了定时设置键标志
byuyuests   	equ    	flh_flag.6	;当前状态已经按下了预约设置键标志

sec3sjs			db	?
com_flag2		db	?
b2m	    	    equ		com_flag2.0 	
b1min			equ		com_flag2.1
tmax			db	    ?		
tmin			db	    ?		
nochangejs		db	    ?
r_nopan			db		?			;2015-8-19 9:20:42   用于软启动
pwm_zhiqian		db		?
;**************************************
;micro define area 
;**************************************
sav_data		macro
				mov		backup_acc,a
				mov		a,status
				mov		backup_status,a
endm

;				
res_data		macro
				mov		a,backup_status
				mov		status,a
				mov		a,backup_acc
endm

;///
bcpl			macro	s1,s2
				mov		a,s2
				xorm	a,s1
endm

;/////////////// initial  main program normal service//////////////
;=========================================================================================
;=========================================================================================
;=========================================================================================
;////////// application program /////////////////
democode    .section at 000h       'code'

```assembly
        org     0000h
        jmp     reset

        org     0004h
        jmp     ext_int0

		org     0008h
        jmp     ext_cmp1

        org     000Ch
        jmp     ext_cmp2

        org     0010h
        jmp     timer0

		org     0014h
        jmp     timer1

        org     0018h
        reti
```

;////////////////////////////////////////////////////////
;>>>>>>>>>>>>>> reset program <<<<<<<<<<<<<<<<<<<<<<<<<<<
;////////////////////////////////////////////////////////
reset:		
       ;========上电防反插烧机===========
            nop
            nop
            nop
            clr     adcr
            clr		pa
			mov		a,00000110b
			mov		pac,a
			nop
			nop
			nop
					

```assembly
        clr		keyontime
```

res_dly:	

​			nop
​			nop
​			nop
​			nop            	
​            siz		keyontime
​            jmp		res_dly
​            clr     dspparamjs
​            nop
​            nop
​            nop
​            
loop_chkic: sz      p_sur_         ;检测同步脚电平
​		    jmp     reset_next
​		    sz      p_syn_s        ;检测同步脚电平
​		    jmp     reset_next
​		    

		    clr     keyontime
	        inc     dspparamjs
	        mov     a,dspparamjs
	        sub     a,5
	        snz     c
	        jmp     loop_chkic
	        jmp     loop_start

reset_next: clr     dspparamjs
		    inc     keyontime
		    mov     a,keyontime
		    sub     a,5
		    sz      c
loop_main:  jmp     loop_main      ;IC反插程序停在此处
		    jmp     loop_chkic

;////    
loop_start: mov		a,080h-20h
			call	clr_ram				;include init lcd 

	;///note:1=>input,0=>output

```assembly
wdt_out:	mov		a,11001111b
			mov		pac,a
			mov		a,00000000b
			mov		pa,a
			nop 
			nop
			nop			
			mov		a,10000011b
			mov		pbc,a
			mov		a,01100000b     
			mov		pb,a
			nop
			nop
```




			mov		a,00000000b
			mov		pcc,a
			clr		pc		
		    nop
		    nop
		    nop
	
			set 	cmp0en
			set 	cmp1en 
			set 	cmp2en
			
	;///system register define 
			nop
			nop
			mov		a,00000001b
			mov		acsr,a
						
			;mov	a,00001001b		;note5
			mov		a,00001000b		;ht45r0yb修改处
			nop
			mov		ctrl0,a


​			

			;mov	a,01011110b 
			;mov		a,00011010b		;3.25+0.5=3.75 ;ht45r0yb修改处
			mov		a,00011110b		;4us 
			nop
			nop  
			mov		ctrl1,a  
			 
		;ctrl1=>0.76vdd  ctrl2=0.8vdd	 
			mov		a,01100100b	
			nop
			nop
			nop
			mov		ctrl2,a		 
			
			mov		a,00000000b		;test pa5
			mov		ctrl3,a	
						
			nop 
			nop
			nop

;////////////clear ram//////////////////
	;>>>detect have grill function <<<
			mov		a,256-125-9		;时间补偿 timer=2MS/8m
			mov		tmr0,a
			mov		a,10000110b		;64/4=16US 16*125=2MS
			mov		tmr0c,a 
						

			mov		a,255-128  ;00		;timer=250us;设定进入中断时间为100US
			mov		tmr1,a
			mov		a,10000010b	;130
			mov		tmr1c,a 
			 
			mov		a,256-52 	;timer=52*0.25=13us  (1/(fsys/2)_=0.25
			mov		tmr2,a
			mov		a,00H		;
			mov		tmr2c,a
			 
			nop
			nop
			nop
			nop 
			nop
			nop	 
		;///initial ppg program///	ppgtb is no use
			mov		a,pwm_on 		;10us
			mov		ppgta,a
			
		;====取消一些寄存器的设置=====	
			;mov	a,040h		;24us if high voltage protect
			;mov	ppgtb,a
			;mov	a,11h		;130
			;mov	ppgtex,a
			;mov	a,88h   	;136	;总周期为30US；8m osc (256-x)*0.125=30us
			;mov	pwlt,a		;16->104
			mov		a,00000000b
			mov		ppgc,a
			nop
			nop
			nop
			
		;///system variable define 	
			mov		a,128
			mov		adjs,a
			NOP
			NOP
			NOP
			
			;////the calibation comparator and amplifier////	
			;////the calibation comparator and amplifier////	
			call	calibration	
			nop
			nop
			nop
			
			mov		a,vol_220
			mov		vol_in,a
			mov		a,20h
			mov		current,a
			
			set		bendspall		;为了校准OPA，需等待2S
			call    dd_all	
	
			call	beep_1
			;mov     a,chk_maxpower
			;or      a,v250_1300w			
			;orm     a,heatpower
			
			mov		a,00000001b					;enable timer product interrupt
			mov		intc1,a
			mov		a,00000001b
			mov		intc0,a
			set		T0ON
			set		T2ON	
			nop
			set     t1on 
			set     et1i  		  									 
			nop
	        set		bkeyrls	 					;防止上电按键误动作
	        nop 
	        nop	

;==========================================
; Main loop service
;==========================================			
MAIN:		nop
			nop 
			clr     wdt
			clr		wdt1
			nop
			nop 
			call    uart_debounce
	        nop
	        nop	 
		;=== 2ms service ===	 					
			snz		f_2ms
			jmp		main
			clr		f_2ms
			nop
			nop		
			nop
			nop
			call	dsp_digit 
			nop
			nop
			call	ad_prc				
			nop		
			nop
			call	detect_power_down	
			nop
			nop
			call	key_prog
			nop 
			nop			
			inc		count20msjs
			mov		a,count20msjs
			sub		a,10				
			snz		c
			jmp		main 
			clr		count20msjs
			nop
			nop
			call	f20ms_service
			nop
			nop 
;			call    jianguo
			nop 
			nop
			nop
;			call	heat		       
;			nop 
;			nop 
;			call	error                   
			nop    
			nop  
			call	beep_sound           
			nop 
			nop  			 
			nop
			nop
			call	timing    
			nop
			nop			
			call	highvol_surge		;高压保护更新及浪涌电压更新
			nop
			nop			
			call	pro_dingshi
			nop
			nop  
			;call	check_guo
		 

		;///500ms service////			snz		bfun500ms		jmp		main		clr		bfun500ms   		nop		nop		call	fan_pro 		nop 		nop		call	tiaogong		nop		nop		call	function		nop		nop		jmp		main		


​													
;;****************************************************************
;calibration: 2015-8-19 8:42:53   比较器需要正反校正
;;****************************************************************
calibration:		;修改第三点										;2016-4-20 8:49  所有都采用正反校正模式
​		set 	cmp0en  ;打开比较器0
​		clr		C0HYSON ;比较器不延时
​	    mov 	a,40h
​	    mov 	cmp0c,a ;设置比较电压
​        clr 	temp1 
​        mov		a,1fh
​        mov		temp3,a	
​	    CALL	DLY_100US
​	    sz 		c0cmpop ;比较器0输出
​	    jmp 	ac0_low
ac0_high: 
​		inc 	cmp0c
​		inc		temp1 
​		CALL	DLY_100US
​	    sz  	c0cmpop
​	    jmp 	ac0_ok	    
​	    dec		temp3
​		sz		temp3
​		jmp		ac0_high	    
​	    jmp 	ac0_ok
ac0_low:	
​		inc 	cmp0c 
​		inc		temp1
​		CALL	DLY_100US 
​	    snz 	c0cmpop
​	    jmp 	ac0_ok	    
​	    dec		temp3


		sz		temp3	jmp		ac0_low	    	

ac0_ok:											;;;cmp0---1f--00h
		set 	cmp0en  		;打开比较器0
		clr		C0HYSON 		;比较器不延时
	    mov 	a,5fh
	    mov 	cmp0c,a 		;设置比较电压
	    mov		a,1fh
	    mov		temp3,a	
	    mov 	temp2,a	
	    CALL	DLY_100US
	    sz 		c0cmpop 		;比较器0输出
	    jmp 	ac02_low 
ac02_high:
		dec 	cmp0c
		dec		temp2
		CALL	DLY_100US
	    sz  	c0cmpop
	    jmp 	ac02_ok 	    
	    dec		temp3
	   	sz		temp3
		jmp		ac02_high	    
	    jmp 	ac02_ok
ac02_low:	
		dec 	cmp0c
		dec		temp2
		CALL	DLY_100US
	    snz 	c0cmpop
	    jmp 	ac02_ok
 		dec		temp3 
	    sz		temp3
		jmp		ac02_low	    	
ac02_ok:	
		nop
		call	read_average
		mov		cmp0c,a
;;****************************************************************
;///comparator1 00-1f	 
;;****************************************************************
		set 	cmp1en
		clr		C1HYSON
	    mov 	a,60h
	    mov 	cmp1c,a
	    clr 	temp1 
        mov		a,1fh
        mov		temp3,a
	    CALL	DLY_100US
	    sz 		c1cmpop
	    jmp 	ac1_low

ac1_high:
		inc 	cmp1c
		inc		temp1
		CALL	DLY_100US
	    sz  	c1cmpop
	    jmp 	ac1_ok	    
	    dec		temp3  
		sz		temp3
		jmp		ac1_high	    
	    jmp 	ac1_ok


ac1_low: 
		inc 	cmp1c
		inc		temp1
		CALL	DLY_100US
	    snz 	c1cmpop
	    jmp 	ac1_ok	     
	    dec		temp3  
		sz		temp3
		jmp		ac1_low		
ac1_ok:			
;;;;;********1f--00***************			
		set 	cmp1en
		clr		C1HYSON
	    mov 	a,7fh
	    mov 	cmp1c,a
	    mov		a,1fh
	    mov		temp3,a
	    mov		temp2,a 
	    CALL	DLY_100US
	    sz 		c1cmpop 
	    jmp 	ac12_low
ac12_high: 
		dec 	cmp1c
		dec		temp2
		CALL	DLY_100US
	    sz  	c1cmpop
	    jmp 	ac12_ok
	    

	    dec		temp3
	   	sz		temp3	 
		jmp		ac12_high	    
	    jmp 	ac12_ok

ac12_low: 
		dec 	cmp1c
		dec		temp2
		CALL	DLY_100US
	    snz 	c1cmpop 
	    jmp 	ac12_ok	    
	    dec		temp3
	    sz		temp3
		jmp		ac12_low	
	
ac12_ok:	
		call	read_average
		mov		cmp1c,a

;;*****************************************************				
;///comparator2	00-1f
;;*******************************************************
		set 	cmp2en
		clr		C2HYSON
	    mov 	a,60h
	    mov 	cmp2c,a
	    mov		a,1fh
	    mov		temp3,a
	    clr		temp1
	    CALL	DLY_100US
	    sz 		c2cmpop
	    jmp 	ac2_low


ac2_high:
		inc 	cmp2c 
		inc		temp1
		CALL	DLY_100US
	    sz  	c2cmpop
	    jmp 	ac2_ok	    
	    dec		temp3  
		sz		temp3
		jmp		ac2_high	    
	    jmp 	ac2_ok

ac2_low:	
		inc 	cmp2c
		inc		temp1
		CALL	DLY_100US
	    snz 	c2cmpop
	    jmp 	ac2_ok	    
	    dec		temp3  
		sz		temp3
		jmp		ac2_low  	
ac2_ok:					
					;;;1f---0********************** 
		set 	cmp2en 
		clr		C2HYSON
	    mov		a,07fh
	    mov		cmp2c,a 
	    mov		a,1fh
	    mov		temp3,a 
	    mov		temp2,a 
	    CALL	DLY_100US
	    sz 		c2cmpop
	    jmp 	ac22_low
ac22_high:
		dec 	cmp2c
		dec		temp2
		CALL	DLY_100US
	    sz  	c2cmpop
	    jmp 	ac22_ok	    
	    dec		temp3	     
		sz		temp3
		jmp		ac22_high	    
	    jmp 	ac22_ok 
ac22_low:	
		dec 	cmp2c
		dec		temp2
		CALL	DLY_100US
	    snz 	c2cmpop  
	    jmp 	ac22_ok	    
	    dec		temp3
	    sz		temp3
		jmp		ac22_low	  
ac22_ok:	 
		call	read_average
		mov		cmp2c,a 		 
;*******************************
;OPAC的校准：
;*******************************
;;*******************************
;;OPAC的校准;
;;********************************	
		clr		OP2AD0				;disable operational amplifier output connected  to an0  ;关闭放大器连同
		CALL	DLY_100US
		

        NOP    MOV		A,01000000b    MOV		opac1,A				;T3RSEN OPAOFM OPARS        mov 	a,10000000b			;OPAEN,OPAOP OPAOF5~OPAOF0	;10100000b;OPAEN OPAOP OPAOFM OPARS OPAOF3~OPAOF0    mov 	opac,a		    clr 	temp0    clr 	temp1     clr 	temp2     call	dly_100us 		;延时

;-------------------------------------------
;  FROM 0h TO 0fh CANCELLATION  
;-------------------------------------------
        mov 	a,3fh 
        mov 	temp3,a  
        sz 		opac.6
        jmp  	h_to_l 
         
l_to_h: sz 		temp3
        jmp 	l_to_h1
        jmp 	ver_end1
l_to_h1:dec 	temp3
        inc 	temp1
        inc 	opac            ;[opaof3 ~ opaof0] +1
        CALL	dly_100us
        snz 	opac.6
        jmp 	l_to_h
        jmp 	ver_end1         

h_to_l: sz 		temp3
        jmp 	h_to_l1 
        jmp 	ver_end1
h_to_l1:dec 	temp3
        inc 	temp1
        inc 	opac            ;[opaof3 ~ opaof0] +1
        CALL	dly_100us
        sz 		opac.6
        jmp 	h_to_l
;;=================================================
; FROM 0Fh TO 00h CANCELLATION 
;--------------------------------------------
ver_end1:
		CLR     WDT
		CLR		WDT1
		clr		WDT2

		mov 	a,10111111b     ;opa CANCELLATION mode; opan AS THE REFERENCE INPUT.    mov 	opac,a    mov 	a,00111111b    mov 	temp2,a    mov 	a,3fh    mov 	temp3 ,a     sz 		opac.6    jmp  	h_to_la

l_to_ha:sz 		temp3
        jmp 	l_to_ha1
        jmp 	ver_end2
l_to_ha1:   
				dec 	temp3
        dec 	temp2
        dec 	opac
        CALL	dly_100us
        snz 	opac.6
        jmp 	l_to_ha
        jmp 	ver_end2
h_to_la:     
				sz 		temp3
        jmp 	h_to_la1 
        jmp 	ver_end2 
h_to_la1:   
				dec 	temp3
        dec 	temp2  
        dec 	opac
        CALL	dly_100us
        sz 		opac.6
        jmp 	h_to_la
ver_end2: 
		call	read_average 
		mov		a,temp0
     	nop		 
		mov 	opac,a   
        set 	opac.7  
        nop
        MOV		A,00000000b		;关闭比较
        MOV		opac1,A				;T3RSEN OPAOFM OPARS
        SET		op2ad0		;DISABLE OPERATIONAL AMPLIFIER OUTPUT CONNECTED        
		RET
;;;*******************************************************
;================================================
; (temp1 + temp2)/2 = temp0
;===============================================
;;********************************************************
read_average:
		clr 	temp0  
        clr 	c 
        mov 	a,temp1 
        addm 	a,temp0
        clr 	c 
        mov 	a,temp2
        addm 	a,temp0
        clr 	c
        rrc 	temp0  
        mov 	a,temp0 
     	nop
     	ret
;****************************
;dly_100us
;*************************** 
dly_100us:					;加长延时时间50US
		clr		temp4	
dlyy_100us:
;dly_nop:
		inc		temp4		
		mov		a,temp4
		sub		a,10 
		snz		c
		jmp		dlyy_100us
		clr		temp4
		ret	
		   
;****************************
;operate high voltate protech
;and surge voltate:
;***************************     
highvol_surge:
		nop
		nop
		nop
		

		snz		bonoff	ret    


​	 

     	snz		control_igbt	ret		nop	nop	nop	nop	nop	;snz		bheat40ms	;ret	;clr		bheat40ms	nop	nop 

  ;///////////////////
        mov     a,ppgta
        sub     a,pwm_min
        snz     c
        jmp     hsg_a
        

        clr     EC1I    jmp     hg_start

hsg_a:  set     EC1I
hg_start:
		nop
		nop
		nop
		nop
		nop
		nop
		;snz		b_ledmode
       ; jmp		hg_st1
        ;call	led_heathuoli
hg_st1:
		nop 
		nop
		snz		b250volbz
		jmp		hgp_3
		mov     a,p_1300
        mov     heathuoli,a          
hgp_3:		
		

		mov		a,heathuoli			dec		acc	nop	nop	nop  	nop	nop 	nop  	sz		bdown5m		jmp		get_145hvol	 	;sz      bheat125bz    ;jmp     get_125hvol         ;sz      bheat135bz    ;jmp     get_135hvol         ;sz      bheat145bz    ;jmp     get_145hvol        ;sz      bheat155bz    ;jmp     get_165hvol        ;sz      bheat165bz    jmp     get_165hvol    ret

;///		 
get_125hvol:		
     	

		add		a,tab_125hvol	jmp     highvol_com

;///		
;get_135hvol:		
     	;mov		a,heathuoli
		;dec		acc
		;add		a,tab_135hvol
		;jmp     highvol_com		
;///		
get_145hvol:		
     	

		add		a,tab_125hvol	jmp     highvol_com

;///		
;get_155hvol:		
     	;mov		a,heathuoli
		;dec		acc
		;add		a,tab_155hvol
		;jmp     highvol_com	
		
;///		
get_165hvol:		
     	

		add		a,tab_165hvol						

;///		
highvol_com:
		nop
		nop
		nop
		mov		tblp,a
		tabrdl	temp0
     

     	clr		temp1 	 	mov		a,vol_in 	sub		a,vol_180 	snz		c 	jmp		hs_end	mov		temp2,a		mov		a,vol_in 	sub		a,vol_240 	snz		c 	jmp		hs_next		mov		a,5	mov		temp1,a	jmp		hs_end


hs_next:
		mov		a,temp2		
     	sub		a,8
     	snz		c
     	jmp		hs_end
     	mov		temp2,a
     	

     	inc		temp1 	mov		a,temp1 	sub		a,5 	snz		c 	jmp		hs_next

hs_end:	mov		a,temp1
		nop
		nop
		add		a,tab_surge
		nop
		nop
		nop
		mov		tblp,a
		tabrdl	acc
		orm		a,temp0
		

		mov		a,ctrl2	and		a,11000000b	or		a,temp0	mov		ctrl2,a	ret

;****************************
;detect power down:
;****************************   
detect_power_down:
		nop
		nop
		nop
	

		snz		control_igbt			ret

;		snz		EIF				;check pan pin is product interrupt
;		jmp		dp_surge
;		clr		EIF
;		
		
;=======note3  掉电侦测的保护 
;/////////系统连续5次则结束=========		
		snz		LVDO			;detect low voltage detected
		clr		lowvoldetjs
		clr		LVDO
		inc		lowvoldetjs
		mov		a,lowvoldetjs
		sub     a,5
        snz     c
		ret
		clr		lowvoldetjs
;======================================
dp_surge:
		nop
		nop
		nop	
		clr		LVDO
		mov		a,00000000b
		mov		ppgc,a
		mov		a,pwm_on 			;(512-1BB)*0.25
		mov		ppgta,a
		set		bsurge
		clr		langyongjs
		clr		control_igbt
		clr		bheatno
		clr		bheate
		mov		a,delay_check
	   	mov	    pwmdly1sjs,a
		ret

;=======>new part <===================
;*************************************
;
;*************************************
f20ms_service:
		nop		
		inc		adt300msjs
		mov		a,adt300msjs
		sub		a,0eah
		snz		c
		jmp		it0_quit
		clr		adt300msjs
		set		badt300ms
it0_quit:	
		ret			

;>>>>>>>>>>>>>>>>>>new part<<<<<<<<<<<<
;=========================
;control fan program
;==========================
fan_pro:
		nop
		sz		beep_count0
		jmp		fp_ret
					

		sz		bonoff	jmp		fp_s2	snz		bfan	jmp		fp_off		inc		jianguojs   ;fan_counter	mov		a,jianguojs ;fan_counter	sub		a,120		 ;120*0.5=60s	snz		c	jmp		fp_on	clr		bfan	jmp		fp_off			

;///
fp_s2:	
		snz		byuyuests
		jmp		fp_on
			 
		
fp_off: clr		p_fan
		clr		benfan
		jmp		fp_ret

fp_on:	set		p_fan
		set		benfan
fp_ret:	ret

;>>>>>>>>>>>>new part <<<<<<<<<<<<<<<
;************************************
;beep sound
;************************************
beep_sound:
		nop
		sz		beep_count0
		jmp		bs_end
    	clr		bze   	
    	sz		benfan
    	ret		
    	clr		p_buz
    	ret
    	
bs_end: dec		beep_count0
		

	    ret 

;>>>>>>>buz operate part <<<<<<<<			
;************************************
; buzzer ring subroutine
;*************************************
Beep_1:	mov		a,6
		mov		beep_count0,a
		set		bze		;enable buz
		set		p_buz		
		RET

;>>>>>>>dsp digit  part <<<<<<<<			
;************************************
; buzzer ring subroutine
;*************************************
dsp_digit:
		nop
		nop
		nop
		snz		bendspall
		jmp		dd_s1 
		

		nop	inc		gya_js				mov		a,gya_js	sub		a,10	snz		c  	jmp		dd_all 	clr		gya_js

dd_tt1:		
		inc		dya_js
		mov		a,dya_js
		sub		a,100 ;50
		snz		c
		jmp		dd_all	
		clr		bendspall 
		mov		a,current
		mov		init_cur,a	
			
dd_all: set		temp0	
		nop 
		nop
		snz		b_secok
		ret
		clr		b_secok
		

		mov		a,0ffh 
		mov		run_ram1,a 
	    mov		run_ram2,a
	    mov		run_ram3,a
	    mov		run_ram4,a 
	    mov		run_ram5,a 
	    mov		run_ram6,a
	    mov		run_ram7,a 
	    mov		a,0f9h
	    mov		run_ram0,a
	    ret       

dd_send:
		mov		a,dspbuff
		mov		mp0,a
dd_snext:
		mov		a,temp0
		mov		r0,a
		inc		mp0
		mov		a,mp0
		sub		a,dspbuff+dsp_bufnum 
		snz		c
		jmp		dd_snext				
dd_ret:				 
		ret
		
;////		
dd_s1:	clr		temp0
		call	dd_send
		nop
		nop 
										

	;display errorcode	snz		berror	jmp		dd_s2

dd_err:
		mov		a,errorcode
		mov		temp0,a
		
		

		snz		bsnd0	jmp		dd_end	mov		a,temp0	add		a,digitlist	mov		tblp,a 	tabrdl	acc	mov		dspbuf2,a	mov		a,sym_e	mov		dspbuf1,a	jmp		dd_end

;//////
dd_s2:	snz		bbusysts 
		jmp		dd_s7 

		snz		bonoff	jmp		dsp_standby		nop	nop;///display power level///		set		stonoff		nop	nop	call    dsp_workmode2		nop	nop	snz		bwarmh	jmp		dd_chk	mov		a,er_igbtwarm	nop	mov		errorcode,a	jmp		dd_err

dd_chk:	nop
		nop	
		snz	    bendspguo
		jmp	    dd_s3
		sz		bguoon
		jmp	    dd_s3

		nop	nop

;====判断电路故障还是无锅====	
		mov     a,er_nopan
		nop
		nop
		mov  	errorcode,a
		mov     a,dpanjs
		sub     a,2
		sz      c
		jmp     dd_err
		 

		mov     a,er_mainpcb	nop	mov     errorcode,a 	jmp	    dd_err 	

dd_s3:	
		nop
		nop 
		;////////display power led/////
		call	power_bar
		nop
		nop
		call	dsp_dspbuf
		jmp		dd_end
				
dsp_standby:
		mov		a,sym_0
		mov		dspbuf1,a
		mov		a,sym_n
		mov		dspbuf2,a
		jmp		dd_end

dd_s7:
		snz		bsnd0   
		jmp		dd_end	
		
										

		mov		a,sym_heng	mov		dspbuf0,a	mov		dspbuf1,a	mov		dspbuf2,a	mov		dspbuf3,a


​		

		set		stonoff					set		sdot1	set		sdot2	set		sdot3	nop	nop	nop		

;/////		
dd_end:	
		nop
		call	dd_pt 
				

		sz		block		set		stlock 				snz		b_secok	ret	clr		b_secok 				mov		a,ledbuf0    mov		run_ram1,a        mov		a,ledbuf1    mov		run_ram2,a        mov		a,ledbuf2    mov		run_ram3,a          mov		a,dspbuf0    mov		run_ram4,a        mov		a,dspbuf2    mov		run_ram5,a         mov		a,dspbuf3    mov		run_ram6,a     	mov		a,dspbuf1    mov		run_ram7,a         mov		a,run_ram1     add		a,run_ram2    add		a,run_ram3    add		a,run_ram4    add		a,run_ram5    add		a,run_ram6    add		a,run_ram7    mov		run_ram0,a		ret 		

dd_pt:		
		nop
		nop
		mov		a,1
		mov		debug_stage,a
		sz		debug_stage
		call	dsp_debug	
		ret							


;//*********************************
;//display power
;//**********************************
dsp_dspbuf:
		nop 
		nop
		mov		a,seep_state
		sub		a,1
		snz		z
		jmp		ddf_chkv
				
		

		set		stcoulo			nop	nop	mov		a,coulomjsh	mov		temp1,a	call    get_tabcom    mov		a,temp4    mov		dspbuf2,a    mov		a,temp3    mov		dspbuf1,a		mov		a,coulomjsl	mov		temp1,a	call    get_tabcom    mov		a,temp3    mov		dspbuf3,a		mov		a,sym_p	mov		dspbuf0,a	set     sdot0	set		sdot3	nop	nop			ret	

;////	
ddf_chkv:	
		mov		a,seep_state
		sub		a,2
		snz		z
		jmp		ddf_start			
		

		nop	nop	nop		set		stcoulo					    mov		a,vol220_const		mov		to0,a	mov		a,vol_in	mov		data4,a	nop	nop	call	mul88	nop	nop	mov		a,vol_220	mov		data4,a	nop	nop	call	div168	nop	nop	mov		a,to1	mov		data1,a	mov		a,to0	mov		data0,a	mov		a,100	mov		data4,a	call	div168		mov		a,to1	call	gtb_next	mov		a,temp3	mov		dspbuf1,a		mov		a,com	mov		temp1,a	call	get_tabcom		mov		a,temp3	mov		dspbuf2,a	mov		a,temp4	mov		dspbuf3,a	mov     a,sym_u    mov     dspbuf0,a	ret

;////display other param////
ddf_start:
		snz		bflhyu
		jmp		ddf_s1
				
		

		set		stshijian	set     sttimer			snz		bsnd0	ret

ddf_yuyue: 
		mov		a,yhour
		mov		temp0,a
		mov		a,yminute
		mov		temp1,a	
		
ddb_com:
        call    get_tabcom
        mov		a,temp4
        mov		dspbuf3,a
        mov		a,temp3
        mov		dspbuf2,a
        

        mov		a,temp0    mov		temp1,a    call    get_tabcom    mov		a,temp4    mov		dspbuf1,a    mov		a,temp3    mov		dspbuf0,a;===appointment status display high byte====	call	chk_buf0	snz		bsnd0	ret	

ddf_dot:	
		nop
		nop
		nop		
		set		sdot1
		set		sdot2
		set		sdot3			
ddf_ret:        
        ret 
                  
;///
ddf_s1: snz		bflhdin
		jmp		ddf_s2
		
		

		set		stshijian	set     sttimer


​		

		snz		bsnd0	ret	mov		a,minutet	

ddf1_com:
		mov		temp1,a		
		mov		a,60
		call	divx
		mov		temp1,a
		

		mov		a,temp2	mov		temp0,a    jmp		ddb_com

;///
ddf_s2: snz		byuyuests
		jmp		ddf_s3
		

		set		stshijian	set     sttimer			mov		a,dspparamjs	sub		a,12	snz		c	jmp		ddf_yuyue    jmp		ddf_power

;/////
ddf_dingshi:      
		mov		a,tminute
        jmp		ddf1_com
        
;////
ddf_s3:	snz		bsettimests
		jmp		ddf_power
		

		set		stshijian	set     sttimer		mov		a,dspparamjs	sub		a,12	snz		c	jmp		ddf_dingshi

;////
ddf_power:
        snz		btempsts
        jmp		dp_realpower
          

       	nop   	nop             	   	set		sttemp 	                 mov		a,sym_0    mov		dspbuf3,a        mov		a,dsphuoli    dec		acc    nop	nop    add		a,tabdsptemp    nop    nop	mov		tblp,a	tabrdl	temp0	mov		a,temp0      	call	get_buf	mov		dspbuf2,a		swapa	temp0	call	get_buf	mov		dspbuf1,a	mov		a,sym_0	sub		a,dspbuf1	snz		z	jmp		dp_ret	mov		a,sym_off	mov		dspbuf1,a    ret


​		        
dp_realpower:
​		mov		a,sym_0
​		mov		dspbuf3,a
​		mov		dspbuf2,a
​		

		nop	nop		;set		stpower 		mov		a,dsphuoli    dec		acc    nop    nop    add		a,tabdsphuoli        nop    nop             

dpt_com:
       	mov		tblp,a
		tabrdl	temp0

		mov		a,temp0      	call	get_buf	mov		dspbuf1,a		swapa	temp0	call	get_buf	mov		dspbuf0,a

chk_buf0:
		mov		a,sym_0
		sub		a,dspbuf0
		snz		z
		jmp		dp_ret
		mov		a,sym_off
		mov		dspbuf0,a
dp_ret: ret		


;******************************
;get tab com:
;******************************
get_tabcom:
		mov		a,10
		call	divx

	;///get low bit		add		a,tabnum	mov		tblp,a	tabrdl	temp4;///get high bit		mov		a,temp2	

gtb_next: 
		add		a,tabnum
		mov		tblp,a
		tabrdl	temp3
        ret

;//******************************
;//display debug param
;//*****************************
dsp_debug:
		mov		a,debug_stage
		dec		acc
		mov		temp0,a
		

		add		a,tabdebug0-lastpage	mov		tblp,a	tabrdl	acc	Mov		Mp0,A	mov		a,r0	and		a,0fh	ADD		A,DIGITLIST	mov		tblp,a	tabrdl	acc	mov		dspbuf1,a		mov		a,r0	swap	acc	and		a,0fh	ADD		A,DIGITLIST	mov		tblp,a	tabrdl	acc	mov		dspbuf0,a		mov		a,temp0	add		a,tabdebug5-lastpage	mov		tblp,a	tabrdl	acc	Mov		Mp0,A	mov		a,r0	and		a,0fh	ADD		A,tabnum	mov		tblp,a	tabrdl	acc	mov		dspbuf3,a	mov		a,r0	swap	acc	and		a,0fh	ADD		A,tabnum	mov		tblp,a	tabrdl	acc	mov		dspbuf2,a	RET

get_buf:
		and		a,0fh
		ADD		A,DIGITLIST
		mov		tblp,a
		tabrdl	acc
		ret
;**********************************
;display workmode:
;**********************************		
       
dsp_workmode2:
		nop
		mov		a,m_huoguo
        sub		a,mode
        sz		z
        set		sthuoguo

		mov		a,m_shaokao    sub		a,mode    sz		z    set		stshaokao	mov		a,m_zhufan    sub		a,mode    sz		z    set		stzhufan	mov		a,m_baochao    sub		a,mode    sz		z    set		stbaochao	mov		a,m_soupzhou    sub		a,mode    sz		z    set		stsoup	mov		a,m_jianchao    sub		a,mode    sz		z    set		stjianzha        mov	    a,m_zheng    sub	    a,mode    sz		z    set  	stzheng        mov		a,m_shaoshui    sub		a,mode    sz		z    set		stshaoshui    ret 


​				
;**********************************
;display power bar:
;**********************************
power_bar:
​		nop		
​		mov		a,dsphuoli
​        dec		acc
​        add		a,tabdsphled
​        mov		tblp,a
​		tabrdl	temp0
​		nop		
​		sz		tmp0_b0
​		set		st1
​				

		sz		tmp0_b1
		set		st2
		
		sz		tmp0_b2
		set		st3
		
		sz		tmp0_b3
		set		st4
		
		sz		tmp0_b4
		set		st5
		
		sz		tmp0_b5
		set		st6
		
		sz		tmp0_b6
		set		st7
		
		sz		tmp0_b7
		set		st8
		ret		

;>>>>>>>>>>>>NEW PART <<<<<<<<<<<<<<<<<<<<<<<
;************************************************
;		JIANGUO PART
;************************************************
jianguo:	nop
			nop
			nop
			

			snz		bonoff
			ret
			sz		byuyuests
			ret

tch_k8:			
			sz		berror
			ret
			

			sz		bsurge
			ret
			
			mov		a,52
			snz		bguoon
	        jmp		jgrun
	        mov		a,200				
				
			sz		control_igbt
			ret

jgrun:		mov		temp0,a
		

	;///check no pan off 1 minute off///	    	snz		bpan500ms		jmp		jg_s2		clr		bpan500ms				inc		nopanoffjsh		mov		a,nopanoffjsh		sub		a,120		snz		c					jmp		jg_s2										call	power_off		ret


​			

jg_s2:		sz		jianguojs
			jmp		jgencmp
			mov		a,temp0
			mov		jianguojs,a
			inc	    jianguojs

jgencmp:	dec		jianguojs
			mov		a,temp0
			sub		a,jianguojs
			sz		z
			jmp		jguppwm
			ret

;//////step 1
jguppwm:	
			NOP
			NOP
	;///产生PPG 8US signal///	
			mov		a,0c8h ;b0h 	;7us
			mov		ppgta,a
			mov		a,00000100b		;修改处00000000b
			NOP
			NOP
			NOP
			mov		ppgc,a
			set		pst
			

			clr		dpanjs		mov		a,250		mov		temp0,a		nop		nop		nop		nop		nop 		nop		nop		nop					;delay 8us not interrupt		nop		nop		nop		nop		set		EEI		;enable ext0 interrupt

dp_next:	nop
			nop
			nop
			sdz		temp0				
			jmp		dp_next
			clr		EEI

			set		bendspguo	 				mov		a,0bh		nop  		nop		nop		sub		a,dpanjs 		sz		c		jmp		jgyes

jgno:		snz		f_2s
			ret
			clr		f_2s
			call	beep_1
			

			clr 	jianguojs		clr		bguoon		ret

;////
jgyes:	    
			NOP
			NOP
			mov		a,dpanjs				;若小于等于1，则认为是无锅
			sub		a,2
			sz		c
			jmp		jgy_on
			jmp		jgno	

			;sz		dpanjs		;jmp	jgy_on		;jmp	jgno


jgy_on:					
			set		bguoon
			mov		a,pwm_on 	;10us
			mov		ppgta,a
			clr		nopanoffjsh
			mov		a,delay_check
			mov		pwmdly1sjs,a
			ret
			
;************************************************
;		system error detect part    			*
;************************************************
error:		nop
			nop
			nop 
			

			snz		bonoff		ret							sz		bendspall		ret		snz		berror		jmp		er_check				mov		a,er_volmin		nop		sub		a,errorcode		sz		acc		jmp		er_cancel					mov		a,vol_in				sub		a,vol_min1		sz		c		jmp		er_realcan

;///
er_cancel:	mov		a,er_volmax
			nop
			sub		a,errorcode
			sz		acc
			jmp		er_canret
			

			mov		a,vol_in		sub		a,vol_max1		sz		c		jmp		er_canret

er_realcan: clr     errorcode
            clr		berror
er_canret:  ret            	    		

;/////////	   
er_check:  	snz		bpo1m
			jmp		er_s1
			

			mov		a,temp_main		sub		a,main_min+1		sz		c		jmp		er_igbt		mov     a,er_mainmin		nop		jmp     errorbus     


​			
er_igbt:    mov		a,temp_igbt
​			sub		a,igbt_min+1
​			sz		c
​			jmp		er_s1
​			mov     a,er_igbtmin
​			nop
​			jmp     errorbus

;///			
er_s1:		mov		a,temp_main
			sub		a,main_max
			snz		c
			jmp		er_s2

            mov		a,er_mainmax        nop		jmp		errorbus

;///
er_s2:		mov		a,temp_igbt
			sub		a,igbt_max
			snz		c
			jmp		er_s3

            mov		a,er_igbtmax        nop		jmp		errorbus

;///
er_s3:		mov		a,vol_in
			sub		a,vol_min
			sz		c
			clr		dya_js
			

			inc		dya_js		mov		a,dya_js		sub		a,100		snz		c		jmp		er_s4		mov		a,er_volmin		nop		jmp		errorbus

;///
er_s4:		mov		a,vol_in
			sub		a,vol_max
			snz		c
			clr		gya_js
			inc		gya_js
			mov		a,gya_js
			sub		a,100
			snz		c
			jmp		er_s5
			mov		a,er_volmax
			nop
			jmp		errorbus

;///
er_s5:		mov		a,temp_igbt
			sub		a,igbt_110
			sz		c
			set		bwarmh
			

			mov		a,temp_igbt		sub		a,igbt_65		snz		c		clr		bwarmh

;///
er_s6:

		    nop		nop		call	detect_senson_unvalid	    mov     a,errorcode	    sub     a,er_mainerr	    sz      z      				    jmp		errorbus1		mov		a,temp_main		sub		a,main_270		sz		c		jmp		er_ganshao		sz		btempsts		ret				mov		a,m_zhufan    	sub		a,mode    	sz		z		ret	;///other mode///		mov		a,minjs		sub		a,1		snz		c		ret				mov		a,temp_main		sub		a,main_210		sz		c		jmp		er_ganshao		mov		a,heathuoli		sub		a,oldhuoli		sz		z		jmp		er6_nop1				mov		a,heathuoli		mov		oldhuoli,a		clr		delay30sjs		ret

er6_nop1:	snz		bganshao
			ret
er_ganshao:
			mov		a,er_mainwarm
			nop

;///			
errorbus:	mov		errorcode,a
errorbus1:
			call	beep_1
			set		berror
			mov		a,errorcode
			nop
			nop
			nop
			nop
			nop
			sub		a,er_volmin
			sz		z
			ret
			mov		a,errorcode
			nop
			nop
			nop
			nop
			nop
			sub		a,er_volmax
			sz		z
			ret	
			call	power_off
			ret
;************************   
;//////////
;************************  
detect_senson_unvalid:
            sz      minjs  
            jmp     er11_nop1    
            mov     a,temp_main
            mov     tmax,a
            mov     a,temp_main 
            mov     tmin,a		 	
			jmp     er11_nop3
er11_nop1:  
            mov     a,temp_main
            sub     a,tmax   
        	snz     c
        	jmp     er11_nop2
        	mov     a,temp_main
        	mov     tmax,a
        	
er11_nop2:	
            mov     a,temp_main
            sub     a,tmin   
        	sz      c
        	jmp     er11_nop3
        	mov     a,temp_main
        	mov     tmin,a
           
er11_nop3:	snz	   	control_igbt
			jmp	    er11_nop4
			

			sz      byuyuests		jmp	    er11_nop4 				mov     a,tiao_on		sub     a,tiao_zong		snz     z		jmp     er11_nop4				snz     b1min		jmp     error_ret		clr     b1min				sz      bnochange		jmp     er11_nop4  							mov      a,heathuoli		sub      a,4 		snz      c		jmp      er11_nop4 		 		mov      a,temp_main		sub      a,7 		snz      c 		jmp      er11_nop4   		 		mov      a,temp_main		sub      a,18h 		snz      c		jmp      er11_nop5 

er11_nop4:	clr		nochangejs
error_ret:	ret  

;///
er11_nop5:  mov 	a,tmax
			sub		a,tmin
			sub		a,6
			snz     c 
			jmp     er11_nop6
			set	    bnochange
			ret						  
er11_nop6: 
            mov		a,nochangejs
            sub     a,4
			sz      c 
			jmp     er11_nop7
			inc		nochangejs 
			ret                           
er11_nop7:	 
            mov     a,er_mainerr
            mov		errorcode,a        
			ret	
;************************************************
;HEAT SUB PROGRAM
;************************************************
HEAT:	nop
		nop
		nop		
		snz		bonoff
		jmp		heatno
		
		

		sz		bheatno	jmp		heatno		sz		bwarmh	jmp		heatno


​				

		sz		byuyuests	jmp		heatno

tch_k14:		
		sz		berror
		jmp		heatno
		

		snz		bheat40ms	ret	clr		bheat40ms		sz		highvoljs		;判断是否产生高压中断，如有高压中断，则延时减小PPGA	dec		highvoljs		snz		bguoon	ret	snz		bheate	ret	sz		bsurge	ret		sz		control_igbt	jmp		trig1	set		control_igbt		mov		a,pwm_on 			;(512-1BB)*0.25	mov		ppgta,a		mov		a,01100100b		;enable h/w and s/w	nop	nop	nop	mov		ppgc,a	set		pst	set		EC2I			;enable comparator 2 interrupt response	set		EC1I			;enable comparator 1 interrupt response

trig1:	
		nop
		nop
		call	henggong
		

		mov		a,current	sub		a,valuecur	snz		c	jmp		ht_add_s1		mov		temp0,a	sub		a,15	snz		c	jmp		ht_low 	jmp		ht_fast

ht_add_s1:
	 	mov		a,valuecur
		sub		a,current
		mov		temp0,a
		

		;如果高压产生，则延时1.8s 进行减小PPGTA		sub		a,30 ;25 ;40 ;20 ;18 ;50	sz		c	jmp		ht_fast	add		a,30 ;25 ;20 ;18 ;15 ;24 ;50	sub		a,15 ;10 ;20 ;10 ;9  ;20	sz		c	jmp		ht_clrwen

ht_low:	set		bpwmwen
		jmp		ht_start

ht_fast:
		clr	    pwmtiaojs
ht_clrwen:
		clr		bpwmwen

;///
ht_start:	
		sz		pwmtiaojs
		jmp		hdectiaojs
		

		mov		a,temp0	sub		a,3	snz		c	ret		mov		a,2	sz		bpwmwen	mov		a,4 ;5	mov		pwmtiaojs,a	jmp		HTIAO

hdectiaojs:	
		dec	    pwmtiaojs
		ret
		
HTIAO:	mov		a,valuecur
		sub		a,current
		snz		c
		jmp		heatdec		;cur > temp0, jmp heatdec
		

		sz		pwmdly1sjs	jmp		heat_add	;jmp	hcmpmax

;////if ppgta >=0b0h ,then temp1=0b0h
		mov		a,ppgta
		mov		temp1,a
		sub		a,0b0h 
		snz		c
		jmp		htiao_st
		mov		a,0b0h
		mov		temp1,a

htiao_st:		
		mov		a,0B0H
		sub		a,temp1 ;ppgta
		mov		temp1,a
		

		mov		a,current	sub		a,13h	snz		c	jmp		hnopan	;///temp0/13////	mov		a,16	call	divx	mov		a,temp2				add		a,tabminucur	nop	nop	nop	mov		tblp,a	tabrdl	acc	mov		temp0,a		mov		a,vol_in	;sub	a,vol_220	;snz	c	;jmp	ht_jg_s1	;mov	a,vol_220	;jmp	ht_jg_s2

ht_jg_s1:
		;add	a,vol_220
		
ht_jg_s2:		
		sub		a,vol_80
		snz		c
		jmp		hdpan_s1
		mov		temp1,a
		mov		a,6
		call	divx
		mov		a,temp2
		addm	a,temp0		
	        
hdpan_s1:
		mov		a,temp0
		;mov	drefp,a	
		sub		a,current
		snz		c
		jmp		hcmpmax

		;===no pan operate ===

hnopan:	
		set		byanguo
		clr		dyanguojs1
		clr		dtime5sjs
		

		clr		bguoon	clr		jianguojs	nop 	nop    ;call    beep_1

heatno:
ds_com:	
		mov		a,00000000b
		mov		ppgc,a
		clr		pst
		;clr	EC2I
		clr		control_igbt
		clr		bheatno
		clr		bheate
		mov		a,delay_check
	   	mov	    pwmdly1sjs,a
        ret		

;///
heat_add:
		dec		pwmdly1sjs
				
hcmpmax:
		sz		highvoljs		;判断是否产生高压中断，如有高压中断，则延时减小PPGA
		ret

		nop	nop	nop	;snz		b_ledmode    ;jmp		hg_c1    ;call	led_heathuoli

hg_c1:			
		snz		b250volbz
		jmp		hcp_3
		mov     a,p_1300
        mov     heathuoli,a  
        
hcp_3:			
		mov		a,heathuoli	
		dec		acc
		nop  
 		nop
 		nop
 		nop  
 		nop
 		sz		bdown5m	
		jmp		heat_125pwm
		

		;sz      bheat125bz     ;jmp     heat_125pwm                jmp     heat_165pwm    ret

;///       
heat_125pwm:
 		

		add		a,tab_125pwmmax	jmp     heat_pwmcom

;///
;heat_135pwm:
; 		mov		a,heathuoli
;;		dec		acc
;		add		a,tab_135pwmmax
;		jmp     heat_pwmcom

;///		
;heat_145pwm:
; 		mov		a,heathuoli
;		dec		acc
;;		add		a,tab_145pwmmax
;		jmp     heat_pwmcom	

;///		
;heat_155pwm:
; 		mov		a,heathuoli
;;		dec		acc
;		add		a,tab_155pwmmax
;		jmp     heat_pwmcom					

;///		
heat_165pwm:
 		

		add		a,tab_165pwmmax

;///				
heat_pwmcom:
		nop
		nop 
		nop
		mov		tblp,a
		tabrdl	acc
		mov		temp0,a
        

        mov		a,vol_in	sub		a,vol_210	sz		c	jmp		hcmp_s1	mov		a,vol_210	sub		a,vol_in	;clr	c	;rrc	acc	jmp		hcmp_s1a

hcmp_s1:	
		clr		c
		rlc		acc

hcmp_s1a:		
		mov		temp1,a
		

		sub		a,28h  ;30h	snz		c	jmp		hcmp_s2			mov		a,28h  ;30h	mov		temp1,a

hcmp_s2:
		mov		a,temp1
		add		a,temp0
		mov		temp0,a
				

		mov		a,temp0	sub		a,ppgta	sz		c	jmp		hcmp_s4		dec		ppgta	sz		bpwmwen	ret	dec		ppgta

hsetwen:
		ret

;////
hcmp_s4:
		mov		 a,temp0  
		mov      ppgta,a
        ret  

;///		
heatdec:
		mov		a,ppgta		
		sub		a,pwm_min     
		sz		c
		ret
		

		inc		ppgta	sz		bpwmwen	ret	inc		ppgta	ret


​		
;************************************************
;heng gong sub program
;??????:temp0 = ??????????
;1)if vin < vol190, then vin = vin190;
;2)if vin >= volmax, then vin = vinmax;
;3)if vin >= vol230 and heathuoli <=2, then constant current;
;4)else constant power
;************************************************
henggong:       
​        nop
​        nop
​       ; snz		b_ledmode
​        ;jmp		hg_h1
​        ;call	led_heathuoli
hg_h1:
​		             

        mov		a,vol_in	sub		a,vol_240 	snz		c 	clr     b250volbz		nop          sz      b250volbz    jmp     hg_240_250v         nop    nop             mov		a,vol_in	sub		a,vol_250	snz		c	jmp     hg_250v			;vin < vin250

hg_240_250v:		
		set		b250volbz
		mov     a,p_1300
        mov     heathuoli,a     
hg_250v: 		
		mov		a,heathuoli 
		dec		acc
 		nop  
 		nop
 		nop
 		nop  
 		nop
 		sz		bdown5m
 		jmp		heat_145cur
 		

 		sz		bdown3m	jmp		heat_155cur     ;sz      bheat125bz    ;jmp     heat_125cur        ;sz      bheat135bz    ;jmp     heat_135cur        ;sz      bheat145bz    ;jmp     heat_145cur        ;sz      bheat155bz    ;jmp     heat_155cur        ;sz      bheat165bz    jmp     heat_165cur    ret

;///
heat_125cur:        
		add		a,tab_145cur-lastpage
		jmp     current_com
		
;///
;heat_135cur:         
;		add		a,tab_135cur-lastpage
;		jmp     current_com
		
;///
heat_145cur:     
		nop    
		add		a,tab_145cur-lastpage
		nop
		jmp     current_com	
		
;///
heat_155cur:        
		nop
		add		a,tab_155cur-lastpage
		nop
		jmp     current_com
		;///
heat_165cur:        
		nop 
		add		a,tab_165cur-lastpage	
		nop 					
;///		
current_com:
        nop 
		nop 
		nop
		mov		tblp,a
		tabrdl	data0
		clr		data1
		

		mov		a,vol_in	sub		a,vol_210	snz		c	clr		acc				;vin < vin210	add		a,vol_210		sub		a,vol_max	sz		c	clr		acc				;vin >=vinmax	add		a,vol_max	mov		data4,a;///判断是否为最小连续档是否为;若是不电压大于220V时，则当作220V处理	sub		a,vol_220	snz		c	jmp		hg_s1		;vin < vin220		mov		a,heathuoli	sub		a,p_1000+2	;p1000=最小连续档 	sz		c	jmp		hg_s1		 		mov		a,vol_220	mov		data4,a	 

hg_s1:	call	div168		 
		nop
		nop
		mov		a,heathuoli
		sub		a,p_1000+2
		snz		c
		jmp		hg_s2
		

		mov		a,vol_in	sub		a,vol_240	snz		c	jmp		hg_s2		clr		c	rrc		acc	mov		temp1,a								mov		a,to1	sub		a,temp1	mov		to1,a

hg_s2:	mov		a,to1
		mov		valuecur,a

		mov		a,valuecur	sub		a,cur_max	snz		c	ret	mov		a,cur_max	mov		valuecur,a		ret

;****************************
;input:acc,temp1 
;temp used:temp3
; output:temp2
;****************************
divx:	mov		temp3,a
		clr		temp2
		mov		a,temp1

div_n:	sub		a,temp3
		snz		c
		jmp		div_end
		inc		temp2
		jmp		div_n

div_end:
		;sz		temp2
		;ret
		add		a,temp3
		ret

;*****************************
;16bit unsigned div
;;data0,data1/data4---->to0,to1
;商  ：t00,t01,
;余数：com
;******************************
div168:
unbin_div_16:	
			mov		a,16
			mov		count0,a
			clr		com
			clr		to0
			clr		to1
				
div16pro1:	clr		c
			rlc		data1
			rlc		data0
			rlc		com
				

			snz		c		jmp		div16pro2		set		acc		sub		a,data4		inc		acc		addm	a,com		set		c		jmp		div16pro3

div16pro2:	mov		a,com
			sub		a,data4
			sz		c					;不够减
			mov		com,a				;com里面放余数
				
div16pro3:	rlc		to1
			rlc		to0
				

			sdz		count0		jmp		div16pro1		ret

;*****************************
;8 bit unsigned mul
;to0*data4---->data0data1
;******************************
mul88:		clr		data0 ;to0
			clr		data1 ;to1
			clr		count0

rradd:		clr		c
			rlc		data1 ;to1
			rlc		data0 ;to0

			snz		to0.7		jmp		rr1		rl		to0				mov		a,data4				;当前data4.0=1,移位加		addm	a,data1		mov		a,0		adcm	a,data0		jmp		rr2

rr1:		rl		to0
rr2:
			inc		count0
			snz		count0.3
			jmp		rradd					
			ret

;>>>>>>>>new part <<<<<<<<<<<<<<<<<<<<<
;//************************************
;//scan lcd
;//*************************************
timing:	nop
		nop
		nop
		

		inc		buznopanjs	mov		a,buznopanjs	sub		a,100	snz		c	jmp		tim_f1	clr		buznopanjs    set		f_2s

tim_f1:	snz		bflash
		jmp		tim_s1
		

		inc		confirm5sjs	mov		a,confirm5sjs	sub		a,250	snz		c	jmp		tim_s1		sz		bflhyu	jmp		tim5_yu			sz		minutet	jmp		tim_chkvalid	jmp		tim_chkclr	       

;///        
tim_chkvalid:
        mov		a,minutet
        mov		tminute,a
        clr		bdin1min
        clr     t1mjsh
        clr     t1mjsl
        jmp     gs_com

;///
tim5_yu:	
		sz		yhour
		jmp		tim_yuok
		sz		yminute
		jmp		tim_yuok
		jmp		tim_chkclr

tim_yuok:
		clr		y1mjsl
		clr		y1mjsh
		clr		byu1min
		jmp		gs_com

tim_chkclr:
		clr		flh_flag
		
gs_com: clr		bflhyu
		clr		bflhdin
		clr		bflash

;///        
tim_s1:		
		inc		flh_500ms
		mov		a,flh_500ms
		sub		a,25
		snz		c
		jmp		tim1_a
		clr		flh_500ms
		bcpl	time_flag,bit7		;bsnd0
		;inc	flh_second
		
tim1_a:	 
		inc		t_500ms
		mov		a,t_500ms
		sub		a,25
		snz		c
		ret
		clr		t_500ms
		set		bfun500ms
		set		bpan500ms  		
						
		

	;====计算电量及传感器延时处理====	snz		bonoff	jmp		tim_dly5s		snz		control_igbt	jmp		tim_dly5s


​		

	;///calcute  coulometer ////
		inc		cou36sjsl	
		mov		a,cou36sjsl
		sub		a,72
		snz		c
		jmp		tim1_b
		clr		cou36sjsl
	    
	    mov		a,dsphuoli 
	    dec		acc
	    add		a,tabmappower
	   	nop
	   	nop
	   	nop
	   	mov		tblp,a
		tabrdl	acc
	  
	  ;///转换成10进制数////    
	    addm	a,coulomjsl	
	    mov		a,coulomjsl
	    sub		a,100
	    snz		c
	    jmp		tim1_b
	    mov		coulomjsl,a
		inc		coulomjsh	

tim1_b:			 
		sz		bpo1m
		jmp		tim_dly5s
		inc		poweron1mjs	
		mov		a,poweron1mjs
		sub		a,120
		snz		c  
		jmp		tim_dly5s 	
        set		bpo1m
                
tim_dly5s:  
        inc		dspparamjs
        mov		a,dspparamjs
		sub		a,24
		snz		c
		jmp		tim_s2	 
		clr		dspparamjs
        set		bdiscursurge 
        nop
        nop
        sz		bdown5m		;工作后15分钟降火力
		jmp		tim_ss2 
						

		snz		bonoff    	jmp		tim_ss2	    		 	snz		control_igbt   	jmp		tim_ss2  	  	inc      down15mjs  

;		sz		 bdown3m 
;		jmp		 b_down5m
;        mov      a,down15mjs 
;        sub      a,25 
;        snz       c 
;        jmp		 tim_ss2
;        set      bdown3m
;        clr		 bdiscursurge 
;b_down5m:
		mov      a,down15mjs 
        sub      a,40 
        snz       c 
        jmp		 tim_ss2
        set      bdown5m
        clr		 bdiscursurge                		
tim_ss2:        
tim_s2: 
		snz     btemplock
        jmp     sim_s2
        

        inc     lockjs    mov     a,lockjs    sub     a,3    snz     c    jmp     sim_s2    clr     lockjs    clr     btemplock    call    kp7_bp         sz      block    jmp     c_lock        set     block     jmp     sim_s2

c_lock: clr     block

sim_s2:  
 ;====insert start=====		
		snz		bsurge
		jmp		tim2_a
		inc		langyongjs
		mov		a,langyongjs
		sub		a,4
		snz		c
		jmp		tim2_a
		clr		langyongjs
		clr		bsurge

tim2_a: inc		seecoulo15sjs
		mov		a,seecoulo15sjs 
		sub		a,20
		snz		c
		jmp		tim_s3
		clr		seecoulo15sjs
		clr		seep_state

  ;===可以省掉这部份程序，minjs直接在pro_dingshi 
  ;中置位                          
tim_s3:					
		snz		bbusysts
		jmp		tim_ss3

		sz		bonoff 	jmp		tim_ss3				inc		sec3sjs  	mov		a,sec3sjs	sub		a,120	snz		c	jmp		tim_ss3 	clr		sec3sjs	call	power_off

tim_ss3:
		sz		byuyuests
		ret
tch_k17:		
		nop
		nop
		;inc		dtime10sjs
		inc		secjs 
		mov		a,secjs
		sub		a,120 
		snz		c
		ret
		clr		secjs
		inc		minjs

		set		b1min

tim_ret:
		ret

;//>>>>>>>>>>>>>>>new part<<<<<<<<<<<<<<<
;//**************************************
;//check dingshi is end
;//**************************************
pro_dingshi:
		nop


		snz		bonoff	ret	sz		bflash	ret	sz		byuyuests	jmp		pro_yuyue		snz		bdin1min	ret	clr		bdin1min		inc		t1mjsh	mov		a,t1mjsh	sub		a,120	snz		c	ret	clr		t1mjsh	dec		tminute	mov		a,tminute	sz		acc	ret

pd_off:           
;//*************************************
;//power off
;//***********************************
power_off:
		clr		gya_js
		clr		dya_js
		clr 	jianguojs
		clr		bbusysts			
		mov		a,offset yhour	;mode_clear
	    call    stan_clr	
		call	set_noheat
		clr		bonoff
		set		bfan
		call	beep_1
		

		set		byanguo 	clr		dyanguojs1	clr		dtime5sjs	clr		dtime10sjs	clr      down15mjs  	clr		 bdown3m 	clr		 bdown5m			

pd_ret:  
		ret

;//****************new part ***********************
;//************************************************
;//check yuyue  is end
;//************************************************
pro_yuyue:
		snz		byu1min
		ret
		clr		byu1min
		

		inc		y1mjsh	mov		a,y1mjsh	sub		a,120	snz		c	ret	clr		y1mjsh				sz		yminute ;acc	jmp		py_st	dec     yhour	mov		a,59    mov     yminute,a

py_ret:	ret

;///
py_st:	dec		yminute

		sz		yminute	ret	sz		yhour	ret

py_off:	clr		flh_flag
		call	beep_1
		ret

;//>>>>>>>>>>new part <<<<<<<<<<<<<<<
;/************************************/
;/*	断续加热控制子程序					*/
;/************************************/
tiaogong: 
		nop
		nop

		sz		bwarmh	jmp		tg_clr	mov		a,tiaojs	sub		a,tiao_zong	snz		c	jmp		tg_s1		set		bheatyes

tg_clr:	clr		tiaojs
tg_ret:	ret


tg_s1:	mov		a,tiaojs
		sub		a,tiao_on
		snz		c
		jmp		tg_s2
		clr		bheatyes
		
tg_s2:	inc		tiaojs
		ret

;//********************************/ 
;//*  function
;//********************************/
function:
		nop
		nop
		nop		
		sz		byuyuests
		ret
		

		snz		bonoff	ret	sz		berror	ret		

;=========note1 烧水功能干烧保护 ==========================
        nop
        nop 		
		

		snz		bguoon	clr		oldhuoli	mov		a,current	add		a,20	sub		a,20h		sz		c	jmp		fun_s1	mov		a,0feh	jmp		fun_s2

fun_s1:	add		a,20h					
fun_s2:		
		sub		a,cur500ms
		snz		c
		clr		oldhuoli
		

		mov		a,current	mov		cur500ms,a	mov		a,delay30sjs	sub		a,dtemp_150s	snz		c	inc		delay30sjs

;=======================================
		

		mov		a,mode    sub     a,m_huoguo    sz      z    jmp     huo_guo        mov		a,mode    sub     a,m_wuhuo    sz      z    jmp     huo_guo         mov		a,mode    sub     a,m_wenhuo	    sz      z    jmp     huo_guo        sz      btempsts       jmp     control_temp	        mov		a,mode    sub     a,m_soupzhou    sz      z	    jmp     bao_zhou        mov		a,mode    sub     a,m_zhou    sz      z	    jmp     bao_zhou        mov		a,mode    sub     a,m_zheng    sz      z	    jmp     bao_zhou        mov		a,mode    sub     a,m_zhufan    sz      z	    jmp     zhu_fan    		    mov		a,mode    sub     a,m_shaoshui    sz      z		    jmp     shao_shui        mov		a,mode    sub     a,m_milk    sz      z	    jmp     heat_milk    	ret

   ;/////huo guo ///////
huo_guo:
		nop
		nop
    	mov		a,dsphuoli		 	
hg_run:
    	mov		heathuoli,a    	    	
    	call	runpower
fcp_ret:
    	ret

;/************************************************/
;/*bao tang food function:(mode=8)			    */
;/************************************************/
bao_zhou:
		nop
		nop

		sz		comm_state
		jmp		bt_s1
		call	huo_guo
		
		mov		a,minjs
		sub		a,16+1
		sz		c
		jmp		bt0_com
		
		add		a,17
		sub		a,13
		snz		c
		ret
		
		mov		a,dtemp1
		sub		a,18h*2
		snz		c
		ret

bt0_com:
		mov		a,1
    	mov		comm_state,a
    	mov		a,minjs
    	mov     menujs,a
bt1_ret:
    	ret

;///
bt_s1:  mov		a,p_800
		mov		dsphuoli,a
		mov		heathuoli,a
		

		nop


​		

		mov 	a,m_zheng	sub 	a,mode	sz		z	jmp 	huo_guo	   	mov		a,20    mov		tiao_zong,a    mov		a,14    mov		tiao_on,a        mov		a,minjs    sub		a,menujs	mov		temp0,a		sub		a,13	snz		c	jmp		bt3_next		            mov		a,12    mov		tiao_on,a        mov		a,43    sub		a,temp0    sz		c    jmp		bt3_next    		    mov		a,8    mov		tiao_on,a

bt3_next:
        jmp     heatonoff


;*******************************
;heat milk:
;*******************************
heat_milk:
		mov		a,2fh
		mov		temp0,a
		mov		a,2ch
		mov		temp1,a

		mov		a,temp0	sub		a,temp_main	sz		c	jmp		hm_s1	set		bbaowen	jmp		hm_end

;///
hm_s1:	mov		a,temp1
		sub		a,temp_main
		snz		c
		jmp		hm_end
		clr		bbaowen

hm_end:	sz		bbaowen
		jmp		set_noheat
		jmp		huo_guo


;**************************
;shao shui:
;***************************
shao_shui:
        call    huo_guo
        snz		bshuikai
        ret
		jmp		power_off
		
;**************************
;zhu fan:
;***************************
zhu_fan:
		sz		comm_state
		jmp		fz_s1
		
;///
fz_s0:	call	huo_guo
		mov		a,4
		sub		a,minjs
		sz		c
		jmp		fz_com
				

		mov		a,7	sub		a,minjs	sz		c	jmp		set_noheat								mov		a,12	sub		a,minjs	snz		c	jmp		fz0_com		mov		a,10	sub		a,minjs	sz		c	jmp		fz_com		mov		a,dtemp1	sub		a,1bh*2	sz		c	jmp		fz0_com

fz_com:	mov		a,minjs
		sub		a,2
		snz		c
		ret
		mov		a,temp_main
		sub		a,98h
		snz		c
		ret
		
fz0_com:
		mov		a,1
		mov		comm_state,a
		mov		a,minjs
		mov		menujs,a
		ret

;///
fz_s1:	mov		a,p_800
		mov		dsphuoli,a
		mov		heathuoli,a
		

		nop


​		

		mov		a,20	mov		tiao_zong,a	mov		a,14	mov		tiao_on,a		mov		a,minjs	sub		a,menujs	sub		a,4 	snz		c	jmp		heatonoff	mov		a,10	mov		tiao_on,a		mov		a,minjs	sub		a,menujs	sub		a,14	snz		c	jmp		heatonoff		mov		a,6	mov		tiao_on,a	jmp		heatonoff

;/************************************************/
;/*shaokao function:(mode=4)				    	*/
;/************************************************/
control_temp:
		nop
		nop
		
				 

		mov		a,dsphuoli		    dec		acc    add		a,tabtemph    	nop

ctrl_t2:       
       	nop 
       	mov		tblp,a
		tabrdl	acc
     

     	sub		a,temp_main 	mov		temp0,a  	 	sz		c 	jmp		bw_s1 	set		bbaowen

bw_com: jmp     set_noheat
               
;////
bw_s1:  sub		a,8
		sz		c
		jmp		bw_s2
					

		sz		bbaowen	    jmp		bw_com

;///
bw_s2:  clr		bbaowen
		
			

		mov		a,dsphuoli	sub		a,p_1000	snz		c	jmp		bw_s3		call	huo_guo	ret

bw_s3:	mov		a,p_1000		
		jmp		hg_run
		
;//************************************************/
;//*	runpower function:
;//************************************************/
runpower:
		sz		bwarmh
		jmp		set_noheat
		
		

		nop	nop	nop           mov		a,igbt_90	sub		a,temp_igbt	sz		c	jmp		rp_s1	set		bigbtwarm 	jmp		rp_chk 

;///
rp_s1:	mov		a,igbt_80
		sub		a,temp_igbt
		snz		c
		jmp		rp_chk 
		clr		bigbtwarm

rp_chk:	snz		bigbtwarm
		jmp     rp_start
		

		mov		a,heathuoli  	sub		a,p_1300	snz		c	jmp     rp_start	mov     a,p_1300	mov		heathuoli,a

;///        
rp_start:
		mov		a,20
		mov		tiao_zong,a
				

		mov		a,heathuoli	sub		a,p_1000	nop	nop	sz		c	jmp		rp_s2        mov		a,heathuoli    dec		acc    nop    add		a,tabtiaoon       	   	nop   	mov		tblp,a	tabrdl	tiao_on    jmp		rp_com

rp_s2:  clr		tiao_on
		clr		tiao_zong

rp_com: 
heatonoff:
		snz		bheatyes
		jmp		hof_s1
		clr		bheatno
		set		bheate
		ret
		
hof_s1: 
set_noheat:
		set		bheatno
		clr		bheate
rp_ret:	ret

;=======>new part <===================
;*************************************
;key_tprog  
;*************************************
key_prog:
		nop
		mov		a,keydat6
		sub		a,00h
		snz		z
		jmp		kp_s11
				

		clr		bkeyrls		clr		bfastadd  	clr		bfastsub  	clr		btemplock		

kp_ret:
		ret
		
kp_s11: 
		sz		bfastadd
		jmp		kp11_a
		snz		bfastsub
		jmp		kp_s12 


kp11_a:	snz		badt300ms
		ret
		clr		badt300ms
		

		mov		a,0d8h	mov		adt300msjs,a		mov		a,10 	mov		temp1,a 		sz		k_tadd    jmp 	add_1mfast	sz		k_tsub    jmp 	sub_1mfast     ret

kp_s12:        
		sz		bendspall
		ret		
		

		sz		bkeyrls	jmp		kp_ret	set		bkeyrls				 				nop	nop	nop	;sz      block	;jmp     kp_lock						sz		k_tstart    jmp 	key_start        snz		bbusysts    ret         snz		bonoff    jmp		kp_tmenu

kp_lock:        
        snz		k_tlock
		jmp		kp2_111 
		

        sz      btemplock    jmp     tim_cllk1    set     btemplock    jmp     tim_bz1

tim_cllk1:        
        clr     btemplock
tim_bz1:        
        clr     lockjs
        ret
;////		
kp2_111:
		sz		block
		ret	        
              

        sz		k_tadd    jmp 	key_add        sz		k_tsub    jmp 	key_sub    	sz		k_ttimer   	jmp		key_dingyu		;定时，预约键        snz		k_tcoulo    jmp		kp_tmenu        	inc		seep_state   	mov		a,seep_state   	sub		a,3   	snz		c   	jmp		bp_com    jmp     kp7_bp

kp_tmenu:
		snz		k_tmenu
        ret ;jmp		kp_tmenu2      
        nop
        nop 
        inc		modejs
        mov		a,modejs
        sub		a,8+1		;火锅，爆炒，烧烤，热奶，烧水，蒸煮，煲汤
        snz		c
		jmp		md_com3	 
		mov		a,1
 		mov		modejs,a
md_com3:       
        mov		a,modejs  
        dec		acc
        nop
        add		a,tab_mode_a36		
        nop
       	mov		tblp,a 
 		tabrdl	acc
       	mov		mode,a
		jmp		kp_next

;kp_tmenu2:
;		snz		k_tmenu2
;        ret 
;		nop
;        nop 
;        inc		modejs
;        mov		a,modejs
;        sub		a,8+1		;火锅，爆炒，烧烤，热奶，烧水，蒸煮，煲汤
;        snz		c
;		jmp		md_com8	 
;		mov		a,1
; 		mov		modejs,a
;md_com8:       
;        mov		a,modejs  
;        dec		acc
;        nop  
;        add		a,tab_mode_f12		
;        nop
;       	mov		tblp,a 
; 		tabrdl	acc
;       	mov		mode,a
kp_next:		
		call    power_com
		jmp		kp7_bp 
				
		           
;//******************************
;//start key handle part
;//******************************
key_start:			
		sz		berror
		jmp		ks_off
		snz		bbusysts ;bonoff
    	jmp		ks_on
	
ks_off: call    er_realcan
		call	power_off
		ret
		
;///
ks_on: 	set		bbusysts ;bonoff
    	clr		jianguojs
    	
;    	mov		a,m_huoguo
;    	mov		mode,a
;    	mov		modejs,a
;    	call	power_com
    	
ks_com: clr		bwarmh
		call    er_realcan
    	
kp7_bp: clr		seep_state
bp_com: clr     seecoulo15sjs
		call	beep_1
	    ret

;//******************************
;//add key handle part
;//******************************
key_add:
		snz		bflash
		jmp		ka_s1
		mov		a,1
		mov		temp1,a
		call	add_1m
        jmp		ksbf_com

ka_s1:	sz		bautomenu
		ret

		mov		a,dsphuoli		sub		a,huoli_number			sz		c	jmp		ka_ret	inc		dsphuoli


​			        
ka_beep:
​		clr		bdiscursurge

		mov		a,13	mov     dspparamjs,a	clr		delay30sjs

kd_beep:
        call     kp7_bp 
ka_ret:
	    ret
;//******************************
;//sub key handle part
;//******************************
key_sub:
		snz		bflash
		jmp		ks_s1
		mov		a,1
		mov		temp1,a
		call	sub_1m
ksbf_com:
		mov		a,0d0h
		mov		adt300msjs,a
        jmp		kd_beep

ks_s1:	sz		bautomenu
		ret
		
		
		

    	mov		a,dsphuoli	sub		a,2	snz		c	jmp		ka_ret	dec		dsphuoli	jmp		ka_beep

;//****************************
;//timer key handle part
;//****************************
key_dingyu:
		nop
		nop
		snz		bendspdebug
		jmp		kt_real

		call	beep_1	inc		debug_stage	mov		a,debug_stage	sub		a,9	snz		c 	jmp		kt_ret	clr		debug_stage

kt_ret:	ret

;///
kt_real:
		sz		bautomenu
		jmp		key_yuyue

kt_start:		
		sz		bsettimests
		jmp		kt_clr
		clr		minutet
		
ktt_s3:	set		bsettimests
		set		bflhdin
		
ktt_s4:	set		bflash
    	call    ad1m_ret
		jmp		kt_beep		

;///		
kt_clr:	clr		bflhdin
		clr		bflash
		clr		bsettimests
		
get_timing:
		mov		a,mode
        dec		acc
        nop
        add		a,tab_minute
       	nop
       	mov		tblp,a
		tabrdl	tminute
kt_beep:
		call	kp7_bp	
ky_ret:
		ret			
	
;******************************
;appointment key handle part:
;******************************
key_yuyue:
		snz		bautomenu
		ret
		sz		byuyuests
		jmp		kdy_s3
				

        clr		yhour    clr     yminute

ky_com: set		byuyuests
		set		bflhyu
        jmp     ktt_s4
                                    
kdy_s3: clr		flh_flag
	    jmp		kt_beep	

;***************************
;定时按键的处理：
;只有定时功能的处理
;***************************
;key_timer:
;		snz		bendspdebug
;		jmp		ktt_debug

;		call	beep_1
;		inc		debug_stage
;		mov		a,debug_stage
;		sub		a,8
;		snz		c
;		jmp		kt_ret
;		clr		debug_stage
;		ret

;ktt_debug:
;		sz		bautomenu
;		ret
;		jmp		kt_start

;//******************************   
;//power status common operate
;//******************************
power_com:
		nop
		set		bonoff
		nop
		nop       	
		call    get_timing
		mov		a,mode
        dec		acc
        	

        add		a,tabhuoli

pw_s2:
       	mov		tblp,a
       	tabrdl	acc
pw_s3:
		mov		dsphuoli,a
		mov		heathuoli,a
		mov		ledhuoli,a	 	;全灯火力调用
;//*********************************
;//menu initialize :
;//*********************************
init_menu:
		mov		a,13
	    mov     dspparamjs,a
	    clr		bdin1min
	    

	    mov		a,offset y1mjsl	;yclear		
	    ;clear new mode 	
	    call	clr_ram        
	    mov		a,mode    
	    sub		a,m_huoguo   
        sz		z    
        ret	        
        mov		a,mode    
        sub		a,m_wuhuo    
        sz		z    
        ret	             
        mov		a,mode   
        sub		a,m_shaokao    
        sz		z   
        jmp		im_temp       
        mov		a,mode   
        sub		a,m_chaocai   
        sz		z    
        jmp		im_temp        
        mov		a,mode    
        sub		a,m_jianchao   
        sz		z    
        jmp		im_temp        
        mov		a,mode   
        sub		a,m_baochao   
        snz		z    
        jmp		im_auto

im_temp:	    
	    set		btempsts 
	    ret

;////
im_auto:	
		set		bautomenu
		mov		a,mode
	    sub		a,m_warm
	    sz		z
	    jmp		im_temp		
    	ret      
;//********************************
;//adjust hour value
;//********************************
add_1m:	set		bfastadd
		clr		bfastsub
		
add_1mfast:
		sz		bflhyu
		jmp		a1m_yu
		  

		mov		a,temp1	
		addm	a,minutet		
        mov		a,minutet		
        sub		a,180+1

a1m_aaa:
		snz		c
		jmp		ad1m_ret
		clr		minutet

ad1m_ret:
	    clr		badt300ms
		clr		confirm5sjs
		clr		flh_500ms	
		;mov	a,1
		;mov	flh_second,a
	    set		bsnd0
	    ret    

;///
a1m_yu:	mov		a,1  
a1m_com:
		addm	a,yminute
		mov		a,yminute
		sub		a,60
		snz		c
		jmp		ad1m_ret
		mov		yminute,a
		

		inc		yhour	
		mov		a,yhour	
		sub		a,24	
		snz		c	
		jmp		ad1m_ret	
		clr		yhour	;clr	yminute	
		jmp		ad1m_ret

;//********************************
;//adjust hour value
;//********************************
sub_1m:	clr		bfastadd
		set		bfastsub  
	     
sub_1mfast:
		snz		bflhyu
		jmp     s1m_a
		mov     a,60
		jmp		a1m_com  ;s1m_yu
        
s1m_a:	mov		a,minutet
		sub		a,temp1
		sz		c
		jmp		s1m_b
	

		mov		a,180

s1m_b:  mov		minutet,a			
	    jmp		ad1m_ret	
    
;///	dec 1 minute
s1m_yu:	sz		yminute
		jmp		s1m_decm
		sz		yhour
		jmp		s1m_dech
		mov		a,23
		mov		yhour,a
		jmp		s1h_com

s1m_decm:
		dec		yminute
		jmp		ad1m_ret

s1m_dech:
		dec		yhour
s1h_com:
		mov		a,59
		mov		yminute,a
		jmp		ad1m_ret

;************************************************
;A/D convert routine(2.5ms一次)
;************************************************
ad_prc:	
		nop
		mov  	a,ch_igbt
  		mov  	adcr,a
  		set     start
  		clr     start
adigbt:	sz      EOCB
        jmp     adigbt
        mov     a,adrh
        addm    a,igbtl
        sz      c
        inc     igbt_h
        
;++++++++++++++++++++++++++++        
        mov  	a,ch_main
	  	mov  	adcr,a
	  	set     start
	  	clr     start
admain:	sz      EOCB
        jmp     admain
        mov     a,adrh
        addm    a,mainl
        sz      c
        inc     mainh
        
;++++++++++++++++++++++++++++
		mov  	a,ch_vol
	  	mov  	adcr,a
	  	set     start
	  	clr     start
advin:	sz      EOCB
        jmp     advin
        mov     a,adrh
        addm    a,voll
        sz      c
        inc     volh
        
;++++++++++++++++++++++++++++
		nop
		call	get_curad
		call	get_curad
		call	get_curad
		call    get_curad
		call    get_curad
		call    get_curad
		nop
		
;;++++++++++++++++++++++++++++
		sdz		adjs
		jmp		adcount
		mov		a,128
		mov		adjs,a
		rlc		igbtl
		rlca	igbt_h
		sz		igbtl.7
		inc		acc
		mov		temp_igbt,a
		clr		igbtl
		clr		igbt_h	
				

	;///get temp main a.d convert/////	
	rlc		mainl	
	rlca	mainh	
	sz		mainl.7
    inc		acc
    mov		temp0,a	
    clr		mainl	
    clr		mainh		
    sub		a,10h	
    snz		c	
    jmp		ap_com	
    add		a,10h		
    mov		a,temp_main
    add		a,2	
    mov		temp1,a						
    mov		a,temp0	
    sub		a,temp1 ;temp_main+2	
    snz		c	
    jmp		adm_s1	
    dec		temp0	
    jmp		ap_com

adm_s1:	add		a,temp1
		add		a,4     ;2    note
		sub		a,temp1
		

		snz		c	
		jmp		adm_s2		
		mov		a,tmainjs	
		sub		a,0f8h ;A0h		;由于AD得出时间少了一半；	
		sz		c	
		jmp		apc_b	
		inc		tmainjs	
		jmp		ad_vol

adm_s2:	inc		temp0
	
;///
ap_com:	set		bshuiup
		mov		a,temp0
		sub		a,temp_main
		sz		c
		jmp		apc_a			
		clr		bshuiup
		
apc_a:	mov		a,temp0
		mov		temp_main,a
		
apc_b:	mov		a,tmainjs
		mov		dtemp1,a
		clr		tmainjs		
		

		nop	
		call	chk_kaishui	
		nop
		call	det_ganshao	
		nop	;///voltage a.d///// 

ad_vol:
		mov		a,vol_in
		mov		temp0,a
			

		rlc		voll	
		rlca	volh	
		sz		voll.7	
		inc		acc	
		mov		vol_in,a	
		clr		voll	
		clr		volh	;////handle voltage	surge///	
		sub		a,vol_disguo	
		sz		c	
		jmp		ah0_surge			
		add		a,vol_disguo	
		sub		a,temp0	
		sz		c	
		jmp		ah0_s1		
		mov		a,temp0	
		sub		a,vol_in

ah0_s1:	sub		a,25
		snz		c
		jmp		adcount
ah0_surge:
		nop
		call	dp_surge
		nop		
		
;++++++++++++++++++++++++++++
adcount:mov		a,adjs
		and		a,0fh  ;1fh
		sz		acc
		ret
	

	;///cur: 96/64 =>1.5

;++++++++++++++++++++++++++++
		mov		a,current
		mov		temp0,a

		mov		a,curc	
		mov		curd,a	
		mov		a,curb	
		mov		curc,a	
		mov		a,cura	
		mov		curb,a	  	
		rlc		curl	
		rlc		curh	
		rlc		curl	
		rlca	curh	
		mov		cura,a	
		mov		curl,a	
		clr		curh	
		mov     a,curb    
		addm    a,curl    
		sz      c   
        inc     curh	
        mov     a,curc    
        addm    a,curl   
        sz      c    
        inc     curh    	
        mov     a,curd    
        addm    a,curl    
        sz      c    
        inc     curh   ;///curh,curl/4       
        clr		c	
        rrc		curh		;high	
        rrc		curl		;low        
        clr		c	
        rrc		curh		;high	
        rrca	curl		;low   			
        mov		current,a		
        set		bheat40ms 		;///判断是实际加热的初始值;还是真正要用的值		
        sz		init_cur	
        jmp		adc_aaa	
        jmp		adc_bbb

adc_aaa:
		mov		a,current
		sub		a,init_cur
		snz		c
		jmp		adc_bbb
		mov		current,a

adc_bbb:		
		clr		curl
		clr		curh
		clr		cur0

		sub		a,cur_max+10
		sz		c
		jmp		acc_limit
		
	;////handle current surge ////
		mov		a,current		
		sub		a,temp0 
		snz		c 
		jmp		acc_s1
		nop
		nop
		sub		a,20
		sz		c
		jmp		acc_limit

acc_s1:	
		snz		bdiscursurge
		ret
		

	;==================	
		mov		a,valuecur
		add		a,10
		mov		temp0,a
		
		sub		a,90h
		sz		c
		jmp		apc_bbb
		mov		a,90h
		mov		temp0,a

apc_bbb:	
		mov		a,current
		sub		a,temp0
		snz		c
		ret  
		
acc_limit:
		mov		a,ppgta		;pwm>   
		sub		a,pwm_on
		sz		c
		ret					;pwm < 91h
		mov		a,pwm_on
		mov		ppgta,a  
		ret

;*************************
;get current ad:
;*************************
get_curad:
		mov  	a,ch_cur
	  	mov  	adcr,a
	  	set     start
	  	clr     start
adcur:	sz      EOCB
        jmp     adcur

        mov		a,adrl	    
        or		a,0fh    
        addm	a,cur0    
        sz		c    
        inc		curl        
        mov     a,adrh   
        sub		a,0a9h    
        snz		c	
        jmp		gc_s1    
        mov		a,0a9h		

gc_s2:	addm    a,curl
        sz      c
        inc     curh
		ret

;///
gc_s1:	mov		a,adrh
		jmp		gc_s2


;//*********************************
;//check shui kai program
;//*********************************
chk_kaishui:
		nop		
		snz		control_igbt
		jmp		ck_clr	

		mov		a,shui_25m 	
		mov		temp1,a	
		mov		a,shui_15m 	
		mov		temp2,a	
		mov		a,shui_dstart	
		mov		temp3,a		
		mov		a,vol_in	
		sub		a,vol_210	
		sz		c	
		jmp		ck_s1

;///由于钭率值比以前缩小了一半时间
;所以以前/2的都不要除以2
		

		mov		a,vol_210	
		sub		a,vol_in	
		mov		temp4,a		
		clr		c	
		rlc		acc	
		addm	a,temp3		
		mov		a,temp4	
		clr		c	
		rrc		acc	
		clr		c	
		rrc		acc	
		addm	a,temp1	
		clr		c	
		rrc		acc	
		addm	a,temp2

;///		
ck_s1:  mov		a,minjs
		sub		a,temp1
		sz		c
		jmp		ck_ok
		

		add		a,temp1	
		sub		a,temp2	
		snz		c	
		jmp		ck_clr		
		snz		bshuiup	
		ret					
		mov		a,temp_main			;水温大于85度的温度	
		sub		a,main_85	
		snz		c	
		ret	             
		mov		a,dtemp1    
		sub		a,shui_maxt    
		sz		c    
		jmp		ck_ok                            		
		add		a,shui_maxt	
		sub		a,temp3
        snz		c	
        ret	
        inc		dshaoshuijs	
        mov		a,dshaoshuijs	
        sub		a,dtemp_shui10t	
        sz		c	
        jmp		ck_ok		
        mov		a,temp3	
        add		a,shui_pclv28t   ;注意，要考虑到最小电压的工作情况	
        sub		a,dtemp1	
        sz		c	
        ret		
        mov		a,dshaoshuijs	
        sub		a,dtemp_shui7t	
        snz		c	
        ret

ck_ok:				
		set		bshuikai 
		  
		              
ck_clr: clr     dshaoshuijs
        ret

;====================================
;detect gan shao program:
;====================================
det_ganshao:
        snz		control_igbt
        jmp		cg_clr
        

		mov		a,minjs	
		sub		a,2	
		snz		c	
		jmp		cg_clr		
		mov		a,temp_main	
		sub		a,main_210	
		sz		c	
		jmp		cg_gan	   	
		snz		bshuiup   	
		jmp		cg_clr   	   
        mov		a,delay30sjs	;抖锅延时处理;   	
        sub		a,dtemp_150s   
        snz		c   	
        jmp		cg_clr       	
        mov		a,temp_main   	
        sub		a,main_140   	
        snz		c   	
        jmp		cg_clr        
        mov		a,dtemp1    
        sub		a,dtemp_ganshao    
        sz		c    
        jmp		cg_clr	        
        inc     dganshaojs	
        mov		a,dganshaojs	
        sub		a,dtemp_7t	
        snz		c	
        ret

cg_gan:	set    bganshao
cg_clr: clr    dganshaojs
		ret


;**************************************
;timer0 interrupt service(2ms)
;**************************************
timer0:		;clr	wdt2
			;set	f_2ms
			;reti			
			SAV_DATA 
			clr		wdt2
			set		f_2ms
			
			
			

			inc		t1mjsl
			mov		a,t1mjsl 
			sub		a,231		;40

t0_s1:		snz		c  
			jmp		it0_yu
			clr		t1mjsl
			set		bdin1min		 

it0_yu:		inc		y1mjsl 
			mov		a,y1mjsl
			sub		a,231 	 ;40
			snz		c
			jmp		IT0_RET   
			clr		y1mjsl
			set		byu1min
				    		
IT0_RET:	
			RES_DATA
			RETI
	
;**************************************
;interrupt 0 interrupt service(2ms)
;high voltage protect
;**************************************	
ext_int0:	;sav_data
			mov		backup_acc,a
			mov		a,status
			mov		backup_status,a
			inc		dpanjs  
			jmp		int_com
			
;**************************************
;comparator 1 interrupt service(2ms)
;surge voltage protect
;**************************************	
ext_cmp1:	
		

		;==== note2 高压保护宽度侦测的保护 	
		;========浪涌电压宽度侦测的处理======		
		sz		c1cmpop			;若宽度比较窄		
		jmp		ext_cmp1_s1				
		snz		c1cmpop			;若宽度比较宽及更宽的处理;		
		jmp		ext_cmp2

;======加8次================			
			sav_data
			mov		a,7
			addm	a,ppgta

ext_cmp1_com:			
			inc		ppgta
			mov		a,25
			mov		highvoljs,a		;25*60=1.5s disable dec ppgta
			jmp		int_com

ext_cmp1_s1:			
			sav_data
			jmp		ext_cmp1_com
			
;===============================
ext_cmp2:	
			clr		prsen
			clr		pst
			clr		ppgc
			clr		wdt2
			sav_data
			mov		a,pwm_on 			;(512-1bb)*0.25
			mov		ppgta,a
			set		bsurge
			clr		langyongjs
			clr		control_igbt
			clr		bheatno
			clr		bheate
			clr     nopanoffjsh
			mov		a,delay_check
		   	mov	    pwmdly1sjs,a
		   	

		   	set		byanguo	   
            clr		dtime5sjs

int_com:	
			res_data
			reti
	
;**************************************
;Standby Mode
;**************************************
stan_clr:
Clr_Ram:	;Clr	Wdt
			Mov		Mp0,A
			Clr		R0
			Inc		Acc
			Sz		Acc
			Jmp		Clr_Ram
			Ret			
 		
;;*****************************************************************************
;;sen_part		发送数据处理
;;*****************************************************************************
;;***********************************************************************************
;;通讯程序 
;;***********************************************************************************
;主芯片不断发送显示码到显示芯片，2帧码间隔30MS的高电平，一帧码长56位约84ms，
;其中，低:高=1ms:500us表示1，500us:1ms表示0，如下图

;一帧码共64位，DATA0-DATA7.
;DATA0为起始码，为固定值F0
;DATA1-DATA7为显示码，1有效
;DATA1，数码管第1位
;DATA2，数码管第2位
;DATA3，数码管第3位
;DATA4，数码管第4位
;DATA5-DATA6显示LED
;;***************************************************************************
timer1:		
		sav_data
		clr		wdt2
		
;		mov		a,8
;		mov		beep_count0,a
;		set		bze		;enable buz
;		set		p_buz      ；调试时候用
			 
IT1_puls:
		snz		control_igbt
		jmp		timer1_mai_clrt
		  

		snz		PPGC.6
		jmp		timer1_mai_clrt
	
		SZ		EIF
		JMP		timer1_mai_cp 
		inc		r_nopan 
		SNZ		r_nopan.1
		JMP		timer1_ret
	
		mov		a,1
		mov		r_nopan,a
				
		mov		a,ppgta
		mov		pwm_zhiqian,a
				
		mov		a,PWM_ON		
		mov		ppgta,a
			
		mov		a,01100100b
		mov		ppgc,a
			
		SNZ		EIF
		set		pst	
		nop
		nop
		nop
		nop
		nop
		nop
		nop
		mov		a,pwm_zhiqian
		mov		ppgta,a
		CLR		EIF
		jmp		timer1_ret

timer1_mai_cp:
		mov		a,1
		mov		r_nopan,a
		CLR		EIF 
		JMP		timer1_ret
timer1_mai_clrt:  
		clr		r_nopan
timer1_ret:	
		
									
;***************************************************************
;;send_part:  
;;*****************************************************************							
send_part:		           
		nop 			                                          
        sz		senddelay	
		jmp		send_dec	 
		jmp		send_tar 
send_dec:	
		mov		a,senddelay
		nop
		nop
		nop
		sub		a,80		;80*0.125=10ms
		snz		c
		jmp		send_dec2
		dec		senddelay	  	  
		clr    	p_outdata 
		jmp		res_ret
		 
send_dec2:	  
		dec		senddelay		 
		set    	p_outdata
		jmp		res_ret  		
send_tar:	
		sz		send1js
		jmp		sendreset				 
		sz		send0js
		jmp		sendreset 
	                                                                      

        sz		sendjs		
        jmp		send_start		            
        mov		a,64    
        mov		sendjs,a         
        mov		a,85      
        nop    
        mov		senddelay,a                   
        set		b_secok                  
        clr		send0js    
        clr		send1js                    
        jmp		send_low1                   

send_start:   		
		nop
		nop		
		dec		sendjs         
        clr		c               
        rlc		run_ram0		;校验码		0=1+2+3+4+5+6
        rlc		run_ram6
        rlc		run_ram5
        rlc		run_ram7                
        rlc		run_ram4
        rlc		run_ram3   
        rlc		run_ram2 
        rlc		run_ram1         
        sz     c
        jmp     sendhigh        
send_low:        
        mov    a,4				;500us
        mov    send1js,a		
        mov    a,8				;1ms
        mov    send0js,a		
        jmp    sendreset
         
sendhigh:
		mov    a,8				;1ms
        mov    send1js,a		
        mov    a,4				;500us
        mov    send0js,a		        
sendreset: 
			                                      
send_h1:     
		sz     send1js 
        jmp    send_l2 
        jmp    send_l1
send_l2:
        dec    send1js   
send_low1:        
        clr    p_outdata  
        jmp	   res_ret        
send_l1:   
		dec    send0js		
		set    p_outdata									           									
res_ret:														
;>>>>>>>>>>new part <<<<<<<<<<<<<<<<<
;===================================================
;发送口平时为高电平，
;2个下降沿为一位码，一位码长3MS，其中，低电平2MS，高电平1MS表示1；低电平1MS，高电平2MS表示0,如下图：
;K1：A15E
;K2：A25E
;K3：A35C
;K4：A45B
;K5：A55A
;K6：A659
;K7：A758
;===================================================			        
rec_part:  
		nop
		sz	   bendspall	;上电全亮过程中不发送及接收数据
        jmp	   rec_ret 	 
		set		pbc5 
		nop
		nop
		sz		p_uart_in
		jmp		rec_s1	
				 	

		inc		plowjs  		;低电平计数器		
		sz		phighjs
		jmp		rec_s5
		jmp		rec_s4

rec_s5:
		mov		a,phighjs
		mov		oldphighjs,a
		clr		phighjs		
rec_s4:					
		set		p_status  		;记录当前的状态位,允许进行更新数据
		jmp		rec_ret		

;;******************																		
rec_s1:	
		inc		phighjs						
		snz		p_status  
		jmp		nt_s2
		clr		p_status
		

		sz		oldplowjs
		jmp		rec_s2
		mov		a,plowjs
		mov		oldplowjs,a
		clr		plowjs
		clr		oldphighjs 	
		jmp		rec_ret		

rec_s2:					
		mov		a,oldplowjs	
		sub 	a,oldphighjs					
		rlc		uartrevbytel
		rlc		uartrevbyteh
						

		clr		oldphighjs 					
		mov		a,plowjs	
		mov		oldplowjs,a	
		clr		plowjs		 			
		jmp		rec_ret	 		

;///		
nt_s2:		
		mov		a,phighjs 
		sub		a,150			;130*0.125=16ms
		snz		c
		jmp		rec_ret								
		set		brecok 
																				
rec_ret:
		res_data
		reti
						
;*****************************
;uart debounce:数据处理部分
;一共接收8位数据，数据分别为:高四位按键键值,低四位火力值
;火力值包括：1--8为火力档，9为停止加热
;按键值包括：1--5为正常键值，6为键值加温度模式，7为键值加煮饭模式，
;buz  benheat   dsphuoli
;*****************************
uart_debounce:		
		sz		bendspall		;上电不判断结果
		ret
		

		snz		brecok			;已经接收到数据了	
		ret	
		clr		brecok	 	
		clr		phighjs						;====scan_key=====		
		nop	
		nop		 	
		;mov		a,0h	
		;mov		keydat6,a			
		mov		a,uartrevbyteh		;无按键状态	
		sub		a,0ffh	
		snz		z	
		jmp		ud_a11			
		mov		a,uartrevbytel		
		sub		a,00h	
		snz		z	
		jmp		ud_end					
		mov		a,0h	
		mov		keydat6,a			
		jmp		ud_end

ud_a11:						
		mov		a,uartrevbyteh	
		sub		a,0a1h
		snz		z
		jmp		ud_a1		
		mov		a,uartrevbytel	
		sub		a,05eh
		snz		z
		jmp		ud_end		
		set		keydat6.0 
		jmp		ud_end		
ud_a1:		
		mov		a,uartrevbyteh	
		sub		a,0a2h
		snz		z
		jmp		ud_a2		
		mov		a,uartrevbytel	
		sub		a,05dh
		snz		z
		jmp		ud_end		
		set		keydat6.1 
		jmp		ud_end		
ud_a2:	
		mov		a,uartrevbyteh	
		sub		a,0a3h
		snz		z
		jmp		ud_a3		
		mov		a,uartrevbytel	
		sub		a,05ch
		snz		z
		jmp		ud_end		
		set		keydat6.2
		jmp		ud_end		
ud_a3:		
		mov		a,uartrevbyteh	
		sub		a,0a4h
		snz		z
		jmp		ud_a4		
		mov		a,uartrevbytel	
		sub		a,05bh
		snz		z
		jmp		ud_end
		

		set		keydat6.3	
		jmp		ud_end		

ud_a4:
		mov		a,uartrevbyteh	
		sub		a,0a5h
		snz		z
		jmp		ud_a5		
		mov		a,uartrevbytel	
		sub		a,05ah
		snz		z
		jmp		ud_end		
		set		keydat6.4
		jmp		ud_end		
ud_a5:
		mov		a,uartrevbyteh	
		sub		a,0a6h
		snz		z
		jmp		ud_a6		
		mov		a,uartrevbytel	
		sub		a,059h
		snz		z
		jmp		ud_end		
		set		keydat6.5
		jmp		ud_end		
ud_a6:
		mov		a,uartrevbyteh	
		sub		a,0a7h
		snz		z
		jmp		ud_a7		
		mov		a,uartrevbytel	
		sub		a,058h
		snz		z
		jmp		ud_end		
		set		keydat6.6	
		jmp		ud_end
ud_a7:		
		mov		a,uartrevbyteh	
		sub		a,0a8h
		snz		z
		jmp		ud_end		
		mov		a,uartrevbytel	
		sub		a,057h
		snz		z
		jmp		ud_end		
		set		keydat6.7								
ud_end:				
		clr		uartrevbytel
		clr		uartrevbyteh
		ret
;		 			
 												

			ORG		0f00H			

;====================================
;display  digit list 
;====================================			
tabnum:
DIGITLIST:	DC		SYM_0
			DC		SYM_1		
			DC		SYM_2       
			DC		SYM_3		
			DC		SYM_4		
			DC		SYM_5		
			DC		SYM_6		
			DC		SYM_7		
			DC		SYM_8		
			DC		SYM_9	
			DC		SYM_a		
			DC		sym_b		
			DC		sym_c		
			DC		sym_d		
			DC		sym_e
			DC		sym_f		
			DC		SYM_OFF
						
tab_125pwmmax:	
		  	dc		68h	
		  	dc  	68h		 
			dc  	68h	
			dc  	68h	
			dc  	60h
			dc 	 	58h  	 
			dc		48h 	 
			dc		38h  						
tab_165pwmmax:	
		  	dc		68h	
		  	dc  	68h		 
			dc  	68h	
			dc  	68h	
			dc  	58h 
			dc 	 	48h 	
			dc		38h 	 
			dc		30h   
	 
tab_125hvol:
           	dc		00000000b	;0.60vdd
		  	dc  	00000000b	;0.60vdd
			dc  	00000000b 	;0.60vdd 
			dc  	00000000b	;0.60vdd 		
			dc		00000001b	;0.60vdd
		  	dc  	00000001b	;0.60vdd
			dc  	00000010b 	;0.60vdd
			dc  	00000010b			  
tab_165hvol:
           	dc		00000000b	;0.60vdd
		  	dc  	00000000b	;0.60vdd 
			dc  	00000000b 	;0.60vdd
			dc  	00000000b	;0.60vdd 		
			dc		00000001b	;00--0.6---(913v)  
		  	dc  	00000001b	;01--0.64--(974v)
			dc  	00000010b 	;10--0.68--(1035v)
			dc  	00000011b	;11--0.72--(1096V)										
								 
tab_surge:	dc		00000000b	;0.60vdd
		  	dc		00001000b	;0.64vdd
		  	dc  	00010000b	;0.68vdd 
			dc  	00011000b 	;0.72vdd
			dc  	00100000b	;0.76vdd
			dc  	00101000b	;0.80vdd 

;//????????????
tabminucur:  dc	    0Ah ;B0H
			dc	    0Ch ;A0H
			dc	    0Eh ;90H
			dc  	10H ;80H
			dc	    12h ;70H
			dc	    16h ;60H
			dc	    1ah ;50H
			dc  	20h ;40H 
			dc  	25H ;30H	 
			dc  	2CH ;20H	
			dc	    32H ;10H			

tab_145cur:    
			dc  	3ch 
			dc  	3ch  
			dc  	3ch  
			dc  	3ch		
			dc  	43h  
			dc  	4ah 
			dc  	50h	
			dc  	57h	 			 
tab_155cur:  
			dc  	3ch   
			dc  	3ch 
			dc  	3ch  
			dc  	3ch		
			dc  	43h  
			dc  	4ah 
			dc  	54h	
			dc  	5ah		 	

tab_165cur:   
			dc  	3ch 
			dc  	3ch  
			dc  	3ch  
			dc  	3ch		
			dc  	43h  
			dc  	4ah 
			dc  	55h	
			dc  	5fh				

;//display  debug stage
tabdebug0:	dc	offset	keydat1
			dc	   yanguo_ds
			dc     main_ds+4  ;current
			dc     main_ds+3  ;vol_in
			dc     main_ds+2  ;temp_igbt
			dc     main_ds    ;temp_main
			dc     dtem_ds+2  ;dshaoshuijs
	        dc	   1bh 		  ;CMP0C
			dc	   1ch		  ;CMP1C
			
			
tabdebug5:	dc	offset	keydat1
			dc	   yanguo_ds+2	
			dc     main_ds+6  ;valuecur  
			dc     021h       ;ppgta
			dc     main_ds+7  ;dpanjs
     		dc     dtem_ds    ;dtemp1
	        dc     dtem_ds+1  ;dganshaojs
				

			dc	   1dh 		  ;CMP2C			 
			dc	   29h 		  ;OPAC

tabtiaoon:  dc     tiao_200w
	        dc     tiao_400w
	        dc     tiao_800w

;//miscellaneous menu huoli
tabhuoli:	dc      h_huoguo   
            dc      h_chaocai
            dc      h_baochao	
            dc      h_warm 
            

            dc      h_wenhuo
            dc      h_soupzhou		
          	dc      h_zheng
          	dc      h_milk
          	
            dc      h_shaoshui	
            dc      h_zhou		
            dc      h_zhufan
            dc      h_jianchao  
            dc      h_shaokao
            dc      h_wuhuo

;//miscellaneous menu init timer
tab_minute: dc      t_huoguo   
            dc      t_chaocai
            dc      t_baochao	
            dc      t_warm 
            

            dc      t_wenhuo
            dc      t_soupzhou		     
          	dc      t_zheng
          	dc      t_milk
          	
            dc      t_shaoshui	
            dc      t_zhou		
            dc      t_zhufan
            dc      t_jianchao  
            dc      t_shaokao
            dc      t_wuhuo

;///display power ===430
tabdsptemp: dc     dsp_temp1
            dc     dsp_temp2
            dc     dsp_temp3
            dc     dsp_temp4
            dc     dsp_temp5
            dc     dsp_temp6
            dc     dsp_temp7
            dc     dsp_temp8

;////display power value: 
tabdsphuoli:dc     dsp_power1
            dc     dsp_power2
            dc     dsp_power3
            dc     dsp_power4
            dc     dsp_power5
            dc     dsp_power6
            dc     dsp_power7
            dc     dsp_power8  
		
;////display power led 		
tabdsphled: dc     (bit0)
            dc     (bit0+bit1)
            dc     (bit0+bit1+bit2)
            dc     (bit0+bit1+bit2+bit3)
            dc     (bit0+bit1+bit2+bit3+bit4)
            dc     (bit0+bit1+bit2+bit3+bit4+bit5)
            dc     (bit0+bit1+bit2+bit3+bit4+bit5+bit6)
            dc     (bit0+bit1+bit2+bit3+bit4+bit5+bit6+bit7)		
		     
;//system warm value area ==>430
tabtemph:   dc     main_80c      
            dc     main_100c  
            dc     main_120c   
            dc     main_160c   
            dc     main_180c  
            dc     main_200c  
            dc     main_240c   
            dc     main_270c 
                         
                
tabmappower: 
	        dc     4 ;10  
	        dc     6 ;10 
	        dc     8 ;10  
	        dc     10 ;10  
	        dc     12 ;13  
	        dc     13 ;14 ;16  
	        dc     14 ;16 ;18  
	        dc     15 ;18 ;20
     
	        
tab_mode_a36: 				
			dc	   m_baochao
			dc     m_huoguo
			dc     m_zheng
			dc     m_soupzhou 
			dc	   m_zhufan
			dc     m_shaoshui 
			dc     m_jianchao
			dc     m_shaokao   
	          
	          			  												
;tab_mode_f12: 				
;			dc     m_huoguo   
;	        dc     m_chaocai   
;	        dc     m_shaokao
;	        dc     m_shaoshui
;	        dc     m_zheng 	
;	        dc     m_soupzhou  
;			dc	   m_wenhuo 
;			dc	   m_baochao	        
	      
	        
        
	        
			

        	nop
    		END


~~~

