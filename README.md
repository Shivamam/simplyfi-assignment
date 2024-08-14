# Assignments

## Assignment 1
### Design the logo provided as an attachment

![HTML & CSS Logo](/SimplyFI/src/assets/simplyfi.png)

## Assignment 2
### Traveling Route Problem

**Question:**  
Your son took a vacation through Europe without telling you. When the kid returned from the vacation, you asked him where he went. The kid told you: "Dad, I went to these cities: Amsterdam, Kiev, Zurich, Prague, Berlin, Barcelona. I used only train as transportation, and these were the available tickets:
- Paris-Skopje
- Zurich-Amsterdam
- Prague-Zurich
- Barcelona-Berlin
- Kiev-Prague
- Skopje-Paris
- Amsterdam-Barcelona
- Berlin-Kiev
- Berlin-Amsterdam

You know that your kid started with Kiev.  
Write a data structure and algorithm that will give you the route your son was traveling.

**Answer:**

```javascript
function findRoute(tickets, startCity) {
    // Step 1: Build the graph from the tickets
    let graph = {};
    for (let [start, end] of tickets) {
        if (!graph[start]) {
            graph[start] = [];
        }
        graph[start].push(end);
    }

    // Step 2: Implement DFS to find the route
    function dfs(currentCity, route) {
        route.push(currentCity);
        if (route.length === tickets.length + 1) {
            return route;
        }
        if (!graph[currentCity]) {
            route.pop();
            return null;
        }
        for (let i = 0; i < graph[currentCity].length; i++) {
            let nextCity = graph[currentCity][i];
            graph[currentCity].splice(i, 1); // Remove the route to avoid revisiting
            let result = dfs(nextCity, route);
            if (result) {
                return result;
            }
            graph[currentCity].splice(i, 0, nextCity); // Backtrack
        }
        route.pop();
        return null;
    }

    // Initialize the route and start DFS
    let route = [];
    return dfs(startCity, route);
}

// Define the list of tickets and start city
const tickets = [
    ["Paris", "Skopje"],
    ["Zurich", "Amsterdam"],
    ["Prague", "Zurich"],
    ["Barcelona", "Berlin"],
    ["Kiev", "Prague"],
    ["Skopje", "Paris"],
    ["Amsterdam", "Barcelona"],
    ["Berlin", "Kiev"],
    ["Berlin", "Amsterdam"]
];
const startCity = "Kiev";

// Find the route
const route = findRoute(tickets, startCity);
console.log(route);


### Explanation:

I solved this problem by implementing a Depth-First Search (DFS) algorithm.

1. **Constructing the Graph**:
   - I began by creating a graph from the provided train tickets. Each city is treated as a node, and a connection is made to the cities that can be reached directly. This graph is represented as an object where each key is a starting city, and the corresponding value is an array of destination cities.

2. **Implementing Depth-First Search (DFS)**:
   - I then utilized DFS to explore possible travel routes, starting from the specified city, "Kiev". The DFS function pushes each city onto the route as it explores.
   - The algorithm checks if it has visited all the cities (i.e., if the length of the route matches the number of tickets plus one). If so, it returns the route as the solution.
   - If it encounters a dead-end (no more cities to visit from the current one), it removes the last city from the route and continues searching for alternative paths.

3. **Handling Dead-ends with Backtracking**:
   - In cases where the DFS hits a dead-end, I implemented backtracking by removing the last city from the route and reinserting the corresponding connection. This allows the algorithm to explore different paths and eventually find the correct route.

This approach ensures that the correct sequence of cities visited by my son is determined based on the available train tickets.
