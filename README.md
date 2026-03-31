#practical_01

#include <iostream>
#include <vector>
using namespace std;

class SET {
    vector<int> s;

public:
    // Input function
    void input() {
        int n, x;
        cout << "Enter number of elements: ";
        cin >> n;
        cout << "Enter elements:\n";
        for(int i = 0; i < n; i++) {
            cin >> x;
            s.push_back(x);
        }
    }

    // Display set
    void display() {
        cout << "{ ";
        for(int i : s)
            cout << i << " ";
        cout << "}\n";
    }

    // a. isMember
    bool isMember(int x) {
        for(int i : s) {
            if(i == x)
                return true;
        }
        return false;
    }

    // b. Power set
    void powerSet() {
        int n = s.size();
        int pow_size = 1 << n;

        cout << "Power Set:\n";
        for(int i = 0; i < pow_size; i++) {
            cout << "{ ";
            for(int j = 0; j < n; j++) {
                if(i & (1 << j))
                    cout << s[j] << " ";
            }
            cout << "}\n";
        }
    }

    // c. subset
    bool isSubset(SET s2) {
        for(int i : s2.s) {
            if(!isMember(i))
                return false;
        }
        return true;
    }

    // d. Union
    SET Union(SET s2) {
        SET result = *this;
        for(int i : s2.s) {
            if(!result.isMember(i))
                result.s.push_back(i);
        }
        return result;
    }

    // d. Intersection
    SET Intersection(SET s2) {
        SET result;
        for(int i : s) {
            if(s2.isMember(i))
                result.s.push_back(i);
        }
        return result;
    }

    // e. Complement
    SET Complement(SET universal) {
        SET result;
        for(int i : universal.s) {
            if(!isMember(i))
                result.s.push_back(i);
        }
        return result;
    }

    // f. Difference
    SET Difference(SET s2) {
        SET result;
        for(int i : s) {
            if(!s2.isMember(i))
                result.s.push_back(i);
        }
        return result;
    }

    // f. Symmetric Difference
    SET SymmetricDifference(SET s2) {
        SET result;
        for(int i : s) {
            if(!s2.isMember(i))
                result.s.push_back(i);
        }
        for(int i : s2.s) {
            if(!isMember(i))
                result.s.push_back(i);
        }
        return result;
    }

    // g. Cartesian Product
    void CartesianProduct(SET s2) {
        cout << "Cartesian Product:\n";
        for(int i : s) {
            for(int j : s2.s) {
                cout << "(" << i << "," << j << ") ";
            }
            cout << endl;
        }
    }
};

int main() {
    SET A, B, U;

    cout << "Enter Set A:\n";
    A.input();

    cout << "Enter Set B:\n";
    B.input();

    cout << "Enter Universal Set:\n";
    U.input();

    cout << "\nSet A: "; A.display();
    cout << "Set B: "; B.display();

    // isMember
    int x;
    cout << "\nEnter element to check in A: ";
    cin >> x;
    cout << (A.isMember(x) ? "Present\n" : "Not Present\n");

    // Power set
    A.powerSet();

    // Subset
    cout << "\nIs B subset of A? ";
    cout << (A.isSubset(B) ? "Yes\n" : "No\n");

    // Union & Intersection
    SET uni = A.Union(B);
    cout << "Union: "; uni.display();

    SET inter = A.Intersection(B);
    cout << "Intersection: "; inter.display();

    // Complement
    SET comp = A.Complement(U);
    cout << "Complement of A: "; comp.display();

    // Difference
    SET diff = A.Difference(B);
    cout << "A - B: "; diff.display();

    // Symmetric Difference
    SET sym = A.SymmetricDifference(B);
    cout << "Symmetric Difference: "; sym.display();

    // Cartesian Product
    A.CartesianProduct(B);

    return 0;
}


#practical_02

#include <iostream>
using namespace std;

class RELATION {
    int n;
    int a[10][10];

public:
    void input() {
        cout << "Enter number of elements: ";
        cin >> n;

        cout << "Enter relation matrix:\n";
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < n; j++) {
                cin >> a[i][j];
            }
        }
    }

    void display() {
        cout << "Relation Matrix:\n";
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < n; j++) {
                cout << a[i][j] << " ";
            }
            cout << endl;
        }
    }

    // Reflexive
    bool isReflexive() {
        for(int i = 0; i < n; i++) {
            if(a[i][i] != 1)
                return false;
        }
        return true;
    }

    // Symmetric
    bool isSymmetric() {
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < n; j++) {
                if(a[i][j] != a[j][i])
                    return false;
            }
        }
        return true;
    }

    // Anti-Symmetric
    bool isAntiSymmetric() {
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < n; j++) {
                if(i != j && a[i][j] == 1 && a[j][i] == 1)
                    return false;
            }
        }
        return true;
    }

    // Transitive
    bool isTransitive() {
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < n; j++) {
                if(a[i][j] == 1) {
                    for(int k = 0; k < n; k++) {
                        if(a[j][k] == 1 && a[i][k] == 0)
                            return false;
                    }
                }
            }
        }
        return true;
    }

    // Final Check
    void checkRelation() {
        bool r = isReflexive();
        bool s = isSymmetric();
        bool a_s = isAntiSymmetric();
        bool t = isTransitive();

        cout << "\nProperties:\n";
        cout << "Reflexive: " << (r ? "Yes\n" : "No\n");
        cout << "Symmetric: " << (s ? "Yes\n" : "No\n");
        cout << "Anti-Symmetric: " << (a_s ? "Yes\n" : "No\n");
        cout << "Transitive: " << (t ? "Yes\n" : "No\n");

        if(r && s && t)
            cout << "\nRelation is an Equivalence Relation\n";
        else if(r && a_s && t)
            cout << "\nRelation is a Partial Order Relation\n";
        else
            cout << "\nRelation is None\n";
    }
};
int main() {
    RELATION R;

    R.input();
    R.display();
    R.checkRelation();

    return 0;
}


#practical_03

#include <iostream>
using namespace std;

void permute(int a[], int l, int r) {
    if(l == r) {
        for(int i = 0; i <= r; i++)
            cout << a[i] << " ";
        cout << endl;
        return;
    }

    for(int i = l; i <= r; i++) {
        // swap
        int temp = a[l];
        a[l] = a[i];
        a[i] = temp;

        permute(a, l + 1, r);

        // backtrack (swap back)
        temp = a[l];
        a[l] = a[i];
        a[i] = temp;
    }
}

int main() {
    int n;
    cout << "Enter number of digits: ";
    cin >> n;

    int a[10];
    cout << "Enter digits:\n";
    for(int i = 0; i < n; i++)
        cin >> a[i];

    cout << "\nPermutations without repetition:\n";
    permute(a, 0, n - 1);

    return 0;
}
#include <iostream>
using namespace std;

void permuteWithRep(int a[], int n, int k, int result[]) {
    if(k == n) {
        for(int i = 0; i < n; i++)
            cout << result[i] << " ";
        cout << endl;
        return;
    }

    for(int i = 0; i < n; i++) {
        result[k] = a[i];
        permuteWithRep(a, n, k + 1, result);
    }
}

int main() {
    int n;
    cout << "Enter number of digits: ";
    cin >> n;

    int a[10], result[10];
    cout << "Enter digits:\n";
    for(int i = 0; i < n; i++)
        cin >> a[i];

    cout << "\nPermutations with repetition:\n";
    permuteWithRep(a, n, 0, result);

    return 0;
}


#practical_04

#include <iostream>
using namespace std;

int x[10]; // stores solution

void solve(int n, int C, int index) {
    // If we reached last variable
    if(index == n - 1) {
        x[index] = C;

        // Print solution
        for(int i = 0; i < n; i++)
            cout << x[i] << " ";
        cout << endl;
        return;
    }

    // Try all values from 0 to C
    for(int i = 0; i <= C; i++) {
        x[index] = i;
        solve(n, C - i, index + 1);
    }
}

int main() {
    int n, C;

    cout << "Enter value of n: ";
    cin >> n;

    cout << "Enter value of C (<=10): ";
    cin >> C;

    cout << "\nSolutions:\n";
    solve(n, C, 0);

    return 0;
}



#practical_05

a[0] = 9   (constant term)  
a[1] = 2   (n¹)  
a[2] = 4   (n²)

#include <iostream>
#include <cmath>
using namespace std;

int main() {
    int degree, n;
    
    cout << "Enter degree of polynomial: ";
    cin >> degree;

    int a[10];

    cout << "Enter coefficients (from constant term to highest degree):\n";
    for(int i = 0; i <= degree; i++) {
        cin >> a[i];
    }

    cout << "Enter value of n: ";
    cin >> n;

    int result = 0;

    // Evaluate polynomial
    for(int i = 0; i <= degree; i++) {
        result += a[i] * pow(n, i);
    }

    cout << "Value of polynomial = " << result;

    return 0;
}



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
