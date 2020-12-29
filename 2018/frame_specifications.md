# Details of Products specified in Orders
This page outlines the specifications of the pose requirements specified in each Order.

As outlined in the [competition specifications](https://bitbucket.org/osrf/ariac/wiki/2018/competition_specifications), an Order specifies a list of products to be put into each shipment.
Each product has a specified type and required position and orientation in the shipping box.

As specified on the [competition interface](https://bitbucket.org/osrf/ariac/wiki/2018/competition_interface_documentation) page, Orders are communicated to teams with the `osrf_gear/Order` ROS message.

## Type of the product
The type of the product is specified as its product name, such as `gear_part` or `piston_rod_part`.
The availability of these products in the workcell may be determined by querying the `material_locations` ROS service as specified [in this tutorial](http://wiki.ros.org/ariac/2018/Tutorials/GEARInterface#Querying_storage_locations_of_parts).

## Pose of the product in the shipping box
The pose of the product is composed of the position and the orientation of the product **specified in the reference frame of the shipping box**.
It is communicated in a [geometry_msgs/Pose](http://docs.ros.org/kinetic/api/geometry_msgs/html/msg/Pose.html) message.

### Frame of the shipping box
The following image depicts the frame of a shipping box on the conveyor belt.
The x, y, and z axes are represented by red, green and blue markers, respectively.
This shipping box has a `gear_part` with its origin at `(x, y, z) = (0, 0.15, 0)` (units in meters) and a `piston_rod_part` at `(0.1, -0.2, 0)`.
Both products have an orientation of `(roll, pitch, yaw) = (0, 0, 0)` (units in radians) with respect to the frame of the shipping box.

![https://bitbucket.org/osrf/ariac/wiki/2018/img/shipping_box_frame.jpg](https://bitbucket.org/osrf/ariac/wiki/2018/img/shipping_box_frame.jpg)

The following image shows the shipping box with two products on it. In this case,`gear_part` has a position `(x, y, z) = (0, 0.15, 0)` (units in meters) and an orientation `(roll, pitch, yaw) = (0, 0, 1.57)` (units in radians). `Piston_rod_part` has a position `(x, y, z) = (0.1, -0.2, 0)` and an orientation `(roll, pitch, yaw) = (0, 0, 1.57)`.

![https://bytebucket.org/osrf/ariac/wiki/2018/img/rotated_frame.jpg?rev=0d9fd772b7c1edf93b72ff4d06e07697a8cc708b](https://bytebucket.org/osrf/ariac/wiki/2018/img/rotated_frame.jpg?rev=0d9fd772b7c1edf93b72ff4d06e07697a8cc708b)

### Frame of the product
The pose of the product in the workcell environment will vary over time as the product is moved.
The frame of each product is typically at the center of the product: it can be visualized by clicking on the product in the simulated workcell environment and pressing `t`: this will display the axes of the frame of the product.

The following figure shows the frame of the `gear_part`, with the x, y and z axes represented by red, green and blue markers, respectively.

![https://bitbucket.org/osrf/ariac/wiki/2018/img/gear_part_frame.jpg](https://bitbucket.org/osrf/ariac/wiki/2018/img/gear_part_frame.jpg)

Not all products have the frame origin at their center: the `piston_rod_part`, for example, has the origin of its frame off-center, as shown in the following figure.

![https://bitbucket.org/osrf/ariac/wiki/2018/img/piston_rod_frame.jpg](https://bitbucket.org/osrf/ariac/wiki/2018/img/piston_rod_frame.jpg)

### Flipped products

An order could contain a product that requires to be flipped, in which case the requested `roll` for the product will be specified as pi. The `pulley_part` is the only product in the environment designed to be flippable. It has a flat collision surface on its top and bottom ends making it ideal for grasping it with a vacuum gripper. However, the side of the product is hollow, creating a more difficult grasp because of the small contact patch that the edges provide. Teams are not permitted to directly grasp this product from the side when a product flip is required.

![https://bitbucket.org/osrf/ariac/wiki/2018/img/flipped_frame.jpg](https://bitbucket.org/osrf/ariac/wiki/2018/img/flipped_frame.jpg) 

### Determining the product pose in the shipping box programmatically
The logical camera reports the pose of products and shipping boxes with respect to the pose of the camera.
See the [sensor interface tutorial](http://wiki.ros.org/ariac/2018/Tutorials/SensorInterface#Logical_camera) for details of how to use this sensor to programmatically determine the pose of products on the shipping boxes.

Other sensors can also be used if combined with perception algorithms.
Note that some parts have a raised mark on them so that their orientation can be detected.

### Visualizing requested shipments
Shipments can be visualized by passing the `--fill-demo-shipment` option to `gear.py` invocations, which is what is used in the [sensor interface tutorial](http://wiki.ros.org/ariac/2018/Tutorials/SensorInterface).