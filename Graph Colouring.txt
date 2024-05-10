
#include <iostream>
#include <vector>
using namespace std;

const int V = 5; // Assuming V is a global constant

bool isSafeToColor(vector<vector<int>>& graph, vector<int>& color) {
    for (int i = 0; i < V; i++)
        for (int j = i + 1; j < V; j++)
            if (graph[i][j] == 1 && color[j] == color[i])
                return false;
    return true;
}

void printColorArray(vector<int>& color) {
    cout << "Solution colors are: ";
    for (int i = 0; i < color.size(); i++) {
        cout << color[i] << " ";
    }
    cout << endl;
}

void graphInput(vector<vector<int>>& graph) {
    cout << "Enter the adjacency matrix for the graph:" << endl;
    for (int i = 0; i < V; ++i) {
        for (int j = 0; j < V; ++j) {
            cin >> graph[i][j];
        }
    }
}

bool graphColoring(vector<vector<int>>& graph, int m, int i, vector<int>& color) {
    if (i == V) {
        if (isSafeToColor(graph, color)) {
            printColorArray(color);
            return true;
        }
        return false;
    }
    for (int j = 1; j <= m; j++) {
        color[i] = j;
        if (graphColoring(graph, m, i + 1, color))
            return true;
        color[i] = 0;
    }
    return false;
}

int main() {
    vector<vector<int>> graph(V, vector<int>(V, 0));
    graphInput(graph);

    int m = 3; // Number of colors
    vector<int> color(V, 0); // Initialize color vector with size V and default value 0
    if (!graphColoring(graph, m, 0, color)) {
        cout << "No solution exists." << endl;
    }

    return 0;
}
