https://school.programmers.co.kr/learn/courses/30/lessons/12953


```java
class Solution {
    public int solution(int[] arr) {
        if(arr.length == 1) {
            return arr[0];
        }

        int gcd = getGCD(arr[0],arr[1]);

        int lcm = arr[0] * arr[1] / gcd;

        for(int i =2; i < arr.length; i++){
            gcd = getGCD(lcm, arr[i]);
            lcm = (lcm * arr[i])/ gcd;
        }


        return lcm;
    }
    
    public int getGCD(int num1, int num2){

        if(num1 % num2 == 0) {
            return num2;
        }

        return getGCD(num2, num1 % num2);
    }
}
```


최소 공배수 는 유클리드 호제법을 통해서 구할 수 있음.  
$$
(a*b) / gcd(a,b)
$$
최대 공약수는 서로 나눈 나머지가 0이 될 때까지 나누면 됨.  
gcd (최대 공약수)
$$
60\% 48 = 12
$$
$$
48 \% 12 = 0
$$
  

배열로 인해 여러 숫자가 들어온다면? 최소 공배수의 공배수의 공배수의...  
gcd(a,b,c,d) => gcd(gcd(a,b),c,d) => gcd(gcd(gcd(a,b),c),d)  
