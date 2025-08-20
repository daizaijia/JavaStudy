# JavaStudy
**JavaSE面向过程编程练习**
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
**JavaSE面向对象编程练习**
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
**JavaSE集合类编程练习：学生管理系统**  
* Student.java
```
import java.util.Objects;

public class Student {
    private String id;
    private String name;
    private int score;

    public Student(String id, String name, int score) {
        this.id = id;
        this.name = name;
        this.score = score;
    }

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getScore() {
        return score;
    }

    public void setScore(int score) {
        this.score = score;
    }

    @Override
    public String toString() {
        return "Student{" +
                "id='" + id + '\'' +
                ", name='" + name + '\'' +
                ", score=" + score +
                '}';
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return Objects.equals(id, student.id); // 只按学号判断
    }

    @Override
    public int hashCode() {
        return Objects.hash(id); // 只用学号计算hash
    }

}
```
* StudentManager.java
```
import java.util.*;
import java.util.stream.Collectors;

public class StudentManager {
    private final List<Student> students = new ArrayList<>();

    // 添加单个学生
    public void add(Student s) {
        // TODO: 直接添加到 students
        students.add(s);
    }

    // 批量添加
    public void addAll(Collection<Student> batch) {
        // TODO: 批量添加（提示：addAll）
        students.addAll(batch);
    }

    // 打印当前列表
    public void printAll() {
        students.forEach(System.out::println);
        System.out.println("总人数: " + students.size());
    }

    // 排序：分数降序，同分按姓名升序
    public void sort() {
        students.sort(Comparator
                .comparingInt(Student::getScore).reversed() // 分数降序
                .thenComparing(Student::getName)); // 同分按姓名升序
    }

    //删除分数低于minScore的学生
    public void removeBelow(int minScore) {
        students.removeIf(s -> s.getScore() < minScore);
    }

    //去重，仅保留最早录入记录
    public void removeDuplicates() {
        Set<String> seenIds = new HashSet<>();
        students.removeIf(s -> !seenIds.add(s.getId()));
    }

    // ① 最高分学生（可能没有学生，所以用 Optional）
    public Optional<Student> maxScore() {
        // TODO: 用 Comparator.comparingInt(Student::getScore) 求最大
        // 提示：students.stream().max(...)
        return students.stream()
                                .max(Comparator.comparingInt(Student::getScore));
    }

    // ② 平均分
    public double averageScore() {
        // TODO: 用 students.stream().mapToInt(Student::getScore).average()
        return students.stream().mapToInt(Student::getScore).average().orElse(0.0);
    }

    // ③ Top-N 学生（已按你之前的规则：分数降序、同分姓名升序）
    public List<Student> topN(int n) {
        // TODO: 先排序，再 limit(n)，最后收集成 List
        return students.stream()
                .sorted(Comparator
                        .comparingInt(Student::getScore).reversed() // 分数降序
                        .thenComparing(Student::getName))
                .limit(n)
                .toList();
    }
}
```
* ScoreBook.java
```
import java.util.*;
import java.util.stream.Collectors;

public class ScoreBook {
    // 存储：学号 -> 分数（保留最后一次）
    private final Map<String, Integer> scores = new LinkedHashMap<>();

    /* ================== 基础增删改查 ================== */

    // 新增或更新（统一入口）；返回旧分数（可能为 null）
    public Integer put(String id, int score) {
        validate(score);
        return scores.put(id, score);
    }

    // 批量新增/更新
    public List<String> putAll(Map<String, Integer> batch) {
        List<String> errors = new ArrayList<>();
        for (var e : batch.entrySet()) {
            String id = e.getKey();
            int score = e.getValue();
            if (score < 0 || score > 100) {
                errors.add(String.format("学号 %s 分数非法: %d", id, score));
                continue; // 跳过非法数据
            }
            scores.put(id, score);
        }
        return errors; // 返回错误列表（可能为空）
    }

    // 按增量更新（如加分/扣分）；id 不存在则忽略
    public void addDelta(String id, int delta) {
        scores.computeIfPresent(id, (k, v) -> clamp(v + delta, 0, 100));
    }

    // 删除
    public void remove(String id) {
        scores.remove(id);
    }

    // 查询
    public Optional<Integer> get(String id) {
        return Optional.ofNullable(scores.get(id));
    }

    // 打印原始存储（插入顺序）
    public void printAllRaw() {
        scores.forEach((k, v) -> System.out.println(k + " -> " + v));
    }

    /* ================== 排序 / TopN / 分页 ================== */

    // 定义排序规则：分数降序，同分学号升序
    private static final Comparator<Map.Entry<String, Integer>> BY_SCORE_DESC_NAME_ASC =
            Map.Entry.<String, Integer>comparingByValue(Comparator.reverseOrder())
                    .thenComparing(Map.Entry.comparingByKey());

    // 排序后的条目（分数降序，同分学号升序）
    public List<Map.Entry<String, Integer>> sortedEntries() {
        return scores.entrySet()
                .stream()
                .sorted(BY_SCORE_DESC_NAME_ASC)
                .toList();
    }

    // Top-N
    public List<Map.Entry<String, Integer>> topN(int n) {
        if (n <= 0) return Collections.emptyList();
        return sortedEntries().stream().limit(n).toList();
    }

    // 分页（page 从 1 开始）
    public List<Map.Entry<String, Integer>> page(int page, int size) {
        if (page < 1 || size < 1) return Collections.emptyList();
        List<Map.Entry<String, Integer>> sorted = sortedEntries();
        int from = (page - 1) * size;
        if (from >= sorted.size()) return Collections.emptyList();
        int to = Math.min(from + size, sorted.size());
        return sorted.subList(from, to);
    }

    /* ================== 统计分析 ================== */

    // 分档统计（90-100/80-89/.../0-59）
    public Map<String, Long> histogram() {
        // 用 LinkedHashMap 保证输出顺序
        Map<String, Long> bins = new LinkedHashMap<>();
        bins.put("90-100", 0L);
        bins.put("80-89", 0L);
        bins.put("70-79", 0L);
        bins.put("60-69", 0L);
        bins.put("0-59", 0L);

        for (int sc : scores.values()) {
            if (sc >= 90) bins.compute("90-100", (k, v) -> v + 1);
            else if (sc >= 80) bins.compute("80-89", (k, v) -> v + 1);
            else if (sc >= 70) bins.compute("70-79", (k, v) -> v + 1);
            else if (sc >= 60) bins.compute("60-69", (k, v) -> v + 1);
            else bins.compute("0-59", (k, v) -> v + 1);
        }
        return bins;
    }

    // 平均分
    public double average() {
        return scores.values().stream().mapToInt(i -> i).average().orElse(0.0);
    }

    // 及格率（>=60）
    public double passRate() {
        if (scores.isEmpty()) return 0.0;
        long pass = scores.values().stream().filter(v -> v >= 60).count();
        return pass * 100.0 / scores.size();
    }

    /* ================== 工具 ================== */

    private static void validate(int score) {
        if (score < 0 || score > 100) throw new IllegalArgumentException("score must be 0..100");
    }

    private static int clamp(int v, int lo, int hi) {
        return Math.max(lo, Math.min(hi, v));
    }
}
```
* RegistrationSystem.java
```
import java.util.*;
import java.util.stream.Collectors;

public class RegistrationSystem {
    // 使用 Map 按学号存储；LinkedHashMap 便于观察插入顺序（不是必须）
    private final Map<String, Student> byId = new LinkedHashMap<>();

    // 统一的排序规则：分数降序、同分姓名升序、再按学号升序兜底
    private static final Comparator<Student> SCORE_DESC_NAME_ASC_ID_ASC =
            Comparator.comparingInt(Student::getScore).reversed()
                    .thenComparing(Student::getName)
                    .thenComparing(Student::getId);

    /* ========== 功能 1：保留最后一次报名的数据（覆盖旧记录） ========== */

    // 单人报名 / 更新（同学号存在则覆盖）
    public void registerOrUpdate(Student s) {
        byId.put(s.getId(), s); // put 覆盖旧值 → 保留“最后一次”
    }

    // 批量报名 / 更新（同学号后写覆盖前写）
    public void registerOrUpdateAll(Collection<Student> batch) {
        for (Student s : batch)
            byId.put(s.getId(), s);
    }

    // 取消报名
    public void unregisterById(String id) {
        byId.remove(id);
    }

    /* ========== 功能 2：分页查看（基于排序视图） ========== */

    // 返回排序后的完整名单（视图）
    public List<Student> listSorted() {
        return byId.values().stream()
                .sorted(SCORE_DESC_NAME_ASC_ID_ASC)
                .toList();
    }

    // 分页（page 从 1 开始），size>0；越界返回空列表
    public List<Student> listSortedPage(int page, int size) {
        if (page < 1 || size < 1) return Collections.emptyList();
        List<Student> sorted = listSorted();
        int from = (page - 1) * size;
        if (from >= sorted.size()) return Collections.emptyList();
        int to = Math.min(from + size, sorted.size());
        return sorted.subList(from, to);
    }

    /* ========== 辅助输出 ========== */

    public void printAllRaw() {
        // 原始 Map 内容（最后一次写入为准）
        byId.values().forEach(System.out::println);
    }
}
```
* Main.java
```
import java.util.*;

public class Main {
    public static void main(String[] args) {
        ScoreBook sb = new ScoreBook();

        // 初始化（含覆盖）
        sb.put("1001", 86);
        sb.put("1002", 92);
        sb.put("1003", 75);
        sb.put("1002", 78);   // 覆盖：最后一次为准
        sb.putAll(Map.of("1004", 91, "1005", 59));

        System.out.println("== 原始存储（插入顺序） ==");
        sb.printAllRaw();

        // 再次更新与加分
        sb.put("1002", 95);           // 覆盖
        sb.addDelta("1003", +10);     // 75 -> 85
        sb.addDelta("1005", +3);      // 59 -> 62（及格）
        sb.addDelta("9999", +5);      // 不存在，忽略

        System.out.println("\n== 排序视图（分数降序，同分学号升序） ==");
        sb.sortedEntries().forEach(e -> System.out.println(e.getKey() + " -> " + e.getValue()));

        System.out.println("\n== Top-3 ==");
        sb.topN(3).forEach(e -> System.out.println(e.getKey() + " -> " + e.getValue()));

        System.out.println("\n== 分页 page=1,size=2 ==");
        sb.page(1, 2).forEach(e -> System.out.println(e.getKey() + " -> " + e.getValue()));
        System.out.println("== 分页 page=2,size=2 ==");
        sb.page(2, 2).forEach(e -> System.out.println(e.getKey() + " -> " + e.getValue()));

        System.out.println("\n== 统计 ==");
        System.out.printf("平均分: %.2f%n", sb.average());
        System.out.printf("及格率: %.2f%%%n", sb.passRate());
        System.out.println("分档: " + sb.histogram());

        System.out.println("\n== 删除学号 1005 后 ==");
        sb.remove("1005");
        sb.printAllRaw();
    }
}
```
