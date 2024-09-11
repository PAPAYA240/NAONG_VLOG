## 델레게이트 정의

함수를 전달하여 어떤 행위를 하였을 때 그 함수를 실행한다.
플레이어 충돌 처리에 사용되는 델리게이트이다.

```cpp
void AR1Player::BeginPlay()
{
	Super::BeginPlay();

	GetCapsuleComponent()->OnComponentBeginOverlap.AddDynamic(this, &AR1Player::OnBeginOverlap);
}

void AR1Player::OnBeginOverlap(UPrimitiveComponent* OnComponentBeginOverlap, AActor* OtherActor, UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult)
{
	GEngine->AddOnScreenDebugMessage(-1, 2.0f, FColor::Red, TEXT("On Begin Overlap"));
}

```

양꼬치처럼 체이닝도 가능하다.
```cpp
static void Main(string[] args)
{
    _func += DoWork1;
    _func += DoWork2;

    _func.Invoke();
}

static void DoWork1()
{
    Console.WriteLine("DoWork1");
}

static void DoWork2()
{
    Console.WriteLine("DoWork2");
}
```

여러 개의 함수를 리스트처럼 연속해 등록을 시켜주는 것이다. 이때 _func에 등록된 모든 함수들이 실행된다.
또한, 리스너 패턴(구독자 패턴)을 만들기 안성맞춤이다. 