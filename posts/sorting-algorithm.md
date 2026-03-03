---
title: 排序算法 Sorting Algorithm
date: 2025/12/1
tags: [Sorting Algorithm, Data Structure]
pinned: true
head:
  - - meta
    - name: description
      content: 十大经典排序算法详解
  - - meta
    - name: keywords
      content: 十大经典排序算法详解
---

十大经典排序算法详解

---

## 1. 冒泡排序 (Bubble Sort)
#### 排序思想
冒泡排序模拟了“气泡上浮”的过程，通过不断地比较相邻两个元素并将较大的值向右交换，使得每一轮遍历都能将当前未排序部分的最大值移动到末尾。整个排序过程分为多轮，每轮都会让一个最大值归位，最终整个数组变为有序。它的核心思想是重复比较相邻元素，发现逆序则交换，通过多轮将最大值逐步移动到右侧。当某一轮遍历中未发生任何交换时，说明数组已经有序，可以提前结束排序。
#### 算法步骤
1. 外层循环控制排序轮数，共进行 `n - 1` 轮（`n` 为数组长度）；
2. 在第 `i` 轮中（`i` 从 `0` 到 `n-2`），内层循环从数组开头遍历到第 `n - 2 - i` 个元素；
3. 在内层循环中，依次比较相邻的两个元素 `arr[j]` 和 `arr[j+1]`；
4. 如果 `arr[j] > arr[j+1]`，则交换它们的位置；
5. 每完成一轮，当前未排序部分的最大值会“冒泡”到该轮末尾；
6. 重复上述过程，直到完成所有 `n - 1` 轮，此时数组有序。

#### C语言实现
```c
#include <stdio.h>

void bubbleSort(int[] arr, int n) {
	for (int i = 0; i < n - 1; i++) {
		for (int j = 0; j < n - 1 - i; j++) {
			if (arr[j] > arr[j + 1]) {
				int temp = arr[j];
				arr[j] = arr[j + 1];
				arr[j + 1] = temp;
			}
		}
	}
}
```


## 2. 选择排序 (Selection Sort)
#### 排序思想
选择排序的核心思想是：每一轮从待排序部分中选择最小（或最大）的元素，将其放到已排序序列的末尾（或开头）。通过不断地选择和交换，最终整个数组变为有序。它不依赖相邻比较，而是全局扫描未排序区域寻找最值，然后和当前起始位置交换。由于每次都明确选出最小值，其交换次数固定为 `n-1` 次。
#### 算法步骤
1. 外层循环控制排序轮数，共进行 `n - 1` 轮（`n` 为数组长度）；
2. 在第 `i` 轮中（`i` 从 `0` 到 `n - 2`），假设当前位置 `i` 是未排序部分的最小值位置；
3. 内层循环从 `i + 1` 开始，遍历到数组末尾（即索引 `n - 1`）；
4. 在内层循环中，依次将元素 `arr[j]` 与当前记录的最小值 `arr[minIndex]` 比较；
5. 若发现 `arr[j] < arr[minIndex]`，则更新 `minIndex = j`；
6. 内层循环结束后，将 `arr[i]` 与 `arr[minIndex]` 交换位置，使最小值就位；
7. 重复上述过程，直到完成所有 `n - 1` 轮，此时数组有序。
#### C语言实现
```c
#include <stdio.h>

void selectionSort(int[] arr, int n) {
	for (int i = 0; i < n - 1; i++) {
		int minIndex = i;
		
		for (int j = i + 1; j < n; j++) {
			if (arr[j] < arr[minIndex]) {
				minIndex = j;
			}
		}
		
		if (minIndex != i) {
			int temp = arr[i];
			arr[i] = arr[minIndex];
			arr[minIndex] = temp;
		}
	}
}
```

## 3. 插入排序 (Insertion Sort)
#### 排序思想
插入排序的基本思想是：构建有序序列，对于未排序数据，从后向前扫描已排序序列，找到相应位置并插入。它模拟的是打扑克牌时理牌的过程，每次将新牌插入到合适的位置。插入排序通过构建一个逐步扩大的有序区，不断将新的元素插入其中，最终使整个数组有序。插入过程依赖于比较和移动。

#### 算法步骤
1. 外层循环从第 2 个元素开始（索引 `i = 1`），共进行 `n - 1` 轮（`n` 为数组长度）；
2. 在第 `i` 轮中，将当前元素 `arr[i]` 视为待插入的“关键字”（`key`）；
3. 内层循环从 `i - 1` 开始，向前遍历已排序部分（索引从 `i-1` 到 `0`）；
4. 在内层循环中，若已排序元素 `arr[j]` 大于 `key`，则将其向后移动一位（`arr[j+1] = arr[j]`）；
5. 继续向前比较，直到找到 `key` 的正确插入位置（即 `arr[j] <= key` 或到达数组开头）；
6. 将 `key` 插入到该位置（`arr[j+1] = key`）；
7. 重复上述过程，直到所有元素都被插入到已排序部分，此时数组有序。
#### C语言实现
```c
#include <stdio.h>

void insertionSort(int[] arr, int n) {
	for (int i = 1; i < n; i++) {
		int key = arr[i];
		int j = i - 1;
		
		while (j >= 0 && arr[j] > key) {
			arr[j + 1] = arr[j];
			j--;
		}
		arr[j + 1] = key;
	}
}
```

## 4. 希尔排序 (Shell Sort)
#### 排序思想
希尔排序是插入排序的改进版，采用分组插入的思想。它首先将整个待排序元素分为若干个小组（由步长 gap 决定），在每组中进行插入排序，然后逐渐缩小 gap，最终 gap=1 时对整体做一次插入排序。这样可以在初期就让元素快速移动到接近最终位置，从而加快整体排序速度。原理上它是通过“预排序 + 缩小增量”的策略减少整体比较次数，是不稳定的排序算法。

#### 算法步骤
1. 选择一个**递减的增量序列**（gap sequence），初始增量 `gap` 通常取数组长度的一半（`n / 2`）；
2. 当 `gap > 0` 时，重复以下过程：
    - 将数组按当前 `gap` 分成若干个子序列（每个子序列由相距 `gap` 的元素组成）；
    - 对每个子序列**分别进行插入排序**；
3. 每轮排序完成后，将 `gap` 缩小（通常取 `gap = gap / 2`）；
4. 重复步骤 2–3，直到 `gap` 减小为 0；

#### C语言实现
```c
#include <stdio.h>

void shellSort(int arr[], int n) {
	for (int gap = n / 2; gap > 0; gap /= 2) {
		for (int i = gap; i < n; i++) {
			int key = arr[i];
			int j = i;
			
			while (j >= gap && arr[j - gap] > key) {
				arr[j] = arr[j - gap];
				j -= gap;
			}
			arr[j] = key;
		}
	}
}
```

## 5. 归并排序 (Merge Sort)

#### 排序思想
归并排序是一种典型的分治算法。它将一个大问题分解成小问题，逐步解决，然后合并结果。归并排序的思想是将数组分成两半，对每一半递归地进行归并排序，最终合并两个有序的子数组。归并排序时间复杂度稳定在 O(n log n)，适用于大数据量排序。

#### 算法步骤
1. 若子数组长度大于 1，则从中间将其分为左右两部分；
2. 递归对左半部分和右半部分分别排序；
3. 将两个已排序的子部分合并为一个有序数组：
    - 依次比较两部分的当前元素，取较小者放入原数组；
    - 剩余元素直接追加到末尾；
4. 递归完成后，整个数组有序。

#### C语言实现
```c
#include <stdio.h>

void merge (int arr[], int n) {
	int temp[right - left + 1];
	int i = left, j = mid + 1, k = 0;
	
	while (i <= mid && j <= right) {
		if (arr[i] <= arr[j]) temp[k++] = arr[i++];
		else temp[k++] = arr[j++];
	}
	
	while (i <= mid) temp[k++] = arr[i++];
	while (j <= right) temp[k++] = arr[j++];
	
	for (int p = 0; p < k; p++) arr[left + p] = temp[p];
}

void mergeSort(int arr[], int left, int right) {
	if (left < right) {
		int mid = (left + right) / 2;
		mergeSort(arr, left, mid);
		mergeSort(arr, mid + 1, right);
		merge(arr, left, mid, right);
	}
}
```


## 6. 快速排序 (Quick Sort)
#### 排序思想
快速排序同样采用分治法，它通过选择一个“基准”元素，将数组分成两部分，左边部分小于基准元素，右边部分大于基准元素。然后递归地对左右两部分进行排序，最后合并。

快速排序通常比归并排序更快，因为它的内存访问模式更加局部，且避免了归并排序的额外空间开销。虽然快速排序的最坏时间复杂度是 O(n²)，但通常它在平均情况下能达到 O(n log n)。

#### 算法步骤
1. 从数组中选择一个“基准”元素；
2. 通过一次排序操作，将比基准元素小的元素放在左边，比基准元素大的元素放在右边；
3. 分别对左右子数组递归进行快速排序；
4. 直到子数组的长度为 1 或 0，排序完成。

#### C语言实现
```c
#include <stdio.h>

int partition (int arr[], int low, int high) {
	int pivot = arr[high];
	int i = low - 1;
	
	for (int j = low; j < high; j++) {
		if (arr[j] <= pivot) {
			i++;
			int temp = arr[i];
			arr[i] = arr[j];
			arr[j] = temp;
		}
	}
	
	int temp = arr[i + 1];
	arr[i + 1] = arr[high];
	arr[high] = temp;
	
	return i + 1;
}

void quickSort(int arr[], int low, int high) {
	if (low < high) {
		int pivotIndex = partition(arr, low, high);
		quickSort(arr, low, pivotIndex - 1);
		quickSort(arr, pivotIndex + 1, high);
	}
}
```

## 7. 堆排序 (Heap Sort)
#### 排序思想
堆排序是一种选择排序，它利用堆这种数据结构的特性来进行排序。堆是一种完全二叉树，满足堆的性质：每个节点的值都大于或小于其子节点的值。堆排序首先将待排序数组构建成一个大顶堆（或小顶堆），然后交换堆顶元素和堆的最后一个元素，并重新调整堆，重复此过程直到整个数组有序。

#### 算法步骤
1. 将待排序数组构建成一个大顶堆；
2. 交换堆顶元素与堆的最后一个元素；
3. 对剩余的元素进行堆化，保证堆的性质；
4. 重复步骤 2 和 3，直到堆中只剩一个元素。

```c
#include <stdio.h>

void heapify(int arr[], int n, int i) {
	int largest = i;
	int left = 2 * i + 1; // 左孩子
	int right = 2 * i + 2; // 右孩子
	
	if (left < n && arr[left] > arr[largest]) largest = left;
	if (right < n && arr[right] > arr[largest]) largest = right;
	if (largest != i) {
		int temp = arr[i];
		arr[i] = arr[largest];
		arr[largest] = temp;
		
		heapify(arr, n, largest);
	}
}

void heapSort(int arr[], int n) {
	for (int i = n / 2 - i; i >= 0; i--) {
		heapify(arr, n, i);
	}
	
	for (int i = n - 1; i > 0; i--) {
		int temp = arr[0];
		arr[0] = arr[i];
		arr[i] = temp;
		
		heapify(arr, i, 0);
	}
}
```

## 8. 计数排序 (Counting Sort)
#### 排序思想
计数排序是一种非比较排序，它通过统计每个元素出现的次数来实现排序。该算法的核心思想是：根据输入数据的范围创建一个计数数组，并记录数组中每个元素出现的次数。然后根据计数数组的统计结果，将元素重新填充到排序后的数组中。

计数排序的时间复杂度是 O(n+k)，其中 n 是输入数组的大小，k 是元素值的范围。它是一种稳定的排序算法，但对数据范围有要求，适用于范围较小的整数排序。

#### 算法步骤
1. 找到数组中的最大值和最小值；
2. 创建一个计数数组，记录每个元素出现的次数；
3. 将计数数组的值累加，得到每个元素在排序后的数组中的位置；
4. 从原数组中取出元素，放入排序后的数组。

```c
#include <stdio.h>

void countingSort(int arr[], int n) {
	int max = arr[0];
	for (int i = 1; i < n; i++) {
		if (arr[i] > max) max = arr[i];
	}
	
	int count[max + 1];
	
	for (int i = 0; i <= max; i++) {
		count[i] = 0;
	}
	
	for (int i = 0; i < n; i++) {
		count[arr[i]]++;
	}
	
	int idx = 0;
	for (int i = 0; i <= max; i++) {
		while (count[i] > 0) {
			arr[idx++] = i;
			count[i]--;
		}
	}
}
```

## 9. 基数排序 (Radix Sort)

#### 排序思想
基数排序是一种非比较排序，它通过对整数的各个“位”进行排序，从低位到高位，逐步地将数组排列成有序。基数排序使用了计数排序作为子排序方法。它适用于排序整数或字符串等数据类型，特别是在数据范围较大时能够提供优于比较排序的性能。

#### 算法步骤
1. 将输入数组按每个数的低位到高位依次排序；
2. 使用稳定的排序算法（如计数排序）对每个“位”进行排序；
3. 每次排序后，固定该位的顺序，再对下一位进行排序；
4. 重复进行，直到所有位排序完成。

```c
#include <stdio.h>

void countingSortByDigit(int arr[], int n, int exp) {
	int output[n];
	int count[10] = {0};
	
	for (int i = 0; i < n; i++) {
		int digit = (arr[i] / exp) % 10;
		count[digit]++;
	}
	
	for (int i = 1; i < 10; i++) {
		count[i] += count[i - 1];
	}
	
	for (int i = n - 1; i >= 0; i--) {
		int digit = (arr[i] / exp) % 10;
		output[count[digit] - 1] = arr[i];
		count[digit]--;
	}
	
	for (int i = 0; i < n; i++) {
		arr[i] = output[i];
	}
}

void radixSort(int arr[], int n) {
	int max = arr[0];
	for (int i = 1; i < n; i++) {
		if (arr[i] > max) max = arr[i];
	}
	
	for (int exp = 1; max / exp > 0; exp *= 10) {
		countingSortByDigit(arr, n, exp);
	}
}
```

## 10. 桶排序 (Bucket Sort)
#### 排序思想
桶排序是一种基于分布的排序算法，其思想是将数据分到有限数量的桶里，每个桶内部进行排序，然后再把所有桶里的数据合并起来。桶排序假设输入数据均匀分布在一个有限的区间内，因此它将输入数据划分为若干个小区间（桶），然后分别对每个桶进行排序。桶排序的核心思想是通过把数据分散到不同的桶中，减少了排序过程中比较的次数，从而提高排序的效率。每个桶内部使用其他排序算法（如插入排序）进行排序，最终将桶中的元素合并得到有序序列。

#### 算法步骤
1. 确定输入数据的范围并将数据划分为若干个桶。每个桶的大小通常由输入数据的最大值和最小值决定，桶的数量根据数据规模和范围来确定。
2. 将数据分配到各个桶中。每个数据项根据其值分配到对应的桶里。
3. 对每个桶内部进行排序。可以使用其他排序算法（如插入排序）对桶内的数据进行排序。
4. 将所有桶中的元素合并，得到最终的排序结果。

```c
#include <stdio.h>
#include <math.h>

void insertionSort(float arr[], int n) {
	for (int i = 1; i < n; i++) {
		float key = arr[i];
		int j = i - 1;
		while (j >= 0 && arr[j] > key) {
			arr[j + 1] = arr[j];
			j--;
		}
		arr[j + 1] = key;
	}
}

void bucketSort(float arr[], int n) {
	if (n <= 1) return;
	
	float min = arr[0], max = arr[0];
	for (int i = 1; i < n; i++) {
		if (arr[i] < min) min = arr[i];
		if (arr[i] > max) max = arr[i]; 
	}
	
	int bucketCount = (int)sqrt(n);
	if (bucketCount == 0) bucketCount = 1;
	
	float buckets[bucketCount][n];
	int counts[bucketCount];
	
	for (int i = 0; i < bucketCount; i++) {
		counts[i] = 0;
	}
	
	for (int i = 0; i < n; i++) {
		int index;
		if (max == min) {
			index = 0;
		} else {
			index = (int)((arr[i] - min) / (max - min + 1e-9) * bucketCount);
			if (index >= bucketCount) index = bucketCount - 1;
		}
		buckets[index][counts[index]++] = arr[i];
	}
	
	for (int i = 0; i < bucketCount; i++) {
		if (counts[i] > 0) {
			insertionSort(buckets[i], counts[i]);
		}
	}
	
	int idx = 0;
	for (int i = 0; i < bucketCount; i++) {
		for (int j = 0; j < counts[i]; j++) {
			arr[idx++] = buckets[i][j];
		}
	}
}
```

# 排序算法比较表

| 排序算法 | 时间复杂度（平均）  | 时间复杂度（最差）  | 时间复杂度（最好）  | 空间复杂度    | 排序方式  | 稳定性 |
| ---- | ---------- | ---------- | ---------- | -------- | ----- | --- |
| 冒泡排序 | O(n²)      | O(n²)      | O(n)       | O(1)     | 原地排序  | 稳定  |
| 选择排序 | O(n²)      | O(n²)      | O(n²)      | O(1)     | 原地排序  | 不稳定 |
| 插入排序 | O(n²)      | O(n²)      | O(n)       | O(1)     | 原地排序  | 稳定  |
| 希尔排序 | O(n log n) | O(n²)      | O(n log n) | O(1)     | 原地排序  | 不稳定 |
| 归并排序 | O(n log n) | O(n log n) | O(n log n) | O(n)     | 非原地排序 | 稳定  |
| 快速排序 | O(n log n) | O(n²)      | O(n log n) | O(log n) | 原地排序  | 不稳定 |
| 堆排序  | O(n log n) | O(n log n) | O(n log n) | O(1)     | 原地排序  | 不稳定 |
| 计数排序 | O(n + k)   | O(n + k)   | O(n + k)   | O(k)     | 非原地排序 | 稳定  |
| 基数排序 | O(nk)      | O(nk)      | O(nk)      | O(n + k) | 非原地排序 | 稳定  |
| 桶排序  | O(n + k)   | O(n²)      | O(n + k)   | O(n + k) | 非原地排序 | 稳定  |