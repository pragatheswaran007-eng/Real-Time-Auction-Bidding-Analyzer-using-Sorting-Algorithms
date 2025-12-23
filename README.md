#include <stdio.h>
#include <string.h>
struct Bid {
 char name[50];
 float amount;
};
void swap(struct Bid *a, struct Bid *b) {
 struct Bid temp = *a;
 *a = *b;
 *b = temp;
}
int partition(struct Bid arr[], int low, int high) {
 float pivot = arr[high].amount;
 int i = (low - 1);
 for (int j = low; j < high; j++) {
 if (arr[j].amount > pivot) { // Descending order
 i++;
 swap(&arr[i], &arr[j]);
 }
 }
 swap(&arr[i + 1], &arr[high]);
 return (i + 1);
}
void quickSort(struct Bid arr[], int low, int high) {
 if (low < high) {
 int pi = partition(arr, low, high);
 quickSort(arr, low, pi - 1);
 quickSort(arr, pi + 1, high);
 }
}
int main() {
 int n;
 printf("Enter number of bids: ");
 scanf("%d", &n);
 struct Bid bids[n];
 for (int i = 0; i < n; i++) {
 printf("\nEnter Bidder Name: ");
 scanf("%s", bids[i].name);
 printf("Enter Bid Amount: ");
 scanf("%f", &bids[i].amount);
 }
 quickSort(bids, 0, n - 1);
 printf("\n--- Sorted Bids (Highest First) ---\n");
 for (int i = 0; i < n; i++) {
 printf("%s - ₹%.2f\n", bids[i].name,
bids[i].amount);
 }
 printf("\nHighest Bidder: %s (₹%.2f)\n",
bids[0].name, bids[0].amount);
 return 0;
}
