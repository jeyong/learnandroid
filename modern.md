## Kotlin
 * 
## layout
 * LinearLayout
 * FrameLayout
 * ConstraintLayout
  * 최고!
  * animation

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
 
