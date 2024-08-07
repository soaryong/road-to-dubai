# 005. Go Concurrency 
> 이 아티클에서는 Go 언어의 동시성 프로그래밍에 대한 기초를 코드 위주로 설명한다. 고루틴(goroutine)과 채널(channel), select 문, sync 패키지 등을 사용하여 동시성을 제어하는 방법을 설명한다. 이 모듈은 선택 사항으로, 필요한 경우 추가 학습을 통해 동시성 프로그래밍 능력을 향상시킬 수 있다.

## 목차
0. 고루틴(goroutine)
1. 채널(channel)
2. 채널(channel) 이용한 동시성 제어

## 0. 동시성
우선 간단하게 동시성하면 빠질 수 없는 동시성/병렬성 개념부터 짚어보자. 
- 동시성(Concurrency): 여러 작업을 한꺼번에 다루는 것. 여러 개 논리적 제어 흐름을 가진다. 
- 병렬성(Parallel): 여러 작업을 한꺼번에 실행하는 것. 논리적 제어 흐름 하나 또는 그 이상이다. 

동시성은 논리적으로 여러 작업 처리 방법에 대해 바라보기 때문에 여러 개 논리적 제어 흐름을 필수적으로 가진다. 반면에, 병렬성은 물리적으로 여러 작업을 실제로 처리하는 방법이다. 이는 여러 작업을 어떻게 다루는 것이 아닌 실행 해법에 더 관심이 있다. 이미지 처리나 딥러닝에서 쓰이는 싱글코어에 SIMD로 논리적 제어 흐름 하나만 가지고 병렬 처리하는 방법도 있고, CPU 명령어 수준 병렬 처리 해법으로 파이프라이닝, 비순차 실행, 추측 실행 등이 있다. 이러한 기법으로 32bit보다 64bit 컴퓨터를 쓰면 단일 명령으로 한번에 처리할 수 있는 데이터가 많아져 성능 향상으로 이어진다

흔히 사용하는 스레드, lock을 이용한 멀티 쓰레딩 기법으로 이러한 개념을 다시 정리해보면 여러 작업을 한꺼번에 다룰 수 있는 제어 흐름(ex. mutex,  scheduler, critical section 등)을 가진 동시성 프로그램을 병렬로 동작하는 하드웨어(멀티코어)에서 실행하는 것이다. 이러한 프로그램을 상대하기 까다로운 이유는 비결정적(nondeterministic)이기 때문이다. 

그래서 Cosmos SDK 애플리케이션 개발을 할 때는 결정적이고 안정적인 코드를 작성해야 하기 떄문에 동시성 프로그래밍을 지양하고 있다. 하지만, 더 나아가본다면 이러한 동시성 프로그래밍을 이해하고 사용할 수 있다면, 더욱 효율적인 코드를 작성할 수 있을 것이다.

## 0. 고루틴(goroutine)
고루틴은 경량 스레드를 사용하여 멀티 쓰레드 기법을 구현한 것이다. 고루틴은 OS 스레드보다 적은 메모리를 사용하며, 더 빠르게 생성되고 실행된다. 고루틴은 Go 런타임 스케줄러에 의해 관리되며, Go 런타임은 고루틴을 여러 스레드에 분배하여 실행한다. 이러한 설계로 수천 개의 고루틴을 생성해도 성능에 큰 영향을 주지 않는 장점이 있다. 이는 고 언어의 인기에 한 몫을 하였다. 


## 1. 채널(channel)
채널은 고루틴 간의 안전한 통신을 가능하게 하며, 동시성 제어의 주요 수단으로 사용된다. 또한, 채널은 blocking 통신을 기본으로 하여, 데이터를 주고받을 때 고루틴을 자동으로 동기화한다. 채널은 타입을 지정하여 선언하며, make 함수를 사용하여 생성한다.
- 동기화: 채널을 통해 값을 주고받을 때 고루틴 간에 동기화가 이루어진다.
- 방향성: 채널은 양방향이거나 송신 전용, 수신 전용으로 선언할 수 있다.

다음은 채널을 사용하여 고루틴 간에 데이터를 주고받는 예제 코드이다:
```go
package main

import (
	"fmt"
)

func main() {
	// 채널 생성
	ch := make(chan int)

	// 고루틴에서 채널에 값 보내기
	go func() {
		ch <- 42
	}()

	// 채널에서 값 받기
	val := <-ch
	fmt.Println(val) // 42
}
```
> 예제 코드 확인하기: [05_channel](../code/05_channel/)

### channel을 이용한 동시성 제어
버퍼링된 채널을 사용하면 비동기적으로 데이터를 주고받을 수 있으며, 고루틴이 블록되지 않고 작업을 계속 수행할 수 있습니다. 이는 고루틴 간의 효율적인 작업 분배와 부하 분산을 가능하게 한다. 다음 버퍼링된 채널을 사용하는 방법을 보여준다:
```go
package main

import (
	"fmt"
)

func main() {
	// 버퍼 크기 2인 채널 생성
	ch := make(chan int, 2)

	// 채널에 값 보내기
	ch <- 1
	ch <- 2

	// 채널에서 값 받기
	fmt.Println(<-ch) // 1
	fmt.Println(<-ch) // 2
}
```
> 예제 코드 확인하기: [05_buffer_channel](../code/05_buffer_channel/)


