# Interpolation search
- Given a sorted integer array and a target, determine if the target exists in the array or not using an interpolation search algorithm. If the target exists in the array, return the index of it.

For example,
```c
----------------------------------------------
- Input: arr[] = [2, 3, 5, 7, 9]
- target = 7 
- Output: Element found at index 3
-----------------------------------------------
- Input: arr[] = [1, 4, 5, 8, 9]
- target = 2
- Output: Element not found

```

```c
[2, 4, 6, 8, 10, 12, 14, 16, 18, 20]

target = 12

position = low + ((target - arr[low]) * (high - low)) / (arr[high] - arr[low])
position = 0 + ((12 - 2) * (9 - 0)) / (20 - 2)
position = 0 + (10 * 9) / 18
position = 0 + 90 / 18
position = 0 + 5
position = 5
```

- Interpolation search is an algorithm similar to binary search for searching for a given target value in a sorted array. It parallels how humans search through a telephone book for a particular name, the target value by which the book’s entries are ordered.

- We know that binary search always chooses the middle of the remaining search space, discarding one half or the other depending on the comparison result between the mid-value and the target value. The remaining search space is reduced to the part before or after the mid-position.

- By comparison, at each search step, Interpolation search calculates wherein the remaining search space the target might be present, based on the low and high values of the search space and the target’s value. The value found at this estimated position is then compared to the target value. If it’s not equal, then the remaining search space is reduced to the part before or after the estimated position depending on the comparison. This method will only work if calculations on the size of differences between target values are sensible.

- Interpolation search uses the following formula to calculate the mid-position where A[low…high] is our search space, and target is the given target:
```c
mid = low + ((target – A[low]) * (high – low) / (A[high] – A[low]));
```

# Example
```c
#include <stdio.h>
 
// Function to determine if target exists in a sorted array `A` or not
// using an interpolation search algorithm
int interpolationSearch(int A[], int n, int target)
{
    // base case
    if (n == 0) {
        return -1;
    }
 
    // search space is A[low…high]
    int low = 0, high = n - 1, mid;
 
    while (A[high] != A[low] && target >= A[low] && target <= A[high])
    {
        // estimate mid
        mid = low + ((target - A[low]) * (high - low) / (A[high] - A[low]));
 
        // target value is found
        if (target == A[mid]) {
            return mid;
        }
        // discard all elements in the right search space, including the middle element
        else if (target < A[mid]) {
            high = mid - 1;
        }
        // discard all elements in the left search space, including the middle element
        else {
            low = mid + 1;
        }
    }
 
    // if a target is found
    if (target == A[low]) {
        return low;
    }
 
    // target doesn't exist in the array
    else {
        return -1;
    }
}
 
int main(void)
{
    int A[] = {2, 5, 6, 8, 9, 10};
    int target = 5;
 
    int n = sizeof(A)/sizeof(A[0]);
    int index = interpolationSearch(A, n, target);
 
    if (index != -1) {
        printf("Element found at index %d", index);
    }
    else {
        printf("Element not found in the array");
    }
 
    return 0;
}

```
Output:-
```c
Element found at index 1


```

~~~c
#include <stdio.h>

// Function to perform interpolation search
int interpolationSearch(int arr[], int size, int target) {
    int low = 0;
    int high = size - 1;

    while (low <= high && target >= arr[low] && target <= arr[high]) {
        // Calculate the estimated position using the interpolation formula
        int pos = low + ((double)(high - low) / (arr[high] - arr[low]) * (target - arr[low]));

        // Ensure pos is within the bounds of the array
        if (pos < low || pos > high) {
            return -1;
        }

        // Check if target is found at pos
        if (arr[pos] == target) {
            return pos;
        }

        // If target is larger, target is in the upper part of the array
        if (arr[pos] < target) {
            low = pos + 1;
        }
        // If target is smaller, target is in the lower part of the array
        else {
            high = pos - 1;
        }
    }

    // If the element was not found
    return -1;
}

int main() {
    int arr[] = {10, 20, 30, 40, 50, 60, 70, 80, 90, 100};
    int size = sizeof(arr) / sizeof(arr[0]);
    int target = 45;

    int result = interpolationSearch(arr, size, target);

    if (result != -1) {
        printf("Element found at index %d\n", result);
    } else {
        printf("Element not found\n");
    }

    return 0;
}



~~~

Example Explanation

# Interpolation Search Example

Let's say you have a sorted array:
```markdown
A = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]

pos = low + ( (target - A[low]) * (high - low) ) / (A[high] - A[low])


pos = 0 + ( (45 - 10) * (9 - 0) ) / (100 - 10)
    = 0 + ( 35 * 9 ) / 90
    = 0 + 3.5
    = 3.5


## Performance
- Each iteration of the above code requires between five and six comparisons. On average, the interpolation search makes about log(log(n)) comparisons if the elements are uniformly distributed, where n is the 
 total number of elements to be searched. In the worst case, it can make up to O(n) comparisons. The worst-case might happen when the numerical values of the targets increase exponentially.

### Complexity:
- Runtime: The average runtime complexity of interpolation search is O(log log N) and has a worst case of O(N), which happens when the keys increase exponentially.

- Space: O(1) for initializing variables high, low, mid.
