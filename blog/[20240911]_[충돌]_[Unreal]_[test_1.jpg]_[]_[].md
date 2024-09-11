# Collision Enabled

**No Collision**
Collsion 기능을 사용하지 않을 때 적용한다.

**Query Only(No Physics Collision**
물체와 물체끼리 충돌 그리고 영역 안에 들어온 것(오버랩 : 공간적 질의)을 탐지할 때 적용한다.

**Physics Only (No Query Collision)**
물리적인 시뮬레이션이 없는 충돌 판정을 하라 때 적용한다.

이 두 가지를 자주 사용한다.

# Object Type
오브젝트의 채널이다. 
블록/Query Only 을 체크했을 때 플레이어가 이 충돌 오브젝트를 지나가지 못한다.
도 설정할 수 있다.

**World Static**
월드 세상에 존재하는 정적인 객체

**World Dynamic**
월드 세상에 존재하는 동적인 객체

**Pawn**
플레이어(캐릭터) 등의 객체 

**Physics Body**
물리 적용이 되어야 하는 객체

**Vehicle**
차량

> Overlap 사용 시  GenerateOverlap Event(오버랩 이벤트 생성) 를 반드시 켜줘야 작동 된다.

[20240911]_[충돌]_[Unreal]_[test_1.jpg]_[]_[]
# 프로젝트 콜리전 환경 설정
> Project Setting -> Engine -> Collision -> Object Channels

**Object Channel**은 물리적인 채널, **Trace Channel**은 개념에 대한 채널이다. **Preset**을 통해 타입 정보를 지정할 수 있다.
 매번마다 충돌 처리를 선정해주는 것이 번거롭기 때문에 환경 설정에서 채널을 설정할 수 있다. 새로운 오브젝트 타입을 파는 것과 같다. 커스텀한 콜리전은 설정하고 다시 Object Type에서 사용할 수 있는 것을 볼 수 있다.

하지만 채널을 설정하고 새 채널은 프리셋 정보를 설정해줘야 한다.

이 정보는 Project > Config 쪽 어딘가서 저장이 된다.

