# problem statement 

Consider we are building an algorithm for an elevator system for a highrise building like Burj Khalifa. Typically these buildings would have a considerable number of floors / stops. E.g. Burj Khalifa has 165 but let us assume that the number can go upto 200.

## solution

when ever a user press an lift button it becomes a elevator request and add to request array .
request array contains lift of requests (request objects) by user


# elevator request array:
```
request:{
    id,
    floorNumber,
    destFloorNumber,  #inside elevator when users press destination floor
    direction - up or down,
    time,
    assigned - elevatorNumber (which elevator alloted to user),

}
```
# Elevator (lift) object--
```
Elevator{
    elevatorId,
    elevator_State: IDLE / UP / DOWN,  //initally the state is IDLE
    fullCapacity: true/false,
    floorNumber: (lift position )
    stops:[]  
}
```
# Algorithm:
when ever user request for a elevator, check for the nearest elevator and assign the elevator to the user.

nearest elevator choosen by :
 - without full capacity
 - nearest elevator to user
 - and make sure elevator is idle or same direction of user


 pseudocode:
```
 for each request in elevator-request-array{
     assignNearOrIdleElevator(Elevators,request) //passing parameter of elevators objects and request object to assignNearElevator function 
 }
 ```

 # assign an near elevator or idle elevator to user 
```
assignNearOrIdleElevator(Elevators,request){
    nearestElevator = findNearestElevator(Elevators, request) 
	nearestElevator.stops.add(request.floorNumber)
	if nearestElevator.elevator.state == idle
		nearestElevator.elevator.state = request.direction
	request.assigned = nearestElevator.elevatorId
}
```

# method to find nearest elevator based on elevator state , current position ,direction and distance
```
findNearestElevator(Elevators, request) {
	nearestElev = null
	minFloorDiff = INT.MAX
	for each elevator in Elevators {
        		if (fullCapacity == true)  //if elevator is full then we need to check other elevators
			continue;
		if (request.direction == elevator.state  || elevator.state == 'IDLE') {  // if elevator is in same direction of user or lift is idle
			if (elevator.state = up and elevator.floorNumber <= request.floorNumber)  //  checking direction and user floor number
				floorDiff = request.floorNumber - elevator.floorNumber
			else if (elevator.state = down and elevator.floorNumber >= request.floorNumber)
				floorDiff =   elevator.floorNumber - request.floorNumber
			else 
				wait till an elevator is idle or an elevator changes direction
			if (floorDiff < minFloorDiff) {
				minFloorDiff = floorDiff
				nearestElev = elevator
			}
		} 
	}
	return nearestElev;
}
```
# -> after user enters in elevator  press the destination floorNumber button  where user want to go  
```
addDestinationFloorToElevator(Elevator,request){
    Elevator.stops.add(request.destFloorNumber)
}
```


# For morning 8-9 am and for evening 5pm - 9pm  
 
```

for each elevator in  Elevators {	
	if (elevator.idle) {
		if  time between 8 am to 9 am
			elevator.state = down until floor number is 0
		if time between 5 pm  to 9 pm
			elevator.state = up until floor number is top floor
	}
}

```

# it's better to divide the floors to zone 
 No. of zones= total floors/ total elevators
 each zone will be provided with some elevators = total elevators/No. of zones

 consider our algo for burj Khalifa
# example : 
  Burj Khalifa has 165 but let us assume that the number can go upto 200
  total Elevator(lifts) 50
   so the No. of zones for burj khalifa is=200/40 = 5
   divide floors to 5 zones
    so that each zone will have 40/5= 8 lifts for each zone
