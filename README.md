# shortest-path-bfs
The SP class implements a Breadth-First Search algorithm to find the shortest path in an unweighted graph represented as an adjacency matrix.
The SP class implements a Breadth-First Search algorithm to find the shortest path in an unweighted graph represented as an adjacency matrix.

import java.util.*;

public class SP {
    public static void main(String[] args) {
        int[][] graph = {
                { 0, 1, 0, 0, 0 },
                { 1, 0, 1, 1, 0 },
                { 0, 1, 0, 0, 0 },
                { 0, 1, 0, 0, 1 },
                { 0, 0, 0, 1, 0 }
        };

        int start = 0;
        int end = 4;

        List<Integer> shortestPath = SP.bfsShortestPath(graph, start, end);
        System.out.println("Shortest path from " + start + " to " + end + ": " + shortestPath);
    }
    // public static List<Integer> bfsShortestPath(int[][] graph, int start, int end)
    // requires: a graph represented as adjacency matrix, the start node and the desired destination,unweighted graphs
    // effect: returns a list representing the shortest path betweent the start and the end, if no path exists it returns null

    public static List<Integer> bfsShortestPath(int[][] graph, int start, int end) {
        int n = graph.length;
        int[] parents = new int[n];
        boolean[] visited = new boolean[n];
        Arrays.fill(parents, -1);

        Queue<Integer> queue = new LinkedList<>();
        queue.add(start);
        visited[start] = true;

        while (!queue.isEmpty()) {
            int removed = queue.remove();
            if (removed == end) {
                return reconstructPath(parents, start, end);
            }

            for (int i = 0; i < graph.length; i++) {
                if (!visited[i] && graph[removed][i] == 1) {
                    queue.add(i);
                    visited[i] = true;
                    parents[i] = removed;
                }
            }
        }
        return null;
    }

    // public static List<Integer> reconstructPath(int[] parent, int start, int end)
    // requires: the start node, the destination node and the parent array
    // returns: the shortest path between the start and the end(the path is in order from start to end)
    public static List<Integer> reconstructPath(int[] parent, int start, int end) {
        List<Integer> path = new ArrayList<>();
        int current = end;
        while (current != start) {

            path.add(current);
            current = parent[current];
        }
        path.add(start);
        Collections.reverse(path);
        return path;
    }
}

