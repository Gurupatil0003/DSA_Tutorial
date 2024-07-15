# Selection Sort
![image](https://github.com/user-attachments/assets/092d4f7d-2d3a-4105-85c0-faec33464a8a)


```c
#include <stdio.h>

// Function to perform Selection Sort on an array
void selectionSort(int arr[], int n) {
    int i, j, minIndex, temp;

    // Outer loop: iterate over each element of the array
    for (i = 0; i < n-1; i++) {
        // Assume the current element is the minimum
        minIndex = i;

        // Inner loop: find the smallest element in the remaining unsorted array
        for (j = i+1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;  // Update minIndex if a smaller element is found
            }
        }

        // Swap the found minimum element with the first element of the unsorted part
        temp = arr[minIndex];
        arr[minIndex] = arr[i];
        arr[i] = temp;
    }
}

// Function to print the elements of an array
void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

// Main function to test the selectionSort function
int main() {
    int arr[] = {64, 25, 12, 22, 11};
    int n = sizeof(arr)/sizeof(arr[0]);

    printf("Unsorted array: \n");
    printArray(arr, n);

    selectionSort(arr, n);

    printf("Sorted array: \n");
    printArray(arr, n);

    return 0;
}
```
