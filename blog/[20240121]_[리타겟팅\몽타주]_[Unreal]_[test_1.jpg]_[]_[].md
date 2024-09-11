# 애니메이션 Retargeting
> Animation Retargeting은 같은 스켈레톤 에셋을 공유하나 비율이 크게 다른 캐릭터 간의 애니메이션을 재사용할 수 있도록 해주는 기능이다.

*작동 원리
Retargeting 시스템에서 타깃을 새로 잡는 것은 Bone의 Translate Component 뿐이다.

https://dev.epicgames.com/documentation/ko-kr/unreal-engine/animation-retargeting-in-unreal-engine?application_version=5.1

IK_Rig를 통해 Retargeting 하고 있다. 
(<../img/user/스크린샷 2024-09-10 164946.png>)
큰 틀에서 IK를 봤을 때 "리타겟 체인"이라는 것이 있는데 인위적으로 맵핑하여 이 체인을 참고하여 애니메이션을 변환하는 기능이 존재한다. 

# 사용하는 법
Retargeting Animation을 만들기 전에 IK릭이라는 걸 먼저 만들어야 한다.
> **Animation -> Retargeting -> IK릭**

후에 IK 리타겟팅을 통해 각 범위마다 체인을 추가해준다.

# 애니메이션 몽타주
> 정해진 순서에 따라 실행되는 애니메이션 조건에 맞게 재생한다. 콤보 Action과 같은 것이 예시가 될 수 있다.