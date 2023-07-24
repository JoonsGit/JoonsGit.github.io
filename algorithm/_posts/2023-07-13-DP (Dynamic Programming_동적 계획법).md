---
layout: post
title: DP (Dynamic Programming / 동적 계획법)
description: >
 Dynamic Programming 과 관련돈 이론적인 설명 및 예제 풀이
sitemap: false
hide_last_modified: true
---


# DP (Dynamic Programming_동적 계획법)


<hr>

## Dynamic Programming ?


Dynamic Programming(*이하 DP*)이란, 최적화 기법의 한 종류로, 특정 범위까지의 값을 구하기 위해서 그것과 다른 범위까지의 값을 이용하여 효율적으로 값을 구해내는 알고리즘 설계기법이다. 숩게 말하면, 불필요한 중복 계산을 최소화하여 최적해를 보다 효율적인 방법으로 산출해내는 방법이라고 할 수 있다.

<br>

<hr>


## DP를 사용하는 이유


우리가 익히 알고 있는 **분할 정복 기법**(*큰 문제를 작은 문제로 세분화하여 풀이하는 기법*)은 같은 계산을 반복적으로 해야 하는 상황이 자주 발생하는데, 이는 대다수의 경우가 프로그램 구동 과정에서의 시간 복잡도의 비약적인 상승으로 귀결된다. 



피보나치 수열의 경우를 예를 들어 생각해보자.

피보나치 수열의 점화식은 아래와 같다.


![점화식](https://blog.kakaocdn.net/dn/kJaf3/btraRwWFWtZ/olMoTdfkKp0fzLF67T3Ckk/img.gif)


일반적으로 위의 점화식을 이용하여 N번째 항을 구하는 프로그램을 작성한다면, 이와 같이 작성할 것이다.


```C++

#include <iostream>

using namespace std;



//피보나치 수열을 계산하는 함수 by 재귀

int fibo(int x) {

	if (x <= 1) return x;

	return fibo(x - 1) + fibo(x - 2);

}





int main() {

	int T;

	cin >> T;

	cout << fibo(T);

}

```


이와 같은 코드가 정상적으로 작동한다고 할 수 있겠지만, 무엇이 문제이길래 이처럼 코드를 작성하지 않는것일까?



<hr>



위의 코드를 실행시켜 **fibo(5)** 값을 구한다고 가정해보자.



프로그램은 변수 사용자에게 **5**라는 값을 입력받아 **T**변수에 저장하고 **fibo()** 함수에 T에 저장된 5라는 값을 파라미터로 전달하여 함수를 실행시킬 것 이다. 

함수는 fibo(5)라는 값을 구하기 위해 **fibo(5-1)** 과 **fibo(5-2)** 를 다시 계산하여야 하고, fibo(4)를 계산하기 위해 fibo(3) 과 fibo(2) 를 계산한다.

또한 fibo(3)을 계산하기 위해 fibo(2)와 fibo(1)을 계산하게 된다.



이와 같은 과정을 전부 거쳐 fibo(5)의 값을 구하는 과정 속에서 프로그램은 **fibo(2)** 값을 총 **3번**계산하게 되는 것이다. 



![fibo(5)](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Ft3PF0%2FbtqSgLZbXTp%2FdRqSxgLwa4padvt3qtAqNk%2Fimg.png)



<br>



결론적으로, **N**번째 항을 구하려면 **2의 N번 거듭제곱**번의 계산을 해야만 해를 구할 수 있는 것이다.



<hr>



이와같이 상당수의 분할 정복 기법은 기존에 이미 한번 이상 해결했던 계산일지라도, 현재 실행에서는 이를 기억하지못하여 중복계산한다는 치명적인 단점이 존재한다. 



따라서 이와 같이 **같은 Input에 대한 반복되는 호출을 하는 솔루션을 만났을 때,** 우리는 DP를 이용하여 프로그램을 최적화 할 수 있게 되는 것 이다.

<hr>


## 어떤 상황에서 사용할 수 있을까 ?


그렇다면 DP는 어떠한 경우에 사용할 수 있는 걸까? 



DP가 올바르게 적용되기 위해서는 아래 두가지 조건을 만족해야 한다.

<br><br>

1. **Overlapping Subproblems** *(겹치는 부분 문제)*

2. **Optimal Substructure** *(최적 부분 구조)*

<br><br>



① Overlapping Subproblems

<br>



DP는 기본적으로 어떠한 문제를 작은 문제들로 쪼개서, 하위 문제들의 값을 재활용하여 보다 큰 문제의 값을 구하는 방식을 취한다. 때문에 동일한 하위 문제들이 반복하여 나타나는 경우에 대해 사용이 가능 한 것이다.



② Optimal Substructure

<br>



이는 부분 문제의 최적 결과가 전체 문제의 최적 결과를 도출해내는데 사용되는 경우를 의미한다. 주로 최적경로 문제에서 자주 마주할 수 있는 상황으로, 부분 최적 경로를 구하고, 다음 경로에서의 최적해를 구하는 과정에서 이전에 계산된 부분 최적 경로가 동일하게 작용된다면, 이를 재활용아여 다음 최적 경로를 구할 수 있게 되는 것이다.

<hr>


## DP의 종류 : Memoization 과 Tabulation


DP를 구현하는 종류는 크게 **Memoization**과 **Tabulation**으로 구분 할 수 있는데, 이는 후에 계산 과정에서 최적해를 도출해내는 과정을 결정짓게 된다.

<br>



#### 1. Memoization

<br>

Memoization은 흔이 말하는 **Top-Down approach** *(하향식 접근)* 으로, 재귀를 이용하여 dp[n]의 값을 찾기 위해 위에서 dp[n]부터 호출을 시작하여 기저 상태인 dp[0] *(기저는 상황에 따라 상이할 수 있음)* 에 도달한 후에 결과값을 재귀시켜 재활용하여 dp[n]을 구해내는 방식이다. 

이와 같이 이전에 완료한 계산을 저장(memo)하여 후에 재사용 한다는 의미를 가지기에 Memoization이라 칭하는 것이다.



#### 2. Tabulation

<br>

Tabulation은 Memoization과 달리 **Bottom-Up approach** *(상향식 접근)* 을 기반으로 동작한다. 

이는 *상향식 접근*이라는 이름에서 유추할 수 있듯이 dp[n]의 값을 구하기 위해 기저 상태인 dp[0]부터 시작하여 반복문을 통해 dp[n]까지 도달하여 계산하는 방식이다. 이 과정에서 반복분 내에는 주로 점화식이 사용되며, 이는 본인이 문제 상황에 따라 알맞은 점화식을 도출하여 구혀해야 한다.

<hr>



## DP문제 해결 과정


여러 DP문제를 해결하는 과정은 크게 다르지 않기에, 주로 아래의 과정을 밟아가면 어렵지 않게 정답에 도달할 수 있다.

<br><br>

1. DP가 적용 가능한 문제인지 확인

2. 변수로 사용할 요소들 확인

3. 점화식 만들기

4. 구현 방식 설정하기 (Top-down or Bottom-Up)

5. 기저 상태 파악하여 설정하기

6. 알맞은 방법을 통해 구현하기

<br><br>



위의 단계를 따라 문제를 해결하다보면, 일반적으로 *3.점화식 만들기* 가 가장 어렵게 느껴지기 마련인데, 이는 문제 상황을 정확하게 파악하고 어떠한 패턴이 반복되며 값이 산출되는지 따라가다 보면 어렵지 않게 점화식을 도출해낼 수 있을 것이다.

<hr>



## BaekJoon의 DP 예시 문제


<hr>



### 1. [백준 1463번](https://www.acmicpc.net/problem/1463)



코드



```C++

#include <iostream>

#include <algorithm>

#include <vector>

using namespace std;



int main() {

	int n;

	cin >> n;

	vector<int>dp(n + 1, 0);	// 벡터 동적 할당



	dp[1] = 0;	// dp 벡터의 index 1에 0 을 할당. 

	dp[2] = 1;	// dp 벡터의 index 2에 1 을 할당.

	dp[3] = 1;	// dp 벡터의 index 3에 1 을 할당.



	for (int i = 4; i < n + 1; i++) {

		dp[i] = dp[i - 1] + 1;

		if (i % 3 == 0) {

			dp[i] = min(dp[i / 3] + 1, dp[i]);

		}

		if (i % 2 == 0) {

			dp[i] = min(dp[i / 2] + 1, dp[i]);

		}

	}

	cout << dp[n] << endl;

	return 0;

}

```



<hr>



### 2. [백준 11053번](https://www.acmicpc.net/problem/11053)



코드

```C++

#include <iostream>

using namespace std;



#define MAX 1010

int arr[MAX];

int DP[MAX];



int Max(int A, int B) {

	if (A > B) {

		return A;

	}

	return B;

}



int main() {

	int N;

	cin >> N;

	

	if (N > MAX) {

		return 0;

	}



	for (int i = 0; i < N; i++) {	// arr에 수열 입력받기

		cin >> arr[i];

	}



	// 계산

	int result = 0;

	for (int i = 0; i <= N; i++) {

		DP[i] = 1;

		for (int j = i - 1; j >= 0; j--) {

			if (arr[i] > arr[j]) {

				DP[i] = Max(DP[i], DP[j] + 1);

			}

		}

		result = Max(result, DP[i]);

	}

	

	cout << result;

	return 0;

}

```

<hr>


### 3. [백준 2579번](https://www.acmicpc.net/problem/2579)



코드 



```C++

#include <iostream>

using namespace std;

#define MAX 301



int arr[MAX];

int DP[MAX];



int Max(int A, int B) {

	if (A > B) {

		return A;

	}

	return B;

}



int main() {

	int N;

	cin >> N;

	for (int i = 1; i <= N; i++ ) {	// idx 1이 1층 계단

		cin >> arr[i];

	}



	// DP 계산

	DP[1] = arr[1];

	DP[2] = arr[1] + arr[2];

	DP[3] = Max(arr[1] + arr[3], arr[2] + arr[3]);

	// 점화식에 n-3가 들어감으로 DP[3] 까지는 직접 계산.



	for (int i = 4; i <= N; i++) {	// 4~N 까지 탐색

		DP[i] = Max(DP[i - 2] + arr[i], DP[i - 3] + arr[i - 1] + arr[i]);

	}



	cout << DP[N];

	return 0;



}

```

<hr>


### 4. [백준 1520번](https://www.acmicpc.net/problem/1520)



코드 

```C++

#include <iostream>

using namespace std;



#define MAX 500

int MAP[MAX][MAX];

int DP[MAX][MAX];	// DP[a][b] == (a,b) 에서 (N-1, M-1) 까지 가능한 경로의 개수

int N, M;	// N : 세로 , M : 가로

int result = 0;

int dx[] = { 0, 0, 1, -1 };

int dy[] = { 1, -1, 0, 0 };



int DFS(int x, int y) { // (x, y)에서 도착점까지 갈 수 있는 경우의 수를 리턴

	// 사전 검사

	if (x == N - 1 && y == M - 1) {	// 도착점 도달

		return 1;

	}

	if (DP[x][y] != -1) {	// -1이 아니다 == 이미 탐색한 지점이다 ->  기존에 계산했던 DP[x][y]를 리턴

		return DP[x][y];

	}

	// 검사 통과 -> 계산 진행

	DP[x][y] = 0;

	for (int i = 0; i < 4; i++) {	// 오른쪽, 왼쪽, 아래, 위 방향으로 1번씩 검사

		int nx = x + dx[i];

		int ny = y + dy[i];

		if (nx >= 0 && ny >= 0 && nx < N && ny < M) { // 다음 위치 좌표가 유효한지 검사

			if (MAP[nx][ny] < MAP[x][y]) {

				DP[x][y] = DP[x][y] + DFS(nx, ny); 

				// 여기가 핵심. 다음 이동할 칸이 모든 조건을 통과했다면, 현재 칸의 DP 값에 DFS(nx, ny) 값을 더해줌

			}

		}

	}

	return DP[x][y];

}



int main() {

	cin >> N >> M;

	for (int i = 0; i < N; i++) {

		for (int j = 0; j < M; j++) {

			cin >> MAP[i][j];

			DP[i][j] = -1; // 초기 상태는 -1로 설정.

		}

	}

	// DP 계산

	result = DFS(0, 0);

	cout << result;

	return 0;

}

```

<hr>



### 5. [백준 9095번](https://www.acmicpc.net/problem/9095)



코드 

```C++

#include <iostream>

using namespace std;



#define MAX 11

int DP[MAX];	// 결과 저장

int N;



void Input() {

	cin >> N;

}



void Solution() {

	// 3으로 나누었을 때 나머지가 남지 않는 값들은 계산

	DP[0] = 0;

	DP[1] = 1;

	DP[2] = 2;

	DP[3] = 4;



	if (N > 3) {

		for (int i = 4; i <= N; i++) {

			DP[i] = DP[i - 1] + DP[i - 2] + DP[i - 3];

		}

	}

	cout << DP[N] << endl;

}



void Activate() {

	int trial;

	cin >> trial;



	for (int i = 0; i < trial; i++) {

		Input();

		Solution();

	}

}

int main() {

	

	Activate();



	return 0;

}

```

<hr>



### 6. [백준 2748번](https://www.acmicpc.net/problem/2748)



코드

```C++

#include <iostream>

using namespace std;



#define MAX 91

long long DP[MAX];

int N;



void Input() {

	cin >> N;

}



void Solve() {

	DP[0] = 0;

	DP[1] = 1;

	for (int i = 2; i <= N; i++) {

		DP[i] = DP[i - 1] + DP[i - 2];

	}

	cout << DP[N] << endl;

}



void Activate() {

	Input();

	Solve();

}

int main() {

	Activate();

	return 0;

}

```

<hr>



### 7. [백준 15486](https://www.acmicpc.net/problem/15486)



코드

```C++

#include <iostream>

using namespace std;

#define endl "\n"

#define MAX 1500001

int T[MAX];

int P[MAX];

int N;

int DP[MAX];	// DP[N] == N일까지(1 ~ N-1 일 동안) 벌 수 있는 최대 금액

int result;



int Max(int A, int B) {

	if (A > B) {

		return A;

	}

	else {

		return B;

	}

}



void Input() {

	cin >> N;

	for (int i = 1; i <= N; i++) {

		cin >> T[i] >> P[i];

	}

}



void Solve() {

	int currMax = 0;

	for (int i = 1; i <= N + 1; i++) {	// N + 1 일에도 돈을 받을 수 있으므로, N+1까지 반복 (N일에도 일을 할 수 있다.)

		currMax = Max(currMax, DP[i]);	// currMax == Max(i일 전까지(이전 시행까지) 계산된 최대 금액, 기존에 계산된 i일까지의 최대 금액)

		if (i + T[i] > N + 1) {	// 돈을 받는 날짜가 N+1일 이후이면 해당 루프 스킵 (== 일을 N일까지 끝마치치 못하는 경우)

			continue;

		}

		DP[i + T[i]] = Max(currMax + P[i], DP[i + T[i]]);



		/* 

			i일에 할 수 있는 상담이 끝나는 날까지 벌 수 있는 최대 금액

			= Max(위에서 계산된 currMax(==i일 전까지 최대 값) + i일에 하루 일하고 받을 수 있는 금액, 기존에 계산되어 있던 i + T[i]일 까지의 최대 금액 (==DP[i + T[i]]))

		*/



		result = currMax;

	}

}



void Activate() {

	Input();

	Solve();

	cout << result << endl;

}



int main() {

	Activate();

	return 0;

}

```

<hr>


### 8. [백준 11726](https://www.acmicpc.net/problem/11726)



코드 

```C++

#include <iostream>

using namespace std;



#define endl "\n"

#define MAX 1001

int DP[MAX];

int N, result;



void Input() {

	cin >> N;

}



int Add(int x) {

	int sum = 1;	

	int add1 = 2; // 홀수용 초기 adder

	int add2 = 1; // 짝수용 초기 adder

	if (x % 2 == 1) { // 홀수번

		for (int i = 1; i <= x / 2 - 1; i++) {

			sum += add1;

			add1 += 2;

		}

		return sum;

	}

	else if (x % 2 == 0) {	// 짝수번

		for (int i = 1; i <= x / 2 - 1; i++) {

			sum += add2;

			add2 += 2;

		}

		return sum;

	}

}



void Solve() {

	DP[0] = 0;

	DP[1] = 1;

	DP[2] = 2;

	DP[3] = 3;



	for (int i = 4; i <= N; i++) {

			DP[i] = DP[i - 1] + Add(i);

	}



	cout << DP[N] << endl;

}



void Activate() {

	Input();

	Solve();

}



int main() {

	Activate();

	return 0;

}

```

<hr>


