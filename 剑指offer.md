---
title:剑指offer
typora-copy-images-to: images
---

## 数论和数字规律篇

### *整数中1出现的次数（43）

题目描述

求出1~13的整数中1出现的次数,并算出100~1300的整数中1出现的次数？为此他特别数了一下1~13中包含1的数字有1、10、11、12、13因此共出现6次,但是对于后面问题他就没辙了。ACMer希望你们帮帮他,并把问题更加普遍化,可以很快的求出任意非负整数区间中1出现的次数（从1 到 n 中1出现的次数）。

思路分析

解法1：

> 从1开始到n去遍历数，判断其是否含1，将最后的结果相加就是所求
>
> 那么如何判断呢？利用循环。
>
> 1. 目标数与10求余后得1说明其个位为1，
> 2. 再将目标数除10得到其他位是否为1
>
> 举例：11：
>
> 先从1开始，1%10=1，此时number+1=1，1/10后得到0，退出while循环；
>
> 2,3....9一样；number = 0
>
> 10开始，10%10 = 0 ，注意此时10是比大于等于10的数，对10进行10/10后得到的n=1,在while循环里得到number =  1，
>
> 11进入判断，11%10 = 1，个位为1，得到number = 1；11再除以10后，得到1，也就是再while循环里还需要判断一次，此时number=2；
>
> 最后结果1+1+2 = 4；

解法2

> 知识点： 
>
> ```
> /*
> 设N = abcde ,其中abcde分别为十进制中各位上的数字。
> 如果要计算百位上1出现的次数，它要受到3方面的影响：百位上的数字，百位以下（低位）的数字，百位以上（高位）的数字。
> ① 如果百位上数字为0，百位上可能出现1的次数由更高位决定。比如：12013，则可以知道百位出现1的情况可能是：100~199，1100~1199,2100~2199，，...，11100~11199，一共1200个。可以看出是由更高位数字（12）决定，并且等于更高位数字（12）乘以 当前位数（100）。
> ② 如果百位上数字为1，百位上可能出现1的次数不仅受更高位影响还受低位影响。比如：12113，则可以知道百位受高位影响出现的情况是：100~199，1100~1199,2100~2199，，....，11100~11199，一共1200个。和上面情况一样，并且等于更高位数字（12）乘以 当前位数（100）。但同时它还受低位影响，百位出现1的情况是：12100~12113,一共114个，等于低位数字（113）+1。
> ③ 如果百位上数字大于1（2~9），则百位上出现1的情况仅由更高位决定，比如12213，则百位出现1的情况是：100~199,1100~1199，2100~2199，...，11100~11199,12100~12199,一共有1300个，并且等于更高位数字+1（12+1）乘以当前位数（100）。
> */ 
> public class Solution {
>     public int NumberOf1Between1AndN_Solution(int n) {
>         int count = 0;//1的个数
>         int i = 1;//当前位
>         int current = 0,after = 0,before = 0;
>         while((n/i)!= 0){           
>             current = (n/i)%10; //高位数字
>             before = n/(i*10); //当前位数字
>             after = n-(n/i)*i; //低位数字
>             //如果为0,出现1的次数由高位决定,等于高位数字 * 当前位数
>             if (current == 0)
>                 count += before*i;
>             //如果为1,出现1的次数由高位和低位决定,高位*当前位+低位+1
>             else if(current == 1)
>                 count += before * i + after + 1;
>             //如果大于1,出现1的次数由高位决定,//（高位数字+1）* 当前位数
>             else{
>                 count += (before + 1) * i;
>             }    
>             //前移一位
>             i = i*10;
>         }
>         return count;
>     }
> }
> ```

```java
public class Solution {
    public int NumberOf1Between1AndN_Solution(int n) {
        int number = 0;// 用来计算每次1的次数
        for(int i=1;i<=n;i++){
            // 从1开始循环遍历n，一次比较大小
            number +=  NumberOf1(i);
        }
        return number;
    }
    public int NumberOf1(int n){
        // 
        int number = 0;
        while(n > 0){
            if(n % 10 == 1){
                // 先判断n的个位是否为1,是，number+1
                number ++;
            }
            n = n / 10; // 对于大于10的数，先除10
        }
        return number;
    }
}
```

### 数值的整数次方(16)

给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。保证base和exponent不同时为0

```java
class Solution16 {
    public double Power(double base, int exponent) {
        // 判断base为0的情况
        if (base == 0.0) {
            return 0.0;
        }
        if(exponent == 0){
            return 1.0;
        }
        // 如果exponent为负数
        return exponent > 0 ? powerWithUnsignedExponent(base,exponent):1.0/powerWithUnsignedExponent(base,-exponent);

    }

    // 进行运算
    private double powerWithUnsignedExponent(double base, int exponent) {
        double result = 1.0;
        for (int i = 1; i <= exponent; i++) {
            result *= base;
        }
        return result;
    }
}
```
### 最小的K个数（40）

输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。

思路分析：





代码实现

```java

```

### 数字在排序数组中出现的次数（53）

统计一个数字在排序数组中出现的次数。

```
{1, 2, 3, 3, 3, 3}， 3
```

思路分析

> 基本思想，排序树组想到二分查找法，
>
> 1. 先判断k的合法性；
> 2. 找到k首次出现的位置；
> 3. 再找到k最后出现的位置；
> 4. 步长就是所求；
>
> 如何进行2的操作呢？递归结束条件是起始下标大于末尾下标
>
> 1. 利用一个函数递归处理，传入数组，目标值，起始位置和最终位置，先算出中间值
> 2. 比较
>    - 中间值和k值一样，那么就去看中间值前面的元素是不是k，不是的话说明找到的就是起始k；如果中间值前面的元素值为k，那往前面查找即可，将末尾下标置为mid-1
>    - 中间值大于k，就去中间值的前半部分找，将末尾下标置为mid-1，
>    - 中间值小于k，就去后半部分查找，将起始下标置为mid+1
>
> 如何求得4？
>
> 1. 同样，中间值和k比较，
>    - 中间值等于k，看是否满足下标小于数组长度-1且mid后一个元素值为k不是的话，此时mid就是最后的元素，如果值是k，那就往右边继续查找
>    - 中间值大于k，往前边查找
>    - 中间值小于k，往后边找

代码实现

```java
class Solution53 {
    public int GetNumberOfK(int[] array, int k) {
        int res = 0; // 记录k出现次数
        // k的合法性
        if (k <= 0) return -1;
        if (array != null && array.length != 0) {
            // 找到k首次出现位置
            int first = getFirstK(array, k, 0, array.length - 1);
            // 找到k最后出现位置
            int last = getLastK(array, k, 0, array.length - 1);
            if (first > -1 && last > -1)
                res = last - first + 1;
        }
        return res;
    }

    // 找首次出现的k
    private int getFirstK(int[] array, int k, int low, int high) {
        if (low > high) return -1;
        int mid = (high + low) >> 1;

        if (array[mid] == k) {
            // 中间值是k，判断mid前一个元素是否也是k，不是则说明k是首次出现；返回下标
            if (mid > 0 && array[mid - 1] != k || mid == 0) {
                return mid;
            } else { // mid前一个元素也是k，查前半段
                high = mid - 1;
            }
        } else if (array[mid] > k) {
            // 从左边查找
            high = mid - 1;
        } else {
            low = mid + 1;
        }
        return getFirstK(array, k, low, high);
    }

    // 找最后出现的k
    private int getLastK(int[] array, int k, int low, int high) {
        if (low > high) return -1;

        int mid = (high + low) >> 1;

        if (array[mid] == k) {
            // 中间值就是k，mid=array.length-1说明到了尽头
            if (mid < array.length-1 && array[mid + 1] != k || mid == array.length - 1) {
                return mid;
            } else {
                low = mid + 1;
            }
        } else if (array[mid] < k) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }

        return getLastK(array, k, low, high);
    }
}
```





## 数组与矩阵篇

array.length 是列长度

array[i].length 是行长度

### 二维数组的查找（1）

```java
public class Solution {
    public boolean Find(int target, int [][] array) {
        boolean found = false; // 标志位，true表示找到，false表示未找到
        int rows = array.length; // 得到行数
        int columns = array[0].length;//得到列数
        
        if(rows > 0 && columns > 0){
            int row = 0;
            int column = columns - 1;
            while(row < rows && column >= 0){
                if(array[row][column] == target){ //相等即为找到
                    found = true;
                    break;
                }else if(array[row][column] > target){ //大于则往左上走
                    column--;
                }else{ //小于则往右下走
                    row++;
                }
            }
        }
        return found;
    }
}
```

### 替换空格（2）

<https://www.runoob.com/java/java-stringbuffer.html>

请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

```java
public class Solution {
	public static String replaceSpace(StringBuffer str) {

        // 1.遍历得到空格字符的个数
        int spaceNum = 0;
        for(int i = 0; i<str.length();i++){
            if(str.charAt(i) == ' '){
                spaceNum++;
            }
        }

        // 2.新的字符串长度
        int newLength = str.length() + 2 * spaceNum;
        // 3.确定两个指针，一个新的，一个旧的
        int indexOfOriginal = str.length()-1; //注意指针范围是0-str.length()-1
        int indexOfNew = newLength-1;
        // 4.执行扩容操作，防止越界
        str.setLength(newLength);

        // 5. 业务处理
        while(indexOfOriginal >= 0 && indexOfNew > indexOfOriginal){//旧的指针一直在前面，并且不会越界
            if(str.charAt(indexOfOriginal) == ' ')
            //如果旧的指针指向的字符为空，就从新的指针的下一位开始依次存入0,2,%
            {
                str.setCharAt(indexOfNew--,'0');
                str.setCharAt(indexOfNew--,'2');
                str.setCharAt(indexOfNew--,'%');
            }else{
                //不为空，则把旧的字符一一放到新的指针指向的位置
                str.setCharAt(indexOfNew--,str.charAt(indexOfOriginal));
            }
            indexOfOriginal--;
        }
        return str.toString();
    }
}
```

### 从尾到头打印链表（3）

输入一个链表，按链表值从尾到头的顺序返回一个ArrayList。

```java
/**
*    public class ListNode {
*        int val;
*        ListNode next = null;
*
*        ListNode(int val) {
*            this.val = val;
*        }
*    }
*
*/
import java.util.ArrayList;
import java.util.Stack;
public class Solution {
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
  
        //2. 压栈操作
        Stack<Integer> stack = new Stack<>();
        while(listNode != null){
            stack.push(listNode.val);
            listNode = listNode.next;
        }
        //3. 返回一个List
        ArrayList<Integer> list = new ArrayList<>();
        while(!stack.empty()){
            list.add(stack.pop());
        }
        return list;
        }
}
```

### 顺时针打印矩阵(29)

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字，例如，如果输入如下4 X 4矩阵： 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 则依次打印出数字1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.

思路分析：

>牛客网 云台的思路：
>
>左上和右下的坐标来确定一圈要打印的数据，每打印完一圈，左上的对角前进一个单位，右下的对角后退一个单位。
>
>1. 首先拿到该矩阵的列高和行高，如果为0 则报null;
>
>2. 定义左上和右下的坐标，只要左边小于右边，上边大于下边，用它们来确定要转几圈才打印完
>
>   left = 0 ,top = 0, right = col-1;bottom = row - 1;
>
>   1. 从左到右打印一行
>
>      > top不动，left从0到right,依次将值加到列表里
>
>   2. 从上往下打印一行
>
>      > right不动，top从top+1到bottom，依次将值加到列表里
>
>   3. 从右往左打印一行
>
>      > bottom不动，right从right-1到left, 依次将值加到列表里
>
>   4. 从下往上打印一行
>
>      > left不动，bottom从bottom-1到top,依次将值加到列表里
>
>3. 左上前进，右下后退
>
>   > left++;top++;right--;bottom--;
>
>

```java
import java.util.ArrayList;
public class Solution {
    public ArrayList<Integer> printMatrix(int[][] matrix) {
        int row = matrix.length; // 行数
        int col = matrix[0].length;//列数
        // 判断为空
        if (col == 0 || row == 0) {
            return null;
        }
        //
        int left = 0, top = 0, right = col - 1, bottom = row - 1;
        ArrayList<Integer> list = new ArrayList<>();
        while (left <= right && top <= bottom) {
            //
            for (int i = left; i <= right; i++) {
                list.add(matrix[top][i]);
            }
            //
            for (int i = top + 1; i <= bottom; i++) {
                list.add(matrix[i][right]);
            }
            //
            if ( top != bottom) {
                for (int i = right - 1; i >= left; --i) {
                    list.add(matrix[bottom][i]);
                }
            }
            //
            if (right != left) {
                for (int i = bottom - 1; i >= top + 1; --i) {
                    list.add(matrix[i][left]);
                }
            }
            left++;
            top++;
            right--;
            bottom--;
        }
        return list;
    }
}
```

### 连续子数组的最大和(42)

HZ偶尔会拿些专业问题来忽悠那些非计算机专业的同学。今天测试组开完会后,他又发话了:在古老的一维模式识别中,常常需要计算连续子向量的最大和,当向量全为正数的时候,问题很好解决。但是,如果向量中包含负数,是否应该包含某个负数,并期望旁边的正数会弥补它呢？例如:{6,-3,-2,7,-15,1,2,2},连续子向量的最大和为8(从第0个开始,到第3个为止)。给一个数组，返回它的最大连续子序列的和，你会不会被他忽悠住？(子向量的长度至少是1)

思路分析

> O(n)
>
> 考虑输入数组长度为0的情况；
>
> 链接：https://www.nowcoder.com/questionTerminal/459bd355da1549fa8a49e350bf3df484
> 来源：牛客网
>
> 用total记录累计值，maxSum记录和最大
> 基于思想：对于一个数A，若是A的左边累计数非负，那么加上A能使得值不小于A，认为累计值对
>           整体和是有贡献的。如果前几项累计值负数，则认为有害于总和，total记录当前值。此时若和大于maxSum 则用maxSum记录下来。

```java
public class Solution {
 public int FindGreatestSumOfSubArray(int[] array) {
        // 数组长度等于0
        if(array.length == 0) return 0;
        int maxSum = array[0]; // 记录最大的和
        int total = array[0];
        // for循环遍历整个数组
        for(int i = 1;i<array.length;i++){
            if(total <= 0){
                // 说明下标为i的元素对整体无贡献，不要
                total = array[i];
            }else{
                // 加
                total += array[i];
            }
            if(total > maxSum){
                maxSum = total;
            }
        }
        return maxSum;
    }
}
```

### 调整数组顺序使奇数位于偶数前面(21)

输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。



第一种方法类似于冒泡排序，不好想；

```java
package tmdoffer66;

/**
 * @ClassName: Demo21_ReOrderArray
 * @author: benjamin
 * @version: 1.0
 * @description: 输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，
 * 所有的偶数位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。
 * @createTime: 2019/08/29/10:09
 */

public class Demo21_ReOrderArray {
    public static void main(String[] args) {
        int[] array = {1,2,3,4,5};
        Solution21 solution21 = new Solution21();
        solution21.reOrderArray(array);
        for(int i = 0 ; i<array.length;i++){
            System.out.println(array[i]);
        }
    }

}

class Solution21 {
    public void reOrderArray(int[] array) {

        // 数组长度为0或1直接返回
        if (array.length == 0 || array.length == 1) {
            return;
        }
        // 遍历整个数组 O(n^2)
        for (int i = 0; i < array.length; i++) {
            for (int j = array.length - 1; j > i; j--) {
                // 判断奇偶
                if ((array[j] & 1) == 1 && (array[j-1] & 1) == 0) {
                    swap(array, j, j-1);
                }
            }
        }
    }

    // 交互数组元素
    private void swap(int[] array, int i, int j) {
        int temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }
}
```

第二种方法

用空间换时间

```java
public void reOrderArray2(int[] array) {
        //最简单的思路，创建同样大的数组，把原数组遍历2遍，
        //第一遍取出奇数放到新数组中，第二遍取出偶数放到新数组中
        int[] resultArr = new int[array.length];
        int temp = 0;

        for (int i = 0; i < array.length; i++) {
            // 为奇数加入
            if ((array[i] & 1) == 1) {
                resultArr[temp++] = array[i];
            }
        }
        for (int i = 0; i < array.length; i++) {
            // 为偶数加入
            if ((array[i] & 1) == 0) {
                resultArr[temp++] = array[i];
            }
        }
        System.arraycopy(resultArr, 0, array, 0, resultArr.length);
    }
```

补充：

Java中System.arraycopy的用法

System提供了一个静态方法arraycopy(),我们可以使用它来实现数组之间的复制。其函数原型是：

```java
public static native void arraycopy(Object src,int srcPos,Object dest, int destPos,int length)；
```

> ```
> * @param      src      the source array. 源数组
> * @param      srcPos   starting position in the source array. 源数组的起始位置
> * @param      dest     the destination array. 目标数组
> * @param      destPos  starting position in the destination data. 目标数组的起始位置
> * @param      length   the number of array elements to be copied. 复制的长度
> ```

举个栗子：

将array数组复制到新的数组中；

```java
int[] array = {1, 2, 3, 4, 5};
int[] targetArr = new int[array.length];
System.arraycopy(array,0,targetArr,0,array.length);
```

### 数组中只出现一次的数字（56）

一个整型数组里除了两个数字之外，其他的数字都出现了两次。请写程序找出这两个只出现一次的数字。

思路分析

> 1. 一个数异或自己还是0；
> 2. 依次异或这个数组中的元素，得到的值肯定是两个不相同的数的异或值
>
> 操作：
>
> 1. 根据这个值将数组分成第index位和该数一样的，和不一样的；
> 2. 分别异或这两个数组得到的值就是所求。
>
> 注意：
>
> 如何找到这个数的第index位为1呢，我们将这个数每次右移一位，直至该数**与1的值为0.**
>
> 如何判断某个数的从右数index位为1呢，同理，将这个数从移动index位与1之后如果为0说明是的。
>
> 总结：
>
> 右移index位与1为0说明该值index位为1.

代码

```java
//num1,num2分别为长度为1的数组。传出参数
//将num1[0],num2[0]设置为返回结果
public class Solution {
    public void FindNumsAppearOnce(int [] array,int num1[] , int num2[]) {
        int length = array.length;
        // 参数校验
        if (length == 2) {
            num1[0] = array[0];
            num2[0] = array[1];
            return;
        }
        // 遍历数组异或每一个元素，结果肯定是相异的那两个数的异或值
        int bitResult = 0;
        for (int i = 0; i < length; ++i) {
            bitResult ^= array[i];
        }
        // 找到该数第一个为1的位的位置
        int index = findFirst1(bitResult);
        // 遍历整个数组，对两个数组分别求异或即可。
        for (int i = 0; i < length; ++i) {
            if (isBit1(array[i], index)) {
                num1[0] ^= array[i];
            } else {
                num2[0] ^= array[i];
            }
        }
    }

    // 第index位为1
    private int findFirst1(int bitResult) {
        int index = 0;
        while (((bitResult & 1) == 0) && index < 32) {
            bitResult >>= 1;
            index++;
        }
        return index;
    }
    // 判断目标数的二进制表示中从右起数的index位是不是1
    private boolean isBit1(int target, int index) {
        return ((target >> index) & 1) == 1;
    }
}
```

### 和为S的两个数字（57）

题目描述

输入一个递增排序的数组和一个数字S，在数组中查找两个数，使得他们的和正好是S，如果有多对数字的和等于S，输出两个数的乘积最小的。

输出描述:

```
对应每个测试案例，输出两个数，小的先输出。
```

思路分析

> 排序数组，定义两个指针p1,p2
>
> p1指向小的数，p2指向大的数
>
> 如果array[p1] + array[p2] == s 加入集合输出
>
> array[p1] + array[p2] < s ,p1++，p1右移
>
> array[p1] + array[p2] == s ,p2--,p2左移

代码实现 

```java
import java.util.ArrayList;
public class Solution {
 public ArrayList<Integer> FindNumbersWithSum(int[] array, int sum) {
        ArrayList<Integer> list = new ArrayList<>();
        if (array == null || array.length == 0 || sum < 0)
            return list;
        int p1 = 0;
        int p2 = array.length - 1;
        while (p1 < p2) {
            if (array[p1] + array[p2] == sum) {
                list.add(array[p1]);
                list.add(array[p2]);
                break;
            } else if (array[p1] + array[p2] < sum) {
                p1++;
            } else {
                p2--;
            }
        }
        return list;
    }
}
```

### 和为S的连续正数序列（57）

小明很喜欢数学,有一天他在做数学作业时,要求计算出9~16的和,他马上就写出了正确答案是100。但是他并不满足于此,他在想究竟有多少种连续的正数序列的和为100(至少包括两个数)。没多久,他就得到另一组连续正数和为100的序列:18,19,20,21,22。现在把问题交给你,你能不能也很快的找出所有和为S的连续正数序列? Good Luck!

输出描述:

```
输出所有和为S的连续正数序列。序列内按照从小至大的顺序，序列间按照开始数字从小到大的顺序
```

思路分析

>  双指针问题，当总和小于sum，大指针继续+，否则小指针+
>
> 复盘：应该将list用的时候再创建，每次往result中加的是新的list对象；

代码描述

```java
import java.util.ArrayList;
public class Solution {
    public ArrayList<ArrayList<Integer>> FindContinuousSequence(int sum) {
        // 左神：双指针问题，当总和小于sum，大指针继续+，否则小指针+
        ArrayList<ArrayList<Integer>> result = new ArrayList<>();
        int plow = 1;
        int phigh = 2;
        while (phigh > plow) {
            // 算出两个指针之间的和
            int curSum = (phigh + plow) * (phigh - plow + 1) >> 1;
            // 相等，先放入list中，再放入result中
            if (curSum == sum) {
                ArrayList<Integer> list = new ArrayList<>();
                for (int i = plow; i <= phigh; i++) {
                    list.add(i);
                }
                result.add(list);
                plow++;
            } else if (curSum < sum) {
                phigh++;
            } else {
                plow++;
            }
        }
        return result;
    }
}
```

### 数组中重复的数字

在一个长度为n的数组里的所有数字都在0到n-1的范围内。 数组中某些数字是重复的，但不知道有几个数字是重复的。也不知道每个数字重复几次。请找出数组中任意一个重复的数字。 例如，如果输入长度为7的数组{2,3,1,0,2,5,3}，那么对应的输出是第一个重复的数字2。

思路分析

> map集合加入数值，value记为0。如果包含这个数，那么就说明重复了，然后将这个数放入输出数组中，返回真。

代码实现

```java
public boolean duplicate(int numbers[],int length,int [] duplication) { 
    HashMap<Integer,Integer> map = new HashMap<>();
    for(int i =0;i<length;i++){
        if(map.containsKey(numbers[i])){
            duplication[0] = numbers[i];
            return true;
        } else {
            map.put(numbers[i],0);
        }
    }
    return false;
}
```

### 数组中出现次数超过一半的数字(39) 不懂

数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。例如输入一个长度为9的数组{1,2,3,2,2,2,5,4,2}。由于数字2在数组中出现了5次，超过数组长度的一半，因此输出2。如果不存在则输出0。

思路分析

> 如果有符合条件的数字，则它出现的次数比其他所有数字出现的次数和还要多。
> 在遍历数组时保存两个值：
>
> - times：次数
> - result：当前数字
>
> 遍历下一个数字时，若它与之前保存的数字相同，则次数加1，否则次数减1；若次数为0，则保存下一个数字，并将次数置为1。
>
> 遍历结束后，所保存的数字即为所求。
>
> 之后，还要再判断它是否符合大于数组的一半。

代码实现

```java

```

### 旋转数组的最小数字

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。
输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。
例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。
NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。

思路分析

> 数组可以分为两个排序子数组，前面的子数组大于后面的子数组的值。
>
> 两个指针p1和p2
>
> p1指向数组的最左边
>
> p2 指向数组的最右边
>
> 计算中间midIndex的值。
>
> 如果发现midIndex的值在左边的数组，也就是说arr[midIndex] >= arr[p1] 此时说明，最小值在右边的子树，让p1指向midIndex即可
>
> 如果发现midIndex的值在右边的数组，也就是说arr[midIndex] <= arr[p1] 此时说明，最小值在左边的子树，让p2指向midIndex即可
>
> 还有一种情况array[minIndex] == array[p1] && array[minIndex] == array[p2]的情况，此时需要遍历找到最小的值。

代码实现

```java
public int minNumberInRotateArray(int[] array) {
    if (array == null || array.length == 0) {
        return 0;
    }
    int p1 = 0;
    int p2 = array.length - 1;
    int minIndex = 0;

    while (array[p1] >= array[p2]) {
        if (p2 - p1 == 1) {
            minIndex = p2;
            break;
        }
        minIndex = (p1 + p2) >> 1;
        if (array[minIndex] == array[p1] && array[minIndex] == array[p2])
            return minInOrder(array, p1, p2);
        if (array[minIndex] >= array[p1]) {
            p1 = minIndex;
        } else if (array[minIndex] <= array[p2]) {
            p2 = minIndex;
        }
    }
    return array[minIndex];
}


int minInOrder(int[] arr, int p1, int p2) {
    int result = arr[p1];
    for (int i = p1 + 1; i < p2 + 1; i++) {
        if (result > arr[i])
            result = arr[i];
    }
    return result;
}
```

### 把数组排成最小的数(45)

输入一个正整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。例如输入数组{3，32，321}，则打印出这三个数字能排成的最小数字为321323。

思路分析

> 将数组变成链表，然后借用链表中的方法进行排序，需要注意重写的方法，太巧妙了。
>
> ​        Collections.sort(list, new Comparator<Integer>() {
>             @Override
>             public int compare(Integer o1, Integer o2) {
>                 String s1 = o1 + "" + o2;
>                 String s2 = o2 + "" + o1;
>                 return s1.compareTo(s2);
>             }
>         });

代码描述

```java
class Solution45 {
    public String PrintMinNumber(int[] numbers) {
        // numbers有效
        if (numbers == null || numbers.length == 0) return "";
        String result = ""; // 返回结果
        // 将数组变成链表；
        ArrayList<Integer> list = new ArrayList<>();
        for (int num : numbers) {
            list.add(num);
        }
        // 集合工具类
        Collections.sort(list, new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                String s1 = o1 + "" + o2;
                String s2 = o2 + "" + o1;
                return s1.compareTo(s2);
            }
        });
        // 将list转为字符串；
        for(int j : list){
            result += j;
        }
        return result;
    }
}
```





## 链表篇

### 从尾到头打印链表（6）

输入一个链表，按链表从尾到头的顺序返回一个ArrayList。

思路分析：

> 方法一：利用栈的先进后出思想实现，加上判断条件后17ms，刚开始24ms

```java
class Solution {
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        // 1.判断链表为空或为1
        // 判断链表为空的情况
        if (listNode == null) {
            return new ArrayList<Integer>();
        }
        // 判断链表为1的情况，不用反转
        if (listNode.next == null) {
            return new ArrayList<>(listNode.val);
        }
        //2. 只要链表不为空，压栈操作,一直找下一个节点,直到空
        Stack<Integer> stack = new Stack<>();
        while (listNode != null) {
            stack.push(listNode.val);
            listNode = listNode.next;
        }
        //3.新建一个list用来存入弹出的值
        ArrayList<Integer> list = new ArrayList<>();
        //4.只要栈不为空，就弹出来
        while (!stack.empty()) {
            list.add(stack.pop());
        }
        //5. 返回list
        return list;
    }
}


class Solution6_2 {
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {

        //2. 压栈操作
        Stack<Integer> stack = new Stack<>();
        while (listNode != null) {
            stack.push(listNode.val);
            listNode = listNode.next;
        }
        //3. 返回一个List
        ArrayList<Integer> list = new ArrayList<>();
        while (!stack.empty()) {
            list.add(stack.pop());
        }
        return list;
    }

}
```

> 方法二：利用递归思想实现
>
> 注意：要将list定义在递归函数外面。

```java
import java.util.ArrayList;
public class Solution {
    ArrayList<Integer> list = new ArrayList<>();
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        if(listNode!=null){
            printListFromTailToHead(listNode.next);
            list.add(listNode.val);
        }
        return list;
    }
}
```

> 方法三：利用list中的方法：add(int index, Object ele):在index位置插入ele元素

```java
public class Solution {
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        ArrayList<Integer> list = new ArrayList<>();
        ListNode tmp = listNode;
        while(tmp!=null){
            list.add(0,tmp.val);
            tmp = tmp.next;
        }
        return list;
    }
}
```

总结：

1. ad(0, ele):在0位置插入ele元素,再次调用的时候，会把之前的元素放到顺次移动

   ```java
       public static void main(String[] args) {

           List<Integer> list = new ArrayList<>();
           for(int i = 0;i<10;i++){
               list.add(0,i);
           }

           System.out.print("测试list的add方法"+list);
           // 测试list的add方法[9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
           // void add(int index, Object ele):在index位置插入ele元素
       }
   ```

2. 注意所给链表为空或长度为1的情况，需要给出判断

### 链表中环的入口结点（23）

给一个链表，若其中包含环，请找出该链表的环的入口结点，否则，输出null。

思路分析：

> 两个指针：p1慢指针，p2快指针，同时从头结点出发
>
> 1. p2比p1快两个单位，走得快，所以将其作为while循环的判断条件
> 2. p2指向第二个节点，p1指向第一个节点
> 3. 只要p2等于p1说明链表中存在环，此时我们需要将p2重新指向头结点，然后直到p1等于p2的时候，该节点位置就是环的入口处；
>
> 证明见：
>
> <https://www.nowcoder.com/profile/631996/codeBookDetail?submissionId=1501635>

```java
/*
 public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}
*/
public class Solution {

    public ListNode EntryNodeOfLoop(ListNode pHead)
    {
        // 判断链表数目<=2
        if(pHead == null || pHead.next == null || pHead.next.next == null){
            return null;
        }
        // 定义两个节点，刚开始都指向头节点
        ListNode p1 = pHead;
        ListNode p2 = pHead;

        while(p2 != null && p2.next != null){
            // p1走一步， p2 走两步
            p1 = p1.next;
            p2 = p2.next.next.next;
            if(p1 == p2){ // 此时p1与p2相遇
                p2 = pHead; 
                // 再次将p1和p2进行移动
                while(p1 != p2){
                    p1 = p1.next;
                    p2 = p2.next;
                }
                // p1 和p2再次相遇即为入口
                if(p1 == p2){
                    return p1;
                }
            }
        }
        return null;
    }
}
```

### 反转链表（24）



### 删除链表中重复的结点（18）（不太懂）

在一个排序的链表中，存在重复的结点，请删除该链表中重复的结点，重复的结点不保留，返回链表头指针。 例如，链表1->2->3->3->4->4->5 处理后为 1->2->5

>思路分析：
>
>

代码实现：

```java
/*
 public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}
*/
public class Solution {
    public ListNode deleteDuplication(ListNode pHead) {
        // 当前链表为空或者为1直接返回
        if (pHead == null || pHead.next == null) return pHead;
        // 引入一个头结点
        ListNode Head = new ListNode(0);
        Head.next = pHead;
        ListNode pre = Head;
        ListNode last = Head.next;
        while (last != null) {
            if (last.next != null && last.next.val == last.val) {
                while (last.next != null && last.next.val == last.val) {
                    last = last.next;
                }
                pre.next = last.next;
                last = last.next;
            } else {
                pre = pre.next;
                last = last.next;
            }
        }
        return Head.next;
    }
}
```

小插曲乱入：

LeetCode237 题：[删除链表中的节点](https://leetcode-cn.com/problems/delete-node-in-a-linked-list/)

示例 1:

输入: head = [4,5,1,9], node = 5
输出: [4,1,9]
解释: 给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
示例 2:

输入: head = [4,5,1,9], node = 1
输出: [4,5,9]
解释: 给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.


说明:

链表至少包含两个节点。
链表中所有节点的值都是唯一的。
给定的节点为非末尾节点并且一定是链表中的一个有效节点。
不要从你的函数中返回任何结果。

思想：

> 待删节点为m，它的下一个节点是n，如果我们先将n的值拷给m，再把m的指针指向n的下一个节点，不就是很OK了。这道题明确指出不用考虑尾结点的情况，而且至少有两个节点，不用考虑节点为空的情况。如果题目没有说的话，需要怎么办呢？大家想一想，具体可以参考剑指offer的第18题。

解法：

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public void deleteNode(ListNode node) {
        // 把node下一个元素的值给node
        // node指向下一个元素的下一个元素位置
        node.val = node.next.val;
        node.next = node.next.next;
    }
}
```

### 反转链表（24）

输入一个链表，反转链表后，输出新链表的表头。

思路分析

>以3个节点为例：
>
>用pre记录当前节点的前一个节点
>
>用next记录当前节点的后一个节点
>
>1. 当前节点a不为空，进入循环，先记录a的下一个节点位置next = b;再让a的指针指向pre
>
>
>2. 移动pre和head的位置，正因为刚才记录了下一个节点的位置，所以该链表没有断，我们让head走向b的位置。
>3. 当前节点为b不为空，先记录下一个节点的位置，让b指向pre的位置即a的位置，同时移动pre和head
>4. 当前节点c不为空，记录下一个节点的位置，让c指向b，同时移动pre和head，此时head为空，跳出，返回pre。

画图

![1566641981584](D:\JavaNote\img\1566641981584.png)

代码

```java
/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
public class Solution {
    public ListNode ReverseList(ListNode head) {
         // 判断链表为空或长度为1的情况
        if(head == null || head.next == null){
            return head;
        }
        ListNode pre = null; // 当前节点的前一个节点
        ListNode next = null; // 当前节点的下一个节点
        while( head != null){
            next = head.next; // 记录当前节点的下一个节点位置；
            head.next = pre; // 让当前节点指向前一个节点位置，完成反转
            pre = head; // pre 往右走
            head = next;// 当前节点往右继续走
        }
        return pre;
    }
}
```

### 链表中倒数第K个节点（22）

输入一个链表，输出该链表中倒数第k个结点。

解法1：

需要遍历两次链表，不好，

第一次遍历求得链表的长度，第二次遍历从0遍历到size-k处；

注意：需要设置一个临时变量来进行遍历操作；

```java
/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
public class Solution {
  public ListNode FindKthToTail(ListNode head, int k) {
    // 判断当前链表是否为空,或长度为1
    if (head == null || head.next == null) {
      return head;
    }
    int size = 0; // 记录链表的长度
    ListNode temp = head;
    // 遍历得到当前链表的长度
    while (temp != null) {
      size++;
      temp = temp.next;
    }
    // k必须大于等于0，k必须小于size
    if (k <= 0 || k > size) {
      return null;
    }
    // 只需遍历size-k次即可
    for (int j = 0; j < size - k; j++) {
      head = head.next;
    }
    return head;
  }
}
```

解法2：

```java
/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
public class Solution {
   public ListNode FindKthToTail(ListNode head, int k) {
    // 判断当前链表是否为空或者k=0
    if (head == null || k == 0) {
      return null;
    }
    // 定义两个指针
    ListNode p1 = head;
    ListNode p2 = head;

    // 让p1先走k-1的位置
    for (int i = 0; i < k - 1; i++) {
      // 如果出现k的长度大于链表长度时，也就是说，链表遍历完，k-1还没有走到，此时需要返回null
      if (p1.next != null) {
        p1 = p1.next;
      } else {
        return null;
      }
    }
    // p1走到链表尾，p2也就走到了k的位置
    while (p1.next != null) {
      p1 = p1.next;
      p2 = p2.next;
    }
    return p2;
  }
}
```

### 两个链表的第一个公共结点

输入两个链表，找出它们的第一个公共结点。

利用HashMap的原理。O(mn)

一个存，一个在map中判断是否有这个key存在；

```java
import java.util.HashMap;
public class Solution {
 public ListNode FindFirstCommonNode(ListNode pHead1, ListNode pHead2) {

        if (pHead1 == null || pHead2 == null) return null;

        HashMap<ListNode, Integer> hashMap = new HashMap<ListNode, Integer>();
        ListNode node1 = pHead1;
        ListNode node2 = pHead2;

        // 遍历链表1,将node1作为key传入
        while (node1 != null) {
            hashMap.put(node1, node1.val);
            node1 = node1.next;
        }

        while (node2 != null) {
            if(hashMap.containsKey(node2))
                return node2;
            node2 = node2.next;
        }

        return null;
    }
}
```

解法二：

借助栈的后进先出的思想，这个怎么想到的呢？

链表1

> {1,2,3,6,7}

链表2

> {4,5,6,7}

![1566898520877](D:\JavaNote\images\1566898520877.png)

我们可以看到

> 1. 链表是单向的，如果有了公共节点，那么后面的节点一定是重合的:即6后面不可能再指向除7以外的其他节点了
> 2. 链表是单向的，所以只能从前往后进行寻找，如果我们能从后往前开始找的话，从最后一个公共节点出发，倒数的节点中最后一个节点就是我们要找的目标节点。

也就是将这两个链表的节点方法两个栈中，每次弹出尾结点进行比较，如果不同，说明上一个节点就是要找的公共节点。

peek和pop区别：

相同点：大家都返回栈顶的值。

不同点：peek 不改变栈的值(不删除栈顶的值)，pop会把栈顶的值删除。

代码实现

> 两个栈，分别存入链表1和链表2的节点
>
> 遍历入栈即可
>
> 出栈时：只要栈不为空且栈顶的元素一直相等。

```java
/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
import java.util.Stack;
public class Solution {
 public ListNode FindFirstCommonNode(ListNode pHead1, ListNode pHead2) {

     if (pHead1 == null || pHead2 == null) return null;
        Stack<ListNode> stack1 = new Stack<>();
        Stack<ListNode> stack2 = new Stack<>();
        // 入栈
        while (pHead1 != null) {
            stack1.push(pHead1);
            pHead1 = pHead1.next;
        }
        while (pHead2 != null) {
            stack2.push(pHead2);
            pHead2 = pHead2.next;
        }
        ListNode resultNode = null;
        // 出栈,栈不为空
        while (!stack1.isEmpty() && !stack2.isEmpty() && stack1.peek() == stack2.peek()) {
            stack2.pop();
            resultNode = stack1.pop();
        }
        return resultNode;
    }
}
```

解法3：

```java
/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
public class Solution {
   public ListNode FindFirstCommonNode(ListNode pHead1, ListNode pHead2) {

        if (pHead1 == null || pHead2 == null) return null;

        int length1 = getListlength(pHead1);
        int length2 = getListlength(pHead2);
        int dif = length1 - length2;

        ListNode pLong = pHead1;
        ListNode pShort = pHead2;

        if (length2 - length1 > 0) {
            pLong = pHead2;
            pShort = pHead2;
            dif = length2 - length1;
        }

        // 先让长链表走dif距离
        for (int i = 0; i < dif; i++) {
            pLong = pLong.next;
        }
        // 再让两链表同时出发
        while (pLong != null && pShort != null && pLong != pShort) {
            pLong = pLong.next;
            pShort = pShort.next;
        }
        return pShort;
    }

    public int getListlength(ListNode node) {
        int size = 0;
        while (node != null) {
            ++size;
            node = node.next;
        }
        return size;
    }
}
```

### 合并两个排序的链表（25）

输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。

归并排序

```java
class Solution25 {
    public ListNode Merge(ListNode list1, ListNode list2) {
        // 判断链表是否为空
        if(list1==null){
            return list2;
        }else if(list2==null){
            return list1;
        }
        // 存放结果
        ListNode resultList = null;
        // 根据每个链表中节点的大小取出小的值放到新的链表中
        if (list1.val < list2.val) {
            resultList = list1;
            resultList.next = Merge(list1.next, list2);
        } else {
            resultList = list2;
            resultList.next = Merge(list1, list2.next);
        }
        return resultList;
    }
}
```

### 复杂链表的复制(35)

输入一个复杂链表（每个节点中有节点值，以及两个指针，一个指向下一个节点，另一个特殊指针指向任意一个节点），返回结果为复制后复杂链表的head。（注意，输出结果中请不要返回参数中的节点引用，否则判题程序会直接返回空）

思路分析：

走完第一个函数后得到的新链表信息

![1567220326260](D:\JavaNote\images\1567220326260.png)



复制原始链表节点之间random的对应关系，拷贝到新节点对应节点上

此时链表奇数位置为原始链表，奇数位置为拷贝链表，返拷贝的那一部分

>  先将要返回的值记入newHead中，然后借助pNode和cloneNode来找出新链表和旧链表

如何操作呢？

假设此时pNode为1结点

只要pNode不为空，我们进入while循环中，先记录当前pNode的下一个节点位置，存到cloneNode中，比如1‘；

让pNode指向cloneNode的下一个节点位置也就是2的位置，让cloneNode指向它的下一个位置的下一个位置也就是2';

此时移动node节点到达它的下一个位置即2结点的位置处；

代码实现

```java
/*
public class RandomListNode {
    int label;
    RandomListNode next = null;
    RandomListNode random = null;

    RandomListNode(int label) {
        this.label = label;
    }
}
*/
public class Solution {
    public RandomListNode Clone(RandomListNode pHead) {
        // 链表为空直接返回
        if (pHead == null) return null;
        CloneNode(pHead);
        ConnectRandomNodes(pHead);
        return ReconnectNodes(pHead);
    }

    // 1. 复制原始链表的任意节点N并创建新节点N',再把N'连到N后面
    private void CloneNode(RandomListNode pHead) {
        // 记录头结点的位置
        RandomListNode pNode = pHead;
        while (pNode != null) {
            // 只拷贝N的值，注意next指针的变换，
            // 先把新节点插进去，再让原始节点指向下一个节点的位置，新节点指向当前节点的下一个位置
            // 创建新的节点，来自每次遍历到的节点；
            RandomListNode pCloned = new RandomListNode(pNode.label); // 先存入原始链表的结点值
            // 插
            pCloned.next = pNode.next;
            pNode.next = pCloned;
            // 动
            pNode = pNode.next.next;

        }
    }

    // 2. 复制原始链表节点之间random的对应关系，拷贝到新节点对应节点上
    // 注意，此时的链表是原始链表加拷贝链表
    private void ConnectRandomNodes(RandomListNode pHead) {
        RandomListNode pNode = pHead;
        // A
        while (pNode != null) {
            // pNode.next 新节点，比如说A'
            if (pNode.random != null) {
                // 觉得这句不好理解，可以画个图
                // pNode此时为1,1的random不为空，指向4,4的位置是pNode.random
                // 此时要让1’的random指向4'.也就是pNode.next.random 指向4的下一个位置4';
                pNode.next.random = pNode.random.next;
            } else {
                pNode.next.random = null;
            }

            // pNode移动，指向B
            pNode = pNode.next.next;
        }

    }

    // 3. 此时链表奇数位置为原始链表，奇数位置为拷贝链表，返拷贝的那一部分
    private RandomListNode ReconnectNodes(RandomListNode pHead) {
        RandomListNode pNode = pHead; //A
        RandomListNode newHead = pHead.next; // 记录新链表的头结点位置
        
        while(pNode != null){
            RandomListNode cloneNode = pNode.next;
            pNode.next = cloneNode.next;
            cloneNode.next = cloneNode.next == null ? null : cloneNode.next.next;
            pNode = pNode.next;
        }
        return newHead;
    }
}
```



## 栈和队列篇

### 用两个栈实现队列(9)

用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。

思路分析:

> 画图分析：
>
> 队列：先入先出。
>
> 1. 两个栈:stack1，stack2，我们将元素统一放入stack1中，要完成先入先出的pop()形式，借助于stack2
> 2. 依次将stack1中的元素弹入stack2中，这样，stack2的栈顶放的就是第一个进入的元素，达到了先入先出的效果；
> 3. 只要栈2为空，我们就依次往里面填入栈1的元素。最后依次返回栈2的元素；

代码：

```java
import java.util.Stack;

public class Solution {
    Stack<Integer> stack1 = new Stack<Integer>();
    Stack<Integer> stack2 = new Stack<Integer>();
    
    public void push(int node) {
        stack1.push(node);
    }

    public int pop() {
        if(stack1.empty()&&stack2.empty()){
            throw new RuntimeException("Queue is empty!");
        }
        // 只要stack2为空，就把stack1的数压入，再弹出
        if(stack2.empty()){
            while(!stack1.empty()){ // 栈1中元素数大于0，就一次压入栈2
                stack2.push(stack1.pop());
            }
        }
        return stack2.pop();
    }
}
```

小插曲：

使用队列实现栈的下列操作：https://leetcode-cn.com/problems/implement-stack-using-queues

push(x) -- 元素 x 入栈
pop() -- 移除栈顶元素
top() -- 获取栈顶元素
empty() -- 返回栈是否为空
注意:

你只能使用队列的基本操作-- 也就是 push to back, peek/pop from front, size, 和 is empty 这些操作是合法的。
你所使用的语言也许不支持队列。 你可以使用 list 或者 deque（双端队列）来模拟一个队列 , 只要是标准的队列操作即可。
你可以假设所有操作都是有效的（例如, 对一个空的栈不会调用 pop 或者 top 操作）。

```java
// 利用两个队列实现栈
class MyStack {
    private Deque<Integer> deque;

    /** Initialize your data structure here. */
    public MyStack() {
        deque = new LinkedList<>();
    }

    /** Push element x onto stack. */
    public void push(int x) {
        deque.add(x);
    }

    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        int last = deque.getLast();
        deque.removeLast();
        return last;
    }

    /** Get the top element. */
    public int top() {
        return deque.getLast();
    }

    /** Returns whether the stack is empty. */
    public boolean empty() {
        return deque.isEmpty();
    }

  }
```

```java
双链表

```



队列是一种特殊的线性表，它只允许在表的前端进行删除操作，而在表的后端进行插入操作。

LinkedList类实现了Queue接口，因此我们可以把LinkedList当成Queue来用。

```java
import java.util.LinkedList;
import java.util.Queue;
 
public class Main {
    public static void main(String[] args) {
        //add()和remove()方法在失败的时候会抛出异常(不推荐)
        Queue<String> queue = new LinkedList<String>();
        //添加元素
        queue.offer("a");
        queue.offer("b");
        queue.offer("c");
        queue.offer("d");
        queue.offer("e");
        for(String q : queue){
            System.out.println(q);
        }
        System.out.println("===");
        System.out.println("poll="+queue.poll()); //返回第一个元素，并在队列中删除
        for(String q : queue){
            System.out.println(q);
        }
        System.out.println("===");
        System.out.println("element="+queue.element()); //返回第一个元素 
        for(String q : queue){
            System.out.println(q);
        }
        System.out.println("===");
        System.out.println("peek="+queue.peek()); //返回第一个元素 
        for(String q : queue){
            System.out.println(q);
        }
    }
}

```

输出：

```
a
b
c
d
e
===
poll=a
b
c
d
e
===
element=b
b
c
d
e
===
peek=b
b
c
d
e
```



总结：

**offer，add 区别：**

一些队列有大小限制，因此如果想在一个满的队列中加入一个新项，多出的项就会被拒绝。

这时新的 offer 方法就可以起作用了。它不是对调用 add() 方法抛出一个 unchecked 异常，而只是得到由 offer() 返回的 false。

**poll，remove 区别：**

remove() 和 poll() 方法都是从队列中删除第一个元素。remove() 的行为与 Collection 接口的版本相似， 但是新的 poll() 方法在用空集合调用时不是抛出异常，只是返回 null。因此新的方法更适合容易出现异常条件的情况。

**peek，element区别：**

element() 和 peek() 用于在队列的头部查询元素。与 remove() 方法类似，在队列为空时， element() 抛出一个异常，而 peek() 返回 null。



### 包含min函数的栈（30）

定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。

思路分析

push

> 

pop

> 

min

> 

解法

```java
  Stack<Integer> dataStack = new Stack<Integer>();
    Stack<Integer> minStack = new Stack<Integer>();

    public void push(int node) {
        // 入栈
        // 首先往一个空的数据栈压值，都压入
        if(dataStack.isEmpty()){
            dataStack.push(node);
            minStack.push(node);
        } else if (node > dataStack.peek()) {
            // 再压入一个值如果比数据栈的元素大,大元素压入数据栈，
            // 先压辅助栈压入原来最小值
            minStack.push(minStack.peek());
            dataStack.push(node);
        } else {
            // 压入的值比数据栈栈顶元素小，都压入
            dataStack.push(node);
            minStack.push(node);
        }
    }

    public void pop() {
        // 如果数据栈为空，直接返回
        if (dataStack.isEmpty()) return;
        // 数据栈和辅助栈的栈顶元素相等，两个都弹出来
        if(dataStack.peek() == minStack.peek()){
            dataStack.pop();
            minStack.pop();
        } else {
            // 不等，只弹辅助栈栈顶元素
            minStack.pop();
        }
    }

    public int top() {
        return dataStack.peek();
    }

    public int min() {
        if(minStack.isEmpty()) return 0;
        return minStack.peek();
    }
```

### 栈的压入、弹出序列(31)

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否可能为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4,5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）

> 出栈序列是个什么东西?
>
> 比如，AB两个元素，入栈顺序为AB，出栈情况有两种：
>
> （1）入A，出A，入B，出B，出栈顺序为AB；
>
> （2）入A，入B，出B，出A，出栈顺序为BA。
>
> 出栈序列有两种情况。

思路分析

> 在数组pushA中取一个元素，先压入辅助栈中，
>
> 1. 比较栈顶元素与数组popA中的元素是否相同，相同就弹栈，数组popA中下标往前走一位。
> 2. 不等，直接压入栈，
> 3. 关于判断条件这里，首先想到的是肯定栈顶元素与popA序列中的元素相同，即stack.peek() == popA[j]，然后由于不断的要弹栈，肯定栈不为空。最后一个判断条件，数组popA的下标越界问题，因为j是不断的++的，不能加到popA.length位置，所以每次加完后判断一下j是否小于数组长度；大于说明数组popA完事了

```java
import java.util.ArrayList;
import java.util.Stack;
public class Solution {
     public boolean IsPopOrder(int[] pushA, int[] popA) {
        // 定义一个辅助栈
        Stack<Integer> stack = new Stack<>();
        // i用来遍历序列A，j用来遍历序列B
        for (int i = 0, j = 0;i < pushA.length; i++) {
            stack.push(pushA[i]); // 将A中的元素放入栈中
            // 发现栈不为空，且栈顶元素就是要弹出的元素（栈顶元素与popA序列中的元素相同）
            while(j < popA.length && stack.peek() == popA[j] && !stack.isEmpty()){
                stack.pop();
                j++;
            }
        }
        return stack.isEmpty();
    }
}
```



## 二叉树篇

### 重建二叉树（4）

### 二叉树的深度（55）

输入一棵二叉树，求该树的深度。从根结点到叶结点依次经过的结点（含根、叶结点）形成树的一条路径，最长路径的长度为树的深度。

```java
/**
public class TreeNode {
    int val = 0;
    TreeNode left = null;
    TreeNode right = null;

    public TreeNode(int val) {
        this.val = val;

    }

}
*/
public class Solution {
    public int TreeDepth(TreeNode root) {
        // 树不为空
        if(root == null)
            return 0;
        int nLeft = TreeDepth(root.left);
        int nRight = TreeDepth(root.right);
        return nLeft>nRight?nLeft+1:nRight+1;
    }
}
```

### 二叉树的镜像（27）

操作给定的二叉树，将其变换为源二叉树的镜像。

思路分析

顺次交换左右孩子信息；

> 1. 二叉树不能为空
> 2. 二叉树如果为一个节点的时候，也就是左右孩子为空，跳出
> 3. 到这二叉树肯定有孩子，先交换左右孩子
> 4. 如果左边孩子还有孩子，继续1,2,3
> 5. 如果右边孩子还有孩子，继续1,2,3

```java
/**
public class TreeNode {
    int val = 0;
    TreeNode left = null;
    TreeNode right = null;

    public TreeNode(int val) {
        this.val = val;

    }

}
*/
public class Solution {
    public void Mirror(TreeNode root) {
        TreeNode temp;
        // 二叉树如果为空
        if (root == null) {
            return;
        }
        if(root.left == null && root.right == null){
            return;
        }
        // 左右交换
        temp = root.left;
        root.left = root.right;
        root.right = temp;
        
        if (root.left != null) {
            Mirror(root.left);
        }
        if (root.right != null) {
            Mirror(root.right);
        }
    }
}
```

### 平衡二叉树（）

输入一棵二叉树，判断该二叉树是否是平衡二叉树。

> 是空树或者左右子树高数差的绝对值<= 1且左右子树都是AVL

```java
class Solution000 {

    public boolean IsBalanced_Solution(TreeNode root) {

        return getDepth(root) != -1;
    }

    private int getDepth(TreeNode root) {
        // 树为空返回0，它也是AVL
        if (root == null) {
            return 0;
        }
        // 判断左子树的高度
        int left = getDepth(root.left);
        // 如果子树的高度为-1,停止遍历，        
        if (left == -1) {
            return -1;
        }
        // 判断右子树的高度
        int right = getDepth(root.right);
        // 如果子树的高度为-1,停止遍历，
        if (right == -1) {
            return -1;
        }
        // 如果左子树和右子树的高度差绝对值大于1，说明不是平衡树，返回-1，否则返回当前高度
        return Math.abs(left - right) > 1 ? -1 : 1 + Math.max(left, right);
    }
}
```

### 树的子结构(26)

输入两棵二叉树A，B，判断B是不是A的子结构。（ps：我们约定空树不是任意一个树的子结构）

思路分析：

> 分为两步：
>
> ```
> // 01.树中结点含有分叉，树B是树A的子结构
> //                  8                8
> //              /       \           / \
> //             8         7         9   2
> //           /   \
> //          9     2
> //               / \
> //              4   7
> ```
>
> 1. 造一个result标志位记录是否有相同节点
> 2. A 和B不为空，8 = 8，此时去判断A中是否含有B的子树
> 3. B不为空，A也不为空。 8 = 8 ，去判断A中根节点8的左孩子与B中8的根节点的左孩子值是否一致
> 4. 9和8不等，返回false,都不用看&&的右边判断A的右孩子与B的右孩子的值了
> 5. 此时发现A的根节点8不是，我们往下走，先遍历8的左孩子作为起点，去判断时候包含B
> 6. 标志位还是false，8 = 8 ，以这个8节点为为起点判断是否包含B
> 7. 根节点对应上，看左孩子；左孩子也可以
> 8. 看右孩子

```java
class Solution26 {
    public boolean HasSubtree(TreeNode root1, TreeNode root2) {
        boolean flag = false;
        // 判断两树不为空
        if (root1 != null || root2 != null) {
            // 遍历root1找到与root2根节点相同的节点
            if (root1.val == root2.val) {
                flag = doesTree1HaveTree2(root1, root2);
            }
            // 从根节点的左子树开始匹配Tree2
            if (!flag) {
                flag = HasSubtree(root1.left, root2);
            }
            // 如果左子树没有匹配成功则继续在右子树中继续匹配Tree2
            if (!flag) {
                flag = HasSubtree(root1.right, root2);
            }
        }
        return flag;

    }

    private boolean doesTree1HaveTree2(TreeNode root1, TreeNode root2) {
        // 证明Tree2已经遍历结束，匹配成功
        if (root2 == null) return true;
        // 证明Tree1已经遍历结束，匹配失败
        if (root1 == null) return false;
        if (root1.val != root2.val) {
            return false;
        }
        // 递归验证左子树和右子树是否包含Tree2
        return doesTree1HaveTree2(root1.left, root2.left) && doesTree1HaveTree2(root1.right, root2.right);
    }

}
```

### 从上往下打印二叉树(32)

从上往下打印出二叉树的每个节点，同层节点从左至右打印。

思路分析：

> BFS 思想，也就是分层打印，每一层完了以后再进行下一层的打印
>
> 如何操作呢？
>
> 一个链表用来把节点弹出来，一个链表用来存放每次弹出来的值
>
> 1. 首先检验该树是否为空，为空返回null
> 2. 新建一个用来存放值的链表A
> 3. 新建一个用来存放节点的队列B，加入根节点
> 4. 只要队列B不为空，我们进入循环首先记录其节点数
> 5. for循环遍历该层依次弹出节点，将该节点放入A中，如果该节点有左右孩子，进行相应的入队列操作

代码实现：

```java
 // 分层依次打印
    public ArrayList<Integer> PrintFromTopToBottom(TreeNode root) {
        // 新建一个队列，存放树中的值
        ArrayList<Integer> res = new ArrayList<>();
        // 判断树是否为空
        if (root == null) {
            return res;
        }
        // 新建一个队列，存放节点
        LinkedList<TreeNode> queue = new LinkedList<>();
        queue.add(root);

        while (!queue.isEmpty()) {
            // 用来记录每一层的节点数目
            int levelSize = queue.size();

            for (int i = 0; i < levelSize; i++) {
                TreeNode currNode = queue.poll();
                res.add(currNode.val);
                if (currNode.left != null)
                    queue.add(currNode.left);
                if (currNode.right != null)
                    queue.add(currNode.right);
            }
        }
        return res;
    }
```

### 把二叉树打印成多行

从上到下按层打印二叉树，同一层结点从左至右输出。每一层输出一行。

```java
// 同层节点按照从左到右的顺序打印，每一层打印到一行
public ArrayList<ArrayList<Integer>> Print(TreeNode root) {
    if (root == null) {
        return root;
    }
    // 新建一个队列，存放树中的值
    ArrayList<ArrayList<Integer>>  res = new ArrayList<>();

    // 新建一个队列，存放节点
    LinkedList<TreeNode> queue = new LinkedList<>();
    queue.add(root);

    while (!queue.isEmpty()) {
        // 用来记录每一层的节点数目
        int levelSize = queue.size();
        ArrayList<Integer> currLevel = new ArrayList<>();
        for (int i = 0; i < levelSize; i++) {
            TreeNode currNode = queue.poll();
            currLevel.add(currNode.val);
            if (currNode.left != null)
                queue.add(currNode.left);
            if (currNode.right != null)
                queue.add(currNode.right);
        }
        res.add(currLevel);
    }
    return res;
}
```

### 二叉搜索树的后序遍历序列（33）

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。如果是则输出Yes,否则输出No。假设输入的数组的任意两个数字都互不相同。

思路分析

> 1. 首先检测数组不能为空，
> 2. 将需要递归的部分抽取出来，直接返回即可
>
> 如何递归呢？
>
> 1. 首先找到根节点，然后用一个分割点将这个数组分成两部分，
> 2. 前面比根节点的值小，后面的值比根节点大。
> 3. 这个分割点如何找呢？从刚开始 找到左右子树的分割点，即左边的值一直小于根节点值。此时的split一定是右边子树的第一个元素的位置；
> 4. 这样我们就可以将右边的子树进行遍历，看有无比根节点小的数存在，如果存在，那就报错。
> 5. 否则我们递归左子树和右子树，当两者都成立说明是BST.

代码实现

```java
public class Solution {
    public boolean VerifySquenceOfBST(int[] sequence) {
        int length = sequence.length;
        // 数组为空
        if (length == 0) {
            return false;
        }
        return isRight(sequence, 0, length - 1);
    }

    private boolean isRight(int[] sequence, int start, int end) {
        // 终止条件
        if (start >= end)
            return true;
        // 拿到root节点
        int root = sequence[end];
        // 找到左右子树的分割点，即左边的值一直小于根节点值。
        int split = start;
        for (; split < end && sequence[split] < root; split++) ;
        // 此时split是右子树的第一个元素的位置，判断右边子树有无小于根节点的值，有直接报错，因为不符合BST定义
        for (int i = split; i < end; i++) {
            if (sequence[i] < root) {
                return false;
            }
        }
        // 分别看左右子树的情况
        return isRight(sequence, start, split - 1) && isRight(sequence, split, end - 1);
    }
}
```

### 二叉树中和为某一值的路径（34）

输入一颗二叉树的根节点和一个整数，打印出二叉树中结点值的和为输入整数的所有路径。路径定义为从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。(注意: 在返回值的list中，数组长度大的数组靠前)

思路分析

> 

代码实现

```java

```



### 二叉搜索树与双向链表（36）不懂

输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的双向链表。要求不能创建任何新的结点，只能调整树中结点指针的指向。

思路分析

不懂

定义一个curr用来遍历整个二叉树；

用一个栈实现中序遍历操作；

pre用来保存中序遍历的上一个节点的位置；

1. curr = 10, stack为空
2. stack中加入10；
3. curr指向左孩子，即6，stack入6，curr指向4,4入stack
4. 此时curr指向4已经没有左孩子了，跳出while循环；
5. 弹出栈顶元素4，此时curr指向4
6. isFirst为true，让pRootOfTree指向4；pre指向4节点，isFirst置false;
7. 此时curr还是4；检查他的右孩子，curr.right指向了null;while循环进不去，直接弹出栈顶元素6，发现isFirst为false,pre的右节点置为6，然后让pre

代码实现

```java
class Solution36 {
    public TreeNode Convert(TreeNode pRootOfTree) {
        TreeNode curr = pRootOfTree;
        // 为空直接返回
        if(curr == null) return null;

        Stack<TreeNode> stack = new Stack<>();
        TreeNode pre = null;//保存中序遍历序列的上一节点
        boolean isFirst = true;
        while(curr!= null || !stack.isEmpty()){
            while(curr!= null){
                stack.add(curr);
                curr = curr.left;
            }
            curr = stack.pop();
            if(isFirst){
                pRootOfTree = curr;
                pre = curr;
                isFirst = false;
            } else{
                pre.right = curr;
                curr.left = pre;
                pre = curr;
            }
            curr = curr.right;
        }

        return pRootOfTree;
    }
}
```

### 对称的二叉树(28)

请实现一个函数，用来判断一颗二叉树是不是对称的。注意，如果一个二叉树同此二叉树的镜像是同样的，定义其为对称的。

思路分析

> 首先根节点以及其左右子树，左子树的左子树和右子树的右子树相同左子树的右子树和右子树的左子树相同即可，采用递归
>
> 

代码实现

```java
public class Solution {
    boolean isSymmetrical(TreeNode pRoot)
    {   
        return isSymmetrical(pRoot,pRoot);
    }
    boolean isSymmetrical(TreeNode root1,TreeNode root2){
        if(root1 == null && root2 == null) return true;
        if(root1 == null || root2 == null) return false;
        if(root1.val != root2.val) return false;
        
        return isSymmetrical(root1.left,root2.right) && isSymmetrical(root1.right,root2.left);
    }
}
```

DFS使用stack来保存成对的节点

1. **出栈**的时候也是**成对**成对的 ，
   1. 若都为空，继续；
   2. 一个为空，返回false;
   3. 不为空，比较当前值，值不等，返回false；
2. 确定入栈顺序，每次入栈都是成对成对的，如left.left， right.right ;left.rigth,right.left

```java
boolean isSymmetricalDFS(TreeNode pRoot)
{
    if(pRoot == null) return true;
    Stack<TreeNode> s = new Stack<>();
    s.push(pRoot.left);
    s.push(pRoot.right);
    while(!s.empty()) {
        TreeNode right = s.pop();//成对取出
        TreeNode left = s.pop();
        if(left == null && right == null) continue;
        if(left == null || right == null) return false;
        if(left.val != right.val) return false;
        //成对插入
        s.push(left.left);
        s.push(right.right);
        s.push(left.right);
        s.push(right.left);
    }
    return true;
}
```





## 字符串篇

lastIndexOf() 方法有以下四种形式：

- **public int lastIndexOf(int ch):** 返回指定字符在此字符串中最后一次出现处的索引，如果此字符串中没有这样的字符，则返回 -1。
- **public int lastIndexOf(int ch, int fromIndex):** 返返回指定字符在此字符串中最后一次出现处的索引，如果此字符串中没有这样的字符，则返回 -1。
- **public int lastIndexOf(String str):** 返回指定字符在此字符串中最后一次出现处的索引，如果此字符串中没有这样的字符，则返回 -1。
- **public int lastIndexOf(String str, int fromIndex):** 返回指定字符在此字符串中最后一次出现处的索引，如果此字符串中没有这样的字符，则返回 -1。

public String substring(int beginIndex, int endIndex)

- **beginIndex** -- 起始索引（包括）, 索引从 0 开始。
- **endIndex** -- 结束索引（不包括）。

### 字符串的排列（38）不懂

题目描述

输入一个字符串,按字典序打印出该字符串中字符的所有排列。例如输入字符串abc,则打印出由字符a,b,c所能排列出来的所有字符串abc,acb,bac,bca,cab和cba。

输入描述:

```
输入一个字符串,长度不超过9(可能有字符重复),字符只包括大小写字母。
```

思路分析

str.toCharArray() : 将字符串转换为字符数组。

String.valueOf(char [ ] ): **输出的是字符数组的数值。**

代码

递归算法

解析：http://www.cnblogs.com/cxjchen/p/3932949.html  (感谢该文作者！)

* 对于无重复值的情况
* 固定第一个字符，递归取得首位后面的各种字符串组合；
* 再把第一个字符与后面每一个字符交换，并同样递归获得首位后面的字符串组合； *递归的出口，就是只剩一个字符的时候，递归的循环过程，就是从每个子串的第二个字符开始依次与第一个字符交换，然后继续处理子串。
* 假如有重复值呢？
* 由于全排列就是从第一个数字起，每个数分别与它后面的数字交换，我们先尝试加个这样的判断——如果一个数与后面的数字相同那么这两个数就不交换了。
* 例如abb，第一个数与后面两个数交换得bab，bba。然后abb中第二个数和第三个数相同，就不用交换了。
* 但是对bab，第二个数和第三个数不 同，则需要交换，得到bba。
* 由于这里的bba和开始第一个数与第三个数交换的结果相同了，因此这个方法不行。
* 换种思维，对abb，第一个数a与第二个数b交换得到bab，然后考虑第一个数与第三个数交换，此时由于第三个数等于第二个数，
* 所以第一个数就不再用与第三个数交换了。再考虑bab，它的第二个数与第三个数交换可以解决bba。此时全排列生成完毕！

```java
class Solution38 {
    public ArrayList<String> Permutation(String str) {
        // 存入list中
        ArrayList<String> list = new ArrayList<String>();
        if (str != null && str.length() > 0) {
            PermutationHelper(str.toCharArray(), 0, list);
            Collections.sort(list);
        }
        return list;
    }
    // str.toCharArray() {a,b,c}
    private void PermutationHelper(char[] chars, int i, ArrayList<String> list) {
        if (i == chars.length - 1) {
            list.add(String.valueOf(chars));
        } else {
            Set<Character> charSet = new HashSet<Character>();
            for (int j = i; j < chars.length; ++j) {
                if (j == i || !charSet.contains(chars[j])) {
                    charSet.add(chars[j]);
                    swap(chars, i, j);
                    PermutationHelper(chars, i + 1, list);
                    swap(chars, j, i);
                }
            }
        }
    }

    private void swap(char[] cs, int i, int j) {
        char temp = cs[i];
        cs[i] = cs[j];
        cs[j] = temp;
    }
}
```

### 翻转单词顺序列(58)

牛客最近来了一个新员工Fish，每天早晨总是会拿着一本英文杂志，写些句子在本子上。同事Cat对Fish写的内容颇感兴趣，有一天他向Fish借来翻看，但却读不懂它的意思。例如，“student. a am I”。后来才意识到，这家伙原来把句子单词的顺序翻转了，正确的句子应该是“I am a student.”。Cat对一一的翻转这些单词顺序可不在行，你能帮助他么？

思路分析

>Student. a is He
>
>先翻转整个字符串 .tnedutS a si eH
>
>再翻转单个单词，根据空格的位置进行判断
>
>最后一个单词需要特殊处理，即就是需要判断i是否到了边界
>
>总结：
>
>1. str.toCharArray()将字符串转为字符数组
>2. String.ValueOf(chars)将字符数组变成字符串
>3. chars[i] == ' ' : 字符用单引号，空格用`' '`标记

 代码实现

```java
 public String ReverseSentence(String str) {
        if (str == null || str.length() == 0) {
            return str;
        }
        char[] chars = str.toCharArray();
        // 先翻转整个字符数组
        Reverse(chars, 0, chars.length - 1);
        int start = 0; // 单词的起始位置。
        // 再根据空格挨个翻转
        for (int i = 0; i <= chars.length; i++) {
            // 注意最后一个单词末尾是没有空格的，因此需要加上i==chars.length判断
            if (i == chars.length || chars[i] == ' ') {
                // 翻转i前面的数
                Reverse(chars, start, i-1);
                start = i+1;// 到了下一个单词了
            }
        }
        return String.valueOf(chars);
    }

    // 翻转字符串
    void Reverse(char[] chars, int p1, int p2) {
        while (p1 < p2) {
            char temp = chars[p1];
            chars[p1] = chars[p2];
            chars[p2] = temp;
            p1++;
            p2--;
        }
    }
```

### 左旋转字符串（58）

汇编语言中有一种移位指令叫做循环左移（ROL），现在有个简单的任务，就是用字符串模拟这个指令的运算结果。对于一个给定的字符序列S，请你把其循环左移K位后的序列输出。例如，字符序列S=”abcXYZdef”,要求输出循环左移3位后的结果，即“XYZdefabc”。是不是很简单？OK，搞定它！

思路分析

> 由hello world =>world hello得到的启示：
>
> world hello可以看成是向左移动了若干位得到的
>
> 那么abcXYZdef，左移3位后的结果，即“XYZdefabc”
>
> 先将其前三位翻转一下，得到cba
>
> 再将XYZdef 翻转一下得fedZYX
>
> 此时字符数组cbafedZYX，再翻转一次，得到XYZdefabc

代码实现

```java
public class Solution {
    public String LeftRotateString(String str,int n) {
        // 字符串为空，长度为0，或n为0，直接返回。
        if (str == null || str.length() == 0|| n == 0) {
            return str;
        }
        // 判断n合法
        if(n > str.length() || n < 0){
            throw new IndexOutOfBoundsException("输入n不合法");
        }

        char[] chars = str.toCharArray();
        // 先翻转0-n-1位置的元素
        Reverse(chars, 0, n-1);
        // 再翻转n到字符数组末尾的元素
        Reverse(chars, n, chars.length-1);
        // 再转整体
        Reverse(chars,0,chars.length-1);

        return String.valueOf(chars);
    }

    // 翻转字符串
    void Reverse(char[] chars, int p1, int p2) {
        while (p1 < p2) {
            char temp = chars[p1];
            chars[p1] = chars[p2];
            chars[p2] = temp;
            p1++;
            p2--;
        }
    }
}
```

### 字符流中第一个不重复的字符（50）

请实现一个函数用来找出字符流中第一个只出现一次的字符。例如，当从字符流中只读出前两个字符"go"时，第一个只出现一次的字符是"g"。当从该字符流中读出前六个字符“google"时，第一个只出现一次的字符是"l"。

输出描述:

```
如果当前字符流没有存在出现一次的字符，返回#字符。
```

思路分析

> 定义一个HashMap来存放，key用来存放字符，value 存放字符出现的次数
>
> 遍历HashMap找到次数为1的那个key即可。
>
> 知识点：
>
> String str = " " + 字符，可以将字符加入String中；
>
> 字符数组默认初始化为null;

```java
class Solution50 {
    HashMap<Character,Integer> map = new HashMap<>();
    String str = "";
    //Insert one char from stringstream
    public void Insert(char ch)
    {
        str += ch;
        if(map.get(ch) == null){
            map.put(ch,1);
        }else {
            map.put(ch,map.get(ch)+1);
        }
    }
    //return the first appearence once char in current stringstream
    public char FirstAppearingOnce()
    {
        char[] chars =  str.toCharArray();
        // 遍历HashMap
        for(char ch:chars){
            if(map.get(ch) == 1) return ch;
        }
        return '#';
    }
}
```

### 第一个只出现一次的字符（50）

在一个字符串(0<=字符串长度<=10000，全部由字母组成)中找到第一个只出现一次的字符,并返回它的位置, 如果没有则返回 -1（需要区分大小写）.

思路分析

> 利用hashmap，将字符作为key,如果重复了就将value+1，这里注意的是刚开始key值为null的情况。
>
> 最后for循环遍历找到字符数组中的位置。

代码实现

```java
import java.util.HashMap;

public class Solution {
    public int FirstNotRepeatingChar(String str) {
        // 转换为字符数组
        char[] chars = str.toCharArray();
        HashMap<Character, Integer> map = new HashMap<>();
        for (int i = 0; i < chars.length; i++) {
            if (map.get(chars[i]) == null) {
                map.put(chars[i], 1);
            } else {
                map.put(chars[i], map.get(chars[i]) + 1);
            }
        }
        for(int i = 0;i<chars.length;i++){
            if(map.get(chars[i]) == 1) return i;
        }
        return -1;
    }
}
```



把字符串转换成整数

将一个字符串转换成一个整数(实现Integer.valueOf(string)的功能，但是string不符合数字要求时返回0)，要求不能使用字符串转换整数的库函数。 数值为0或者字符串不是一个合法的数值则返回0。

输入描述:

```
输入一个字符串,包括数字字母符号,可以为空
```

输出描述:

```
如果是合法的数值表达则返回该数字，否则返回0
```

示例1

输入

```
+2147483647
    1a33
```

输出

```
2147483647
    0
```

思路分析

> 

代码实现

```java

```

### 正则表达式匹配（19）

请实现一个函数用来匹配包括`'.'`和`'*'`的正则表达式。模式中的字符`'.'`表示任意一个字符，而`'*'`表示它前面的字符可以出现任意次（包含0次）。 在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串`"aaa"`与模式`"a.a"`和`"ab*ac*a"`匹配，但是与`"aa.a"`和`"ab*a"`均不匹配

思路分析

> 

代码实现

```java

```



### 表示数值的字符串（20）

请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。例如，字符串"+100","5e2","-123","3.1416"和"-1E-16"都表示数值。 但是"12e","1a3.14","1.2.3","+-5"和"12e+4.3"都不是。

思路分析

> 正则表达式的应用。

代码实现

```java
class Solution20 {
    //正则表达式解法
    public class Solution {
        public boolean isNumeric(char[] str) {
            String string = String.valueOf(str);
            return string.matches("[\\+\\-]?\\d*(\\.\\d+)?([eE][\\+\\-]?\\d+)?");
        }
    }
/*
以下对正则进行解释:
[\\+\\-]?            -> 正或负符号出现与否
\\d*                 -> 整数部分是否出现，如-.34 或 +3.34均符合
(\\.\\d+)?           -> 如果出现小数点，那么小数点后面必须有数字；
                        否则一起不出现
([eE][\\+\\-]?\\d+)? -> 如果存在指数部分，那么e或E肯定出现，+或-可以不出现，
                        紧接着必须跟着整数；或者整个部分都不出现
*/
}
```


## 排序和查找篇



## 递归和循环篇

总结

> 2^(n-1)可以用位移操作进行: 1<< (n-1)
> 如果递归不好思考的话，可以找规律，代码很简单

### 斐波那契数列（10）

大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项（从0开始，第0项为0）。

n<=39

```java
public class Solution {
    public int Fibonacci(int n) {
        // 先判断n必须在范围内取值
        if(n > 39 && n <= 0) return 0;
        // 为1直接返回
        if(n == 1) return 1;
        
        int a = 0;
        int b = 1;
        int result = 0;
        for(int i = 2;i<=n;i++){
            result = a + b;
            a = b;
            b = result;
        }    
        return result;       
    }
}
```

### 跳台阶(10)

一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）。

```java
public class Solution {
    public int JumpFloor(int target) {
        if(target == 1) return 1;
        if(target == 2) return 2;
        int a = 1;
        int b = 2;
        int result = 0;
        for(int i = 3;i<=target;i++){
            result = a + b;
            a = b;
            b = result;
        }
        return result;
    }
}
```

### 变态跳台阶
一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

```java
class Solution {
    public int JumpFloorII(int target) {
        if(target == 1) return 1;
        return (int)Math.pow(2,target-1);
    }
}

public class Solution {
    public int JumpFloorII(int target) {
        if(target == 1) return 1;
       // return (int)Math.pow(2,target-1);
        return 1<<(target -1);
    }
}
```

```
我们可以用2*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2*1的小矩形无重叠地覆盖一个2*n的大矩形，总共有多少种方法？
```

> 思路分析：
>
> 画图吧，少年。
>
> 1. n = 0 时， 0种；
> 2. n = 1 时，1个2 * 1的小矩形去覆盖1个2 * 1 的矩形，1种；
> 3. n = 2 时，1个2 * 1的小矩形去覆盖2个2 * 1 的矩形，2种；
> 4. n = 3 时，1个2 * 1的小矩形去覆盖3个2 * 1 的矩形，3种；

斐波那契数列由此可以推导出公式：

公式是：f(n) = f(n-1)+f(n-2), n>2

f(1) = 1，f(0) = 0 ,f(2) = 2

```java
public class Solution {
    public int RectCover(int target) {
        if(target == 0) return 0;
        if(target == 1 || target == 2) 
            return target;
        // n>=2的情况
        return RectCover(target - 1) + RectCover(target - 2);
    }
}
```

## 位运算篇

实战中常用的位运算符

x & 1 == 0 偶数  == 1 奇数代替（x%2== 1)

x = x & (x - 1) 清零最低位的1

x & -x 得到最低位的1





### 二进制中1的个数(15)

思路分析：

一般思路：是直接将n与1进行与运算，为1，则count加1，继续将n进行右移一位。循环直至n为0；但是n如果是负数，则会导致死循环；

进一步：

我们不移动n了，左移数字1

先将n与1运算，为1，则表示最低位是1

> 2^(n-1)可以用位移操作进行: 1<< (n-1)
> 如果递归不好思考的话，可以找规律，代码很简单

否则将这个1进行左移1位

为1则表示n的次低位也是1；

直至循环到1左移为0的时候结束。

更优解法：

> 有一个整数a，如果a不为0，则表示a的二进制形式中至少有一位是1
>
> 1. 最后一位是1，a-1，则二进制中最后一位为0，其他位不变。就等价于最后一位取反
> 2. 假设最后一位是0，而第m位是1，a-1，则二进制中第m位前面的位数不变，第m位变为0，第m位后面的位数变为1
>
> 由1,2可以分析，只要一个数减1，最右边的1变为0，如果最右边还有0，则把所有的0变为1，而它的左边的所有位都不变。
>
> 一个整数n和它减去1即n-1的整数进行与运算，相当于将整数的最右边的1变为0；
>
> 如： 1100   
>
> 1. 减1 后得到 1011
> 2. 1100 & 1011 得到 1000 
>
> 这样操作一次，说明原来整数中就存在一个1；

```java
public class Solution {
    public int NumberOf1(int n) {
        int count = 0;
        while(n != 0){
             count++;
             n = (n-1) & n;
          }
          return count;
        }
}
```

## 回溯和DFS篇







## 求1+2+3+...+n

求1+2+3+...+n，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

```java
public class Solution {
    public int Sum_Solution(int n) {
        int sum = (int) (Math.pow(n,2) + n);
       return sum>>1;
    }
}


解题思路：
1.需利用逻辑与的短路特性实现递归终止。 2.当n==0时，(n>0)&&((sum+=Sum_Solution(n-1))>0)只执行前面的判断，为false，然后直接返回0；
3.当n>0时，执行sum+=Sum_Solution(n-1)，实现递归计算Sum_Solution(n)。
    public int Sum_Solution(int n) {
        int sum = n;
        boolean ans = (n>0)&&((sum+=Sum_Solution(n-1))>0);
        return sum;
    }
    

链接：https://www.nowcoder.com/questionTerminal/7a0da8fc483247ff8800059e12d7caf1
来源：牛客网
```



## 不用加减乘除做加法

5+7 如何进行运算

5对应的二进制是101

7对应的二进制是111

1. 二进制各位相加但不进位，得到010
2. 记录进位：1010
3. 2和3的结果相加得到1100 即就是12

代码实现思路

> 1. 相当于两数求异或，得到一个sum
> 2. 记录进位相当于将两数先与再左移一位，得到一个carry
> 3. 1,2步骤重复进行，把sum值当num1,carry当num2，直到num2左移为0为止。

```java
public class Solution {
    public int Add(int num1,int num2) {
        int sum,carry;
        while(num2 != 0){
            // 1.两个数进行异或运算
            sum = num1 ^ num2;
            // 2.两个数先与找到1的位置，再往左移动1位，产生进位效果
            carry = (num1 & num2) << 1;
            // 3.
            num1 = sum;
            num2 = carry;
        }
        return num1;
    }
}
```

## 构建乘积数组

给定一个数组A[0,1,...,n-1],请构建一个数组B[0,1,...,n-1],其中B中的元素B[i]=A[0]*A[1]*...*A[i-1]*A[i+1]*...*A[n-1]。不能使用除法。

思路分析：

>

