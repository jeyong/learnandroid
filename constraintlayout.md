# ConstraintLayout

## visual editor
 * match_constraint
   * guideline
     * anchor로 사용
     * guideline에 view를 연결
   * barrier
     * view group의 일종
     * 실제 코드에서 'group'으로 불린다
     * barrier의 왼쪽 or 오른쪽으로 view를 옮긴다.
   * 1.0
     * Margins
     * Baselines
     * Chains
   * 2.0
     * Guideline
     * Barriers
     * Groups
     * Helpers
 * constraint
   * size 정보만을 가리킴
# MotionLayout
 * Motion Editor
 * Constraint Layout을 이용해서 동적인 layout 구현
 * 기능
   * 접히는(Collapsible) 헤더
   * state feedback
   * transition
 * Motion
   * start <-> end
   * MotionLayout -> MotionScene -> (Start/End)
   * MotionScene
     * layout과 분리되는 xml 파일
     * 

## 참고
 * [영상](https://www.youtube.com/watch?v=hqEfshM5Vfw)
 