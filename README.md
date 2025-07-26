# JavaStudy
JavaSE面向过程编程练习
```
public class Main {
    public static void main(String[] args) {
        //水仙花数
        for (int i = 100; i < 1000; i++) {
            int a = i / 100;
            int b = (i / 10) % 10;;
            int c = i % 10;
            if (a*a*a + b*b*b + c*c*c == i){
                System.out.println(i);
            }
        }
        //九九乘法表
        for (int i = 1; i < 10; i++) {
            for (int j = 1; j <= i; j++) {
                System.out.print(j + " * " + i + " = " +j * i + " ");
            }
            System.out.println("");
        }
        //斐波那契数列
        int a = 0;
        int b = 1;
        int target = 5;
        if (target == 0) {
            System.out.println(a);
        }else if (target == 1) {
            System.out.println(b);
        }else {
            for (int i = 0; i < target; i++) {
                int tmp = b;
                b = a + b;
                a = tmp;
            }
            System.out.println(b);
        }
    }
}
```
JavaSE面向对象编程练习
```
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] arr = new int[]{3, 5, 7, 2, 9, 0, 6, 1, 8, 4};
        BubbleSort(arr);
        System.out.println(Arrays.toString(arr));

        int[] arr1 = {1, 3, 4, 6, 7, 8, 10, 11, 13, 15};
        int target = 3;
        BinarySearch(arr1, target);
        BinarySearch1(0,arr1.length - 1, arr1, target);

        System.out.println(jump(5));
        System.out.println(jump1(5));

        System.out.println(Palindrome("ABCBA"));

        TowerOfHanoi('A','B', 'C', 3);
    }

    //汉诺塔
    public static void TowerOfHanoi(char a, char b, char c, int n){
        if (n == 1) {
            System.out.println(a + " -> " + c);
        }else {
            TowerOfHanoi(a, c, b, n - 1);
            System.out.println(a + " -> " + c);
            TowerOfHanoi(b, a, c, n - 1);
        }
    }
    //回文判断
    public static boolean Palindrome(String str) {
        char[] arr = str.toCharArray();
        int left = 0;
        int right = arr.length - 1;
        while (left < right) {
            if (arr[left] != arr[right]) {return false;}
            left++;
            right--;
        }
        return true;
    }
    //青蛙跳台
    public static int jump(int n){
        int a = 0;
        int b = 1;
        for (int i = 1; i <= n; i++) {
            int tmp = b;
            b = b + a;
            a = tmp;
        }
        return b;
    }
    //青蛙跳台递归
    public static int jump1(int n) {
        if (n == 0 || n == 1) return 1;
        return jump1(n - 1) + jump1(n - 2);
    }
    //二分搜索
    public static void BinarySearch(int[] arr, int target) {
        int low = 0;
        int high = arr.length - 1;
        while (low <= high) {
            int mid = (low + high) / 2;
            if (arr[mid] == target) {
                System.out.println(mid);
                break;
            }
            if (arr[mid] < target) {
                low = mid + 1;
            }
            if (arr[mid] > target) {
                high = mid - 1;
            }
        }
    }
    //二分搜索递归
    public static void BinarySearch1(int start, int end, int[] array, int target) {
        int mid = (start + end) / 2;
        if (array[mid] == target) {
            System.out.println(mid);
        }else if (array[mid] < target) {
            BinarySearch1(mid,end,array,target);
        }else if (array[mid] > target) {
            BinarySearch1(start,mid,array,target);
        }
    }
    //冒泡排序
    public static void BubbleSort(int[] arr) {
        for (int i = 0; i < arr.length - 1; i++) {
            boolean flag = false;
            for (int j = 0; j < arr.length - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                    flag = true;
                }
            }
            if (!flag) {
                break;
            }
        }
    }
}
```
