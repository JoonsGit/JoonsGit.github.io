---
layout: post
title: Algorithm_week_2
description: >
  Algorithm_week_2
sitemap: false
hide_last_modified: true
---


# Algorithm_week_2

---

<br>


## 1



### 코딩테스트 연습 > 연습문제 > 덧칠하기



```cpp

#include <string>

#include <vector>

using namespace std;



// 이거 n MAX값 보니까 하나씩 하면 무조건 시간초과 나겠네

// 이거 DP 문제

// top-down / bottom-up ? 잠깐만 이거 점화식을 만들 수 있나

// n이 칸수 / m이 롤러 폭 / section이 다시 칠할 칸들

/*

    if (n <= m) result는 section과 관계 없이 반드시 1

    section을 어떻게 뜯을까.. 이거 뜯을 필요가 없다. 그냥 section 하나씩 받아서 그 칸이 이전 시행에서 칠해졌는지 확인만 하면 된다.

    

    section 탐색 -> gray칸 탐지 -> answer++ & section(gray칸 idx + m 까지는 탐색 pass (무조건 칠해짐) 

    ->  section(gray칸 idx + m) 이후로 다시 탐색 -> 같은과정 반복 

*/

    

int solution(int n, int m, vector<int> section) {

    int answer = 0;

    int done = 0;

    for (int i = 0; i < section.size(); i++) {

        if (done > section[i]) {

            continue;

        } 

        else {

            answer++;

            done = section[i] + m;

        }

    }

    

    return answer;

}

```

---

<br>


## 2



### 코딩테스트 연습 > 2023 KAKAO BLIND RECRUITMENT > 개인정보 수집 유효기간



```cpp

// today : "YYYY.MM.DD"

// terms : "약관종류 유효기간" -> substr이랑 stoi 이용해서 변수에 따로 저장 (기준변수)

//         Ex) "A 6"

// privacies : "수집날짜 약관종류" -> 날짜-stoi, 약관종류-substr로 privacies[i]에서 긁어오기 (형식 고정임)

//             EX) "YYYY.MM.DD A"



/* 

    특정 알고리즘을 이용한 풀이를 요구하는 문제인지 잘 모르겠다. 

    그냥 문제에서 주어진 흐름대로 작성하되, 시공간적으로 최적화 시키는 것이 완성도의 차이를 만들어낼 것 같은 느낌.

    기본정보를 저장해야 할 기준 변수들이 많아질 것 같은데, 메모리를 최대한 심플하게 사용해볼것.

*/

#include <string>

#include <vector>

#include <map>

#include <set>

#include <sstream>

using namespace std;

map<char, int> std_term;  // terms의 기준변수 만들기 : term의 value는 '달'이 기준

pair<string, char> pri;   // privacies에서 긁어와서 만들기



string date_adder(string col_date, char term1) {

    string until;

    int adder = std_term[term1]; // std_term에서 term1의 유효기간 받아오기

    // 날짜 저장

    int y = stoi(col_date.substr(0,4)); 

    int m = stoi(col_date.substr(5,2));

    int d = stoi(col_date.substr(8,2));

    

    // 계산

    m += adder;

    if (m > 12) {

        int mock = m / 12;

        m %= 12;

        y += mock;

    }

    

    until = to_string(y) + '.' + to_string(m) + '.' + to_string(d); // 정수 -> 문자열 합치기

    return until;

}





set<int> solution(string today, vector<string> terms, vector<string> privacies) {

    set<int> answer;

    // terms로 term 만들기

    for (int i = 0; i < terms.size(); i++) {

        stringstream iss(terms[i]);

        char temp1;

        int temp2;

        iss >> temp1 >> temp2;

        std_term[temp1] = temp2;

    }

    

     // privacies로 pri 만들기

    for (int i = 0; i < privacies.size(); i++) {

        pri.first = privacies[i].substr(0, 10); // 날짜 저장

        pri.second = privacies[i][11];  // term 저장

        

        // 유효기간 계산

        string until_date = date_adder(pri.first, pri.second);

        

        // 오늘 날짜와 유효기간 비교

        if (today >= pri.first && today <= until_date) {

            answer.insert(i+1);

        }

    }

    

    return answer;

}

```

---

<br>


## 3



### 코딩테스트 연습 > 연습문제 > 콜라 문제



```cpp

#include <string>

#include <vector>



using namespace std;



// 주어진 방향대로 짜면 그냥 될 듯 ..?

// "빈 병 a개 -> 쌔삥 b개" 인 가게에 n개를 주면 answer개를 받음을 return



int solution(int a, int b, int n) {

    int answer = 0;

    

    while(n >= a) {  // 조건 : 보유 빈 병 >= 기준 병 수

       int get_and_drink = (n / a) * b;

        n %= a; // 남은 빈 병 

        answer += get_and_drink; // 마신 만큼 더해주기

        n += get_and_drink; // 마신 병은 빈병이 되니까 남은 빈병에 더해주기

    }

    return answer;

}

```

---

<br>


## 4



### 코딩테스트 연습 > Summer/Winter Coding(~2018) > 배달



```cpp





```

---

<br>


## 5



### 코딩테스트 연습 > 연습문제 > N개의 최소공배수



```cpp

#include <string>

#include <vector>



using namespace std;

// 비슷한 문제 풀어봤던 것 같네

// 최소공배수 = 두 수의 곱 / 최대공약수 



// 최대공약수

int GCD (int a, int b) {    

    int large = max(a, b);

    int small = min(a, b);

    int remainder = large % small;

    

    // remainder == 0 이면 당연히 GCD는 small, 아니라면 GCD(big, small) = GCD(small, big % small)

    // 이거 이름 까먹었었는데, 유클리드 호제법이더라. 

    while(remainder > 0)   

    {

        large = small;

        small = remainder;

        remainder = large % small;

    }

    

    return small;

}



// 최소공배수

int LCM (int a, int b) {

    return a * b / GCD(a, b);

}





int solution(vector<int> arr) {

    int answer = 1;

    

    for (int i = 0; i < arr.size(); i++) {

        answer = LCM(answer, arr[i]);

    }

    

    return answer;

}

```

---

<br>

