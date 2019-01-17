# Problem
For a given list of locations of restaurants, find the k nearest restaurants.

# Solution
```java
public class Solution
{
    List<List<Integer>> nearestRestaurant(int totalRestaurants, List<List<Integer>> allLocations, int numRestaurants) {
        List<List<Integer>> recommends = new ArrayList<>();

        // no recommends when does not meet to condition
        if(numRestaurants > totalRestaurants || totalRestaurants != allLocations.size() || numRestaurants == 0) {
            return recommends;
        }
        
        // will use MaxHeap with size X to find X nearest restaurants
        PriorityQueue<Restaurant> knn = new PriorityQueue<Restaurant>((x, y) -> Double.compare(y.getDist(), x.getDist()));
        for(List<Integer> locations : allLocations) {
            Restaurant r = new Restaurant(locations);
            // just add this restaurant when the max heap is not full
            if(knn.size() < numRestaurants) {
                knn.add(r);
            }
            // when the heap is full and the max distance in the heap is longer than current restaurant's distance, 
            // it should be removed from the heap and current restaurant should be added.
            else if(r.getDist() < knn.peek().getDist()) {
                knn.poll();
                knn.add(r);
            }
        }
        
        // now remove X restaurants from the max heap and add to the list to return
        while(knn.size() > 0) {
            recommends.add(0, knn.poll().getCoord());
        }
        
        return recommends;
    }
}

class Restaurant {
    private double dist;
    private List<Integer> coord;
    
    public Restaurant(List<Integer> coord) {
        this.coord = coord;
        this.dist = Math.sqrt(Math.pow(coord.get(0), 2) + Math.pow(coord.get(1), 2));
    }
    public List<Integer> getCoord() {
        return this.coord;
    }
    public double getDist() {
        return this.dist;
    }
}
```
