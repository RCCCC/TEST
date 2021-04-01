# Leetcode刷题打卡 2020/04//01
## 1006.笨阶乘
![题目介绍](QQ截图20210401114308.png)

***
题目分析：
> 算是找规律了 不过我找的规律太表面了： N小于4，可以直接按照N值输出； N>=4，第前三个数组成的乘除是正值，然后加上第四个数，继续下一个乘除操作，不过这里的乘除结果是负值，需要减去；一直循环下去就行。 最简单的规律： N<=4的时候还是直接返回相应的值； N>4时，返回N+offset[N%4],其中offset[] = {0,1,2,6,7}
***

```cpp
class Solution {
public:
    int clumsy(int N) {
        int clumsyResult = 0;
        int markRun = 0;
        int tempNumber = 0;
        if (N < 4) {
            switch (N) {
                case 3:
                    return 6;
                    break;
                case 2:
                    return 2;
                    break;
                case 1:
                    return 1;
                    break;
                default:
                    std::cout << "N is too small" << std::endl;
                    break;
            }
        }else {
            clumsyResult += N * (N - 1) / (N - 2);
            for(int i = N - 3; i > 0; i--) {
                switch (markRun) {
                    case 0:
                        clumsyResult += i;
                        markRun++;
                        break;
                    case 1:
                        tempNumber = i;
                        markRun++;
                        break;
                    case 2:
                        tempNumber *= i;
                        markRun++;
                        break;
                    case 3:
                        tempNumber /= i;
                        clumsyResult -= tempNumber;
                        tempNumber = 0;
                        markRun = 0;
                        break;
                    default:
                        break;
            }
        }
        if(tempNumber != 0) clumsyResult -= tempNumber;
        }
        return clumsyResult;
    }
};
```