# Introduction

This is the second and final qualification task for the 2018 Agile Robotics for Industrial Automation Competition (ARIAC).

_Participants from ARIAC 2017 should note that the Qualifiers for ARIAC 2018 will be automatically evaluated under the same conditions as the Finals, instead of being run "at home" by competitors._

# Overview

ARIAC qualification task 2 has been designed to evaluate your performance against the challenges that will be present in the final competition.
Up to ten teams will qualify for the Finals through qualification tasks based on their performance.
Teams that did not participate in the first qualification task, and teams that participated but did not qualify, are eligible and encouraged to participate in the second qualification round.

The second qualification task is composed of two parts:

-   Part A: trial config file released to participants for practice.
    - Includes the dropped product, order update and sensor blackout agility challenges.
-   Part B: trial config file not released to participants.
    - Can include any of the agility challenges released when the qualification task was announced.

The qualification task will be evaluated once through the [automated evaluation procedure](https://bitbucket.org/osrf/ariac/wiki/2018/automated_evaluation).
Teams will submit a single system that will be automatically evaluated against Part A and Part B.
Teams will have _one_ attempt: if their system fails, there are no opportunities for a repeat attempt.
Teams will be able to test their system against Part A "at home", but Part B will be previously-unseen and will test system autonomy.

# Important dates

**Qualification task 2 announced:** April 2 2018

**Submissions close:** April 13 2018, 11:59pm PST.

# Qualifying

Up to 10 teams will qualify for the Finals through their performance in the qualifiers.
The scoring metrics that will be used for evaluating the second qualifier [are available here](https://bitbucket.org/osrf/ariac/wiki/2018/scoring) (unchanged from the first qualifier).
Only automated evaluation metrics will be used for the second qualifier.

Any participants found violating submission guidelines will not qualify for the Finals.

# Developing your system

Develop your system so that it can solve:

- qualification task 2 Part A.
- all potential [agility challenges](https://bitbucket.org/osrf/ariac/wiki/2018/agility_challenges) that may be present in qualification task 2 Part B:
    - faulty products.
    - high-priority order interruption.
    - flipped products.
    - faulty gripper resulting in dropped products.
    - updates to previously requested orders.
    - lost sensor communication.

[Details of how to run Part A and what can be expected in Part B are available here](https://bitbucket.org/osrf/ariac/wiki/2018/qualifiers/qual2_scenarios).

To ensure that your system can adapt to previously-unseen scenarios, we recommend that you test your system against all released sample trials, in addition to a variety of custom trials that you create following [this tutorial](https://bitbucket.org/osrf/ariac/wiki/2018/configuration_spec).


# Submission procedure

You will find details on how to prepare your submission, which will allow your system to undergo automated evaluation, on [the automated evaluation page](https://bitbucket.org/osrf/ariac/wiki/2018/automated_evaluation).
Keep in mind that the submission process is not trivial and should be prepared in advance of the submission deadline.

Submissions will be made through secure workspaces directly with competition controllers.
All registered teams must contact ariac@nist.gov to have their workspace prepared in advance of when they intend to submit. **This must not be left to the last minute** or teams risk missing the submission deadline. If you are planning a submission and do not yet have a secure workspace, you must contact ariac@nist.gov ASAP; a *minimum* of 24 hours is required.

# Re-run policy
**Competitors will have one and only one chance to have their system automatically evaluated.**
If your system does not install correctly, you will score 0 points.
If your system does not run correctly, crashes/freezes during trials, or does not score as expected for any other reason, **you will not have a second chance**: the score that your system obtains will be the score that will be used in the rankings.
For that reason it is imperative that teams thoroughly test their submission in the mock automated evaluation setup.

The only circumstance in which re-runs will be warranted are if a bug in the simulation impacts the competitor's performance in a trial.
This includes reported issues [#115](https://bitbucket.org/osrf/ariac/issues/115) and [#116](https://bitbucket.org/osrf/ariac/issues/116) and potentially others at the discretion of the competition controllers.

# Important notes
Teams are advised to review the [update policy](https://bitbucket.org/osrf/ariac/wiki/2018/update_policy) and pay attention to the [updates page](https://bitbucket.org/osrf/ariac/wiki/2018/updates) for upcoming and released changes to the software, rules and scoring metrics.
Notifications when changes to the Updates page are made can be subscribed to [via this Discourse.ros.org thread](https://discourse.ros.org/t/4009).

# Where to go for help
We strive to provide responsive and high-quality support for our software.
Please use [the GEAR/ARIAC issue tracker](https://bitbucket.org/osrf/ariac/issues?status=new&status=open) for submitting and following bugs, feature requests and enhancements.

If you have any questions about competition specifics that you would like to ask in private, please contact ariac@nist.gov.

You can use [the GEAR/ARIAC support forum](https://discourse.ros.org/c/ariac-users) for public discussions about the competition in which other competition participants may participate.