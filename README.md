#include <iostream>
#include <vector>
using namespace std;

pair<int, int> findSubarrayWithTargetSum(const vector<int>& arr, int target) {
    int start = 0, currentSum = 0;

    for (int end = 0; end < arr.size(); end++) {
        currentSum += arr[end]; // Add the current element to the window

        // Shrink the window from the left if the current sum exceeds the target
        while (currentSum > target && start <= end) {
            currentSum -= arr[start];
            start++;
        }

        // Check if the current sum equals the target
        if (currentSum == target) {
            return {start, end}; // Return the 0-based indices
        }
    }

    return {-1, -1}; // No subarray found
}

int main() {
    int n, target;
    
    // Input array size and target sum
    cout << "Enter the size of the array: ";
    cin >> n;

    vector<int> arr(n);
    cout << "Enter the elements of the array: ";
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    cout << "Enter the target sum: ";
    cin >> target;

    // Find subarray with the target sum
    pair<int, int> result = findSubarrayWithTargetSum(arr, target);

    if (result.first == -1) {
        cout << "No subarray with the target sum found." << endl;
    } else {
        cout << "Subarray found from index " << result.first << " to " << result.second << "." << endl;
    }

    return 0;
}
