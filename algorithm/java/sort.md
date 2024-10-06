# 常用排序算法



## 归并排序
```Java
@Slf4j
public class MyTest {

    @Test
    public void test() {
        int[] array = {3, 2, 5, 6, 4, 9, 10, 1, 7, 8};
        System.out.println(Arrays.toString(array));
        // 升序排序
        sort(array, 0, array.length - 1);
        System.out.println(Arrays.toString(array));
    }

    public void sort(int[] array, int low, int high) {
        int mid = (low + high) / 2;
        if (low < high) {
            sort(array, low, mid);
            sort(array, mid + 1, high);
            merge(array, low, mid, high);
        }
    }

    public void merge(int[] array, int low, int mid, int high) {
        int[] temp = new int[high - low + 1];
        int i = low;
        int j = mid + 1;
        int k = 0;
        while (i <= mid && j <= high) {
            if (array[i] < array[j]) {
                temp[k++] = array[i++];
            } else {
                temp[k++] = array[j++];
            }
        }
        while (i <= mid) {
            temp[k++] = array[i++];
        }
        while (j <= high) {
            temp[k++] = array[j++];
        }
        for (int l = 0; l < temp.length; l++) {
            array[l + low] = temp[l];
        }
    }
}
```

## 堆排序
```Java
@Slf4j
public class MyTest {

    @Test
    public void test() {
        int[] array = {3, 2, 5, 6, 4, 9, 10, 1, 7, 8};
        System.out.println(Arrays.toString(array));
        // 降序排序
        myHeapSort(array);
        System.out.println(Arrays.toString(array));
    }

    public void myHeapSort(int[] array) {
        int i;
        int len = array.length;
        for (i = len / 2 - 1; i >= 0; i--) {
            adjustment(array, i, len);
        }
        for (i = len - 1; i >= 0; i--) {
            int temp = array[0];
            array[0] = array[i];
            array[i] = temp;
            adjustment(array, 0, i);
        }
    }

    public void adjustment(int[] array, int pos, int len) {
        int child = 2 * pos + 1;
        if (child + 1 < len && array[child] > array[child + 1]) {
            child++;
        }
        if (child < len && array[pos] > array[child]) {
            int temp = array[pos];
            array[pos] = array[child];
            array[child] = temp;
            adjustment(array, child, len);
        }
    }
}
```

## 基数排序
```Java
@Slf4j
public class MyTest {

    @Test
    public void test() {
        int[] array = {3, 2, 5, 6, 4, 9, 10, 1, 7, 8};
        System.out.println(Arrays.toString(array));
        // 升序排序
        basicSort(array);
        System.out.println(Arrays.toString(array));
    }

    public void basicSort(int[] array) {
        int max = 0;
        for (int i = 0; i < array.length; i++) {
            if (array[i] > max) {
                max = array[i];
            }
        }
        int times = 0;
        while (max > 0) {
            max = max / 10;
            times++;
        }
        List<ArrayList<Integer>> queen = new ArrayList<>();
        for (int i = 0; i < 10; i++) {
            ArrayList<Integer> q = new ArrayList<>();
            queen.add(q);
        }
        for (int i = 0; i < times; i++) {
            for (int j = 0; j < array.length; j++) {
                int x = array[j] % (int) Math.pow(10, i + 1) / (int) Math.pow(10, i);
                ArrayList<Integer> q = queen.get(x);
                q.add(array[j]);
            }
            int count = 0;
            for (int z = 0; z < 10; z++) {
                while (queen.get(z).size() > 0) {
                    ArrayList<Integer> c = queen.get(z);
                    array[count] = c.get(0);
                    c.remove(0);
                    count++;
                }
            }
        }
    }
}
```

## 冒泡排序
```Java
@Slf4j
public class MyTest {

    @Test
    public void test() {
        int[] array = {3, 2, 5, 6, 4, 9, 10, 1, 7, 8};
        System.out.println(Arrays.toString(array));
        // 升序排序
        bubbleSort(array);
        System.out.println(Arrays.toString(array));
    }

    public void bubbleSort(int[] array) {
        int t = 0;
        for (int i = 0; i < array.length - 1; i++) {
            for (int j = 0; j < array.length - 1 - i; j++) {
                if (array[j] > array[j + 1]) {
                    t = array[j];
                    array[j] = array[j + 1];
                    array[j + 1] = t;
                }
            }
        }
    }
}
```

## 快速排序
```Java
@Slf4j
public class MyTest {

    @Test
    public void test() {
        int[] array = {3, 2, 5, 6, 4, 9, 10, 1, 7, 8};
        System.out.println(Arrays.toString(array));
        // 升序排序
        quickSort(array, 0, array.length - 1);
        System.out.println(Arrays.toString(array));
    }

    public void quickSort(int[] array, int low, int high) {
        int pivot, p_pos, i, t;
        if (low < high) {
            p_pos = low;
            pivot = array[p_pos];
            for (i = low + 1; i <= high; i++) {
                if (array[i] < pivot) {
                    p_pos++;
                    t = array[p_pos];
                    array[p_pos] = array[i];
                    array[i] = t;
                }
            }
            t = array[low];
            array[low] = array[p_pos];
            array[p_pos] = t;

            quickSort(array, low, p_pos - 1);
            quickSort(array, p_pos + 1, high);
        }
    }
}
```


## 希尔排序
```Java
@Slf4j
public class MyTest {

    @Test
    public void test() {
        int[] array = {3, 2, 5, 6, 4, 9, 10, 1, 7, 8};
        System.out.println(Arrays.toString(array));
        // 升序排序
        shellSort(array);
        System.out.println(Arrays.toString(array));
    }

    public void shellSort(int[] array) {
        for (int step = array.length / 2; step > 0; step /= 2) {
            for (int i = step; i < array.length; i++) {
                int value = array[i];
                int j;
                for (j = i - step; j >= 0 && array[j] > value; j -= step) {
                    array[j + step] = array[j];
                }
                array[j + step] = value;
            }
        }
    }
}
```

## 插入排序
```Java
@Slf4j
public class MyTest {

    @Test
    public void test() {
        int[] array = {3, 2, 5, 6, 4, 9, 10, 1, 7, 8};
        System.out.println(Arrays.toString(array));
        // 升序排序
        insertionSort(array);
        System.out.println(Arrays.toString(array));
    }

    public void insertionSort(int[] array) {
        for (int i = 1; i < array.length; i++) {
            for (int j = i; j > 0; j--) {
                if (array[j] < array[j - 1]) {
                    int temp = array[j - 1];
                    array[j - 1] = array[j];
                    array[j] = temp;
                }
            }
        }
    }
}
```

## 选择排序
```Java
@Slf4j
public class MyTest {

    @Test
    public void test() {
        int[] array = {3, 2, 5, 6, 4, 9, 10, 1, 7, 8};
        System.out.println(Arrays.toString(array));
        // 升序排序
        selectSort(array);
        System.out.println(Arrays.toString(array));
    }

    public void selectSort(int[] array) {
        for (int i = 0; i < array.length - 1; i++) {
            int index = i;
            for (int j = i + 1; j < array.length; j++) {
                if (array[j] < array[index]) {
                    index = j;
                }
            }
            if (index != i) {
                // 找到了比array[i]小的则与array[i]交换位置
                int temp = array[index];
                array[index] = array[i];
                array[i] = temp;
            }
        }
    }
}
```