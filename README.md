# Assignments

## Assignment 1
### Design the logo provided as an attachment

![simplyfi](https://github.com/user-attachments/assets/7740ceb4-d83f-416e-8ce3-a3b4fb6f4691)

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
const trainRoutes = {
    "Kiev": ["Prague"],
    "Prague": ["Zurich", "Kiev"],
    "Zurich": ["Amsterdam", "Prague"],
    "Amsterdam": ["Barcelona", "Berlin"],
    "Berlin": ["Kiev", "Amsterdam"],
    "Barcelona": ["Berlin"]
};

function findRoute(start, visited, route) {
    const citiesToVisit = new Set(["Amsterdam", "Kiev", "Zurich", "Prague", "Berlin", "Barcelona"]);
    
    if (visited.size === citiesToVisit.size) {
        return route;
    }

    for (const neighbor of trainRoutes[start]) {
        if (!visited.has(neighbor)) {
            visited.add(neighbor);
            const result = findRoute(neighbor, visited, [...route, neighbor]);
            if (result) {
                return result;
            }
            visited.delete(neighbor);
        }
    }

    return null;
}

const visitedCities = new Set(["Kiev"]);
const initialRoute = ["Kiev"];
const route = findRoute("Kiev", visitedCities, initialRoute);

console.log("The route taken is:", route);

```
### Explanation:

To find the route my son took during his vacation, I created a program that uses a graph to represent the cities and train routes. Here’s how I did it:
1. I started by creating an object called trainRoutes. This object lists all the cities and the direct train connections between them. For example, from Kiev, my son could travel to Prague.
2. To explore the possible routes, I implemented a function called findRoute. This function uses a technique called Depth-First Search (DFS). It helps me explore all the paths starting from the city where my son began, which is Kiev.
3. The findRoute function takes three parameters:
        The current city (start) where my son is.
        A set of cities (visited) that he has already visited.
        An array (route) that keeps track of the route he has taken so far.
4. Inside the function, I first check if my son has visited all the required cities (Amsterdam, Kiev, Zurich, Prague, Berlin, and Barcelona). If he has, I return the current route.
5. If he hasn’t visited all the cities, I look at all the cities he can travel to directly from the current city. For each neighboring city, I check if he has already visited it. If not, I mark it as visited and add it to the current route.
6. After adding a neighbor to the route, I call the findRoute function again with the new city, updated visited cities, and the new route. This allows me to continue exploring from the new city.
7. If I reach a point where I can’t find a valid route, I backtrack by removing the last visited city and trying a different path. This way, I can explore all possible routes.
8. Starting the Search: I start the search from Kiev, initializing the visited cities set with only Kiev and the initial route with just Kiev. Then, I call the findRoute function to find the complete route.
9. Finally, I print the route that my son took, which includes all the cities he visited.

    ![Assignment2 Output](/src/assets/assignment2.png)

By using this approach, I was able to determine the exact route my son traveled during his vacation in Europe!
