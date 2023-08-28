---
layout: post
title: Algorithm Study_week_3
description: >
  Algorithm_week_3
sitemap: false
hide_last_modified: true
---

# Algorithm_week_3

---

<br>




## 1. 코딩테스트 연습 > 2022 KAKAO BLIND RECRUITMENT > 신고 결과 받기



```cpp

/*

    문제 요구사항 따라가면서 짜면 될 듯.

    

    과정 생각.

    1. a가 b를 신고했음. (메일 발송 위해서)

    2. c가 n번 신고를 받았음. (한사람에게 받은 다중 신고는 1회로 처리.)

    3. n > 1 인 모든 c를 체크.

    4. 3.에서 체크된 c를 신고한 사람들을 체크.

    5. 4.를 완료한 뒤 체크된 횟수를 return.

    

    변수를 어떻게 최소한으로 사용할지를 고민해야 할 듯.

    잡아먹는 메모리 용량이 중요한 느낌.

    ! id_list에서의 idx를 고유 idx로 사용해보자. - 이거 검색+추출 어떻게 할래 ?

    

    ! 필요 변수

    - 'a가 신고당한 횟수 b번' 을 저장할 map

    - 'a를 신고한 사람 b, c, d ...' 를 저장할 map

    - 'a가 확인메일을 받은 횟수 b번' 을 저장할 map 

    

*/



#include <string>

#include <vector>

#include <map>

#include <set>

#include <sstream>

using namespace std;



map<string, int> reported_cnt;          // 'a가 신고당한 횟수 b번' 을 저장 (이하 '1번 자료')  

map<string, vector<string>> for_mail;   // 'a를 신고한 사람 b, c, d ...' 를 저장할 map

map<string, int> mailed_cnt;            // 'a가 확인메일을 받은 횟수 b번' 을 저장할 map

set<string> check_unique;               // 'a가 b를 신고한 적이 있음'을 저장할 set(중복신고방지) : set은 이름으로 검색할 수 있고, cnt를 위한 int가 필요하지 않으므로 set이 적당하겠다.



void download_and_mail(vector<string> id_list, vector<string> report, int k) {



    // user name 받아서 자료 세팅하기

    for (int i = 0; i < id_list.size(); i++) {

        reported_cnt.insert(make_pair(id_list[i], 0));              // 1번 자료 세팅

        for_mail.insert(make_pair(id_list[i], vector<string>()));   // 2번 자료 세팅

        mailed_cnt.insert(make_pair(id_list[i], 0));                // 3번 자료 세팅

    }



    // 전달받은 신고목록(report 벡터)에서 자료 긁어와서 저장

    for (int i = 0; i < report.size(); i++) {

        stringstream ss(report[i]);

        string reporting_user, reported_user;   

        ss >> reporting_user >> reported_user;  // 신고인, 피신고인 긁어오기



        string report_combo = reporting_user + "_" + reported_user;  // 신고인_피신고인 콤보 문자열 만들기



        // 이번 시행에서 만든 콤보 문자열의 유일성 확인 

        if (check_unique.find(report_combo) == check_unique.end()) {    // set에서 찾았는데 없으면 

            check_unique.insert(report_combo);    // set에 추가해주고

            reported_cnt[reported_user]++;     // 피신고인 신고 당한 횟수++

            for_mail[reported_user].push_back(reporting_user);  // 피신고인을 신고한 사람 목록에 추가

        }

    }

    

    // 3번 자료에 데이터 넣기

    for (const auto entry : reported_cnt) {    // for문 이렇게 한번 써보자 ㅋㅋ

        if (entry.second >= k) {    // value가 k 이상이면 

            for (const string& reporter : for_mail[entry.first]) {  // 해당 사람을 신고한 전원에게 메일 발송

                mailed_cnt[reporter]++; // 메일 보낸 횟수++

            }

        }

    }

    

}



vector<int> solution(vector<string> id_list, vector<string> report, int k) {

    vector<int> answer;



    download_and_mail(id_list, report, k);



    // mailed_cnt에서 user 이름 검색으로 cnt값 긁어와서 push_back

    for (const string& id : id_list) {

        answer.push_back(mailed_cnt[id]);

    }



    return answer;

}





```

---

<br>



## 2. 코딩테스트 연습 >연습문제 > 햄버거 만들기

 

 ```cpp

 // 문제 주어진대로 짜면 될 듯.

// for문으로 검사하니까, 햄버거가 완성돼서 벡터에서 빠지고 idx가 sec_bread로 줄어들었을 때, 탐색 범위에 에러가 생기네.

// while문으로 돌리자.

// 이거 탐색을 i로 하면 안되겠다. 변수 따로 만들자.

// 어렵네 이거 ;;

// 숫자를 string에 받아서 고고



#include <string>

#include <vector>

using namespace std;



int solution(vector<int> ingredient) {

    int answer = 0;

    string download = "";

    int idx = 0; // 검사 시작 idx 설정





    // 문자열에 숫자 받기 

    for (int i = 0; i < ingredient.size(); i++) {

        download += to_string(ingredient[i]);

    }



    // 탐색

    while (idx < download.length()) {

        if (download.length() - idx >= 4) {

            string temp = download.substr(idx, 4);  // 검사할 부분 추출

            if (temp == "1231") {

                // 패턴을 찾았을 때 해당 부분을 제거하고, "1234"의 이전 문자부터 다시 탐색 시작

                download.erase(idx, 4);

                idx = max(0, idx - 3); // idx 재설정

                answer++;

            } else {    // temp != "1234"니까 다음 숫자로 이동

                idx++;

            }

        } else {    // 문자열이 4개보다 적게 남으면 break

            break;

        }

    }



    return answer;

}



 ```

---

<br>



## 3. 코딩테스트 연습 > 2018 KAKAO BLIND RECRUITMENT > [1차]프렌즈 4블록



```cpp
// codes

```





---

<br>

## 4. 코딩테스트 연습 > 2017 팁스타운 > 짝지어 제거하기



```cpp

// *풀이법 참고했음.

// stack를 사용해야 하는 이유를 떠올리기가 너무 어렵다.

// stack을 써야겠다 생각 하니까 끝.



#include <iostream>

#include <string>

#include <stack>

using namespace std;



int solution(string s) {

    stack<char> steak;

    

    for (char c : s) {  // s에서 하나씩 받아서

        if (!steak.empty() && steak.top() == c) {   // 비어있지x && 지금 받아온 문자랑 stack의 top이 같으면

            steak.pop();    // pop

        } else {    // 같지 않으면

            steak.push(c); // 방금 받은 문자를 push

        }

    }

    

    return steak.empty() ? 1 : 0;   // 비어있으면 1, 아니면 0 return

}

```

---

<br>



## 5. 코딩테스트 연습 > 연습문제 > 땅따먹기



```cpp

// 부분 최적해 -> 전체 최적해 니까 dp? 근데 dp로 안풀어도 될 것 같으니까 일단 해보자 

// 못한다 이거 ;

// top-down으로 해야겠음

// 점화식 구할 필요가 없어서 dp중에서는 쉬운 편인듯 ?



#include <iostream>

#include <vector>

#include <algorithm>    // max 사용 위해

using namespace std;



int dp[100001][4];



int solution(vector<vector<int>> land)

{

    int answer = 0;

    // 초기값 설정 : 첫번째 행은 이전 값이 없어서 참조를 못해. 그래서 직접 넣어줘야되는거임. row 2 부터는 가능하겄지.

    for (int i = 0; i < 4; i++) {

        dp[0][i] = land[0][i];

    }

    

    for (int i = 1; i < land.size(); i++) { // i는 행 idx

        for (int j = 0; j < 4; j++) {       // 한 행 탐색

            // '해당 열 제외하고 최댓값 + 현재 위치의 값'

            if(j==0) {  // dp[i][0] 설정

                dp[i][j] = max({dp[i-1][j+1], dp[i-1][j+2], dp[i-1][j+3]}) + land[i][j];

            }

            if(j==1) {  // dp[i][1] 설정

                dp[i][j] = max({dp[i-1][j-1], dp[i-1][j+1], dp[i-1][j+2]}) + land[i][j];

            }

            if(j==2) {  // dp[i][2] 설정

                dp[i][j] = max({dp[i-1][j-2], dp[i-1][j-1], dp[i-1][j+1]}) + land[i][j];

            }

            if(j==3) {  // dp[i][3] 설정

                dp[i][j] = max({dp[i-1][j-3], dp[i-1][j-2], dp[i-1][j-1]}) + land[i][j];

            }

            

            answer = max(answer, dp[i][j]); // 최댓값 갱신

        }

    }

    return answer;

}

```

