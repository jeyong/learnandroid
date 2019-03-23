# View Model
 * UI component를 위한 data를 제공하는 object
 * configuration 변경 가능

## 상세
 * 예제) rotation 시
   * activity가 새로 생성되는 경우
     * activity에 data를 저장하는 것이 아니라 ViewModel에 저장
## 필요성
 * single responsibility
   * UI에 필요한 모든 데이터는 지니고 있는 object
   * activity는 그냥 화면에 그리는 것과 담당

## 구성
 * Activity
   * UI 그리기
   * 사용자 입력 수신
 * ViewModel
   * UI data 저장
 * Repository
   * app data를 저장 및 load를 위한 API
 * Presenter
   * UI를 위한 data 처리

## Reactive UI
 * ViewModel + LiveData + Data Binding

## 주의
 * Context를 ViewModel에 저장하지 마라!
   * ViewModel로 context를 전달하지마라!

## ToDo
 * 예제 좀 더 보자
 