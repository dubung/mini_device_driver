# mini_device_driver

라즈베리파이(또는 리눅스)에서 동작하는 mini device driver 프로젝트입니다.  
아래 디바이스들을 커널 모듈/드라이버 형태로 제어합니다.

## 구성 디바이스
- **Rotary Encoder**: 회전 입력 + 버튼 인터럽트 처리
- **SSD1306 OLED**: 상태/시간/메뉴 출력
- **DS1302 RTC**: 시간 읽기/설정 
- **LED Bar (8ch)**: 상태 표시 (LED00~LED02 모드 1,2,3 표시, LED03~07은 모드 2,3 타이머 완료시 3회 점멸)
- **Tact Switch**: 모드 전환/확인 입력

## 핀맵
| 디바이스               |      신호 | GPIO(BCM) | 비고          |
| ------------------ | ------: | --------: | ----------- |
| **DS1302 RTC**     | SDA(IO) |        17 | 3-wire      |
|                    |     SCL |        27 | 3-wire      |
|                    | RST(CE) |        22 | 3-wire      |
| **SSD1306 OLED**   |     SDA |         0 | I2C0 SDA    |
|                    |     SCL |         1 | I2C0 SCL    |
|                    |     RES |         5 | Reset GPIO  |
| **LED Bar (8ch)**  |    LED0 |         7 |             |
|                    |    LED1 |         8 |             |
|                    |    LED2 |         9 |             |
|                    |    LED3 |        10 |             |
|                    |    LED4 |        11 |             |
|                    |    LED5 |        12 |             |
|                    |    LED6 |        13 |             |
|                    |    LED7 |        14 |             |
| **Rotary Encoder** |      S1 |        23 | A           |
|                    |      S2 |        24 | B           |
|                    |     KEY |        25 | 버튼(인터럽트)    |
| **TACT Switch**    |      SW |        20 | 입력(인터럽트/폴링) |



## 주요 기능
- Rotary 입력으로 메뉴 이동 / 값 조절
- Tact switch로 선택/뒤로가기 등 입력 처리
- DS1302에서 읽은 시간 정보를 SSD1306에 표시
- 이벤트(모드/상태)에 따라 8-LED bar 패턴 출력

## 빌드/설치
> # make kernel version
> ubuntu@ubuntu:~/linux$ cat /home/ubuntu/linux/include/config/kernel.release
6.1.93-v8+
> 

### 1) 빌드
```bash
make



