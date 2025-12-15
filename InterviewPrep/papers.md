# how safe is safe enough?  Automatic Safety Constraints Boundary

Estimation for Decision-Making in Automated Vehicles

Our main contribution is a method to automatically

explore the performance limits of AV safety models

using Robustness as a continuous metric of safety.

• We evaluate this approach with a case study of the

RSS safety model where the RSS parametric space

is explored to create robustness-based safety profiles

of a pre-crash scenario database; obtaining as result

the parametric boundaries of RSS for collision-free

behaviors.

• Furthermore, we evaluate the trade-offs between AV

safety and utility within the found safe RSS parameter

space through a simulated, naturalistic-like benchmark.

• Finally, we provide the library implementation de-

scribed in this paper as an open-source project that

can be found under the following URL: https://

github.com/nellro/rgt.

![](/Users/xonxis/Library/Application%20Support/marktext/images/2025-12-15-07-16-46-image.png)

**Search Algorithm**

Simulated annealing (SA) is a gradient-free stochastic optimization algorithm for approximating the global optimum of a given function [25]. At each iteration k, a new sample pointˆ x∈X0 is generated using hit-and-run proposal scheme [28]. SA accepts x as xk+1 with a probability:

P(xk+1 = ˆ x |xk) = 1 if ρk+1 ≤ρk (2)

e−Tk (ρk+1−ρk ) if ρk+1 >ρk

where ρk = ρϕ(xk), ρk+1 = ρϕ(ˆ x) and Tk >0 is a current

“temperature” parameter. In particular, if a new sampleˆ x

reduces the robustness value (ρϕ(ˆ x) ≤ ρϕ(xk)), the new sample is accepted with certainty. Otherwise, the proposal

may still be accepted with probability e−Tk (ρk+1−ρk ).

# On Responsibility Sensitive Safety in Longitudinal Follow-up Situations: A Parameter Analysis on German Highways

we focus on finding reasonable parameters of RSS. Based on the physical limits, legal requirements and human driving behavior, we propose scopes and parameter sets that allow for a sound safety verification while not hindering traffic flow. Furthermore, we present an approach that explains seemingly frequent human drivers’ RSS violations on highways and may lead to a useful extension of RSS.

# IV 2020: Evaluation of Responsibility-Sensitive Safety (RSS) Model based on Human-in-loop Driving Simulation

This paper evaluates the safety performance of RSS using

human-in-loop driving simulation. Two microscopic car-

following simulation scenarios are designed according to

Shanghai Naturalistic Driving Study. By embedding two

different RSS models into a Model Predictive Control (MPC)

based ACC algorithm and connecting it to vehicles in SCANeR,

drivers are tested to evaluate the safety performance of the three

different system setups: ACC with two different RSS models

(original and improved) and ACC without RSS. Safety

perception of the models is analyzed considering a reaction time,

the maximum deceleration and a safety score.

Results show that the Original RSS model is

significantly safer than the non-embedded RSS model from the

perspective of human drivers. There was small, but significant

differences between the Efficiency-optimal RSS model and the

non-embedded RSS model in drivers' subjective scores

# SAE WCX 2022: Evaluation of Operational Safety Assessment (OSA) Metrics for Automated Vehicles Using Real-World Data

A methodology was developed using computer vision to localize the

vehicles using the video data and fusing them with a map

representation to obtain vehicle-vehicle relations and the maneuvers in

which they are involved. Longitudinal conflicts in car-following

scenarios were filtered to compute the safety envelope OSA metrics.

Analysis of the safety envelope OSA metrics results were conducted

to identify the usefulness of the various metrics in the car-following

scenarios and to make a comparison to the observations from

simulation.

# 2022 TRB: **RSS Model Calibration and Evaluation** for AV Driving Safety based on Naturalistic Driving Data

Utilizing the responsibility-sensitive safety (RSS) model, a new methodology is proposed to calibrate the RSS model based on naturalistic driving data. Without significantly relying on (large) safety-critical or collision data, the proposed method defines an optimization framework to calibrate the RSS model parameters and describes AV driving safety through both safe and safety-critical data in a cross-checking manner. Evaluation of the calibrated RSS model is discussed based on naturalistic driving data in Los Angeles, USA

The optimization problem is solved by a genetic algorithm (GA), which is a method for solving nonlinear (even nonconvex) constrained optimization problems based on a natural selection process that mimics biological evolution. To find the optimal solution, at each generation, GA randomly modifies the individuals and then uses them as the parents of the next generation. After successive generations, the population evolves until the terminal conditions are satisfied

<img src="file:///Users/xonxis/Library/Application%20Support/marktext/images/2025-12-15-07-38-00-image.png" title="" alt="" width="704">

# 2022 SAE WCX: To err is human

Our analysis demonstrated that human driver derived

safety metrics are inadequate in their application to the perfor-

mance of automated vehicles, and new metrics such as the

Minimum Safe Distance Violation are more meaningful in

the consideration of the safety performance of AVs.
