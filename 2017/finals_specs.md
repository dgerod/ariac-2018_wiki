# Finals Specifications

[See this page for details of how the Finals will be run.](https://bitbucket.org/osrf/ariac/wiki/2017/finals)

## *Competition management*

### **How many trial runs will be run?**

The competition will be made up of 15 trial runs. Each trial run will use a unique competition scenario configuration.

### **Will there be a time limit for each trial run?**

Yes, 500 simulation seconds. With a real-time factor of 1.0, this equates to 500 real seconds. With a real-time factor of 0.5, this equates to 1000 real seconds. Teams can listen to the `/clock` ROS topic to know the simulation time ([see 'Using Simulation Time from the /clock Topic'](http://wiki.ros.org/Clock#Using_Simulation_Time_from_the_.2BAC8-clock_Topic)).

### **What happens in the event of a tie?**

If two or more teams are tied for first after the 15 trial runs, those teams will participate in a tie-breaker round. The tie-breaker round will be made up of 3 trial runs with new scenarios. Additional tie-breaker rounds will be completed if necessary until a single team is determined as the winner.

### **Can each trial run be done with different solutions? E.g., using a scanner over the belt in one trial, but using a logical camera over the belt in another trial?**

One sensor configuration file is to be used for all trials. Teams must provide a single "system" that will be used for all trials: the same system will be run multiple times in exactly the same way. The system will not have access to the trial number or other information about the trial configuration at startup time.

## *Parts*

### **Which storage bins will be used to store parts?**

Only the four bins closest to the conveyor belt (those used in the qualifiers) will be used in the final competition. In a given trial, any combination of the four bins may be used as storage locations for parts.

### **How can we know the starting configuration of parts in the bins?**

The number of parts that are stored in a given bin and their configuration will vary with each trial run. Logical cameras should be used to detect the part configurations; the information will not be communicated to teams through other means.

### **Which parts will be used in the competition?**
The five models used in qualifiers will be used in the competition; no additional parts will be added. The piston rod, gear, gasket and disk parts may be stored in the bins or on the conveyor belt, while the pulley part will only ever be stored in the bins, never on the conveyor belt.

### **Will storage bins ever contain more than one type of part?**
No, there will be at most one type of part per bin. The belt, on the other hand, may have multiple types of parts.

### **Do we have an estimate on the probability of defective parts in the bin and/or conveyor belt?**

Approximately 10% of parts in the bins can be expected to be faulty.
Parts on the conveyor belt are of higher quality: approximately 5% can be faulty.

## *Orders*

### **How many orders per trial run can we expect?**

There will be at most two orders per trial run. If two orders are received, the second of those is the high priority order.

### **How do we know the priority of an incoming order?**

The most recently received order is the highest priority.

### **What are the limitations of the orders?**

Orders may be made up of parts available from the bins and/or the conveyor belt. Each order may have up to 2 kits. No kit will have more than 8 parts. The only part that will be requested to be flipped is the pulley part.

### **Will there always be enough parts to fill the required kits?**

Between the storage bins and the conveyor belt, sufficiently many non-faulty parts of each type will appear in the environment during a trial to complete the kits in the requested orders.

## *Topics and services*

### **Will there be a topic or service from which we will be able to read the conveyor speed?**

Such a topic/service for reading the conveyor belt speed will not be provided; sensors are to be used.

### **Will the belt speed be controllable programmatically? **
The speed of the conveyor belt will not be controllable by teams. Retrieving parts from the conveyor belt is required to complete some of the 15 trial runs, but it will not be required for all of them.

### **Which of the services can be used during the Finals? **
The topics/services listed in [in the ARIAC interface page](https://bitbucket.org/osrf/ariac/wiki/2017/competition_interface_documentation) that are not labelled as "cheats" will be available during the finals. All other interfaces with the simulation will be blocked, and attempts to use them will not be permitted.
## *Conveyor belt*

### **Will the belt speed be held constant between runs?**

The speed of the conveyor belt will be held constant over all runs, in the same direction.

### **Where will the parts on the conveyor belt start?**

As in the qualifiers, parts will appear on the conveyor belt in front of AGV1. Parts will only ever appear one at a time, centered on the belt. Parts may have any orientation in yaw but they will never appear upside-down.

### **For the parts that are available on the conveyor belt, how many of each part will appear during a trial run?**

A limited number of each part will appear during a trial. The number will vary between trials.

## *Sensors*

### **Is there a minimum/maximum number of sensors?**

A minimum of one sensor is required, no maximum.

### **Is it compulsory to place sensors over the AGVs?**

No, but without sensors over the AGVs teams will not be able to detect where a part lands if the gripper fails and the part is dropped.