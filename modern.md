## Kotlin
 * 
## layout
 * LinearLayout
 * FrameLayout
 * ConstraintLayout
  * 최고!
  * animation
 * navigation graph 이용하기

## Adapter Views
 * ListView
 * GridView
 * Gallery

 * RecyclerView
  * 
## Fragment
 * core platform 대신 support library 사용
 * Navigation

## Activity
 * single activity
 * animation
 * fragment
 * navigation

## life cycle
 * LifecycleOwner
       |
    Lifecycle
  /                      \
 LifecycleObserver      (code)  (query lifecycle state)
 (lifecycle events 수신)               

```java
public class Fragment implements LifecycleOwner

getLifecycle().setLifecycleObserver()
```

## Views & Data
 * Views
 * Data for views
 * Lifecycle tracking
 * Data Change tracking

## Data for Views
 * ViewModel
   * LiveData<type> data
     * Data for views
     * Lifecycle tracking
     * Data change tracking - observe()


## Room
 * Local data persistence 
 * 컴파일 타임 유효
 * LiveData

## Data Paging
 * Paging Library
   * RecyclerView
   * background thread
   * LiveData를 통한 change Observe

## Graphics
 * OpenGL ES 3.1/3.2 Vulkan
 * HW 가속
 * VectorDrawable
 * 추천 Library : Glide, Picasso, Lottie
 
## navigation 사용법
 * Navigation graph
   * xml 파일
   * fragment 이동 관련 정보를 독점적으로 저장
   * 이동시 ui 효과 적용 가능
 * NavHostFragment
   * layout에 추가하는 fragment widget
   * fragment navigation을 담는 일종의 그릇
   * 일종의 fragment를 끼우고 빼는 window라 할 수 있음
 * NavController
   * 각 NavHostFragment는 1개의 NavController를 가진다
   * findNavController().navigate("destination or action_id");
   * action xml 
   * safearg
     * navigation graph 기반으로 fragment 이동시 argument 전달시 type safe 를 위해
     * argument passing
   * 참고 : https://www.youtube.com/watch?v=Y0Cs2MQxyIs
   
