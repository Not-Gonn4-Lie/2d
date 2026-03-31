










#practical_06


#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Enter number of vertices: ";
    cin >> n;

    int a[10][10];

    cout << "Enter adjacency matrix:\n";
    for(int i = 0; i < n; i++) {
        for(int j = 0; j < n; j++) {
            cin >> a[i][j];
        }
    }

    bool isComplete = true;

    for(int i = 0; i < n; i++) {
        for(int j = 0; j < n; j++) {

            if(i == j) {
                // Diagonal must be 0
                if(a[i][j] != 0)
                    isComplete = false;
            }
            else {
                // All other elements must be 1
                if(a[i][j] != 1)
                    isComplete = false;
            }
        }
    }

    if(isComplete)
        cout << "Graph is a Complete Graph";
    else
        cout << "Graph is NOT a Complete Graph";

    return 0;
}




#practical_07

#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Enter number of vertices: ";
    cin >> n;

    int a[10][10];

    cout << "Enter adjacency matrix:\n";
    for(int i = 0; i < n; i++) {
        for(int j = 0; j < n; j++) {
            cin >> a[i][j];
        }
    }

    int indegree[10] = {0};
    int outdegree[10] = {0};

    // Calculate degrees
    for(int i = 0; i < n; i++) {
        for(int j = 0; j < n; j++) {

            if(a[i][j] == 1) {
                outdegree[i]++;  // row sum
                indegree[j]++;   // column sum
            }
        }
    }

    // Display result
    cout << "\nVertex\tIn-degree\tOut-degree\n";
    for(int i = 0; i < n; i++) {
        cout << i << "\t" << indegree[i] << "\t\t" << outdegree[i] << endl;
    }

    return 0;
}
