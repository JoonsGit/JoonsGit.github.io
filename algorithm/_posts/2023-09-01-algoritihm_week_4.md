---
layout: post
title: Algoritihm_week_4
description: >
   Algoritihm_week_4
sitemap: false
hide_last_modified: true
---


# Algoritihm_week_4

---

<br>




## 1. 코딩테스트 연습 > 2023 KAKAO BLIND RECRUITMENT > 택배 배달과 수거하기



<br>



```cpp

// 코드 날아감;

```



---

<br>




## 2. 코딩테스트 연습 > 2022 KAKAO TECH INTERNSHIP > 성격 유형 검사하기



<br>



```cpp

#include <string>

// 잘하면 진짜 간단하게 풀 수 있을듯 ?

#include <vector>

#include <map>

using namespace std;



string solution(vector<string> survey, vector<int> choices) {

    string answer = "";

    map<char, int> score = {

        {'R', 0},

        {'T', 0},

        {'C', 0},

        {'F', 0},

        {'J', 0},

        {'M', 0},

        {'A', 0},

        {'N', 0}

    };



    for (int i = 0; i < survey.size(); i++) {

        char fore = survey[i][0];

        char rear = survey[i][1];

        

        // 점수 계산

        switch (choices[i]) {

            case 1:

                score[fore] += 3;

                break;

            case 2:

                score[fore] += 2;

                break;

            case 3:

                score[fore] += 1;

                break;

            case 4:

                break;

            case 5:

                score[rear] += 1;

                break;

            case 6:

                score[rear] += 2;

                break;

            case 7:

                score[rear] += 3;

                break;

        }

    }



    // RT

    if (score['R'] >= score['T']) {

        answer += "R";

    } else {

        answer += "T";

    }

    // CF

    if (score['C'] >= score['F']) {

        answer += "C";

    } else {

        answer += "F";

    }

    // JM

    if (score['J'] >= score['M']) {

        answer += "J";

    } else {

        answer += "M";

    }

    // AN

    if (score['A'] >= score['N']) {

        answer += "A";

    } else {

        answer += "N";

    }

    // return

    return answer;

}



```



---

<br>




## 3. 코딩테스트 연습 > 연습문제 > 둘만의 암호



<br>



```cpp

// skip의 알파벳을 제외시킨 새로운 알파벳 문자열을 만들어서 계산하는게 편할 듯.

// s의 알파벳을 숫자화 시켜서 index를 더해준 숫자를 전체 문자열로 나눈 나머지값을 index로 하는 알파벳을 출력히면 될 듯.

#include <string>

#include <vector>



using namespace std;



string solution(string s, string skip, int index) {

    string answer = "";

    string alphabet = "abcdefghijklmnopqrstuvwxyz";

    // skip 제외된 알파벳 문자열 만들기

    for (int i = 0; i < skip.length(); i++) {

        int search = alphabet.find(skip[i]);

        alphabet.erase(search, 1);

    }

    int alpha_len = alphabet.length();

    // s를 숫자화 시켜서 index와 합치기

    for (int i = 0; i < s.length(); i++) {

        char curr = s[i]; // 문자

        int curr_idx = alphabet.find(s[i]) + index; // 그 문자의 s에서의 idx

        

        if (curr_idx >= alpha_len) {

            curr_idx %= alpha_len;

        }

        

        answer += alphabet[curr_idx];

    }

    return answer;

}

```



---

<br>




## 4. 코딩테스트 연습 > 연습문제 > 대충 만든 자판



<br>



```cpp

// key로 검색이니까 map에 각 알파벳 별로 요구되는 min 입력값 저장해놓고 result에서 긁어오고 바로 찾아서 도출해내면 될 듯.

// keymap에서 행 별로 길이가 다르니까 이중 for문으로 size 받아서 하면 될 듯.

// idx가 0인 문자의 최소 type수는 1이니까 idx에 + 1 씩 해서 저장해야될 듯.

// 어떤 케이스에서 에러가 뜨는지 알 수가 없네 하

// 해당 문자가 자판에 없을 때 -1을 출력하라는걸 잘못 이해했었음;

#include <string>

#include <vector>

#include <map>



using namespace std;



vector<int> solution(vector<string> keymap, vector<string> targets) {

    vector<int> answer;

    map<char, int> min_type; // 요구되는 min 입력값

    // min_type 만들기

    for (int i = 0; i < keymap.size(); i++) {

        for (int j = 0; j < keymap[i].size(); j++) {

            char curr = keymap[i][j];   // curr 긁어오기

            if (min_type.find(curr) == min_type.end() || j + 1 < min_type[curr]) { // min_type[curr]는 정수값이므로 .end()와 비교연산을 할 수가 없잔아..

                min_type[curr] = j + 1;

            } 

        }

    }

    // search

    for (int i = 0; i < targets.size(); i++) {

        int sum = 0;

        for (int j = 0; j < targets[i].size(); j++) {

            char search = targets[i][j];

            if (min_type.find(search) != min_type.end()) {

                sum += min_type[search];

            } else {

                sum = -1;

                break;

            }

        }

        answer.push_back(sum);

    }

    return answer;

}

```



---

<br>




## 5. 코딩테스트 연습 > 연습문제 > 숫자 짝궁



<br>



```cpp

// 마지막에 숫자를 조합할 때 결과적으로 큰 수부터 앞에 배치하는 방식이니까.. map에 1~9 저장해놓고 개수 카운팅해서 앞에서부터 채워주면 될듯.

// X에서 하나씩 긁어서 Y에서 찾게 하니까 시간초과 뜬다.

// X랑 Y의 map을 각각 만들어서 따로 개수를 cnt하고, 둘중에 min값를 짝꿍의 개수로 설정하면 훨씬 빠를듯?

// 다 뜯어 고쳐야됨. 그냥 처음부터 다시

// 고쳤는데 어떤 케이스에서 에러가 발생하는건지 모르겠음;

#include <string>

#include <vector>

#include <map>

#include <algorithm>



using namespace std;



string solution(string X, string Y) {

    string answer = "";

    map<char, int> count_X;

    map<char, int> count_Y;

    // 탐색

    for (char curr : X) {

        count_X[curr]++;

    }

    for (char curr : Y) {

        count_Y[curr]++;

    }

    // 숫자 조합 : 9 -> 0

    for (char i = '9'; i >= '0'; i--) {

        int smaller = min(count_X[i], count_Y[i]); // smaller == 'i'의 짝꿍 생성 개수

        // i == '0' && '0' 이전에 짝꿍이 없어서 answer.empty() 인 경우 : 여기 실행

        if (i == '0' && answer == "") {

            if (smaller == 0) { // 전체에서 중복 x 경우

                answer += "-1";

                break;

            } else if (smaller > 0) { // '0'이전에 짝기 없었는데, '0'은 짝이 있는 경우 -> '0'은 한개만 가능

                answer += '0';

                break;   

            }

        }

        // 9 ~ 1 은 무조건 여기 실행 / i == '0' && '0' 이전에 짝꿍이 있어서 !answer.empty() 인 경우

        if (smaller > 0) {

            for (int j = 0; j < smaller; j++) {

            answer += i;

            }

        }   

        

    }

    return answer;

}

```



---

<br>

