#  Pick Apples - JAVA
#### Description:
Alice and Bob work in a beautiful orchard. There are N apple trees in the orchard. The apple trees are arranged in a row and they are numbered from 1 to N.
Alice is planning to collect all the apples from K consecutive trees and Bob is planning to collect all the apples from L consecutive trees.
They want to choose to disjoint segements (one consisting of K trees of Alice and the other consisting of L trees for Bob) so as not to disturb each other. you should return the maximum number of apples that they can collect.

N is an integer within the range: [2, 600]
K and L are integers within the range: [1, N - 1]
each element of array A is an integer within the range: [1, 500]
######Examples
Example 1:

input:
A = [6, 1, 4, 6, 3, 2, 7, 4]
K = 3
L = 2
Output: 
24
Explanation: 
beacuse Alice can choose tree 3 to 5 and collect 4 + 6 + 3 = 13 apples, and Bob can choose trees 7 to 8 and collect 7 + 4 = 11 apples.Thus, they will collect 13 + 11 = 24.
Example 2:

Input:
A = [10, 19, 15]
K = 2
L = 2
Output: 
-1
Explanation: 
beacause it is not possible for Alice and Bob to choose two disjoint intervals.

### Solution
`182 mstime cost - 14.50 MBmemory cost - Your submission beats 85.80 %Submissions`

```
public class Solution {
      /**
       * @param A: a list of integer
       * @param K: a integer
       * @param L: a integer
       * @return: return the maximum number of apples that they can collect.
       */
  public int PickApples(int[] A, int K, int L)
  {
      if (K + L > A.length) {
              return -1;
          }
      if (K + L == A.length){
              int sum = 0;
              for (int value : A) {
                  sum += value;
              }
              return sum;
          }
      int maxWhenAliceGoFirst = maxNumber(A, K, L);
      int maxWhenBobGoFirst = maxNumber(A, L, K);
      return Math.max(maxWhenAliceGoFirst, maxWhenBobGoFirst);
      }
  private int maxNumber(int [] arr, int first, int second) {
      int len = arr.length; 
      int index = 0;
      int summation = 0;
      for (int i = 0; i < len - first - second + 1; i++) {
          index = i;
          int sumFirst = 0;
          int sumSecond = 0; 
          for(int j = i; j < i + first; j++){
              sumFirst += arr[j];
          }
          for(int j= index + first; j < len && j < len - second + 1; j++) {
              int sum = 0;
              for(int l = j; l < j + second; l++){
                  sum += arr[l];
              }
              sumSecond = Math.max(sumSecond, sum);
          }
          summation = Math.max(summation, sumFirst + sumSecond);
      }
      return summation;
      }


  //    for (int i = 0; i < len - L - K + 1; i++) {
  //       index = i;
  //       int sumAlice = 0;
  //       int sumBob = 0; 
  //       for(int j = i; j < i + K; j++){
  //           sumAlice += A[j];
  //       }
  //       for(int j= index + K; j < len && j < len - L + 1; j++) {
  //           int sum = 0;
  //           for(int l = j; l < j + L; l++){
  //               sum += A[l];
  //           }
  //           sumBob = Math.max(sumBob, sum);
  //       }
  //       maxWhenAliceGoFirst = Math.max(maxWhenAliceGoFirst, sumAlice+sumBob);
  //    } 
}
```
