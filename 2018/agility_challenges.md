# Details of agility challenges

This page explains the details of agility challenges that may be present in trials.
Each challenge has at least one accompanying sample trial config file provided in the `config` directory that can be used to practice.
The sample trial config files explain the expected behavior at the top of the file.
See the [configuration tutorial](https://bitbucket.org/osrf/ariac/wiki/2018/configuration_spec) for how to use these trial config files.

## Faulty products

Sample trial: `sample_not_enough_products.yaml`

Faulty products should not be used to fulfill the orders.
See [this page](http://wiki.ros.org/ariac/2018/Tutorials/GEARInterface#Faulty_products) for details on working with faulty products.

## Insufficiently many products

Sample trial: `sample_not_enough_products.yaml`

Not enough non-faulty products are in the environment to fulfill all requested orders.

## Flipped products

Sample trial: `sample_flipped.yaml`

An order contains products that must be flipped.
Only the `pulley_part` will ever be requested to be flipped.
See [this page](https://bitbucket.org/osrf/ariac/wiki/2018/frame_specifications#markdown-header-flipped-products) for details on working with flipped parts.

## In-process order update

Sample trial: `sample_order_update.yaml`

An update to a previously assigned order is sent, identifiable with the order ID such as "order_0_update_0".
Shipments will be evaluated against the updated order.
Teams should respond by filling the updated order as usual (submitting shipments named "order_0_shipment_0" still), instead of the original order.

## Sensor blackout

Sample trial: `sample_sensor_blackout.yaml`

Communication with the sensors will be lost temporarily, referred to as a "sensor blackout".
Teams should continue to fill the order as usual during this time.

At the start of the trial the sensors will be publishing data normally, and at a particular instance *all* sensors will *stop* publishing for a fixed period of time.
This applies to team-specified sensors and sensors that are present by default in the environment such as the quality control sensors.

The communication will be lost for a duration in the range of 10 to 100 simulation seconds.

Note that re-connecting to some sensors during development will cause them to resume publishing data, but this functionality is blocked in the automated evaluation setup.

## Dropped products

Sample trial: `sample_dropped_products.yaml`

The gripper becomes faulty at various instances, e.g. when a product is retrieved from the storage bins, or when a product is being placed into a shipping box.
Recovery could include retrieving the dropped product or fetching a new product.

## In-process order interruption

Sample trial: `sample_interruption1.yaml`, `sample_interruption2.yaml`

A second order is announced part-way into the completion of the first order.
Shipments from both orders can be submitted after this time, but the second order is higher priority and for maximum points it should be completed as fast as possible.
To complete the second order, teams can choose to remove the products already in the shipping box(es) or switch to an empty shipping box.