7장 FreeRTOS

RTOS: Real Time Operting System

OS(Operating System, 운영체제)
컴퓨터와 그 주변에 장착된 하드웨어를 효과적으로 사용하기 위한 소프트웨어
PC, 스마트폰 등 대부분의 전자기기는 OS환경하에서 사용됩니다.
MCU는 작은 일을 처리할 때, 순차적으로 프로그래밍되며, 동시에 두 가지 일을 하기 힘듭니다. 앞의 예에서 처럼 인터럽트를 사용하여 여러가지 일을 동시에 처리하도록 할 수 있습니다.

RT(Real Time, 실시간)
반응속도가 불연속적이고 지연이 있지만, 실제로는 거의 연속적이고 즉각적인 시간반응을 가지고 있다고 생각해도 됩니다. 어떤 "불연속적이고 시간 지연을 가진 시스템"이 다른 대상에 영향을 주지 않을 정도로 충분히 빠르면 실시간 시스템이라고 부릅니다.
예를 들어, 휴대폰 버튼 센싱은 불연속적이고 센싱을 위해 휴대폰 내부의 장치는 시간을 소모합니다. 휴대폰 버튼을 누를 때 폰이 충분히 버벅거리지 않으면 실시간 시스템이라고 합니다.

Real Time System은 상대적으로 절대 빠르기는 없습니다.
(명령어를 1usec 이내로 처리하면 실시간 시스템이고 1usec보다 빠르면 실시간이 아니고 이런 것은 없습니다. 처리하는 대상에 따라 다릅니다.
예를 들면, 세탁기의 회전을 센싱하는 MCU는 대략 0.1초 정도마다 회전 속도를 감지할 수 있고 이를 처리하여 보고할 수 있으면, 실시간 센싱시스템이라고 할 수 있습니다.
9600bps로 전송되어 오는 데이터를 처리하는 시스템은 최속 초당 1만 번 이상 신호의 높낮이를 확인할 수 있어야 합니다. 따라서 9600bps수신기는 0.1msec 신호의 높낮이를 확인할 수 있어야 합니다. 따라서 9600bps수신기는 0.1msec보다 더 빠르게 반복적으로 일을 처리해야 실시간 시스템으로 생각할 수 있습니다.)

Real Time System OS
한 개의 코어를 가지는 MCU(컴퓨터)는 한 번에 한가지 일만 주어진 클럭의 빠르기로 할 수 있습니다. 한 개의 일을 끝내기 전에 다른 일을 또 시킬 때, 지금하던 일을 중지하고 새로 시킨 일을 할지, 이전 일을 조금하고 새로운 일을 조금하고를 반복할 지, 이전 일을 그냥 할 지.. 이러한 과정을 순차적으로 프로그래밍으로 작성하는 것은 대단히 힘듭니다.
주어진 여러 가지 일들을 실시간으로 처리할 수 있도록 도와주는 컴퓨터 소프트웨어를 실시간 운영체제라고 합니다.

FreeRTOS
윈도우, 리눅스, iOS, Android 모두 Real time OS입니다. 더 정확히는 Real Time을 가능하게 하는 OS입니다. 이런 범용 OS는 보통 그냥 OS라고 합니다. RealTime OS라고 칭하는 RealTime 수식어가 붙어 있는 경우 대부분 임베디드 시스템에 RealTIme이라는 단어를 사용합니다. 이유는 OS의 크기가 작아야 하고 속도도 원하는 만큼 빨라야 하고, 멀티테스킹을 지원할 수 있어야 하기 때문입니다.
그래서 가격을 줄이기 위해, MCU의 메모리가 작고 성능이 낮아도 RealTime이 되는지 안되는지가 중요하기 때문입니다. 이들 중 FreeRTOS는 무료이고 가볍고 가장 간단한 기능만 가진 OS라서, 메모리가 32k 넘는 작은 MCU에 많이 사용됩니다.
FreeRTOS는 C소스코드 형태의 OS를 활용할 수도 있으며, 4000Line 이내이며 AVR, 8051, ARM CortexM3, M7, ARM9, X86등 다양한 8, 16,32bit MCU에Porting 가능합니다.

지금 제가 사용하고 있는 보드인 F103RB MCU의 메모리 사이즈는
