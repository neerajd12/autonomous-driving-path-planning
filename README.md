# autonomous-driving-path-planning

The idea is to create a cost funciton that will help a autonomous vehicle controller decide the lane it should take on a highway

## The Cost Function

The cost is calculated in "calculate_lane_costs" function.

Costs are only calculated for adjacent lanes because there is no point in looking at other lanes if it's not safe to cross over to adjacent once.

For now the logic initializes costs for all lanes to 0 and adds 1 to the lane cost for every car it finds in the buffer distance 20 m from the car. For each lane, if we see 1 car in front or back of our car the cost for that lane is 1. If there are 2 cars then the cost is 2 and so on.

This approach tells the controller that lanes with higher number of cars is not a good candidate for switching as there are for variables that can cause congestion or can have a car coming from behind that might be a problem.


Finally, the cost for lanes on the other side of the highway or outside of the road is set to a sufficently high number, which is impossible in the buffer distance.


## Deciding Lane and speed

logic to decide lane and speed of the car is in "decide_lane_and_speed" function.

### Deciding lane

* The lane is only changed if the cost for current lane is more then the adjacent lanes.
* If the costs are same than the current lane is preferred.
* Of the lowest cost lanes right lane is preferred. This can be changed if required.

### Deciding Speed

* The speed is continously increased untill it reaches the max safe speed and the cost of the lane is zero.
* If the lane cost is not zero the speed is continously reduced with no lower bounds.
* Speed is reduced at a faster rate compared to increasing it. This helps in better stopping.
