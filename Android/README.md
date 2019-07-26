# Proguard
* 난독화 가능(릴리즈시 앱 내 변수명을 의미없는 값으로 변경)

# Android App Bundle(AAB)
* 앱 배포시 Google Play에서 권장하는 파일 포맷
* 사용자 기기에 맞춰 필요한 요소들만을 이용, APK를 빌드하고 배포해줌(Dynamic Delivery)
* 배포 파일의 용량이 줄어드는 효과

## Dynamic Delivery
* Android 5.0(SDK 21) 이상 사용 가능
* 분리된 APK를 하나의 앱으로 만들어 줌(Split APK 메커니즘)

### apk 종류
* Base APK
* Configuration APK : 기기최적화(밀도, cpu, 다국어 등)를 Google Play에서 자동으로 생성해줌
* Dynamic feature APK : 추가 설치가능한 코드 및 리소스를 담음

## webview thread 오류
```
webviewName.post(new Runnable() {
	@Override
	public void run() {
		
	}
});
```
