# Vector

> 단위 벡터
> Animation을 만드는데 필요한 데이터들을 모아두는 Class를 만들었다.

> 방향 벡터
> Animation을 만드는데 필요한 데이터들을 모아두는 Class를 만들었다.

# Vector 응용
```cpp
void AMyGameModeBase::BeginPlay()
{
	for (int i = 0; i < 10; i++)
	{
		APawn* defaultPawn = GetWorld()->GetFirstPlayerController()->GetPawn();
		FVector vPawnLoc = defaultPawn->GetActorLocation();
		FRotator vPawnRot = defaultPawn->GetActorRotation() + FRotator(0.f, m_fCurrent_SpawneeAngle, 0.f);
		FVector vForwardVector = FRotationMatrix(vPawnRot).GetScaledAxis(EAxis::X);
		FVector vFinalLoc = vPawnLoc + vForwardVector * 1000.f;

		AMySpawnee* Spawnee1 = GetWorld()->SpawnActor<AMySpawnee>(AMySpawnee::StaticClass(), vFinalLoc, FRotator(0.f, 0.f, 0.f));
		
		m_fCurrent_SpawneeAngle += m_fSpawneeAngle;

		if (360.f <= m_fCurrent_SpawneeAngle)
			m_fCurrent_SpawneeAngle = 0.f;

		Spawnee_Array.Add(Spawnee1);
	}
}

void AMyGameModeBase::Tick(float DeltaTime)
{
	if (Spawnee_Array.Num() > 0)
	{
		if (nullptr == Spawnee_Array[m_iCurrentSpawnee])
			return;

		AMySpawnee* CurrentSpawnPos = Spawnee_Array[m_iCurrentSpawnee];

		APawn* Player = GetWorld()->GetFirstPlayerController()->GetPawn();

		FVector dir = CurrentSpawnPos->GetActorLocation() - Player->GetActorLocation();

		FVector Direction = dir.GetSafeNormal(); // 방향 벡터

		FVector NewLoc =	 Player->GetActorLocation() + (Direction * 500.f * DeltaTime);

		Player->SetActorLocation(NewLoc);
		Player->SetActorRotation(dir.Rotation());

		if (FVector::Dist(NewLoc, Spawnee_Array[m_iCurrentSpawnee]->GetActorLocation()) < 10.f)
		{
			++m_iCurrentSpawnee;

			if (Spawnee_Array.Num() <= m_iCurrentSpawnee)
				m_iCurrentSpawnee = 0;

			GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Green, FString::Printf(TEXT("향하는 스폰 위치 [ %d ]"), m_iCurrentSpawnee));
		}

	}
	else
		GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Red, TEXT("Failed Array"));
}

```

# Vector의 외적과 내