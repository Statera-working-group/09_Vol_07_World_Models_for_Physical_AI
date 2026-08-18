**Volume 07. World Models for Physical AI**

# Chapter 10. Physics Informed World Models

## 10.01. Why Physical Priors Matter

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

Physical priors matter in world models because Physical AI operates in environments governed by persistent laws rather than arbitrary statistical relationships. Objects have mass, occupy space, resist penetration, exchange forces, conserve momentum, and move according to constraints imposed by geometry and dynamics. A world model that incorporates these regularities can predict physically plausible futures instead of merely reproducing correlations observed in training data.

Purely data-driven models can learn many physical relationships implicitly when trained on sufficiently diverse experience, but this approach may require enormous datasets and still fail in unfamiliar situations. A model may observe thousands of examples of falling objects without explicitly representing gravity, acceleration, or collision. Physical priors introduce structural assumptions that narrow the hypothesis space and encourage the model to learn dynamics consistent with the physical world.

A physical prior does not necessarily mean that every equation of classical mechanics must be explicitly programmed into the model. Priors can appear at many levels, including architectural constraints, loss functions, state representations, differentiable simulation components, geometric relationships, or parameterized dynamics. Even simple assumptions such as temporal continuity, object permanence, non-penetration, bounded acceleration, and smooth motion can substantially improve prediction quality.

For Physical AI, these priors are especially important because prediction errors eventually affect real actions. A language model can generate an incorrect sentence without directly changing the physical environment, whereas a robot acting from an incorrect prediction may collide with an obstacle, lose stability, damage an object, or endanger a person. The world model therefore needs representations that respect feasible motion, contact conditions, actuator limits, and environmental constraints.

Physical priors also improve sample efficiency. When a model already assumes that objects normally move continuously through space, it does not need to rediscover this principle independently for every object category and environment. Knowledge learned from one interaction can therefore constrain predictions in another. This reduces the amount of experience required to learn useful dynamics and becomes particularly valuable when collecting real-world robotic data is expensive, slow, or potentially dangerous.

Another advantage is improved generalization beyond the training distribution. Statistical correlations may change dramatically when a robot encounters a new payload, surface, slope, object geometry, or operating speed. Fundamental physical relationships often remain more stable. A model that represents forces, inertia, contact, geometry, or conservation principles can use these invariant structures to extrapolate more reliably when visual appearance or environmental configuration changes.

Geometry itself provides a powerful class of physical priors. Robots operate in three-dimensional space where objects have position, orientation, extent, and spatial relationships. Representations such as Bird\'s-Eye View, occupancy fields, point clouds, meshes, and object-centric states can encode these properties directly. Geometric priors help the world model understand free space, collision boundaries, visibility, reachability, and how transformations of the robot or sensors affect observations.

Temporal structure provides another essential prior. Physical states normally evolve continuously, even when sensors observe them at discrete intervals. Position, velocity, acceleration, joint configuration, and contact state are related across time rather than being independent observations. Encoding temporal consistency helps distinguish physically meaningful motion from sensor noise and enables the model to estimate hidden states that cannot be directly measured at every instant.

Contact introduces particularly difficult dynamics because interactions can change abruptly when bodies touch, separate, slide, roll, or collide. A manipulation world model that ignores contact structure may predict visually reasonable trajectories while producing impossible object motions. Contact-aware priors can constrain predictions through collision geometry, friction, normal forces, grasp conditions, and rigid-body relationships, making predicted interactions more useful for robotic control.

Actuator and embodiment constraints are equally important. The future state of a robot depends not only on the external environment but also on its morphology, joint limits, wheel configuration, motor characteristics, payload, and control interface. A quadruped, wheeled AMR, manipulator, and humanoid cannot execute identical state transitions. Embodiment-aware physical priors therefore connect world modeling with the actual capabilities and limitations of the physical agent.

Physical priors are also useful for separating possible futures from merely imaginable futures. Generative models may produce diverse predictions, but diversity alone does not guarantee feasibility. When physical constraints are incorporated, the prediction space can be restricted to trajectories satisfying approximate dynamics, collision constraints, kinematic limits, and energy or momentum relationships. This allows computational resources to focus on futures that could realistically occur.

This distinction becomes critical during counterfactual prediction. A robot may internally evaluate what would happen if it accelerated, turned, pushed an object, changed its grasp, or selected another trajectory. Without physical structure, counterfactual predictions can drift toward statistically plausible but dynamically inconsistent outcomes. Physical priors provide stable causal relationships between actions, forces, motion, contact, and resulting states, improving imagined rollouts used for planning.

Physical priors can additionally provide inductive bias without eliminating learning. Real environments contain effects that analytical models cannot perfectly capture, including tire deformation, complex friction, actuator backlash, flexible materials, aerodynamic disturbances, wear, and uncertain payload distributions. Consequently, a useful world model does not need to choose between physics and learning. Instead, known structure can constrain the model while neural components learn residual or unknown dynamics.

This hybrid perspective creates a spectrum between analytical physics and unrestricted learned dynamics. At one end, explicit equations determine state transitions from known parameters. At the other, neural networks learn transitions almost entirely from data. Between them are physics-informed neural networks, differentiable simulators, residual dynamics models, constrained latent models, and architectures that embed conservation laws or geometric structure while retaining adaptive learned components.

Physical priors can also improve interpretability and debugging. When predicted motion violates known constraints, engineers gain meaningful diagnostic signals. Unexpected energy growth, penetration between rigid bodies, discontinuous velocity, or impossible joint configurations can indicate model failure even before task-level performance collapses. Such checks provide additional mechanisms for validating a world model beyond conventional prediction losses measured only against recorded data.

Safety benefits follow naturally from these constraints. Physical AI systems frequently operate near humans, machinery, vehicles, or valuable infrastructure, where rare prediction failures can have serious consequences. A physically constrained model can reject trajectories that exceed acceleration limits, violate stability margins, enter occupied space, or demand impossible actuator behavior. Physical priors therefore contribute not only to prediction accuracy but also to runtime feasibility checking.

The importance of priors increases as prediction horizons become longer. Small inconsistencies in velocity, force, geometry, or contact can accumulate across repeated state transitions until long-horizon rollouts become physically meaningless. Conservation constraints, stable dynamics representations, and structured state transitions can reduce this drift. They do not eliminate uncertainty, but they help prevent prediction errors from expanding into futures that contradict basic properties of the environment.

Physical priors also complement uncertainty modeling. Some physical parameters, such as friction coefficients, object masses, terrain properties, or payload distributions, may be unknown rather than fixed. Instead of assuming exact values, the world model can represent distributions over these quantities and propagate their uncertainty through predicted dynamics. Physics then supplies the structural relationships, while probabilistic learning represents uncertainty about the parameters and unobserved conditions.

Ultimately, physical priors provide a bridge between perception-driven learning and reliable interaction with the real world. They transform world modeling from unrestricted prediction into prediction constrained by what physical systems can actually do. For Physical AI, the strongest world models are therefore likely to combine learned representations, large-scale experience, multimodal observations, action-conditioned prediction, uncertainty estimation, and reusable physical structure rather than relying on any single approach alone.

## 10.02. Learned vs Analytical Dynamics

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

Analytical dynamics models describe how a physical system evolves by using explicitly defined mathematical relationships derived from mechanics, kinematics, thermodynamics, fluid dynamics, or other physical theories. Given a state (s_t), an action (a_t), and known physical parameters, the model computes the next state (s_{t+1}) according to predetermined equations. This provides a structured and interpretable foundation for predicting physical behavior.

In robotics, analytical dynamics often begins with equations such as Newton--Euler mechanics, rigid-body dynamics, or Lagrangian mechanics. Robot mass, inertia, joint configuration, applied torque, gravity, and external forces determine acceleration and subsequent motion. Because the underlying relationships are explicitly represented, engineers can examine why a predicted transition occurs and determine whether the result satisfies known physical constraints.

Analytical models offer strong generalization when their assumptions accurately represent the system. The relationship between force, mass, and acceleration does not need to be relearned whenever the robot enters a new environment. Conservation laws, geometric constraints, and rigid-body relationships remain applicable across many situations. These physical invariances make analytical dynamics particularly useful when training data are limited or when extrapolation beyond observed examples is required.

However, real robotic systems rarely match ideal analytical models perfectly. Friction coefficients may change with surface conditions, tires deform under load, motors exhibit nonlinear responses, joints contain backlash, and mechanical components gradually wear. Flexible structures, cables, fluids, soil, vegetation, and deformable objects introduce additional effects that may be difficult or computationally expensive to model accurately using explicit equations alone.

Learned dynamics approaches address these limitations by estimating state transitions directly from data. Instead of specifying every physical relationship manually, a neural network can learn a transition function such as (s_{t+1}=f_\\theta(s_t,a_t)), where the parameters (\\theta) are optimized from observations of system behavior. The model discovers patterns connecting states, actions, and resulting states without requiring complete analytical knowledge of the underlying physics.

Learned models are particularly attractive when system dynamics are complex, partially unknown, or difficult to parameterize. A mobile robot traversing gravel, mud, grass, slopes, and irregular terrain experiences interactions that may be extremely difficult to capture with a single analytical tire or contact model. Data-driven dynamics can instead learn how commanded velocity, terrain appearance, robot state, slip, vibration, and previous motion jointly influence future behavior.

Another advantage is representational flexibility. Analytical models normally require engineers to choose meaningful state variables and derive equations relating them. Learned dynamics can operate on high-dimensional representations produced directly from cameras, LiDAR, radar, proprioception, or multimodal encoders. Latent dynamics models can therefore predict changes in compact learned representations without reconstructing every physical quantity explicitly at each prediction step.

This flexibility comes with important disadvantages. Learned dynamics can reproduce statistical regularities without discovering the physical mechanisms responsible for them. A model may perform extremely well within its training distribution but behave unpredictably when payload, terrain, speed, morphology, or environmental conditions change. Because its predictions arise from learned parameters distributed across a neural network, diagnosing the physical reason for a failure may also be difficult.

The contrast between analytical and learned dynamics can therefore be understood as a difference in where knowledge originates. Analytical models obtain structure primarily from human knowledge of physics and engineering, while learned models obtain structure primarily from observations and optimization. The former typically provides stronger interpretability and physical consistency, whereas the latter provides greater flexibility for modeling complex effects that cannot easily be written as explicit equations.

Their computational characteristics can also differ significantly. High-fidelity analytical simulation may require repeated collision detection, constraint solving, numerical integration, and contact calculations. A learned dynamics model can approximate these processes with a neural-network forward pass after training. This can make learned models attractive for world-model rollouts where thousands of candidate futures must be evaluated rapidly during planning or model-based reinforcement learning.

Yet computational speed does not automatically imply physical reliability. Neural dynamics models can accumulate small prediction errors during repeated rollout, producing states that gradually violate geometry, stability, contact, or conservation constraints. Analytical models can also accumulate numerical errors, but their explicit structure often provides stronger mechanisms for maintaining physical consistency. Long-horizon world modeling therefore exposes weaknesses in both approaches and motivates structured combinations of them.

System identification provides an important connection between the two paradigms. The governing equations of a system may be known while parameters such as mass, inertia, damping, motor constants, or friction remain uncertain. Observed data can then be used to estimate these parameters rather than learning the entire transition function. In this case, learning improves an analytical model while preserving its physical structure and interpretability.

A complementary strategy is residual dynamics learning. An analytical model first predicts the next state using known physics, and a learned model estimates the remaining discrepancy between that prediction and observed behavior. Conceptually, the transition can be represented as (f=f_{physics}+\\Delta f_{learned}). The physical component captures stable and reusable structure, while the learned residual captures effects such as unmodeled friction, actuator nonlinearities, deformation, and environmental disturbances.

Hybrid physics--learned models extend this principle further by allowing analytical and neural components to interact throughout the world-model architecture. Geometry and rigid-body motion may be represented explicitly while contact parameters are learned, or a neural perception system may infer physical state variables that are subsequently propagated by analytical dynamics. Alternatively, differentiable physics can allow prediction errors to propagate through a simulator so that unknown parameters or neural components are optimized jointly.

The appropriate balance depends strongly on the embodiment and task. Manipulation may benefit from explicit kinematic, collision, and contact constraints, while learned components capture uncertain friction and object properties. Autonomous mobile robots may use analytical vehicle dynamics together with learned terrain interaction and slip models. Quadrupeds and humanoids may combine rigid-body dynamics, contact constraints, learned locomotion representations, and adaptive estimates of external disturbances.

For world models, the choice is therefore not simply whether analytical dynamics or learned dynamics is superior. The central design question is which parts of the physical transition are sufficiently understood to encode explicitly and which parts should be learned from experience. Known physics can reduce the learning problem, constrain impossible predictions, and improve extrapolation, while data-driven components can represent complexity and uncertainty that simplified equations cannot capture.

A practical Physical AI world model can consequently be viewed as a continuum rather than a binary architecture. At one extreme lies a physics simulator driven almost entirely by analytical equations; at the other lies a neural model trained primarily from experience. Between them are system-identified models, physics-informed networks, differentiable simulators, constrained latent dynamics, residual models, and other hybrid architectures combining varying amounts of physical knowledge and learned behavior.

Ultimately, learned and analytical dynamics provide complementary forms of knowledge for Physical AI. Analytical dynamics contributes structure, invariance, interpretability, and physical feasibility, while learned dynamics contributes adaptability, representational capacity, and the ability to capture unknown real-world effects. Combining them allows a world model to preserve what is reliably known about physics while learning what cannot be modeled accurately in advance, providing a stronger foundation for prediction, planning, control, and real-world adaptation.

## 10.03. Physics Informed Neural Networks

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

Physics-Informed Neural Networks (PINNs) combine neural learning with explicit knowledge of physical laws so that predictions are guided not only by observed data but also by equations describing the underlying system. Instead of allowing a network to learn any mapping that minimizes data error, a PINN introduces physical relationships into the learning objective, encouraging solutions that remain consistent with known dynamics even where measurements are sparse.

The central idea is to represent an unknown physical quantity with a neural network while requiring its outputs to approximately satisfy governing equations. If a system is described by a differential equation such as (\\mathcal{F}(u,\\partial_tu,\\nabla u,\\theta)=0), the neural network approximates (u), while automatic differentiation computes the required temporal and spatial derivatives. Violations of the governing equation become part of the training loss.

A typical PINN objective therefore combines several sources of supervision. A data loss measures disagreement between predicted and observed values, while a physics loss measures the residual of the governing equations at selected points in the physical domain. Boundary conditions, initial conditions, conservation constraints, or known geometric relationships can also contribute additional losses, producing an optimization objective that balances empirical evidence with physical consistency.

This formulation is important because physical equations effectively provide supervision at locations where labeled measurements may not exist. A robot may collect only limited observations of velocity, force, temperature, deformation, or terrain interaction, yet the governing physics can constrain many additional states throughout space and time. Physics-informed learning can therefore reduce dependence on expensive real-world data while preventing the network from fitting observations in physically unreasonable ways.

Automatic differentiation (Automatic Differentiation) is a key mechanism enabling this approach. Because neural networks are differentiable functions, derivatives of their outputs with respect to time, position, state variables, or parameters can be calculated through the computational graph. These derivatives can be substituted directly into differential equations, allowing the optimizer to minimize physical residuals without requiring conventional finite-difference approximations at every training step.

PINNs can address both forward problems and inverse problems. In a forward problem, known physical equations and parameters are used to estimate the evolution of a system under specified initial and boundary conditions. In an inverse problem, observations are used to infer unknown quantities such as friction, material properties, damping, diffusion coefficients, external forces, or other system parameters while simultaneously enforcing the known physical relationships.

For Physical AI, the inverse formulation is particularly relevant to system identification (System Identification). A robot may know the approximate structure of its dynamics while important parameters change during operation. Payload mass, tire-ground friction, actuator characteristics, joint damping, or terrain properties may be uncertain. A physics-informed model can estimate such parameters from sensor observations without abandoning the physical structure already known about the robot.

Physics-informed learning also provides an intermediate approach between analytical dynamics and unrestricted learned dynamics. A purely analytical model relies heavily on equations and predetermined parameters, while a purely learned model estimates transitions from data. PINNs retain the representational flexibility of neural networks while embedding equations or constraints into learning, allowing the model to adapt to data without treating the physical world as an unconstrained statistical process.

The physical knowledge included in a PINN does not need to be perfectly complete. Some relationships may be accurately known while other dynamics remain uncertain or difficult to model. The network can therefore be constrained by reliable components such as conservation laws, kinematic relationships, geometric boundaries, or approximate differential equations while learning uncertain effects from data. This makes physics-informed modeling useful when only partial physical knowledge is available.

Conservation laws provide especially valuable constraints because they describe relationships that should remain valid across many operating conditions. Depending on the system, conservation of mass, momentum, energy, or related quantities can be incorporated into the loss function or model structure. Such constraints reduce the space of possible solutions and discourage predictions that fit observations locally while violating fundamental physical behavior globally.

In world modeling, physics-informed constraints can improve temporal prediction by discouraging implausible state transitions. A learned world model may otherwise predict discontinuous motion, impossible accelerations, penetration between objects, or unstable long-horizon trajectories. Incorporating known dynamics into the training objective can guide latent or explicit state evolution toward physically meaningful regions and reduce the accumulation of unrealistic behavior during repeated predictive rollouts.

However, PINNs are not automatically superior to either numerical physics solvers or conventional neural networks. Training can become difficult when different loss components have substantially different scales or optimization landscapes. A network may minimize measurement error while neglecting the physics residual, or satisfy one equation while poorly fitting observations. Selecting loss weights and sampling appropriate points in the physical domain therefore becomes an important part of model design.

Complex physical systems introduce additional challenges. Contact, collision, friction, discontinuities, hybrid dynamics, and rapidly changing boundary conditions can be difficult for smooth neural approximations. Robotic environments frequently contain exactly these phenomena. Consequently, directly applying a classical PINN formulation to manipulation, locomotion, or terrain interaction may require specialized representations, piecewise dynamics, contact-aware constraints, or combination with other physics-learning techniques.

Computational cost can also become significant because training requires derivatives of network outputs and repeated evaluation of physics residuals across many sampled points. Higher-order differential equations may require higher-order derivatives, increasing memory usage and optimization difficulty. For real-time Physical AI, PINNs may therefore be more useful for offline learning, parameter estimation, model adaptation, or constructing compact surrogate dynamics than for solving every physical interaction directly during control.

A broader interpretation of physics-informed neural modeling extends beyond classical PINNs. Physical knowledge can be introduced through loss functions, neural architecture, equivariance, constrained state representations, differentiable simulators, projection operators, or explicit analytical modules. The essential principle remains the same: learning should exploit known structure rather than forcing the network to rediscover every physical relationship solely from examples.

Physics-informed models can also interact naturally with latent world models. Perception modules may encode camera, LiDAR, proprioceptive, and other sensor observations into a latent state, while physics-based constraints regulate how that latent state evolves. The latent variables do not necessarily need to correspond directly to classical physical quantities, but their transitions can still be encouraged to preserve temporal continuity, geometry, conservation, action effects, or other physically meaningful relationships.

For planning and control, the value of physics-informed prediction lies in producing futures that are both data-adaptive and physically credible. Candidate actions can be rolled forward through the world model, while physical constraints help eliminate trajectories that violate known dynamics or operational limits. This can improve model predictive control (Model Predictive Control), counterfactual evaluation, trajectory optimization, and model-based reinforcement learning by making imagined futures more representative of executable behavior.

Physics-Informed Neural Networks therefore represent more than a technique for solving differential equations with neural networks. Within Physical AI world models, they illustrate a broader design philosophy in which physical knowledge becomes part of the learning process itself. By combining observations, differentiable learning, governing equations, constraints, and parameter estimation, physics-informed approaches provide an important bridge between analytical modeling and data-driven world modeling.

## 10.04. Hybrid Physics and Learned Models

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

​

​

​

​

​

​

​

​

​

​

​

​

​

​

​

​

​

​

Hybrid physics and learned models combine explicit physical knowledge with data-driven learning to predict how real systems evolve. Instead of choosing between analytical equations and neural networks, the model assigns different parts of the dynamics to the representation best suited to them. Reliable physical structure can remain explicit, while uncertain, complex, or unmodeled effects are estimated from data.

The basic motivation comes from the limitations of both extremes. Analytical dynamics provides interpretability, physical consistency, and strong extrapolation when the governing equations and parameters are accurate. Learned dynamics provides flexibility and can capture effects that are difficult to formulate mathematically. Real Physical AI systems usually contain both well-understood mechanisms and poorly modeled interactions, making hybridization a natural design strategy.

A hybrid transition model can be expressed conceptually as s

t+1

=f_physics

(s

t

,a

t

,θ)+f

learned

(s

t

,a

t

,z

t

). The physics component predicts behavior using known dynamics and physical parameters θ, while the learned component represents additional effects from observations or latent context z

t

. The precise combination may be additive, corrective, hierarchical, modular, or jointly optimized.

Residual dynamics learning is one of the simplest hybrid architectures. An analytical model first computes a nominal prediction, and a neural network learns the residual between this prediction and the observed next state. If the physical model already explains most of the system, the neural network only needs to learn the remaining error. This can significantly reduce the complexity and amount of data required for learning.

For a mobile robot, for example, analytical kinematics may accurately describe nominal wheel motion while real terrain produces slip, vibration, compliance, and changing traction. The physics model can predict ideal vehicle motion, while a learned residual estimates deviations caused by terrain and operating conditions. The resulting world model preserves known vehicle structure while adapting its predictions to the environment actually encountered.

Hybridization can also occur through parameter learning rather than direct residual correction. The structure of the governing equations may be known, but parameters such as mass, inertia, friction, damping, stiffness, motor constants, or aerodynamic coefficients may be uncertain. A neural estimator can infer these quantities from recent sensor observations and continuously update the analytical model, effectively performing adaptive system identification.

Another architecture uses neural networks to estimate quantities that are difficult to observe directly. Camera, LiDAR, tactile sensing, proprioception, or other modalities can be encoded into estimates of terrain properties, contact states, object parameters, or external disturbances. These inferred physical variables are then passed to an analytical dynamics module. Learning therefore handles perception and estimation, while physics determines how the estimated state evolves.

The opposite arrangement is also possible. An analytical simulator can generate an initial future trajectory, after which a learned model refines the prediction using patterns extracted from real-world experience. This approach is useful when simulation captures the dominant dynamics but exhibits a systematic sim-to-real gap. The learned component effectively transforms idealized simulated behavior into predictions that better reflect actual hardware and environmental interactions.

Differentiable physics provides a deeper form of integration. If the physics module is differentiable, prediction errors can propagate through physical calculations during training. Unknown parameters, perception networks, latent representations, and learned residual components can then be optimized together. The simulator is no longer merely an external source of synthetic data; it becomes an active computational component inside the learning architecture.

Hybrid models can also embed physical constraints directly into learned state transitions. Instead of adding a complete analytical simulator, a neural dynamics model may enforce kinematic limits, collision constraints, conservation relationships, geometric consistency, or stability conditions. Such constrained learned dynamics occupy an intermediate position between classical simulation and unrestricted neural prediction, preserving flexibility while restricting physically impossible transitions.

This approach is especially valuable for latent world models. High-dimensional observations can first be compressed into a latent state, after which learned dynamics predict future latent representations. Physical structure can regulate this latent evolution through action-conditioned transitions, temporal continuity, geometry, conservation constraints, or auxiliary predictions of velocity and contact. The latent space remains learned while its dynamics are encouraged to represent physically meaningful behavior.

The division between physics and learning should depend on confidence rather than convenience. Components governed by reliable equations and stable parameters are strong candidates for explicit modeling. Components involving uncertain friction, deformation, complex contact, environmental disturbances, or hardware-specific nonlinearities are stronger candidates for learning. This allocation prevents neural networks from unnecessarily relearning established physics while avoiding excessive dependence on inaccurate analytical assumptions.

Hybrid models can improve sample efficiency because the learning component starts from a structured physical baseline. A robot does not need to discover rigid-body motion, basic kinematics, or known actuator relationships entirely from experience. Training data can instead focus on the mismatch between nominal physics and reality. This is particularly important for Physical AI because collecting diverse interaction data can require expensive hardware operation and may involve safety risks.

Generalization can also improve when stable physical structure is preserved across environments. Visual appearance, terrain, payload, temperature, and hardware condition may change, but many geometric and mechanical relationships remain valid. The learned component can adapt to changing local conditions while the analytical component supplies invariant structure. This separation can make adaptation more efficient than retraining a completely data-driven dynamics model.

Long-horizon prediction provides another motivation for hybridization. Small errors in unrestricted learned transitions can accumulate during repeated rollouts until predicted trajectories become physically unrealistic. Explicit physics and constraints can anchor the rollout to feasible regions of state space. Learned corrections still compensate for model mismatch, but they operate around a physically meaningful trajectory rather than generating the entire future without structural guidance.

Hybrid models also support uncertainty-aware prediction. The analytical component may contain uncertain physical parameters, while the learned component may encounter observations outside its training distribution. A world model can represent uncertainty over both sources and propagate it through future rollouts. Planning algorithms can then distinguish between uncertainty caused by unknown system parameters and uncertainty caused by incomplete learned knowledge.

For planning and control, hybrid world models provide a useful balance between computational efficiency and physical credibility. Candidate actions can be simulated through an analytical core and corrected by learned dynamics before trajectories are evaluated. Model Predictive Control, trajectory optimization, and model-based reinforcement learning can use these predictions to compare alternative futures while retaining knowledge of actuator limits, geometry, contact, and environmental effects.

There are nevertheless important design challenges. An inaccurate physics model can introduce systematic bias, while an excessively powerful neural correction may learn to ignore the analytical component entirely. Poorly scaled residuals, unstable gradients, conflicting constraints, and errors in estimated physical parameters can also degrade performance. Successful hybrid architectures therefore require careful decisions about interfaces, representations, optimization objectives, and the relative authority of physics and learning.

Hybrid physics and learned models ultimately treat physical knowledge and experience as complementary rather than competing sources of intelligence. Physics provides reusable structure about how the world should behave, while learning captures how a particular real system actually behaves when ideal assumptions fail. For Physical AI world models, this combination offers a practical path toward predictions that are adaptable, data-efficient, physically plausible, and useful for long-horizon planning and control.

t+1

=f

physics

(s

t

,a

t

,θ)+f

learned

(s

t

,a

t

,z

t

t

## 10.05. Conservation Laws and Constraints

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

​

​

​

​

​

​

​

​

Conservation laws provide world models with structural rules that remain valid across many physical situations. Instead of learning every possible state transition independently from data, a model can exploit quantities that must be preserved or transformed according to known relationships. Conservation of mass, momentum, angular momentum, and energy therefore acts as a powerful physical prior that restricts predictions to more plausible regions of the state space.

In classical mechanics, linear momentum is conserved when the net external force on a system is zero. When two objects collide, their individual velocities may change dramatically, but the total momentum of the isolated system must remain consistent before and after the interaction. A world model that respects this relationship can reject predicted collision outcomes that appear visually plausible yet imply physically impossible changes in motion.

Angular momentum introduces similar structure for rotational motion. Robots frequently interact with rotating wheels, articulated links, tools, doors, objects, and their own dynamically moving bodies. Changes in angular velocity depend on torque, inertia, and external interactions rather than arbitrary temporal correlations. Encoding these relationships helps a world model represent rotational dynamics and reason about how actions influence orientation, balance, and physical interaction.

Energy provides another important constraint, although practical robotic systems are rarely perfectly conservative. Mechanical energy may be transformed into heat through friction, supplied by motors, absorbed by damping, or transferred during collisions. The useful prior is therefore not simply that energy always remains numerically constant, but that changes in energy should correspond to physically meaningful sources, sinks, transformations, and exchanges within the modeled system.

Mass conservation is particularly relevant when world models represent fluids, granular materials, deformable substances, or processes involving transport between regions. Material should not spontaneously appear or disappear unless the modeled process explicitly includes a source or sink. Even when a robot primarily interacts with rigid objects, conservation principles can provide useful structural constraints for environmental models involving liquids, gases, soil, powders, or other distributed materials.

Conservation laws can be incorporated into learned world models in several ways. A straightforward approach adds constraint terms to the training objective, penalizing predictions that violate known conservation relationships. If L

data

measures prediction error and L

cons

measures conservation error, training can minimize an objective such as L=L

data

+λL

cons

. The coefficient λ controls the relative influence of empirical observations and physical consistency.

Hard constraints provide a stronger alternative to such soft penalties. Instead of merely discouraging violations through a loss function, the model architecture can be designed so that certain outputs automatically satisfy required relationships. State variables may be parameterized in conservation-preserving forms, predictions may be projected onto feasible manifolds, or specialized numerical structures may preserve invariants during state transitions. This reduces the model\'s ability to generate impossible states.

Not every useful physical constraint is a conservation law. Physical AI systems are also governed by geometric, kinematic, dynamic, actuator, contact, and safety constraints. A robot joint cannot normally rotate beyond its mechanical limits, an actuator cannot produce unlimited torque, two rigid bodies should not occupy the same volume, and a wheeled platform cannot instantaneously move in directions prohibited by its kinematics. These restrictions define feasible state transitions.

Geometric constraints are particularly important because physical interaction occurs in structured three-dimensional space. Object dimensions, collision boundaries, articulated link geometry, reachability, free space, and relative transformations constrain what can happen next. A learned model that predicts an object passing through a wall or a manipulator reaching beyond its workspace may minimize statistical prediction error in some cases while still producing a physically unusable future.

Kinematic constraints describe relationships among positions, velocities, and allowable motion independent of the forces producing them. Differential-drive robots, Ackermann-steered vehicles, manipulators, quadrupeds, and aerial robots each possess different motion constraints. Incorporating embodiment-specific kinematics into a world model prevents the predicted agent from behaving like a generic movable point and connects future prediction directly to the capabilities of the actual physical platform.

Dynamic constraints extend this reasoning to forces, torques, accelerations, inertia, stability, and actuator capabilities. A trajectory may be geometrically collision-free but still impossible because it requires excessive acceleration or torque. For planning-oriented world models, feasibility must therefore include not only where the robot can move but also whether its physical system can execute that motion within available force, power, traction, and stability limits.

Contact constraints become essential when robots manipulate objects or traverse complex terrain. Contact may impose non-penetration, normal-force, friction, sticking, sliding, and complementarity relationships. These conditions can create discontinuous transitions when contact begins or ends. Incorporating contact structure helps distinguish physically valid interactions from trajectories that are geometrically attractive but impossible under realistic friction and force conditions.

Constraints can also operate in latent world models even when the internal representation does not explicitly correspond to conventional physical variables. Auxiliary prediction heads can estimate velocity, depth, occupancy, contact, or energy-related quantities from the latent state, allowing physical consistency losses to regulate representation learning. Alternatively, latent transitions can be constrained so decoded predictions satisfy geometry, dynamics, or conservation relationships.

Long-horizon prediction particularly benefits from conservation-aware and constraint-aware modeling. Small violations that appear insignificant over one prediction step can accumulate during repeated rollouts. An object may gradually gain energy without an external source, robot velocity may exceed feasible limits, or geometry may slowly become inconsistent. Repeated enforcement of physical structure helps prevent such errors from expanding into unrealistic imagined futures.

These principles are also valuable for counterfactual prediction. When a world model evaluates multiple possible actions, each imagined future should remain physically feasible. Conservation laws and constraints reduce the space of candidate futures by eliminating trajectories that violate known invariants, actuator limits, collision conditions, or embodiment capabilities. Planning can therefore allocate computation to alternatives that could actually be executed rather than evaluating arbitrary predictions.

Physical constraints additionally provide useful signals for model validation and runtime monitoring. A prediction that violates a joint limit, creates unexplained momentum, penetrates an obstacle, or demands impossible acceleration can be flagged even when no ground-truth future observation is yet available. Conservation residuals and constraint violations can therefore function as diagnostic indicators for detecting model drift, unusual conditions, or potentially unsafe predictions.

However, constraints must reflect the correct system boundary and assumptions. Momentum is not conserved for a subsystem experiencing external forces, and mechanical energy is not constant when motors, friction, damping, or impacts exchange energy with the environment. Incorrectly imposing an ideal conservation rule can therefore degrade prediction accuracy. Physical constraints should represent the actual open or closed system being modeled rather than an oversimplified textbook abstraction.

For this reason, modern physics-informed world models can combine exact constraints, approximate constraints, learned parameters, and uncertainty. Some relationships may be enforced strictly, while others are represented as probabilistic or weighted penalties because parameters such as friction, mass, external force, or energy dissipation are uncertain. The model can preserve reliable physical structure without pretending that every property of the real environment is perfectly known.

Conservation laws and constraints ultimately reduce the enormous space of statistically conceivable futures to a smaller space of physically credible futures. For Physical AI, this distinction is fundamental because predicted states eventually guide real actions. By embedding invariants, geometry, kinematics, dynamics, contact conditions, actuator limits, and uncertainty into world modeling, the system gains a stronger foundation for stable prediction, feasible planning, safe control, and reliable long-horizon interaction.

data

cons

data

+λL

cons

## 10.06. Contact Friction and Rigid Body Priors

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

![](images/image7.png){width="7.268055555555556in" height="7.268055555555556in"}

Contact, friction, and rigid-body priors provide world models with structural knowledge about how physical objects interact when they touch, push, slide, roll, collide, or support one another. These interactions are fundamental to Physical AI because robots continuously exchange forces with objects and surfaces. Without such priors, a model may predict visually plausible motion while violating basic properties of contact mechanics and rigid-body behavior.

A rigid-body prior assumes that an object\'s shape and internal distances remain approximately unchanged during motion. Instead of independently predicting every point on an object, the world model can represent the object through position, orientation, linear velocity, angular velocity, mass, and inertia. This dramatically reduces the number of physically meaningful degrees of freedom and provides a compact structure for predicting object and robot motion.

Rigid-body motion naturally separates translation from rotation while connecting them through applied forces and torques. The center of mass responds to net force, whereas angular motion depends on torque and the inertia distribution. By incorporating these relationships, a world model can predict how pushing an object at different locations produces different combinations of translation and rotation rather than treating object displacement as an arbitrary visual transformation.

Contact introduces constraints that become active when physical bodies meet. A basic non-penetration condition requires rigid objects not to occupy the same physical volume. When predicted geometries approach one another, the model must determine whether contact occurs and how the resulting forces modify future motion. Contact therefore changes world modeling from independent trajectory prediction into interaction-aware prediction involving coupled physical states.

The normal contact force acts approximately perpendicular to the contact surface and prevents objects from penetrating each other. In many formulations, the normal force becomes active only when bodies are in contact and disappears when they separate. This creates a conditional and potentially discontinuous transition structure that is more difficult to learn than smooth free-space motion but essential for realistic manipulation, locomotion, and navigation.

Friction determines how tangential motion behaves at a contact interface. A commonly used approximation is Coulomb friction, in which the maximum tangential friction force is related to the normal force through a friction coefficient. The relationship distinguishes sticking from sliding and constrains how much tangential force can be transmitted before relative motion begins. Even simplified friction priors can substantially improve predictions of physical interaction.

Friction is particularly difficult because its effective value depends on materials, surface condition, load, velocity, temperature, contamination, deformation, and other factors. A wheel moving on dry concrete may behave very differently on wet flooring, gravel, mud, or grass. Consequently, world models often benefit from combining a known friction structure with learned or estimated parameters rather than assuming one fixed coefficient for every situation.

For wheeled mobile robots, contact and friction priors connect commanded motion to actual vehicle movement. Wheel speed alone does not guarantee corresponding ground velocity because longitudinal or lateral slip may occur. Terrain-dependent traction determines acceleration, stopping distance, turning behavior, and controllability. A physics-aware world model can represent nominal wheel-ground constraints while learning residual slip and traction effects from sensor observations.

Legged robots require even richer contact reasoning. Each foot can alternate between stance, sliding, and free-flight states, creating rapidly changing contact configurations. Ground reaction forces influence body acceleration and balance, while friction determines whether a planned foothold can support the required forces. Contact-aware priors therefore help world models predict stability, locomotion transitions, disturbances, and the consequences of alternative foothold or gait decisions.

Manipulation also depends fundamentally on contact. Grasping, pushing, pulling, insertion, opening, stacking, and tool use require reasoning about where contact occurs and how forces propagate through objects. A small change in contact location or friction can produce a large change in outcome. Representing contact state explicitly or implicitly allows a world model to distinguish free motion from constrained motion and predict action-dependent object behavior.

Collision adds another important regime. During impact, velocities may change over a very short interval as momentum is exchanged between bodies. Simplified models can use impulses and coefficients of restitution, while learned models can estimate complex impact behavior from data. The important prior is that post-impact motion should arise from the geometry, relative velocity, mass properties, and interaction forces rather than from unconstrained temporal correlation.

Contact mechanics can be introduced into world models through soft constraints. Training losses may penalize interpenetration, inconsistent contact forces, impossible friction behavior, or violations of rigid-body geometry. This allows neural networks to retain flexibility while being discouraged from producing physically implausible states. Such losses are especially useful when observations are noisy and exact physical parameters are unavailable.

Hard constraints offer a stronger alternative when reliable structure is known. Predicted poses can be projected onto collision-free configurations, rigid transformations can preserve object geometry, and optimization procedures can explicitly enforce kinematic or contact feasibility. Physics engines or differentiable contact solvers can also be integrated into learned models, ensuring that selected parts of the state transition follow established mechanics by construction.

Contact can also be treated as a latent or discrete mode within a hybrid dynamics model. The system may switch among free motion, contact, sticking, sliding, rolling, and impact regimes, with different transition dynamics associated with each mode. A learned network can estimate the active contact mode from multimodal observations, while specialized physical or learned transition functions predict what happens under that mode.

Multimodal sensing is valuable because contact is not always visually observable. Cameras and LiDAR provide geometry, while force-torque sensors, tactile sensors, joint currents, IMUs, microphones, and proprioception can reveal interaction forces, vibration, slip, or impact. A multimodal world model can fuse these signals to estimate hidden contact states and physical properties that are difficult to infer reliably from vision alone.

Rigid-body and contact priors also improve long-horizon prediction. Small penetration errors, incorrect impulses, or unrealistic friction responses can rapidly accumulate across repeated rollouts. Objects may drift through surfaces, robots may gain impossible traction, or stacked objects may remain stable when they should fall. Enforcing geometric and mechanical consistency helps keep imagined futures within physically credible regions of state space.

These priors are equally important for counterfactual planning. A robot evaluating alternative actions must predict whether a push will move or rotate an object, whether a wheel will slip, whether a grasp will hold, or whether a foothold can support the body. Contact and friction structure constrains these imagined outcomes, allowing planners to compare actions according to executable physical consequences rather than appearance alone.

Exact contact modeling remains difficult, so practical world models should not treat every prior as perfectly known. Geometry and rigid-body structure may be relatively reliable, while friction, compliance, restitution, and terrain properties remain uncertain. Hybrid models can preserve the reliable constraints and learn uncertain interaction parameters or residual dynamics from experience, combining physical structure with adaptation to real-world variability.

Ultimately, contact, friction, and rigid-body priors provide the world model with knowledge of how matter constrains motion during interaction. Rigid-body structure defines how objects can move, contact determines when bodies influence one another, and friction determines how forces can be transmitted along their interfaces. Together, these priors transform prediction from visual motion forecasting into physically grounded interaction modeling for manipulation, locomotion, navigation, planning, and control.

## 10.07. Differentiable Physics

![](images/image8.png){width="7.268055555555556in" height="7.268055555555556in"}

Differentiable physics connects physical simulation with gradient-based learning by making the operations of a physical model differentiable with respect to states, actions, parameters, and sometimes geometry. Instead of treating a simulator as a black box that only produces outcomes, differentiable physics allows information about prediction error to propagate backward through simulated dynamics, creating a direct bridge between analytical modeling and neural optimization.

A conventional simulator computes a forward transition from the current state and action to a future state according to physical equations. A differentiable simulator additionally provides derivatives such as (\\partial s_{t+1}/\\partial s_t), (\\partial s_{t+1}/\\partial a_t), and (\\partial s_{t+1}/\\partial\\theta). These gradients describe how predicted outcomes change when initial conditions, controls, or physical parameters are modified.

This capability is particularly important for Physical AI because many useful quantities are difficult to measure directly but strongly influence robot behavior. Mass, inertia, friction, stiffness, damping, actuator characteristics, and contact properties may initially be uncertain. By comparing simulated trajectories with observations and backpropagating the discrepancy through the simulator, these parameters can be estimated systematically from real interaction data.

Differentiable physics therefore provides a powerful mechanism for system identification. Suppose a robot observes that its actual trajectory differs from the trajectory predicted by its nominal dynamics model. Instead of training an unrestricted neural network to replace the physics, optimization can adjust uncertain physical parameters so that simulated behavior better matches reality. The resulting model retains interpretable physical structure while adapting to the specific system.

The same principle can connect perception directly with dynamics. A neural network may infer object mass, terrain friction, contact state, material properties, or external forces from camera, LiDAR, tactile, or proprioceptive observations. These estimated quantities are passed into a differentiable physics module, which predicts future motion. Prediction losses can then propagate through the physical model back into the perception network, allowing perception to learn variables that are useful for physical prediction.

This creates an important form of end-to-end learning. The system does not need separate supervision for every intermediate physical variable if the final physical outcome provides a useful training signal. For example, a network estimating terrain properties may be trained partly from whether the resulting dynamics correctly predict wheel slip or vehicle motion. Physical simulation becomes part of the computational graph rather than merely an external preprocessing or data-generation tool.

Differentiable physics can also support action optimization. Because future states are differentiable with respect to actions, gradients can indicate how control inputs should change to improve an objective. A robot can optimize steering, torque, force, grasp parameters, or trajectory variables by propagating task losses backward through predicted dynamics. This provides a direct connection between world modeling, trajectory optimization, and model-based control.

For model predictive control, differentiable dynamics can make candidate trajectory refinement more efficient. Instead of evaluating only large numbers of independently sampled action sequences, gradient information can guide candidate actions toward lower-cost solutions. The world model can predict the consequences of an action sequence, compute a task or safety objective, and differentiate that objective with respect to the controls used throughout the prediction horizon.

Differentiable simulation is also valuable for manipulation. Object pose, contact location, applied force, friction, and geometry jointly determine the result of pushing, grasping, insertion, or tool use. If these relationships are differentiable, prediction error or task objectives can update both learned components and action parameters. This enables optimization through physical interaction rather than treating each simulated interaction as an isolated trial.

Contact, however, creates one of the central difficulties for differentiable physics. Collision and contact often introduce discontinuities because forces can appear or disappear abruptly when bodies touch or separate. Sticking can transition to sliding, impacts can instantaneously alter velocity, and contact topology can change. These events may produce undefined, unstable, or uninformative gradients under straightforward differentiation.

Several approaches address this problem by smoothing contact dynamics, using differentiable approximations, applying implicit differentiation, or designing specialized contact solvers. Smoother formulations can provide useful gradients but may reduce physical fidelity near sharp transitions. Consequently, differentiable physics often involves a tradeoff between exact simulation of discontinuous phenomena and gradients that are stable enough for optimization and learning.

Long simulation horizons introduce another challenge. Gradients propagated through many state transitions may vanish, explode, or become highly sensitive to small changes in initial conditions. This resembles difficulties encountered when training recurrent neural networks. Stable numerical integration, carefully designed state representations, regularization, truncated optimization horizons, and hierarchical prediction can help make differentiable physical rollouts more practical.

Computational cost must also be considered. Differentiating through collision detection, constraint solving, numerical integration, and long trajectories can require substantial memory and computation. Storing every intermediate state for reverse-mode differentiation may become expensive. Techniques such as checkpointing, adjoint methods, implicit gradients, reduced-order models, and learned surrogate dynamics can reduce these costs depending on the physical system and application.

Differentiable physics is especially powerful when combined with learned residual dynamics. An analytical simulator can represent known rigid-body, kinematic, or actuator relationships, while a neural component learns effects that the simulator cannot accurately reproduce. Because both components participate in a differentiable computation, optimization can jointly improve physical parameters and learned corrections while preserving useful analytical structure.

This combination can also help address the simulation-to-reality gap. A simulator may represent the dominant physics correctly but use imperfect parameters or simplified interaction models. Real-world observations can provide losses that propagate through the differentiable simulator, adjusting physical parameters or learned correction modules. The world model can therefore become progressively calibrated to actual hardware and environmental conditions without discarding its physical foundation.

Within latent world models, differentiable physics can operate at several levels. A perception encoder may map high-dimensional observations into explicit physical variables before simulation, or a physics-inspired transition module may operate directly within a structured latent space. The decoder then maps predicted states back into task-relevant observations or representations, allowing errors in future prediction to train the entire perception-dynamics pipeline.

Differentiable physics also enables counterfactual reasoning through optimization. A Physical AI system can ask how a predicted outcome would change if it altered an action, contact location, trajectory, or estimated environmental parameter. Gradients provide local sensitivity information about these alternatives. This allows the world model not only to imagine possible futures but also to determine which controllable changes are likely to move those futures toward desired outcomes.

The approach nevertheless depends strongly on model quality. Differentiability does not guarantee that the underlying physics is correct. A highly differentiable but inaccurate simulator can produce precise gradients toward the wrong solution. Practical systems therefore need validation against real measurements, uncertainty estimation, parameter adaptation, and learned corrections when analytical assumptions fail to capture important aspects of the environment.

Differentiable physics ultimately transforms physical simulation from a passive prediction engine into an active component of learning and optimization. By allowing gradients to flow through dynamics, it connects perception, system identification, physical parameters, world-model prediction, planning, and control within a common computational framework. For Physical AI, this offers a powerful foundation for models that learn from experience while remaining anchored to reusable physical structure.

## 10.08. System Identification and Parameter Learning

![](images/image9.png){width="7.268055555555556in" height="7.268055555555556in"}

System identification is the process of constructing or refining a mathematical model of a physical system from observed input-output behavior. In Physical AI, it connects real robot experience with world-model dynamics by estimating how actions produce changes in motion and interaction. Rather than assuming that every property of the robot and environment is perfectly known, system identification uses measurements to determine the parameters or dynamics that best explain observed behavior.

A physical system can be represented conceptually by a transition model such as (s_{t+1}=f(s_t,a_t,\\theta)), where (s_t) is the current state, (a_t) is the applied action, and (\\theta) represents physical parameters. These parameters may include mass, inertia, friction, damping, stiffness, motor constants, wheel radius, actuator delay, or aerodynamic coefficients. Identification seeks values of (\\theta) that make predicted transitions consistent with measured trajectories.

This approach is important because nominal engineering parameters rarely describe a real robot perfectly throughout its lifetime. Manufacturing tolerances, payload changes, tire wear, battery condition, temperature, mechanical aging, and surface properties can alter actual dynamics. Even two robots built from the same design may behave slightly differently. System identification allows the world model to adapt from nominal specifications toward the dynamics of the particular physical platform being operated.

Classical system identification typically begins by selecting a model structure and estimating its unknown parameters from measured inputs and outputs. Linear models, state-space models, transfer functions, autoregressive models, and nonlinear parametric models can all be used depending on the system. The essential idea is to expose the system to informative inputs, observe its responses, and find model parameters that reproduce those responses with sufficiently small error.

For robotics, the state is often only partially observable. Sensors may measure wheel encoders, joint positions, IMU signals, motor currents, force, torque, velocity, or external pose, while important variables remain hidden. State estimation and system identification therefore frequently operate together. Filters, observers, optimization, or learned estimators can reconstruct hidden states while simultaneously determining the physical parameters needed to explain their evolution.

Parameter identifiability is a fundamental consideration. A parameter can only be estimated reliably when the available observations contain enough information to distinguish its effect from those of other parameters. If a robot always moves at constant speed on a flat surface, the data may provide little information about acceleration dynamics or traction limits. Identification experiments therefore require sufficiently rich excitation of the system across relevant operating conditions.

Persistent excitation is especially important when multiple parameters influence behavior in similar ways. Carefully designed steering commands, accelerations, braking events, joint trajectories, or contact interactions can expose different aspects of the dynamics. For Physical AI, however, exploration must remain within safe operational limits. Identification therefore becomes an experimental-design problem that balances information gain with hardware protection, stability, energy consumption, and task requirements.

Online system identification extends parameter estimation into continuous operation. Instead of identifying the robot once before deployment, the system repeatedly updates its model as new observations arrive. This is useful when payload, terrain, friction, actuator response, or environmental conditions change over time. The world model can therefore maintain a dynamic estimate of the physical system rather than relying indefinitely on parameters measured under earlier conditions.

A mobile robot provides a clear example. Nominal kinematics may predict motion from wheel velocities, but actual displacement depends on wheel radius, track width, tire deformation, longitudinal slip, lateral slip, terrain friction, and payload. Sensor observations from encoders, IMUs, cameras, LiDAR, or GNSS can be compared with predicted motion to estimate these quantities or their effective influence, improving future trajectory prediction and control.

For manipulators, parameter learning can estimate link masses, inertial properties, joint friction, motor characteristics, compliance, payload properties, or contact parameters. Accurate estimates improve torque prediction and trajectory control while also helping the world model anticipate how the robot will respond when carrying unfamiliar objects. Online payload estimation is particularly valuable because the effective dynamics can change immediately after an object is grasped.

System identification does not always require every physical parameter to be estimated explicitly. In some applications, a compact set of effective parameters is sufficient to reproduce behavior relevant to planning and control. For example, a terrain representation may encode effective traction and compliance rather than detailed material properties. This task-oriented identification can reduce model complexity while retaining the information required for accurate action-conditioned prediction.

Neural networks expand system identification beyond fixed parametric models. A learned estimator can infer physical parameters from recent observation histories, allowing complex relationships between sensor signals and hidden properties to be captured. Recurrent networks, Transformers, or latent encoders can summarize past interaction into a context representation that conditions future dynamics. The resulting model can adapt its predictions according to inferred operating conditions.

An alternative is to learn the dynamics directly rather than explicitly identifying interpretable parameters. The model estimates (s_{t+1}) from states and actions without requiring quantities such as friction or damping to appear as named variables. This can capture complicated effects but sacrifices some interpretability. Hybrid approaches often provide a useful compromise by identifying meaningful physical parameters while learning residual dynamics that remain unexplained by the analytical model.

Differentiable physics creates a particularly direct mechanism for parameter learning. If a simulator is differentiable with respect to (\\theta), the difference between predicted and observed trajectories can be backpropagated through the physical dynamics. Gradient-based optimization can then adjust mass, friction, stiffness, damping, or other parameters. This integrates system identification naturally with neural learning and allows physical and learned components to be optimized within the same computational framework.

Uncertainty is essential because identified parameters are estimates rather than absolute truths. Limited observations, sensor noise, unmodeled dynamics, and changing environments may produce several parameter values that explain the available data similarly well. Probabilistic identification can represent distributions over parameters rather than single values. A world model can propagate this uncertainty through future predictions and allow planning algorithms to prefer actions that remain safe across plausible dynamics.

Parameter learning also contributes directly to sim-to-real adaptation. Simulation may begin with approximate robot and environment parameters, while real-world trajectories reveal systematic discrepancies. Updating simulator parameters from real measurements can reduce this gap without replacing the entire physics model. Residual neural components can then capture effects that parameter adjustment alone cannot explain, creating an increasingly calibrated hybrid world model.

Long-horizon world modeling benefits substantially from accurate identification because small parameter errors accumulate over repeated predictions. Slight errors in friction, inertia, steering response, or actuator delay may appear insignificant over one timestep but produce large trajectory deviations after several seconds. Continuously calibrated parameters can reduce this systematic drift and provide more reliable rollouts for planning, model predictive control, and counterfactual evaluation.

System identification can itself become an active capability of an intelligent agent. Instead of passively waiting for informative observations, a robot can select safe actions that reduce uncertainty about unknown dynamics. Such active system identification links exploration with control: the robot performs actions not only to accomplish the immediate task but also to improve its internal model when better physical knowledge is expected to increase future performance.

Within a world-model architecture, system identification can therefore be viewed as a feedback loop between observation and prediction. Sensors provide evidence about the real system, the dynamics model predicts future states, prediction errors reveal model mismatch, and parameter learning updates the model. The updated model then generates better predictions, producing a continual cycle of observation, estimation, prediction, comparison, and adaptation.

Ultimately, system identification and parameter learning allow Physical AI world models to remain connected to the physical systems they represent. Analytical knowledge provides an initial structure, while real experience determines how that structure should be calibrated for a particular robot, payload, terrain, and environment. By combining estimation, uncertainty, online adaptation, differentiable physics, and learned residuals, world models can evolve from static approximations into continuously calibrated models of real-world dynamics.

## 10.09. Physics Guided Generalization

![](images/image10.png){width="7.268055555555556in" height="7.268055555555556in"}

Physics-guided generalization enables a learned world model to remain useful when a robot encounters conditions that differ from its training distribution. Instead of relying only on statistical similarities between past and current observations, the model uses physical structure that remains valid across environments. Geometry, dynamics, conservation relationships, contact mechanics, and embodiment constraints can therefore provide stable foundations for prediction under unfamiliar conditions.

Purely data-driven models often generalize well when new observations resemble examples represented in the training dataset. Their predictions can deteriorate when terrain, payload, object properties, lighting, friction, speed, or operating conditions change substantially. Physical AI must operate under precisely these variations, making generalization beyond the observed data distribution a central requirement rather than an exceptional capability.

Physical laws provide a different form of knowledge because many relationships remain applicable even when visual appearance changes. A vehicle still obeys constraints on acceleration and steering when road texture changes, while an object continues to possess mass and inertia under different illumination. By separating persistent physical structure from variable sensory appearance, world models can learn representations that transfer more effectively across domains.

This distinction is particularly important for out-of-distribution generalization. A neural model may encounter combinations of states and conditions that were rare or absent during training. Physics does not eliminate this uncertainty, but it reduces the range of plausible predictions. Conservation laws, feasible motion constraints, and known dynamics can prevent the model from producing futures that contradict basic physical behavior even when statistical evidence is weak.

One strategy is to encode invariant physical quantities or relationships into the model representation. Instead of relying entirely on raw pixels, the world model can reason through position, velocity, orientation, geometry, occupancy, force, contact, or other structured variables. These representations often change more predictably across environments than appearance-level features, helping the model preserve useful knowledge when sensors observe unfamiliar scenes.

Equivariance provides another mechanism for physics-guided generalization. Physical relationships frequently transform systematically under translation, rotation, or changes of reference frame. Architectures that respect these transformations can avoid relearning equivalent situations separately. A model that understands how geometric relationships transform with coordinate systems can generalize more efficiently across object poses, robot orientations, and spatial configurations.

Hybrid physics and learned models naturally support generalization by assigning stable relationships to analytical components and variable effects to learned components. Known kinematics or rigid-body dynamics can remain unchanged across deployments, while neural modules adapt friction, terrain interaction, actuator response, or other uncertain phenomena. This decomposition prevents environmental variation from forcing the entire dynamics model to be relearned.

Parameter adaptation further extends this capability. The mathematical structure of the dynamics may remain valid while parameters such as payload mass, friction, damping, stiffness, or motor efficiency change. System identification can estimate these quantities from recent observations and condition future predictions on the updated values. Generalization then becomes adaptation within a structured family of physical models rather than unrestricted extrapolation.

For mobile robots, terrain change illustrates this principle clearly. A platform trained mainly on indoor flooring may later encounter asphalt, gravel, grass, mud, or slopes. Its geometry and actuator configuration remain largely unchanged, while traction and slip characteristics vary. A physics-guided world model can preserve nominal vehicle dynamics while estimating terrain-dependent parameters or learned residuals that modify predicted motion.

Manipulation presents a similar challenge. A robot may encounter objects with unfamiliar shapes, masses, friction coefficients, or material properties. Memorizing object-specific interaction outcomes cannot scale to every possible object. Rigid-body structure, contact constraints, and learned estimates of physical properties allow the world model to reason about new objects through their relevant physical characteristics rather than requiring an exact training example.

Compositional generalization is another important benefit. A robot may have separately experienced heavy objects, slippery surfaces, and inclined terrain but never their exact combination. A model organized around meaningful physical factors can potentially combine knowledge about mass, friction, gravity, and geometry to predict the new situation. This is more systematic than treating every combination of environmental conditions as an unrelated pattern.

Physics-guided generalization also supports transfer between simulation and reality. Simulators can expose models to broad ranges of geometry, dynamics, and physical parameters, while physical structure helps preserve relationships that should remain valid outside simulation. Domain randomization can vary uncertain properties, and real-world observations can subsequently calibrate parameters or residual models to reduce the remaining simulation-to-reality gap.

Generalization across robotic platforms is more difficult because embodiment itself changes. Different robots possess different dimensions, masses, actuators, sensors, and kinematic structures. However, shared physical principles still provide reusable knowledge. A world model can separate general interaction concepts such as force, contact, momentum, and geometry from embodiment-specific parameters, enabling part of the learned representation to transfer while platform-specific components are adapted.

Uncertainty estimation becomes essential when physics-guided models operate beyond familiar conditions. Physical structure may constrain what is possible without determining exactly what will happen. Unknown friction, hidden contact, uncertain material properties, or unmodeled disturbances can still produce multiple plausible futures. A robust world model should therefore represent uncertainty and avoid interpreting physical constraints as complete knowledge of an unfamiliar environment.

The model can also use prediction error as evidence that adaptation is required. When observed transitions repeatedly differ from physically guided predictions, the discrepancy may indicate changed parameters, previously unseen dynamics, sensor degradation, or an incorrect model assumption. Online system identification and residual learning can then update the model, converting unexpected experience into improved knowledge rather than allowing prediction errors to accumulate.

Long-horizon prediction particularly benefits from physical guidance because extrapolation errors compound over repeated transitions. A purely learned model may gradually violate geometry, energy behavior, actuator limits, or stability constraints when rolled forward beyond familiar trajectories. Physical priors can anchor predictions to feasible regions of state space, while learned components account for variations that cannot be represented accurately by fixed equations.

For planning, physics-guided generalization means that imagined futures remain useful even when the robot operates in situations not explicitly represented in training data. Candidate actions can be evaluated against physical feasibility, contact conditions, dynamic limits, and uncertainty. The planner can therefore reject impossible trajectories and prefer actions that remain robust across plausible variations in environmental and system parameters.

Physics guidance should nevertheless remain adaptable rather than rigid. Simplified equations may fail under deformation, complex contact, extreme terrain, hardware damage, or previously unknown interaction regimes. If incorrect physical assumptions are enforced too strongly, they can prevent the model from learning valid behavior. Effective generalization therefore requires a balance between reliable physical structure and data-driven correction when reality departs from the assumed model.

A practical architecture can combine invariant representations, analytical dynamics, learned residuals, parameter estimation, uncertainty modeling, and online adaptation. Stable physical knowledge provides the reusable core, while learned components capture environment-specific details. New observations continuously test the model, and discrepancies trigger parameter updates or residual learning, allowing generalization and adaptation to operate as complementary processes.

Physics-guided generalization ultimately shifts the goal from memorizing the training distribution to learning reusable principles of interaction. A Physical AI world model should recognize that appearances and operating conditions change while many underlying physical relationships persist. By exploiting these relationships while retaining the ability to learn uncertain effects, the model can produce more reliable predictions across new environments, objects, payloads, terrains, embodiments, and tasks.

## 10.10. Hybrid Physics Learned World Model [w/Code]

![](images/image11.png){width="7.268055555555556in" height="7.268055555555556in"}

![](images/image12.png){width="7.268055555555556in" height="7.268055555555556in"}

A hybrid physics-learned world model combines explicit physical structure with data-driven prediction inside a unified representation of how an environment evolves. Rather than asking a neural network to rediscover every mechanical relationship from observations, the architecture preserves reliable knowledge about geometry, motion, forces, and constraints while learning the uncertain effects that analytical models cannot describe accurately.

The central principle is to divide prediction according to what is known and what must be learned. Established kinematics, rigid-body relationships, actuator limits, conservation constraints, and geometric feasibility can form a physical core. Neural components can model friction variation, deformation, complex contact, terrain interaction, disturbances, actuator nonlinearities, and other phenomena whose equations or parameters are incomplete.

A simplified transition can be represented as (s_{t+1}=f_{phys}(s_t,a_t,\\theta_t)+\\Delta f_{learned}(s_t,a_t,z_t)). The physical model generates a nominal next state using estimated parameters (\\theta_t), while the learned residual predicts corrections conditioned on observations and latent context (z_t). The resulting transition retains physical structure without assuming that analytical dynamics perfectly represent reality.

The architecture begins with multimodal perception. Cameras, LiDAR, radar, tactile sensing, IMUs, joint measurements, motor currents, force-torque sensors, and other signals provide partial evidence about the current world. Encoders transform these observations into explicit physical states, structured latent states, or combinations of both, creating a representation suitable for prediction, parameter estimation, planning, and control.

Structured state representations are particularly useful because they separate persistent physical quantities from appearance-dependent information. Position, orientation, velocity, occupancy, geometry, contact state, object relationships, and embodiment variables can coexist with learned latent features representing properties that are difficult to define explicitly. This allows the world model to preserve interpretable structure while retaining neural representational flexibility.

The physics branch predicts the portion of future evolution that can be described reliably. Depending on the robot, it may include rigid-body dynamics, vehicle kinematics, manipulator equations, gravity, collision geometry, actuator constraints, or simplified contact mechanics. Physical priors restrict the possible transitions and prevent the model from spending learning capacity on relationships already established by mechanics.

The learned branch complements this physical prediction rather than necessarily replacing it. Residual networks can estimate wheel slip, uncertain contact forces, aerodynamic disturbances, compliance, terrain effects, or systematic simulator error. Because these components learn the difference between nominal physics and observed reality, their learning problem can be substantially smaller than learning complete system dynamics directly from raw experience.

Parameter learning provides another adaptive layer. Mass, inertia, friction, damping, stiffness, payload, motor gains, delay, or terrain-dependent coefficients may change between tasks or during operation. A parameter estimator can infer these quantities from recent observations and update the physical model online. The analytical structure therefore remains stable while its operating parameters adapt to the current robot and environment.

Differentiable physics can connect these modules into a common learning system. When physical transitions are differentiable, prediction errors can propagate through the simulator to parameter estimators, perception networks, and learned residual components. The system can jointly optimize how the environment is perceived, which physical parameters are inferred, and how remaining model mismatch is corrected from data.

Physical constraints can be applied as both hard and soft structure. Hard constraints may enforce rigid geometry, joint limits, collision-free configurations, or other relationships that should not be violated. Soft constraints can penalize inconsistent energy behavior, penetration, unrealistic accelerations, or conservation residuals. Combining these mechanisms helps preserve feasibility without requiring uncertain real-world physics to be treated as perfectly known.

Contact and friction require special treatment because they introduce discontinuities and mode changes. A hybrid model can represent free motion, sticking, sliding, rolling, and impact as different interaction regimes. Learned components may infer the active contact mode and uncertain friction properties, while analytical or differentiable contact models impose reliable geometric and mechanical relationships within each regime.

Uncertainty modeling is essential because neither branch is universally correct. The physical model may contain uncertain parameters or simplified equations, while the learned model may encounter observations outside its training distribution. Representing uncertainty over parameters, latent states, contact modes, or future trajectories allows the system to generate multiple plausible futures rather than committing prematurely to one deterministic prediction.

Prediction then becomes a rollout of physically constrained but adaptively corrected futures. Starting from the estimated current state, candidate actions are propagated through the physical dynamics and learned corrections across multiple time steps. Physical constraints help prevent accumulated prediction errors from drifting into impossible states, while learned components compensate for systematic differences between nominal mechanics and actual environmental behavior.

This combination is particularly valuable for long-horizon world modeling. Small errors in friction, actuator delay, contact, or inertia can compound rapidly during repeated prediction. A purely analytical model may accumulate systematic bias, while a purely learned model may gradually violate physical feasibility. Hybrid prediction reduces both failure modes by anchoring rollouts to known structure while continuously correcting model mismatch.

The same architecture supports physics-guided generalization. When terrain, payload, objects, or environmental conditions change, stable physical relationships can remain reusable while parameters and learned residuals adapt. A robot encountering a new surface does not need to relearn its entire motion model; it can preserve vehicle geometry and kinematics while updating traction, slip, or terrain-related latent variables from recent experience.

System identification naturally becomes a continuous feedback mechanism inside the world model. Predicted transitions are compared with subsequent observations, and persistent prediction errors reveal mismatches in parameters or learned dynamics. Parameter estimates and residual models are then updated, producing a closed loop of observation, prediction, comparison, identification, and adaptation that continually calibrates the internal model to reality.

For planning, the hybrid world model can evaluate counterfactual futures under different actions. Candidate trajectories are rolled forward while considering geometry, dynamics, contact, actuator limits, learned environmental effects, and uncertainty. Model Predictive Control, trajectory optimization, and model-based reinforcement learning can therefore reason over futures that are not only statistically plausible but also physically executable.

The architecture can also support different computational levels. Fast analytical dynamics may operate at high control rates, learned residual models may update at intermediate rates, and larger perception or latent world models may reason over longer horizons. Such hierarchical execution is useful for Physical AI because not every prediction requires the same spatial detail, temporal horizon, or computational cost.

Simulation and real-world learning can be integrated within the same framework. Physics-based simulation provides broad experience and reusable structural knowledge, while domain randomization exposes the model to variations in uncertain parameters. Real robot observations subsequently identify actual parameters and train residual corrections, reducing the sim-to-real gap without discarding the physical knowledge acquired during simulation.

Failure detection can emerge from disagreement among model components. Large residual corrections, increasing uncertainty, persistent constraint violations, or disagreement between predicted and observed transitions can indicate that the robot has entered an unfamiliar regime. The system can respond by reducing speed, selecting safer actions, gathering informative observations, or triggering additional online identification before relying on long-horizon predictions.

The ultimate objective is not to maximize the amount of physics or learning independently, but to assign each source of knowledge to the role where it is most reliable. Physics supplies reusable structure, feasibility, interpretability, and extrapolation constraints. Learning supplies adaptation, perception, residual correction, and representations for complex phenomena. Parameter estimation and uncertainty connect these components to changing real-world conditions.

A hybrid physics-learned world model therefore forms a closed adaptive prediction system rather than a fixed simulator or unrestricted neural predictor. Multimodal observations establish the current state, physics generates structured expectations, learning corrects unknown effects, system identification calibrates parameters, and uncertainty expresses what remains unknown. Together, these mechanisms provide Physical AI with physically grounded, adaptive, and increasingly reliable models for prediction, planning, and control.
