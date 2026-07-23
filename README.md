# sorting-algorithms
Professional Structure (সব Sorting-এর জন্য একই)
#include <iostream>
using namespace std;

void sortFunction(int arr[], int n)
{
    // Sorting Logic
}

void printArray(int arr[], int n)
{
    for(int i = 0; i < n; i++)
    {
        cout << arr[i] << " ";
    }
}

int main()
{
    int n;
    cin >> n;

    int arr[n];

    for(int i = 0; i < n; i++)
    {
        cin >> arr[i];
    }

    sortFunction(arr, n);

    printArray(arr, n);

    return 0;
}
