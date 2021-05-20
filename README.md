# Job_Scheduling

## 작업 스케줄링 문제란?
  > n개의 작업, 각 작업의 수행시간 t(i), 그리고 m개의 동일한 기계가 주어질 때 모든 작업이 가장 빨리 종료되도록 작업을 기계에 배정하는 문제입니다. (단, 한 작업은 배정된 기계에서 연속적으로 수행되어야 합니다. 또한 기계는 한 번에 하나의 작업만을 수행합니다.)

  => 모든 작업을 가장 빨리 종료하기 위헤 현재까지 배정된 작업에 대해서 가장 빨리 끝나는 기계에 새 작업을 배정하는 **그리디** 방법을 사용합니다.
  
### Approx_JobScheduling 알고리즘


### 1. 알고리즘 구현과정
  ![image](https://user-images.githubusercontent.com/80517119/118930557-db3b9680-b980-11eb-995d-1ddd0ca76042.png)


  - 1. 각 기계에 배정된 마지막 작업의 종료 시간을 0으로 초기화시킨다.


  ![image](https://user-images.githubusercontent.com/80517119/118930817-2eade480-b981-11eb-9d2b-76eceb3e0680.png)



  - 2. 가장 일찍 끝나는 기계를 찾아 n개의 작업을 1개씩 배정한다. 작업을 배정하고 수행시간을 더하여 갱신한다.

  - 3. 가장 늦게 끝나는 작업의 종료시간을 리턴한다.


### 2. Java 구현
  - 작업의 개수 n = [4,8,16] (작업시간 : 10초 이내의 랜덤값)
  - 기계의 개수 m = 2 
  ``` java
  import java.util.*;

public class Job_Scheduling {
    public static void main(String[] args) {
        Random random = new Random();
        Scanner sc = new Scanner(System.in);
        System.out.println("작업의 개수를 4, 8, 16 중에서 선택하여 입력");

        int n = sc.nextInt(); // 작업의 개수 n = [4, 8, 16]
        int m = 2; // 기계의 개수 m = 2
        int[] L = new int[m]; // m개의 기계 각각의 작업 종료 시간을 넣을 배열 생성
        for (int j = 0; j < L.length; j++) {
            L[j] = 0;
        } // 초기화시킨다
        System.out.println("각 작업 수행 시간");
        int[] time = new int[n]; // 각각의 작업 시간을 10초 이하의 랜덤값으로 생성
        for (int t = 0; t < time.length; t++) {
            time[t] = random.nextInt(9) + 1;
            System.out.println(time[t] + " ");
        }

        // Approx_JobScheduling 알고리즘 수행
        for (int i = 0; i < n; i++) {
            int min = 0;

                if (L[0] > L[1]) {
                    min = 1;
                }
                // 가장 일찍 끝나는 기계 찾기
                L[min] += time[i]; // 작업을 가장 일찍 끝아는 기계에 배정하고 수행시간을 더하여 갱신
            } // n개의 작업에 대해 수행

            int endtime = L[0];
            if (L[0] < L[1]) {
                endtime = L[1];
            } // 가장 늦은 작업 종료 시간

        System.out.println("종료 시간 : " + endtime);

    }
}
```
### 3. 실행 결과
 - n = 4 일 때


![image](https://user-images.githubusercontent.com/80517119/118950860-89513b80-b995-11eb-994a-12b06c7e72ca.png)


 - n = 8 일 때


![image](https://user-images.githubusercontent.com/80517119/118950951-a38b1980-b995-11eb-9f03-e85ab89d889c.png)


 - n = 16 일 때


![image](https://user-images.githubusercontent.com/80517119/118951069-bbfb3400-b995-11eb-8b85-5a515c270f71.png)


### 4. 시간복잡도
  - n개의 작업을 하나씩 가장 빨리 끝나는 기계에 배정하는데 for 루프가 (m-1)번 수행된다.
  - 모든 기계의 마지막 작업 종료 시간을 살펴 보아야 하므로 O(m)의 시간이 걸린다.
  - 따라서 **시간복잡도는**
    n개의 작업을 배정해야하고, 배열 L을 탐색해야하므로
    => n x O(m) + O(m) = **O(nm)** 이다.
    
 ### 5. 근사 비율
   - Approx_JobScheduling 알고리즘의 근사해를 OPT'라 하고, Brute Force의 최적해를 OPT라고 할 때, OPT' < 2OPT 이다.
  
  
  ![image](https://user-images.githubusercontent.com/80517119/118932454-06bf8080-b983-11eb-8dcc-b797e7f49db6.png)
  
  
  - Approx_JobScheduling 알고리즘으로 작업을 배정하였을때, 가장 마지막으로 배정된 작업 i가 T부터 수행되며, 모든 작업이 T+t(i)에 종료된다. 그러므로 **OPT' = T+t(i)** 이다.
  - T'는 작업 i를 제외한 모든 작업의 수행시간의 합을 기계의 수 m으로 나눈 값이다. 따라서 T'는 작업 i를 제외한 평균 종료 시간이다.
  - 그러므로 **T <= T'** 이 된다.
  - T <= T'를 이용한 OPT' < 2OPT 증명
  ![image](https://user-images.githubusercontent.com/80517119/118933100-c4e30a00-b983-11eb-9df3-f4e2b46a99a8.png)
  - **따라서 근사해는 최적해의 2배를 넘지 않는다**.
    
    
    
    
