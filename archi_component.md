# architecture component
 * 테스트 가능하고 문제 없이 잘 돌아가는 앱을 만드는데 도움이 되는 lib의 집합
 * 시작하기
   * UI component lifecycle를 관리하는 class
   * data 처리
 * app의 lifecycle 관리
   * lifecycle-aware components 사용
     * activity와 fragment 관리
     * configuration 변경에도 문제 없음
     * memory leak 회피
     * UI로 data load 쉽게
     * android.arch.lifecycle package
     * lifecycle package를 project에 넣는 방법 : [넣기](https://developer.android.com/jetpack/androidx/releases/lifecycle#declaring_dependencies)
 * LiveData
   * 기반 DB가 변경되는 경우 view에게 통보하는 data object
 * ViewModel
   * UI관련 data를 저장하여 app rotation에도 문제가 없도록
 * Room
   * SQLite object 매핑 library
   * boilerplate 코드 피하고 쉽게 SQLite 테이블 데이터를 java object로 변환
   * Room은 SQLite 구문을 compile 시에 체크하고 RxJava, Flowable, LiveData observables을 반환

## Lifecycle
 * component의(activity, fragment) lifecycle 관한 정보르 가지고 있는 class
 * 다른 obj에서 이런 state를 observe할 수 있게 하는 함
 * 2개 enumeration을 사용하여 lifecycle status를 추적
   * Event
     * framework와 Lifecycle class로부터 dispatch되는 lifecycle event
     * activity나 fragment의 callback과 매핑
   * State
     * Lifecycle object가 추적하는 component의 현재 상태
 * component의 lifecycle 감시
   * method에 annotation을 붙이기
   * Lifecycle 클래스의 addObserver() method를 호출해서 observer를 추가

### LifecycleOwner
 * 단일 method interface로 해당 class가 Lifecycle을 가진다는 것을 표시
 * getLifecycle() mehtod
   * 해당 class에서 implementation을 해야함!
   * 전체 application process를 관리하고자 한다면 ProcessLifecycleOwner을 참조!
 * 이 interface로 각 개별 class로부터의(AppCompatActivity, Fragment) Lifecycle의 ownership을 추상화
 * custom application class에서도 LifecycleOwner interface를 구현 가능
 * LifecycleObserver를 구현하는 component는 LifecycleOwner을 구현하는 component들과 동작한다. owner가 lifecycle을 제공하므로 observer가 감시하도록 등록 가능
 *  https://developer.android.com/topic/libraries/architecture/lifecycle