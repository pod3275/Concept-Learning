# Concept Learning

## What is Concept Learning?

- Concept learning은 (input, output) 형태의 training example을 이용하여 boolean-valued function을 유추하는 것이다.
- 예시

  "Days in which Aldo enjoys his favorite water sport?"
  
  ![image](https://user-images.githubusercontent.com/26705935/41638939-d9f0de20-7496-11e8-9924-bb78d86bdef4.png)
  
  - attribute 종류
  
    ![image](https://user-images.githubusercontent.com/26705935/41639091-826ee09c-7497-11e8-92e2-78f032ea5448.png)
  
## Hypothesis Representation

- Concept learning을 위해서 input attribute에 따른 제약 조건을 <>로 표시한 형태.
- 예시)

  h = (?, Cold, High, ?, ?, ?)  
  ==> Aldo는 Cold, High 인 날씨에 play를 한다. (다른 attribute와는 무관함)
   
- Value
  - ? : 어떤 value가 와도 가능하다.
  - pi (공집합) : 모든 value에 대해서 불가능하다.
  - 특정 a : a에 대해서만 가능하다.
  
- h의 값
  - h(x) = 1 : input x가 h의 모든 제약 조건을 만족하는 경우 : x에 대해 h는 consistent하다.
  - h(x) = 0 : otherwise : x에 대해 h는 inconsistent하다.
  - 예시
  
    ![image](https://user-images.githubusercontent.com/26705935/41639320-41044e8e-7498-11e8-80ce-6cb0e0d42106.png)
    
    h1(x1) = 1, h2(x1) = 1, h3(x1) = 1      
    h1(x2) = 0, h2(x2) = 1, h3(x2) = 0

## General-to-Specific Ordering of hypothesis

- 정의

  ![image](https://user-images.githubusercontent.com/26705935/41639436-b9b70650-7498-11e8-84c0-31e1890fe640.png)
  
- h2가 h1보다 ? 개수가 많고, h2의 특정 value는 h1에 다 있는 경우, h2는 h1보다 more general 하다.
- 반대로 h1은 h2보다 more specific 하다.
- 예시)
  
  h1 = (Sunny, ?, ?, Strong, ?, ?), h2 = (Sunny, ?, ?, ?, ?, ?)  
  ==> h2 *>=g* h1  

## Compact Representation for Version Spaces
 - General Boundary G(H,D): Set of maximally general members of H consistent with D
 - Specific Boundary S(H,D): set of minimally general (i.e., maximally specific) members of H consistent with D
 
 ![image](https://user-images.githubusercontent.com/26705935/41898243-6cf517fa-7964-11e8-918c-25a56c00a738.png)

## Candidate Elimination Algorithm
 - Initialize G to the set of maximally general hypotheses in H
 - Initialize S to the set of maximally specific hypotheses in H
 - For each training example d, do 
 
### (1) Positive input
 - If d is positive example
   - Remove from G any hypothesis inconsistent with d
   - For each hypothesis s in S that is not consistent with d
     - Remove s from S
     - Add to S all minimal generalizations h of s  such that
       h is consistent with d, and some member of G is more general than h 
     - Remove from S any hypothesis that is more general than another hypothesis in S
     
     
 - yes 가 주어지면 : S update
 - 공통되는 부분을 남겨놓고, 나머지 attribute은 ? 로 놓기
 - S update하고, 기존 G 중에 S랑 맞지 않는 hypothesis는 빼버리기


### (2) Negative input
 - If d is negative example 
   - Remove from S any hypothesis inconsistent with d
   - For each hypothesis g in G that is not consistent with d
     - Remove g from G
     - Add to G all minimal specializations h of g  such that
       h is consistent with d, and some member of S is more specific than h
     - Remove from G any hypothesis that is less general than another hypothesis in G
     
 - no 가 주어지면 : G update
 - S랑 data랑 비교, S랑 no랑 같지 않은 attribute에 대해, S의 attribute value 써서 hypothesis 만들기 : 하나.

