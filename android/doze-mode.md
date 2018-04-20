# [Android] Doze mode

## Doze mode란?
: 안드로이드 OS가 6.0으로 업그레이드 되며 새로 추가된 절전 기능이다.

### Doze mode 진입 조건
1. 휴대폰을 충전 중이지 않음.
2. 스크린이 꺼진 후, 일정 시간이 지났을 때

### Doze mode에서 제한되는 동작
- 네트워크 액세스
- Wake Lock
- AlarmManager의 기본 알람
- Wifi 스캐닝
- Sync Adapter 동작
- Job Scheduler 동작

> Doze mode에서 AlarmManager가 제대로 작동하게 하려면 6.0에서 추가된 *setAndAllowWhileIdle()*, *setExactAndAllowWhileIdle()* 메서드를 이용해야 한다.

### Doze mode 테스트

**adb를 이용해 강제 Doze mode 진입**

    $ adb shell dumpsys battery unplug
    $ adb shell dumpsys deviceidle step

: *$ adb shell dumpsys deviceidle step* 작업은 상태가 변할 때 까지 계속 실행한다.

**Doze mode 해제**

    $ adb shell dumpsys deviceidle step
