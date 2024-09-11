
# Target 쫓아가기
```cpp
	FVector vDirection = TargetActor->GetActorLocation() - R1Player->GetActorLocation();

	if (vDirection.Length() < 250.f)
	{
		// 공격
		GEngine->AddOnScreenDebugMessage(-1, 2.0f, FColor::Red, TEXT("ATTACK"));
	}
	else
	{
		// 쫓아가기
		FVector WorldDirection = vDirection.GetSafeNormal();
		R1Player->AddMovementInput(WorldDirection, 1.0f, false);
	}
}

```
(목적지 - 출발지)의 거리를 구한 값 만큼 이를 단위 벡터로 만들어서 AddMovementInput로 플레이어의 이동 값을 적용시킨다.

250.f 인 이유는 단순하다. 언리얼의 단위는 CM이기 때문에 대략적으로 2.5m 이내라고 생각하면 적합한 숫자이다.

# AddMovementInput(방향, 속도, Force)
```cpp
	UPawnMovementComponent* MovementComponent = GetMovementComponent();
if (MovementComponent)
{
	MovementComponent->AddInputVector(WorldDirection * ScaleValue, bForce);
}
else
{
	Internal_AddMovementInput(WorldDirection * ScaleValue, bForce);
}

void APawn::Internal_AddMovementInput(FVector WorldAccel, bool bForce /*=false*/)
{
	if (bForce || !IsMoveInputIgnored())
	{
		ControlInputVector += WorldAccel;
	}
}

```
폰의 이동 컴포넌트를 가져온다면 (WorldDirection * ScaleValue, bForce) 뱡향과 속도를 곱한 값만큼 controlInputVector에 더해준다.


