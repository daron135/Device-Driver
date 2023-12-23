# Device-Driver

## 구현 목표

1. 디바이스 드라이버는 입출력 다중화 (Poll) , Blocking I/O를 구현하여 처리할 데이터가 없을 시 프로세스를 대기 상태로 전환하고 key 인터럽트 발생시 wake uip 하여 준비 /실행 상태로 전환하여 처리

2. 타이머 시간과 LED 값은 APP 실행시 Argument로 전달하여 처리

3. 하드웨어 제어와 상태 정보를 얻기 위해 ioctl 함수 사용하여 명령어를 구현

- TIMER_STATRT : 커널 타이머 시작<br>
- TIMER_STOP : 커널 타이머 정지<br>
- TIMER_VALUE : led on /off 주기<br>

4. key 값은 read()로 읽고 led 값은 write() 로 쓰기
   
| key 값 | key 값에 해당하는 기능                                                                  |
|-------|---------------------------------------------------------------------------------|
| 1     | 타이머를 정지 (TIMER_STOP)                                                            |
| 2     | 키보드로 커널 타이머 시간을 100분의 1초 단위로 입력 받기 (TIMER_VALUE)                                |
| 3     | LED 값을 입력 받아 받은 값으로 on / off (0x00 ~ 0xff)  ‘Q’ 또는 ‘q’ 입력 시 타이머는 멈추고 응용 프로세스 종료 |
| 4     | 커널 타이머를 동작 (TIMER_START)                                                        |

## 구현 결과

1. 모듈 적재

![모듈 적재 전](https://github.com/daron135/Device-Driver/assets/140676907/3e1c1207-27bb-4979-9034-b01f8d450873)

2.  ./ledkey_app_cys 0x55 100
   
![0x55100Hz](https://github.com/daron135/Device-Driver/assets/140676907/b52bcb38-4b4c-4856-89b0-8013956561c8)

3.  TIMER_VALUE를 이용해서 50Hz로 변경

![0x55 50Hz](https://github.com/daron135/Device-Driver/assets/140676907/81d3aad5-27b4-405c-bb03-2d3676bc697f)

4. LED 값을 입력 받은 0xff로 변경
   
![0xff](https://github.com/daron135/Device-Driver/assets/140676907/49732b45-1fc2-449a-98ae-9d2fd1874767)
   
