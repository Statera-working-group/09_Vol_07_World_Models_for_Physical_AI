**Volume 07. World Models for Physical AI**

# Chapter 13. World Models for Planning

## 13.01. From Prediction to Planning

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

A world model becomes operationally valuable when prediction is transformed into planning. Prediction estimates what may happen next given the current state, while planning asks which sequence of actions should be chosen to produce a desirable future. This transition turns a world model from a passive forecasting mechanism into an internal simulator that supports purposeful behavior in a physical environment.

For Physical AI, planning cannot rely only on the most likely future. A robot must consider how different actions change future states and compare the resulting possibilities. Given a current state (s_t) and candidate action (a_t), an action-conditioned world model predicts (s_{t+1}). Repeating this process produces hypothetical trajectories representing different futures the robot could create through its own actions.

This capability establishes an important distinction between forecasting and intervention. A predictive model may estimate that a pedestrian will cross a robot\'s path, but a planning system must evaluate what happens if the robot slows down, stops, turns, or continues moving. The world model therefore becomes a mechanism for counterfactual reasoning: it predicts not simply what will happen, but what could happen under alternative actions.

Planning can consequently be understood as prediction performed repeatedly inside a decision loop. Candidate actions or trajectories are generated, the world model rolls each candidate forward through time, and the predicted consequences are evaluated according to goals, constraints, costs, rewards, and safety requirements. The action sequence associated with the most desirable predicted outcome becomes a candidate for execution.

The planning problem is often expressed as selecting an action sequence (a_{t:t+H}) over a horizon (H) that maximizes expected utility or minimizes cumulative cost. The world model supplies predicted states along each trajectory, while an objective function evaluates properties such as progress toward a goal, collision risk, energy consumption, travel time, stability, comfort, or task completion.

Physical environments make this process more difficult because the future is rarely deterministic. Other agents may behave unpredictably, sensor observations may be incomplete, terrain properties may be uncertain, and the robot\'s own dynamics may vary. A useful planner must therefore reason over distributions of possible futures rather than assuming that every candidate action produces one perfectly known trajectory.

The preceding treatment of uncertainty is especially important at this transition from prediction to planning. Predictive uncertainty becomes decision uncertainty when alternative futures have different consequences for the agent. A trajectory with high expected reward may be undesirable if it also contains a significant probability of collision or instability. Planning therefore combines predicted outcomes with confidence, uncertainty, and risk.

World-model planning also changes the meaning of representation quality. A representation does not need to reconstruct every visual detail of the environment if those details do not influence decisions. Instead, it should preserve information required to predict action-relevant consequences. Geometry, free space, object motion, semantic properties, physical constraints, agent intentions, and uncertainty can therefore be more valuable than photorealistic reconstruction.

This principle motivates planning directly in latent or structured state spaces. Rather than generating complete future camera images for every possible action, a planner may predict future latent states, BEV representations, occupancy fields, object trajectories, or compact semantic states. Such representations can dramatically reduce computational cost while retaining the information required to evaluate candidate actions.

Planning also introduces a fundamental computational tradeoff. More candidate trajectories, longer prediction horizons, richer world representations, and more probabilistic samples can improve decision quality, but they increase inference latency and energy consumption. Physical AI systems must balance planning depth against real-time constraints, especially when decisions are executed on embedded or edge computing platforms.

Hierarchical planning provides one solution to this problem. A high-level planner may reason over goals, routes, tasks, or semantic states across relatively long horizons, while a lower-level planner evaluates detailed motion over shorter horizons. The same world model can potentially support several temporal and spatial scales, allowing coarse long-range reasoning to guide precise local action selection.

Another important property is closed-loop replanning. Predictions inevitably become inaccurate as the horizon grows because disturbances, model errors, and unexpected events accumulate. Instead of committing to an entire predicted trajectory, the robot can execute only the immediate action or a short action segment, observe the resulting environment, update its internal state, and plan again using the newest information.

This repeated prediction-action-observation cycle makes world-model planning naturally compatible with Model Predictive Control. At every planning step, multiple future trajectories can be imagined over a finite horizon, evaluated, and optimized. Only the first action is executed before the process is repeated. Continuous replanning allows the system to correct prediction errors while still exploiting future consequences when selecting present actions.

Planning with a learned world model also allows an agent to evaluate experiences that have never occurred exactly in its training data. By combining learned dynamics with candidate actions, the system can mentally explore alternative trajectories before physically attempting them. This internal experimentation can reduce unnecessary real-world trials, improve data efficiency, and provide a foundation for model-based reinforcement learning.

However, planning quality is ultimately constrained by world-model accuracy in decision-relevant regions. Small prediction errors may be harmless when they concern irrelevant visual details but dangerous when they affect collision boundaries, contact dynamics, stopping distance, or another agent\'s motion. World models for planning should therefore be trained and evaluated according to their effect on decisions, not prediction accuracy alone.

The relationship between prediction and planning is thus bidirectional. Prediction enables planning by estimating the consequences of candidate actions, while planning identifies which predictions matter most. Difficult decisions reveal states, actions, and horizons where model accuracy is especially valuable, creating an opportunity to focus learning and data collection on decision-critical parts of the environment.

In a mature Physical AI architecture, perception estimates the present, the world model represents and predicts possible futures, planning evaluates those futures, and control converts selected actions into physical motion. Feedback from new observations continuously updates this loop. The world model occupies the central bridge between understanding what exists now and reasoning about what the agent should make happen next.

The transition from prediction to planning therefore marks a major conceptual step in world-model development. A system that predicts the future understands aspects of environmental dynamics; a system that predicts futures conditioned on its own possible actions can begin to choose among them. Planning emerges when imagined futures are evaluated according to goals, constraints, uncertainty, and physical consequences.

This perspective provides the foundation for the remainder of world-model-based planning. The next stages concern how an agent can systematically imagine candidate futures, evaluate and select among them, optimize trajectories, predict rewards and values, perform long-horizon reasoning, and incorporate uncertainty and risk into action selection. Together, these mechanisms transform learned predictive dynamics into goal-directed physical intelligence.

## 13.02. Imagine Evaluate and Select

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

A world-model-based planner can be understood through a simple but powerful cycle: imagine possible futures, evaluate their consequences, and select the action that best serves the agent's objectives. Rather than reacting only to the current observation, the agent uses its learned model of environmental dynamics to internally simulate how different actions may transform the present state into alternative future states.

The imagine stage begins from the agent's current state or belief state and generates candidate actions, action sequences, or trajectories. Each candidate is passed through an action-conditioned world model, which predicts how the environment and the agent may evolve over a planning horizon. In this sense, imagination is computational simulation rather than visual fantasy: it is the internal generation of plausible future state sequences.

A candidate action sequence can be represented as (a_{t:t+H}), where (H) defines the planning horizon. Starting from (s_t), the world model repeatedly predicts (s_{t+1}, s_{t+2}, \\ldots, s_{t+H}). Different action sequences therefore produce different imagined trajectories. The planner can explore these alternatives without physically executing every possibility in the real environment.

The imagined future does not necessarily need to be represented as pixels or reconstructed sensor observations. Planning may operate over latent states, BEV representations, occupancy fields, object trajectories, semantic states, or other compact representations. What matters is that the predicted representation preserves information required to distinguish desirable futures from unsafe, inefficient, or unsuccessful ones.

Candidate generation may range from simple sampling to structured search and numerical optimization. A mobile robot might sample alternative velocities and paths, while a manipulator may explore different reaching or grasping motions. More advanced systems can use trajectory optimization, tree search, learned proposal networks, or hierarchical planners to concentrate computation on promising regions of the action space.

The evaluate stage assigns meaning to the imagined futures. A trajectory is useful not merely because it is physically plausible, but because its consequences can be compared against the agent's objectives. An evaluation function may consider task completion, distance to a goal, collision probability, energy consumption, execution time, stability, comfort, manipulation success, constraint violations, or other mission-specific criteria.

Evaluation can be expressed through a cost function, reward function, value function, or combination of these mechanisms. For a predicted trajectory (\\tau), the planner may estimate an objective (J(\\tau)) that summarizes cumulative consequences across the horizon. This converts a complex sequence of predicted states into a quantity that allows alternative imagined futures to be ranked and compared systematically.

Physical AI requires evaluation to incorporate constraints as well as rewards. A trajectory that reaches the goal quickly may still be unacceptable if it passes too close to a person, exceeds actuator limits, enters non-traversable terrain, violates stability margins, or consumes excessive energy. Planning therefore involves finding futures that are not only beneficial but also physically feasible and operationally safe.

Uncertainty further changes how imagined futures should be evaluated. A world model may predict several possible outcomes for the same action sequence because of uncertain object motion, incomplete observations, stochastic dynamics, or limited model knowledge. The planner should therefore consider expected performance together with uncertainty, worst-case outcomes, confidence bounds, or explicit measures of risk.

This means that the highest expected reward does not always correspond to the best action. Suppose one trajectory reaches a destination slightly faster but passes through a region with uncertain occupancy, while another requires more time but remains in well-observed free space. A risk-aware planner may deliberately choose the second trajectory because its predicted outcome is more reliable and its potential failure cost is lower.

The select stage converts evaluation into a decision. After candidate trajectories have been scored, the planner identifies the action sequence that provides the most desirable balance among progress, cost, safety, uncertainty, and constraints. Formally, selection can be viewed as choosing (a\^\*_{t:t+H}) that optimizes the planning objective according to the futures predicted by the world model.

Selection does not imply that the complete chosen action sequence must be executed. In closed-loop planning, the agent commonly executes only the first action or a short segment of the selected trajectory. It then receives new observations, updates its state estimate, generates new imagined futures, reevaluates them, and selects again. This receding-horizon strategy continuously adapts the plan to changing physical conditions.

Imagine, evaluate, and select therefore operate as a repeating computational loop rather than as isolated stages. Imagination expands the space of possible futures, evaluation determines which futures are desirable, and selection converts those comparisons into action. New observations then reset the process from an updated state, allowing the agent to repeatedly revise its intentions as the environment changes.

The quality of this process depends strongly on the diversity of imagined futures. If candidate generation explores only a narrow set of actions, the planner may never discover a better solution even when the world model is accurate. Conversely, generating too many candidates can become computationally expensive. Effective planning must therefore balance exploration of alternatives with the latency and compute constraints of real-time Physical AI.

Planning horizon creates another important tradeoff. Short horizons reduce computation and prediction error but can encourage locally attractive decisions that lead to poor long-term outcomes. Longer horizons reveal delayed consequences and strategic alternatives, but world-model uncertainty and accumulated prediction error increase with time. Practical planners often combine short-horizon precision with longer-horizon coarse reasoning.

Hierarchical imagination can support this balance by representing different futures at different levels of abstraction. A high-level process may imagine semantic outcomes such as reaching a corridor, completing a delivery, or selecting a manipulation strategy. Lower-level planning can then evaluate detailed trajectories, velocities, contacts, and control actions required to realize the selected high-level intention.

Learned value functions can also reduce the need to simulate every trajectory to completion. Instead of rolling the world model forward until the final task outcome is reached, the planner can predict several steps and use a value estimate to approximate the desirability of the remaining future. This combination connects world-model planning with model-based reinforcement learning and long-horizon decision making.

The imagine-evaluate-select framework also provides a natural interface between learned intelligence and engineered constraints. The world model can learn complex environmental dynamics from data, while explicit safety rules, kinematic limits, collision constraints, or mission requirements can participate in evaluation and selection. This allows learned predictions to operate within boundaries defined by physical feasibility and system safety.

Ultimately, imagination without evaluation produces possibilities but no preference, while evaluation without selection produces judgments but no behavior. Selection closes the reasoning process by converting predicted possibilities into physical action. When continuously connected to perception and feedback, these three operations create a practical mechanism through which a Physical AI agent can reason about consequences before acting.

The resulting architecture can be summarized as a recurring flow from current state to candidate actions, imagined future trajectories, evaluation, selection, execution, observation, and replanning. This structure provides the conceptual foundation for more specific planning methods such as Model Predictive Control, latent-space planning, trajectory sampling and optimization, value prediction, model-based reinforcement learning, and uncertainty-aware planning.

## 13.03. Model Predictive Control with World Models

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

Model Predictive Control (MPC) provides a natural mechanism for turning a predictive world model into continuous physical action. Instead of computing a complete plan once and executing it blindly, MPC repeatedly predicts future states, evaluates candidate control sequences, executes only the immediate portion of the selected sequence, and then replans from newly observed conditions.

At time (t), the agent maintains a current state or belief state (s_t) and considers candidate control sequences (a_{t:t+H}) over a finite prediction horizon (H). The world model rolls each sequence forward to estimate (s_{t+1}, s_{t+2}, \\ldots, s_{t+H}). These predicted trajectories provide an internal simulation of how alternative control decisions may influence the future physical system.

The planner evaluates each predicted trajectory using an objective function that can combine goal progress, task reward, motion cost, energy consumption, control effort, collision risk, stability, comfort, and other requirements. Constraints can additionally represent actuator limits, velocity bounds, obstacle clearance, traversability, contact conditions, or operational safety rules that candidate trajectories should satisfy.

The optimization problem can be expressed conceptually as finding (a\^\*_{t:t+H}) that minimizes a cumulative cost (J) or maximizes expected reward over the predicted horizon. Unlike purely reactive control, this optimization considers delayed consequences. An action that appears beneficial immediately may be rejected when the world model predicts that it creates an unsafe, inefficient, or difficult state several steps later.

A defining characteristic of MPC is the receding horizon. Although the planner optimizes an entire sequence (a\^\*_{t:t+H}), the robot normally executes only the first action (a\^\*_t), or a short initial segment. Sensors then observe the resulting state, the internal world representation is updated, the horizon moves forward, and a new optimization problem is solved from the latest available information.

This closed-loop structure is especially important for Physical AI because learned world models are imperfect. Prediction errors accumulate as rollouts become longer, while unexpected disturbances, moving objects, terrain changes, interaction forces, and other agents can invalidate previously predicted futures. Frequent replanning prevents the controller from remaining committed to predictions that no longer describe the physical environment accurately.

Traditional MPC generally depends on analytical or identified mathematical dynamics models. World-model-based MPC extends this principle by allowing learned dynamics to predict complex transitions that may be difficult to describe analytically. Neural latent dynamics, action-conditioned predictive models, BEV world models, occupancy predictors, multimodal models, or hybrid physics-learned models can therefore function as predictive components within the MPC loop.

The predicted state does not need to reproduce complete sensor observations. For efficient control, the world model may operate in a compact latent state containing information relevant to motion and decision making. Alternatively, navigation systems may predict future BEV or occupancy representations, while manipulation systems may model object poses, contacts, robot configurations, and task-relevant semantic properties.

Candidate control sequences can be generated and optimized in several ways. Random or structured sampling can produce many possible trajectories that are evaluated by the world model. Optimization methods can iteratively improve promising sequences, while techniques such as the Cross-Entropy Method (CEM) or Model Predictive Path Integral (MPPI) control can concentrate computation around actions associated with favorable predicted outcomes.

The prediction horizon strongly influences MPC behavior. A short horizon reduces computational requirements and limits accumulated world-model error, making rapid replanning easier. However, it may fail to recognize consequences occurring farther into the future. A longer horizon provides greater foresight but increases prediction uncertainty, optimization complexity, memory requirements, and inference latency.

Control frequency creates a related design constraint. A fast-moving robot may require replanning many times per second, leaving only a small computational budget for world-model rollout and trajectory evaluation. Practical systems must therefore coordinate model complexity, number of candidate trajectories, rollout horizon, representation size, optimization iterations, and hardware capability so that decisions remain available within real-time deadlines.

Hierarchical MPC can distribute this computation across different temporal scales. A higher-level planner may predict routes, semantic goals, or coarse trajectories over longer horizons, while a lower-level MPC controller optimizes detailed velocities, steering commands, joint motions, or contact actions over shorter horizons. This allows long-range intent to guide precise real-time physical control without requiring every prediction to use equal resolution.

Uncertainty-aware MPC extends trajectory evaluation beyond single deterministic predictions. A world model may generate distributions over future occupancy, object motion, contact outcomes, or latent states. Candidate actions can then be evaluated according to expected cost, confidence bounds, worst-case consequences, or explicit risk measures, allowing the controller to prefer trajectories that remain safe across plausible alternative futures.

This capability becomes particularly important near obstacles, humans, unstable terrain, uncertain contacts, or unfamiliar environments. A trajectory with slightly lower nominal performance may be preferable if its predicted outcomes have substantially lower uncertainty. The MPC objective can therefore trade efficiency against robustness, producing behavior that adapts its conservatism according to the confidence of the world model.

World-model-based MPC can also combine learned dynamics with known physical structure. Analytical vehicle kinematics, rigid-body constraints, actuator models, or conservation principles may handle well-understood behavior, while learned residual models estimate effects that are difficult to model explicitly. Such hybrid prediction can improve physical consistency while retaining the flexibility of data-driven world modeling.

The quality of MPC depends not only on average prediction accuracy but on accuracy around trajectories considered by the controller. Errors near collision boundaries, stability limits, contact transitions, or high-speed maneuvers can produce serious planning failures even when overall prediction metrics appear strong. Training data and evaluation should therefore emphasize states and actions that are important to control decisions.

MPC also creates a useful learning loop for improving the world model. During operation, the controller predicts what should happen after an action and subsequently observes what actually happened. Differences between predicted and observed transitions provide information about model error, unfamiliar dynamics, or environmental change. These discrepancies can support system identification, adaptation, and continual refinement of predictive dynamics.

For mobile robots, world-model MPC may jointly reason about future robot motion, dynamic obstacles, traversability, and occupancy. For manipulators, it can predict configurations, contacts, object movement, and task progress. Similar principles can support autonomous vehicles, quadrupeds, humanoids, aerial robots, and other Physical AI systems whenever candidate actions can be simulated and evaluated before physical execution.

The central advantage of combining MPC with world models is therefore not merely better prediction, but the continuous conversion of prediction into corrective action. The system repeatedly asks what will happen under alternative controls, which predicted future best satisfies its objectives, what should be executed now, and how the plan should change after receiving new evidence from the physical world.

World-model-based MPC ultimately forms a closed reasoning-and-control cycle: observe the current state, imagine candidate futures, optimize the action sequence, execute the first action, observe the consequence, update the internal state, and plan again. This receding-horizon process provides a practical bridge between learned predictive intelligence and real-time control, enabling Physical AI systems to act while continuously reconsidering the future.

## 13.04. Latent Space Planning

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

Latent space planning performs decision making inside a compact learned representation of the world rather than directly reasoning over raw sensory observations. Cameras, LiDAR, proprioception, and other inputs are encoded into a latent state (z_t) that captures information relevant to future dynamics and action. Planning then predicts how candidate actions transform this latent state across time.

The central motivation is computational efficiency. Predicting complete future images, point clouds, or other high-dimensional observations for every candidate action can be prohibitively expensive for real-time Physical AI. A latent world model compresses observations into lower-dimensional features and performs future rollouts within this representation, allowing many candidate trajectories to be evaluated with substantially less computation.

A typical architecture begins with an encoder (E) that maps the current observation (o_t) into a latent state (z_t = E(o_t)). An action-conditioned dynamics model then predicts (z_{t+1}=F(z_t,a_t)). Repeated application of this transition model produces a latent trajectory (z_t,z_{t+1},\\ldots,z_{t+H}) for each candidate action sequence over planning horizon (H).

The latent state should not be viewed simply as compressed sensor data. For planning, it should preserve decision-relevant structure such as free space, object relationships, motion, geometry, contact conditions, semantic context, agent state, and uncertainty. Information that does not influence future actions can often be discarded, making the representation more efficient than reconstructing every detail of the physical scene.

Planning proceeds by generating candidate action sequences and rolling them forward through the latent dynamics model. Each sequence produces a different hypothetical latent future. These futures are evaluated using a reward model, cost model, value function, goal representation, or learned evaluator. The planner then selects the action sequence associated with the most desirable predicted latent trajectory.

One important advantage is that thousands of hypothetical futures may be explored without decoding each latent state back into the observation domain. If evaluation can operate directly on (z_t), the expensive generation of images or dense geometry becomes unnecessary during every planning iteration. Decoding can instead be used selectively for visualization, auxiliary supervision, validation, or tasks requiring explicit physical outputs.

Latent planning therefore separates prediction for decision making from prediction for reconstruction. A generative world model may attempt to reproduce future observations with high perceptual fidelity, whereas a planning-oriented latent model primarily needs to preserve features that determine action consequences. A visually imperfect latent prediction may still support excellent planning if its decision-relevant structure remains accurate.

However, compression creates an important risk. If the encoder removes information that later becomes necessary for a decision, no planner operating on the latent representation can recover it. Small obstacles, contact properties, friction changes, human intentions, or subtle geometric relationships may appear insignificant during representation learning but become critical when the robot must choose a safe action.

For this reason, representation learning and planning objectives should be closely connected. A latent space trained only for reconstruction may preserve perceptual detail that is irrelevant to control, while discarding useful causal structure. Planning-aware objectives can encourage the representation to preserve predictable dynamics, controllability, reward-relevant information, safety boundaries, and distinctions between states requiring different actions.

Action conditioning is essential because planning requires the model to distinguish futures produced by different interventions. From the same latent state (z_t), braking, accelerating, turning, grasping, or waiting should generate different latent trajectories. The learned transition function must therefore capture not only temporal regularities in observations but also how the agent\'s actions causally influence future world states.

The geometry of latent space can also affect planning. Ideally, nearby latent states represent physically or behaviorally similar situations, while meaningful transitions form smooth trajectories under feasible actions. Such structure can make trajectory optimization easier because changes in action produce predictable changes in latent futures. Poorly organized latent spaces may instead create discontinuities that make optimization unstable or misleading.

Candidate actions can be searched using sampling, trajectory optimization, Cross-Entropy Method (CEM), Model Predictive Path Integral (MPPI) control, tree search, gradient-based optimization, or learned proposal policies. Because latent rollouts are relatively compact, the planner can often evaluate more candidates or longer horizons than would be practical using high-dimensional observation-space prediction.

Some latent world models are differentiable from action inputs through predicted states to the planning objective. In such systems, gradients of predicted cost or reward can be propagated through the latent dynamics model to improve candidate actions directly. This enables efficient trajectory optimization, although the resulting actions remain dependent on the accuracy and smoothness of the learned latent dynamics.

Latent space planning naturally supports Model Predictive Control (MPC). The current observation is encoded, multiple candidate action sequences are simulated in latent space, the best sequence is selected, and only its first action or short segment is executed. New observations then produce an updated latent state, and the entire optimization is repeated using a receding horizon.

Uncertainty must also be represented within latent planning. A single predicted latent vector may hide several plausible physical futures, particularly under partial observability or stochastic dynamics. Probabilistic latent models can represent distributions over future states, allowing the planner to evaluate expected outcomes, uncertainty, confidence, and risk rather than relying on one deterministic trajectory.

Long-horizon latent planning introduces another challenge because prediction errors can accumulate even in compressed representations. Repeated transitions may gradually move the predicted latent state away from states corresponding to physically plausible situations. Temporal consistency, multi-step training, regularization, stochastic modeling, hierarchical prediction, and frequent closed-loop replanning can reduce this form of latent rollout drift.

Hierarchical latent spaces can represent different planning scales. Fine latent features may describe immediate geometry, velocity, contacts, and control conditions, while higher-level features encode routes, object relationships, task phases, or semantic goals. Long-range planning can operate at a coarse abstraction level before shorter-horizon planners refine selected intentions into detailed physical actions.

Latent goals provide another useful mechanism. Instead of specifying a desired future entirely through explicit coordinates or handcrafted rewards, a target observation or task condition can be encoded into a goal representation (z_g). Planning can then search for actions that move predicted latent states toward regions associated with the desired goal while respecting physical and safety constraints.

For robotics, the latent representation can integrate multiple modalities into a common predictive state. Camera appearance, LiDAR geometry, radar motion, IMU measurements, proprioception, language context, and robot configuration can contribute complementary information. The resulting multimodal latent state provides a compact internal representation from which future consequences of candidate actions can be predicted.

The main benefit of latent space planning is therefore not compression alone, but abstraction for decision making. It allows a Physical AI system to replace expensive prediction of every observable detail with efficient prediction of information that matters for action. When representation learning, dynamics prediction, uncertainty estimation, and planning objectives are aligned, latent space becomes an internal computational environment for imagining and evaluating futures.

In the broader world-model planning architecture, latent space planning connects learned representation directly to trajectory search and control. Observations are encoded into state, actions generate predicted latent futures, objectives evaluate those futures, and the selected action is executed before the state is updated again. This provides an efficient foundation for trajectory optimization, value prediction, model-based reinforcement learning, and long-horizon planning.

## 13.05. Trajectory Sampling and Optimization

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

Trajectory sampling and optimization provide the mechanism through which a world-model-based planner explores alternative ways of reaching a desired future. Instead of predicting the consequence of only one action sequence, the planner generates multiple candidate trajectories, rolls them forward through the world model, evaluates their predicted outcomes, and searches for a trajectory that best satisfies task objectives and physical constraints.

A trajectory can represent a sequence of actions (a_{t:t+H}), control inputs, waypoints, robot configurations, or latent states over a planning horizon (H). Each candidate defines one possible evolution of the agent. An action-conditioned world model predicts the corresponding future states, allowing the planner to compare alternatives internally before committing the robot to physical execution.

The simplest strategy is trajectory sampling. Candidate action sequences are drawn from a predefined or adaptive distribution and evaluated independently. For a mobile robot, samples may represent different steering angles, velocities, accelerations, or paths. For a manipulator, they may describe joint motions, end-effector trajectories, grasp approaches, or contact sequences that could accomplish the task.

Sampling is attractive because it does not require the world model or objective function to be differentiable. Complex neural dynamics, collision functions, discrete decisions, and nonlinear constraints can therefore be incorporated relatively easily. The main limitation is computational cost: sufficiently exploring a large action space may require evaluating many trajectories, particularly when the planning horizon or action dimensionality becomes large.

Uniform random sampling is rarely efficient in high-dimensional planning spaces because most candidates may be poor. Practical systems therefore bias sampling toward useful regions using previous solutions, heuristic proposals, learned policies, motion primitives, or goal-directed distributions. In receding-horizon planning, the previously selected trajectory can also be shifted forward and used as an initial proposal for the next planning cycle.

Trajectory optimization improves candidates rather than relying entirely on independent samples. Starting from one or more initial trajectories, an optimization procedure modifies actions to reduce predicted cost or increase predicted reward. The objective can combine goal progress, travel time, energy, control effort, collision risk, stability, comfort, task success, and other quantities predicted by the world model.

When the world model and objective are differentiable, gradient-based trajectory optimization can propagate derivatives from predicted cost through future states back to the action sequence. The optimizer can then adjust actions in directions expected to improve the trajectory. This approach can be computationally efficient, but its performance depends on smooth latent dynamics and can be sensitive to initialization or local optima.

Sampling-based optimization offers an alternative when gradients are unavailable, unreliable, or undesirable. Rather than differentiating through the world model, the planner repeatedly samples candidate trajectories, evaluates them, and updates the sampling distribution toward better-performing regions. This makes the approach compatible with nonlinear, stochastic, multimodal, or partially non-differentiable planning objectives.

The Cross-Entropy Method (CEM) is a common example. A distribution over action sequences is initialized, many candidate trajectories are sampled, and their predicted returns or costs are evaluated. A subset of high-performing elite samples is then used to update the distribution. Repeating this process concentrates future samples around increasingly promising action sequences.

Model Predictive Path Integral (MPPI) control follows a related sampling-based philosophy. Perturbations are applied to candidate control sequences, the resulting trajectories are predicted and assigned costs, and their contributions are weighted according to performance. Instead of retaining only a small elite subset, MPPI uses cost-weighted information from sampled trajectories to update the control sequence.

World models make these methods particularly powerful because candidate trajectories can be evaluated internally rather than through repeated physical trials. Hundreds or thousands of hypothetical actions may be tested in latent or structured state space before one is executed. This converts computation into a form of internal experimentation, reducing the need to discover poor actions through costly or unsafe real-world interaction.

Trajectory evaluation must reflect physical feasibility as well as task performance. A candidate may have excellent goal progress while violating steering limits, joint constraints, acceleration bounds, collision margins, contact conditions, or terrain restrictions. Hard constraints can reject infeasible trajectories, while soft constraints can introduce penalties that progressively discourage undesirable behavior.

Dynamic environments require candidate trajectories to account for predicted changes in the surrounding world. The robot is not merely searching for a geometrically valid path through a static map. Its world model may predict moving people, vehicles, manipulable objects, changing occupancy, terrain interaction, or other agents. Candidate trajectories must therefore be evaluated against future environmental states rather than only the present scene.

Uncertainty adds another dimension to optimization. The same candidate action sequence may produce several plausible futures because of stochastic dynamics, partial observability, or uncertain behavior of other agents. A planner can evaluate expected cost, variance, confidence bounds, worst-case outcomes, or risk-sensitive objectives so that trajectory quality reflects both nominal performance and reliability.

Sampling can naturally represent multimodal futures. If another agent may move left or right, multiple world-model rollouts can represent these alternatives instead of collapsing them into an unrealistic average prediction. A robust trajectory can then be selected according to its performance across several plausible futures, which is particularly valuable for collision avoidance and interaction with humans or autonomous agents.

The planning horizon determines how large the trajectory search problem becomes. Longer horizons allow the planner to recognize delayed consequences and strategic alternatives but increase action dimensionality and world-model prediction error. Shorter horizons are easier to optimize and permit faster replanning but may produce locally efficient actions that lead to poor states farther in the future.

Hierarchical trajectory optimization can reduce this difficulty. A high-level planner may first select routes, subgoals, motion modes, or semantic strategies using coarse trajectories. Lower-level optimization then searches detailed control sequences within the selected strategy. This limits the effective search space while preserving the ability to reason about both long-term objectives and immediate physical execution.

Latent space planning further increases efficiency by performing trajectory rollouts in compact learned representations rather than reconstructing complete future observations. If the latent state preserves geometry, motion, semantics, controllability, and safety-relevant information, many more trajectories can be evaluated within a fixed compute budget. This is especially important for real-time edge deployment.

Candidate generation can also be learned. A policy or proposal network trained from demonstrations, reinforcement learning, previous planning solutions, or successful trajectories can generate promising initial candidates. The world-model planner then evaluates and refines these proposals. Learned proposals provide speed, while explicit trajectory search provides the ability to reconsider actions when conditions differ from familiar training situations.

A useful planner often combines sampling and optimization rather than treating them as competing approaches. Broad sampling can discover qualitatively different solutions, after which local optimization refines the most promising candidates. Multiple optimized solutions may also be retained to preserve behavioral diversity, preventing the planner from prematurely committing to one narrow region of the action space.

Real-time implementation requires careful allocation of computation. The number of samples, rollout horizon, optimization iterations, world-model complexity, and evaluation cost determine planning latency. Parallel GPU computation can evaluate many trajectories simultaneously, while warm starts, adaptive sampling, pruning, hierarchical search, and compact latent dynamics can reduce unnecessary computation.

Trajectory sampling and optimization are most effective inside a closed-loop architecture. Even a highly optimized trajectory is based on predictions that become less reliable over time. The robot therefore executes only the first action or short portion of the selected trajectory, observes the resulting state, updates the world model input, and repeats the search. This continually corrects both planning and prediction errors.

Within world-model planning, trajectory sampling and optimization form the computational search engine between imagination and action. The world model generates consequences, the objective defines what constitutes a desirable future, and the optimizer searches the space of possible behaviors. Together, these mechanisms allow Physical AI systems to compare many possible futures internally and transform predictive intelligence into practical, goal-directed control.

## 13.06. Value and Reward Prediction

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

Value and reward prediction provides the mechanism that allows a world-model-based planner to distinguish desirable futures from undesirable ones. Predicting future states alone does not tell an agent which trajectory should be selected. The planner therefore needs additional models that estimate the immediate desirability of predicted outcomes and the longer-term consequences that may follow from them.

A reward model estimates the immediate utility associated with a state, action, transition, or short sequence. It can represent progress toward a goal, task completion, energy efficiency, safety, comfort, stability, or other objectives. In Physical AI, reward is therefore not limited to a single scalar notion of success but can summarize multiple operational criteria relevant to physical behavior.

A reward prediction can be written conceptually as (r_t = R(s_t,a_t,s_{t+1})). When a world model predicts the transition from (s_t) to (s_{t+1}) under action (a_t), the reward model estimates how desirable that transition is. Repeating this process across a predicted trajectory produces a sequence of rewards that can be accumulated to evaluate candidate plans.

Immediate rewards are often insufficient for planning because actions may have consequences that appear much later. A robot may temporarily move away from its destination to avoid an obstacle, reduce speed before an uncertain intersection, or reposition its manipulator before grasping. Such actions can have low immediate reward while being essential for achieving a better long-term outcome.

A value function addresses this problem by estimating the expected future return from a state or state-action pair. A state-value function (V(s_t)) estimates how desirable the future is when starting from state (s_t), while an action-value function (Q(s_t,a_t)) estimates the expected return after taking action (a_t) and subsequently following an appropriate policy.

The relationship between reward and value is fundamentally temporal. Reward evaluates relatively immediate consequences, whereas value summarizes consequences that extend beyond the explicitly simulated horizon. This distinction is especially useful when the world model cannot economically roll every candidate trajectory forward until task completion, which may require hundreds or thousands of future transitions.

A planner can therefore combine explicit world-model rollouts with a terminal value estimate. It predicts a candidate trajectory for a limited horizon (H), accumulates predicted rewards along that trajectory, and then estimates the remaining future using (V(s_{t+H})). Conceptually, the trajectory score can combine (\\sum_{k=0}\^{H-1}\\gamma\^k r_{t+k}) with a discounted terminal value (\\gamma\^H V(s_{t+H})).

The discount factor (\\gamma) controls how strongly future outcomes influence current decisions. Smaller values emphasize near-term rewards, while values closer to one preserve the importance of distant consequences. For Physical AI, this choice affects behavior significantly because navigation, manipulation, locomotion, and interaction tasks often require short-term sacrifices to achieve safer or more efficient long-term results.

Value prediction can greatly reduce planning computation. Instead of simulating every candidate until the final goal, the world model may predict only several future steps and allow the value model to approximate what lies beyond the planning horizon. This provides a practical bridge between short-horizon predictive control and long-horizon decision making, particularly when real-time inference budgets are limited.

Reward and value prediction can operate directly in latent space. If observations are encoded into a predictive latent state (z_t), reward models can estimate (R(z_t,a_t,z_{t+1})), while value models can estimate (V(z_t)) or (Q(z_t,a_t)). This avoids reconstructing complete future sensor observations and allows trajectory evaluation to remain inside the compact internal representation used by the world model.

The learned representation must nevertheless preserve information required for evaluating outcomes. A latent state that accurately predicts motion but removes task semantics, safety boundaries, object relevance, or contact conditions may support dynamics prediction while producing poor reward or value estimates. Representation learning should therefore retain features that are predictive not only of future states but also of future utility.

Reward design is particularly challenging in Physical AI because objectives are usually multi-dimensional. Reaching a goal quickly may conflict with collision avoidance, energy efficiency, smooth motion, payload stability, human comfort, or equipment protection. A practical reward function may combine these objectives using weighted terms, constraints, priorities, or hierarchical decision rules rather than relying on task completion alone.

Safety-critical requirements should not always be represented merely as ordinary negative rewards. If collision avoidance or actuator limits are treated only as weighted penalties, a sufficiently large task reward could theoretically compensate for unsafe behavior. Hard constraints, safety filters, runtime assurance, or risk limits can therefore operate alongside reward and value prediction to prevent unacceptable trajectories from being selected.

Reward models may be manually designed, learned from demonstrations, inferred from preferences, obtained through reinforcement learning, or constructed from combinations of explicit and learned objectives. Learned reward models are valuable when task quality is difficult to express analytically, but they introduce another source of model error. The planner may exploit inaccuracies in the learned reward instead of producing genuinely desirable physical behavior.

Value functions introduce similar approximation risks. A value estimate may be inaccurate for unfamiliar states, rare events, or situations outside the training distribution. Because the planner may use terminal value to evaluate futures beyond its explicit rollout horizon, an overestimated value can make a poor trajectory appear attractive. Confidence and uncertainty estimates should therefore accompany value prediction when possible.

Uncertainty-aware value and reward prediction can represent distributions rather than single scalar estimates. The planner may consider expected return together with variance, confidence intervals, downside risk, or worst-case outcomes. This is especially useful when predicted trajectories pass through poorly observed regions or involve uncertain contacts, dynamic agents, unfamiliar terrain, or other conditions where nominal reward alone is insufficient.

Reward prediction also interacts with multimodal futures. One action may lead to several plausible outcomes, each having a different reward. Rather than evaluating only an averaged predicted future, the planner can estimate reward across multiple possible rollouts and aggregate them according to probability and risk preference. This preserves important distinctions between safe, successful, uncertain, and potentially catastrophic outcomes.

Value learning can use experience generated by both real interaction and world-model imagination. Real trajectories provide grounded information about actual outcomes, while model-generated trajectories can expand the range of states considered during training. However, imagined experience inherits world-model errors, so value learning from synthetic rollouts must account for prediction reliability and avoid excessive dependence on unrealistic long-horizon simulations.

The world model, reward model, and value model consequently form complementary components. The world model answers what may happen under a candidate action, the reward model estimates how desirable predicted transitions are, and the value model estimates what those states imply for the longer-term future. Together they transform predicted dynamics into quantities that can guide action selection.

Within a receding-horizon planner, these components are continuously updated through interaction. The agent observes the current state, imagines candidate trajectories, predicts their rewards and terminal values, selects a promising action sequence, executes its first action, and observes the actual consequence. New experience then provides evidence for improving dynamics, reward, and value estimates.

Value and reward prediction therefore connect world modeling directly to goal-directed decision making. They provide the evaluative layer that converts possible futures into preferences and allow limited predictive rollouts to support decisions with long-term consequences. This connection forms a key foundation for model-based reinforcement learning, where learned dynamics, rewards, values, and policies are jointly used to improve behavior through both experience and imagination.

## 13.07. Model Based Reinforcement Learning

![](images/image7.png){width="7.268055555555556in" height="7.268055555555556in"}

Model-Based Reinforcement Learning (MBRL) combines reinforcement learning with an explicit or learned model of environment dynamics. Instead of learning only from actions executed in the physical world, an agent learns how states change under actions and uses this model to simulate possible futures. These imagined experiences support planning, policy improvement, and value estimation before actions are physically executed.

In conventional model-free reinforcement learning, a policy or value function is improved primarily from transitions collected through direct interaction with the environment. MBRL introduces a predictive model that estimates transitions such as (s_{t+1}=F(s_t,a_t)), often together with rewards. The agent can therefore reason about consequences without requiring every candidate behavior to be tested through real-world interaction.

A learned world model provides a particularly powerful form of environment model. Observations from cameras, LiDAR, proprioception, language, or other modalities can be encoded into a compact state (z_t). An action-conditioned dynamics model predicts (z_{t+1}), while reward, value, termination, uncertainty, or task-related models estimate properties required for decision making.

The basic learning cycle begins with real experience. The agent interacts with the environment and collects transitions containing observations, actions, rewards, and subsequent observations. These data are used to train or update the world model. Once the model captures useful dynamics, it can generate imagined trajectories by repeatedly predicting future states under candidate actions or policies.

Imagined trajectories allow reinforcement learning to reuse real experience more efficiently. A transition collected once from the physical environment can contribute to learning the dynamics model, after which the model can simulate many related action sequences. This capability is especially important in Physical AI, where collecting data may consume time, energy, hardware lifetime, human supervision, or expose the robot to physical risk.

Planning is one major way to exploit the learned model. At each decision step, the agent can generate candidate action sequences, roll them forward through the world model, predict rewards or costs, and select the sequence with the best expected outcome. Model Predictive Control (MPC), trajectory optimization, CEM, MPPI, or tree-based search can serve as planning mechanisms within an MBRL system.

Another approach uses imagined experience to train a policy. Rather than performing expensive planning for every action indefinitely, the agent can generate trajectories inside the world model and use them to improve a policy network. The learned policy can then produce actions quickly during execution, while planning may remain available for difficult, uncertain, or strategically important situations.

Value functions can also be learned from imagined trajectories. The world model predicts several steps into the future, reward models estimate intermediate outcomes, and a value function approximates consequences beyond the rollout horizon. This creates a connection between short simulated trajectories and long-term return, allowing the system to reason beyond the depth that can be explicitly simulated within a real-time computational budget.

MBRL therefore supports several relationships between model, planner, policy, and value function. The model can directly support online planning, generate synthetic experience for policy or value learning, or do both simultaneously. Some architectures emphasize planning at inference time, while others use the model primarily during training and deploy a compact policy for fast real-time control.

A central advantage of MBRL is sample efficiency. Because the agent can learn from predicted transitions as well as physical transitions, it may require substantially fewer real-world interactions than purely model-free approaches. For robotics, autonomous vehicles, manipulation, and other Physical AI systems, this can reduce data-collection cost and enable learning in environments where failures are expensive.

However, imagined experience is only useful when the world model is sufficiently accurate. Model errors can accumulate across repeated predictions, causing long synthetic trajectories to drift away from physically plausible states. A policy trained extensively on these inaccurate trajectories may learn to exploit weaknesses in the model rather than acquire behavior that succeeds in the real environment.

This problem is commonly described as model bias. Small one-step prediction errors can compound over long rollouts, especially when the policy visits states that were poorly represented in the training data. MBRL systems therefore often limit rollout length, retrain the model with new real experience, estimate uncertainty, use ensembles, or combine real and imagined data rather than trusting unrestricted synthetic experience.

Uncertainty estimation provides an important defense against model error. The system can identify states or trajectories where predictions are unreliable and reduce their influence on planning or learning. High uncertainty may trigger conservative behavior, shorter imagined rollouts, additional real-world data collection, or preference for trajectories that remain closer to regions where the world model has reliable experience.

This creates a natural exploration mechanism. Instead of exploring randomly, the agent can identify areas where additional experience would most improve its understanding. Exploration can balance expected task reward with information gain, uncertainty reduction, novelty, or coverage. The resulting experience improves the world model and can subsequently improve planning, value estimation, and policy learning.

Latent world models make MBRL computationally practical for high-dimensional sensory environments. Rather than predicting every pixel or point in future observations, the model can simulate compact latent states containing information relevant to dynamics, reward, and control. Policy and value networks can operate directly on these states, allowing many imagined transitions to be generated efficiently.

Representation quality is therefore critical. The latent state must preserve information required not only to predict future observations but also to distinguish actions with different consequences. Geometry, object motion, contacts, task semantics, controllability, safety boundaries, and uncertainty may all be important. A representation optimized only for visual reconstruction may not provide the structure required for effective reinforcement learning.

Hybrid model-based and model-free approaches can combine complementary strengths. Model-based reasoning offers foresight and sample efficiency, while model-free policies provide fast execution and can avoid repeated online optimization. A planner can generate high-quality behavior that trains a policy through imitation or reinforcement learning, and the policy can later provide candidate actions or initial trajectories back to the planner.

Physical knowledge can also be combined with learned dynamics. Known kinematics, rigid-body equations, actuator limits, or contact constraints can provide structured predictions, while neural models learn residual effects or environmental properties that are difficult to specify analytically. Such hybrid models can reduce the amount of learning required while improving physical consistency and generalization.

MBRL naturally supports continual improvement through a real-imagined-real cycle. The robot collects real experience, updates its world model, performs planning or learning through imagined experience, executes the improved behavior, and collects new data. Prediction errors between expected and observed transitions reveal weaknesses in the model and guide subsequent learning toward decision-relevant regions.

Safety remains a separate requirement rather than something guaranteed by reinforcement learning alone. Reward penalties can discourage unsafe behavior, but critical limits may require hard constraints, safety filters, collision checking, runtime assurance, or verified controllers. World-model uncertainty can provide additional evidence for deciding when learned planning should defer to conservative or engineered safety mechanisms.

Long-horizon MBRL can use hierarchical representations and temporal abstraction to reduce prediction depth. Higher-level models may predict subgoals, task stages, routes, or semantic outcomes, while lower-level models predict detailed motion and control. This allows the agent to reason about distant objectives without requiring a single low-level world model to remain accurate across extremely long sequences.

Model-Based Reinforcement Learning ultimately turns the world model into more than a predictor. The model becomes an internal environment in which the agent can practice, compare alternatives, estimate rewards and values, improve policies, and identify uncertainty before committing to physical action. Real experience grounds the model, while imagined experience amplifies the learning value of that experience.

Within Physical AI, this combination provides a bridge between prediction, planning, and learning. The world model predicts what could happen, reward and value models determine which futures are desirable, planning searches among alternatives, and reinforcement learning improves behavior from both real and imagined experience. Together, these components create an adaptive loop in which prediction continuously contributes to better future action.

## 13.08. Long Horizon Planning

![](images/image8.png){width="7.268055555555556in" height="7.268055555555556in"}

Long-horizon planning extends decision making beyond immediate actions and short predictive rollouts toward goals whose consequences unfold over extended periods. A Physical AI agent may need to navigate across large environments, complete multi-stage manipulation tasks, coordinate missions, or preserve resources for future objectives. Such problems require reasoning about sequences whose important outcomes may occur far beyond the current moment.

A straightforward approach would predict every low-level state and action from the present until the distant goal. In practice, this becomes increasingly difficult as the planning horizon grows. The number of possible action sequences expands rapidly, computational requirements increase, and small world-model errors accumulate across repeated transitions. Long-horizon planning must therefore manage both combinatorial complexity and prediction uncertainty.

Prediction error accumulation is particularly important for learned world models. Even when one-step predictions are accurate, repeatedly applying the model can gradually move imagined trajectories away from physically plausible states. Errors in geometry, object motion, contacts, terrain, or agent behavior may compound over time. Consequently, distant predictions should generally be treated with less confidence than near-term predictions.

Long-horizon planning also encounters branching futures. A single decision may lead to several possible environmental responses, each of which creates additional choices later. Explicitly evaluating every branch quickly becomes infeasible. Effective planners must concentrate computation on strategically important alternatives while pruning, abstracting, or approximating branches that are unlikely to influence the final decision.

Temporal abstraction provides a fundamental solution. Instead of representing a distant plan entirely as primitive actions, the planner can reason using higher-level actions that summarize extended behaviors. Commands such as "navigate to the corridor," "approach the object," "grasp the container," or "return to the charging station" represent temporally extended skills that may internally contain many lower-level control steps.

This naturally leads to hierarchical planning. A high-level planner operates over goals, subgoals, semantic states, routes, task phases, or learned skills, while lower-level planners convert selected intentions into detailed trajectories and control commands. The hierarchy reduces effective planning depth because many low-level transitions can be represented by a single higher-level decision.

Subgoal decomposition makes distant objectives more manageable. Rather than optimizing directly from the current state to a remote final goal, the planner identifies intermediate states that divide the problem into shorter segments. Each subgoal creates a locally meaningful target, while the sequence of subgoals preserves global task direction. World models can then predict transitions both between detailed states and between higher-level task abstractions.

Hierarchical world models can support this process by representing dynamics at multiple temporal scales. A fine-scale model may predict motion over fractions of a second, while intermediate models predict local maneuvers or interactions, and higher-level models predict task progression over seconds or minutes. Different levels can therefore provide the resolution appropriate to different parts of the planning horizon.

Latent representations are especially useful for long-horizon prediction because generating complete future sensory observations at every step is computationally expensive. A world model can instead predict compact latent states that preserve task-relevant geometry, semantics, object relationships, progress, and controllability. Higher levels of the latent hierarchy may become increasingly abstract as the prediction horizon extends.

Value functions provide another mechanism for avoiding excessively long explicit rollouts. The planner can simulate candidate trajectories for a limited number of steps and then estimate the remaining long-term return using a terminal value (V(s_{t+H})). This allows near-term consequences to be modeled explicitly while distant consequences are summarized through learned experience.

The quality of terminal value estimation becomes increasingly important when explicit rollout horizons are shortened. If the value model accurately recognizes states that lead to successful future outcomes, the planner can make useful long-range decisions without simulating every intermediate transition. However, inaccurate values can create false optimism or pessimism, particularly in unfamiliar states or situations outside the training distribution.

Search methods can also operate at multiple levels of abstraction. Tree search may explore alternative subgoals or strategies at a high level, while trajectory optimization or Model Predictive Control refines the selected branch locally. Learned policies can propose promising high-level actions, reducing the number of branches that require expensive world-model evaluation.

Long-horizon planning must consider delayed rewards. Some actions provide little immediate benefit but create opportunities that become valuable much later. A robot may spend time recharging before a long mission, reposition an object to enable later manipulation, or take a longer route that avoids a region likely to become congested. Short-sighted optimization may fail to recognize these strategic advantages.

Resource reasoning is therefore an important part of extended planning. Battery energy, computation, communication bandwidth, payload capacity, time, actuator temperature, and other limited resources can influence whether a future plan remains feasible. A long-horizon world model should predict not only spatial and semantic states but also resource states that constrain later actions.

Uncertainty generally increases with prediction distance, so long-horizon planners should avoid treating distant futures as precise forecasts. Probabilistic predictions can represent multiple plausible outcomes, while confidence estimates indicate where the world model becomes unreliable. The planner can use this information to preserve flexibility rather than committing too early to one detailed distant trajectory.

Contingency planning provides a practical response to uncertain futures. Instead of producing one rigid sequence of actions, the agent can maintain alternative branches conditioned on future observations or events. A plan may specify one strategy if a passage remains open and another if it becomes blocked. Such conditional plans transform long-range planning from fixed trajectory prediction into adaptive future reasoning.

Replanning further reduces the need for perfect long-term prediction. The agent can maintain a strategic direction over a long horizon while repeatedly recomputing detailed actions from new observations. Near-term decisions are executed with high precision, whereas distant portions of the plan remain coarse and revisable. This combines long-term intent with short-term closed-loop correction.

This principle connects long-horizon planning with Model Predictive Control. Conventional MPC usually optimizes a limited horizon, but hierarchical or value-augmented MPC can incorporate information about more distant consequences. High-level goals and terminal values provide strategic guidance, while repeated short-horizon optimization handles immediate dynamics, disturbances, and newly observed environmental changes.

Memory also becomes important when tasks extend over long periods. The planner may need to remember previously visited locations, completed subtasks, failed strategies, object interactions, commitments, or changes in the environment. A world model with temporal memory can maintain task context beyond the limited observation window used for immediate control.

For multi-agent Physical AI, long-horizon planning may additionally include coordination across robots or humans. Decisions about task allocation, rendezvous points, shared resources, communication opportunities, and future interference can have consequences much later than local motion decisions. Hierarchical representations can separate mission-level coordination from robot-level trajectory control.

Planning efficiency depends on allocating computation according to relevance. Near-term states often require precise geometry and dynamics, while distant states may need only coarse semantic predictions. Adaptive resolution allows the planner to spend computation where accuracy matters most. As the horizon extends, representations can become progressively more abstract until new observations justify detailed replanning.

Learning can improve this allocation by identifying recurring long-term structures. Policies, skills, options, subgoal generators, and value functions can capture solutions repeatedly encountered in experience. Instead of rediscovering every plan from primitive actions, the agent can reuse learned behavioral components and employ the world model primarily to adapt them to the current situation.

Long-horizon planning therefore does not require predicting the distant future with perfect detail. Its central challenge is to preserve strategically important consequences while controlling uncertainty, computational growth, and model error. Hierarchy, temporal abstraction, subgoals, value prediction, uncertainty estimation, memory, and closed-loop replanning jointly make extended reasoning computationally and physically practical.

Within a world-model architecture, long-horizon planning connects immediate predictive control with persistent goal-directed behavior. The agent reasons coarsely about distant objectives, predicts intermediate consequences, refines near-term actions, executes them, observes the resulting world, and repeatedly restructures its plan. This enables Physical AI to pursue complex objectives while remaining responsive to an uncertain and changing environment.

## 13.09. Uncertainty and Risk Aware Planning

![](images/image9.png){width="7.268055555555556in" height="7.268055555555556in"}

Uncertainty and risk-aware planning extends predictive decision making by recognizing that future states cannot be known with complete certainty. Sensor noise, partial observability, stochastic dynamics, model approximation, environmental change, and unpredictable agents all create multiple possible futures. A Physical AI system must therefore reason not only about what is likely to happen, but also about how reliable those predictions are.

A deterministic planner may represent each candidate action sequence with a single predicted trajectory. This simplification is efficient, but it can conceal important alternatives. The same action may succeed under one plausible future and cause collision, instability, or task failure under another. Risk-aware planning instead evaluates candidate actions across distributions or sets of possible future outcomes.

Uncertainty can originate from several different sources. Aleatoric uncertainty represents inherent variability in the environment, such as unpredictable pedestrian motion, terrain interaction, or noisy measurements. Epistemic uncertainty reflects limitations in the model\'s knowledge and often increases in unfamiliar states or situations poorly represented by training data. Distinguishing these sources helps determine how the planner should respond.

A world model can represent uncertainty by predicting probability distributions rather than single future states. Instead of estimating only (s_{t+1}), it may model (p(s_{t+1}\\mid s_t,a_t)). Repeated probabilistic transitions generate distributions over future trajectories, allowing the planner to estimate not only expected outcomes but also their variability, confidence, and potentially dangerous alternatives.

Multiple future hypotheses can also be represented explicitly. For example, a pedestrian approaching a robot may continue forward, slow down, stop, or change direction. Averaging these possibilities into one predicted trajectory can produce a future that is physically unlikely. Multimodal prediction preserves distinct hypotheses so that planning can evaluate each plausible interaction separately.

Model ensembles provide another practical mechanism for representing epistemic uncertainty. Several world models are trained with different initializations, data subsets, or architectures and independently predict future transitions. Agreement among models suggests greater confidence, while disagreement indicates regions where the system has limited knowledge. The planner can use this disagreement as a signal of prediction reliability.

Uncertainty becomes increasingly important as the prediction horizon grows. Near-term dynamics may be predicted accurately, while distant futures accumulate uncertainty through repeated transitions and branching events. A risk-aware planner should therefore avoid treating every point along a long rollout with equal confidence. Prediction confidence can decrease with horizon length and influence how strongly distant outcomes affect current actions.

Expected reward alone may be insufficient for selecting actions under uncertainty. Two trajectories can have similar expected returns while possessing very different risk profiles. One may produce consistently acceptable outcomes, whereas another combines very high reward with a small probability of catastrophic failure. Physical systems often require the planner to distinguish between these alternatives explicitly.

Risk-sensitive objectives modify trajectory evaluation to account for this distinction. The planner can consider expected cost together with variance, downside risk, probability of constraint violation, worst-case outcomes, or other measures of uncertainty. A candidate trajectory with slightly lower expected performance may therefore be preferred when it provides substantially more reliable and safer outcomes.

Chance constraints provide a probabilistic method for expressing safety requirements. Instead of requiring that a constraint hold for only one nominal trajectory, the planner can require the probability of collision, instability, or another undesirable event to remain below a specified threshold. This allows uncertainty to be incorporated directly into the feasibility conditions used during trajectory optimization.

Conditional Value at Risk (CVaR) provides another useful concept for safety-oriented planning. Rather than evaluating only average performance, CVaR emphasizes outcomes in the unfavorable tail of a distribution. A planner using this principle pays particular attention to severe low-probability failures, making it useful when rare collisions, falls, equipment damage, or mission failures have unacceptable consequences.

Robust planning takes a related but often more conservative approach. Instead of optimizing average performance across predicted futures, the planner searches for actions that remain acceptable across a defined range of disturbances or model variations. This can protect the system from unfavorable conditions, although excessive robustness may produce behavior that is unnecessarily slow, cautious, or inefficient.

The appropriate level of risk sensitivity depends on context. A robot moving through an empty warehouse may tolerate greater uncertainty than the same robot operating near people, fragile equipment, stairs, or moving vehicles. Risk-aware planning can therefore adapt safety margins, speed, trajectory clearance, and control aggressiveness according to environmental context and prediction confidence.

Uncertainty can also influence information-gathering behavior. When several actions provide similar task progress, the planner may prefer an action that produces better observations or reduces uncertainty about the environment. Moving to improve visibility, slowing down to obtain more reliable perception, or approaching an object from a better sensing angle can increase information before committing to a more consequential action.

This principle connects planning with active perception and exploration. Actions are selected not only because of their immediate physical consequences but also because of the information they are expected to provide. A world model can predict how future observations may reduce uncertainty, allowing the planner to trade short-term task progress against information gain when additional knowledge improves later decisions.

Risk-aware planning is especially important under partial observability. The true physical state may not be directly available because of occlusion, limited sensing, ambiguous observations, or hidden properties. The planner can therefore maintain a belief state representing probabilities over possible world states and plan according to how actions affect both the physical world and the agent\'s knowledge about it.

Trajectory sampling provides a natural way to propagate uncertainty. For each candidate action sequence, the planner can sample multiple possible future trajectories from the probabilistic world model. Rewards, constraints, and safety measures are evaluated across these rollouts, producing estimates of expected performance and risk. More samples improve coverage but increase computational cost.

Latent-space planning can make this process more practical by representing uncertainty in compact predictive states. Distributions over latent variables can encode alternative futures without generating complete sensor observations for every sample. The planner can then evaluate large numbers of uncertain trajectories using reward, value, safety, and uncertainty models operating directly within the latent representation.

Uncertainty estimates must themselves be calibrated. A model that is confidently wrong can be more dangerous than one that openly reports uncertainty. Calibration aims to ensure that predicted confidence corresponds reasonably well to actual prediction reliability. Evaluation should therefore examine not only prediction accuracy but also whether uncertainty increases appropriately when the system encounters unfamiliar or ambiguous situations.

Out-of-distribution detection is closely related to this requirement. When the robot encounters states far from its training experience, world-model predictions may become unreliable. Detecting such conditions can trigger shorter planning horizons, reduced speed, larger safety margins, additional sensing, fallback controllers, human assistance, or other conservative strategies rather than allowing uncertain predictions to drive aggressive behavior.

Closed-loop replanning provides another defense against uncertainty. The robot does not need to commit to an entire uncertain future trajectory. It can execute only the first action or short segment, collect new observations, update its belief and world model state, and optimize again. As new evidence becomes available, uncertainty can decrease and previously ambiguous alternatives can be reconsidered.

Safety-critical planning should combine learned risk estimates with explicit constraints and runtime safeguards. Reward penalties alone may not prevent dangerous actions when models are inaccurate. Collision checking, control limits, safety filters, verified fallback controllers, emergency stopping, and runtime assurance can provide additional layers that remain active even when the learned world model produces incorrect predictions.

Uncertainty and risk-aware planning therefore changes the central planning question from "Which trajectory has the highest predicted reward?" to "Which action remains desirable when prediction uncertainty and harmful alternatives are considered?" This distinction is essential for Physical AI because actions have real consequences, and rare failures may matter far more than small improvements in average performance.

Within a world-model architecture, uncertainty-aware planning integrates probabilistic prediction, multimodal futures, risk-sensitive evaluation, constraints, active information gathering, and closed-loop replanning. The resulting system does not merely imagine the most likely future; it reasons across plausible futures, measures confidence, protects against harmful outcomes, and adapts its behavior as new evidence arrives.

## 13.10. World Model Based Planner [w/Code]

![](images/image10.png){width="7.268055555555556in" height="7.268055555555556in"}

A world-model-based planner transforms predictive representations of an environment into goal-directed action. Rather than reacting only to the current observation, the planner uses an internal model to imagine how alternative actions may change the future. It evaluates these predicted futures according to objectives, constraints, uncertainty, and long-term consequences before selecting an action for physical execution.

The planning process begins from an estimated current state (s_t) or latent state (z_t). This state may integrate cameras, LiDAR, radar, proprioception, maps, language, task context, and memory. The world model then provides an action-conditioned transition function that predicts how the internal state evolves when different candidate actions are applied.

Conceptually, the predictive dynamics can be expressed as (s_{t+1}=F(s_t,a_t)), or probabilistically as (p(s_{t+1}\\mid s_t,a_t)). By repeatedly applying this transition model, the planner constructs hypothetical trajectories over a prediction horizon. Each trajectory represents one possible future generated by a particular sequence of actions.

Prediction alone, however, does not constitute planning. The system also requires an evaluation mechanism that determines which predicted futures are preferable. Reward functions, cost functions, value models, goal similarity, safety constraints, resource requirements, and risk measures can all contribute to trajectory evaluation. Planning emerges from the combination of predictive dynamics and preference over predicted outcomes.

Candidate actions can be generated through random sampling, structured motion primitives, learned policies, trajectory proposals, optimization procedures, or search algorithms. The planner may evaluate hundreds or thousands of alternatives in parallel. Efficient candidate generation is important because the space of possible action sequences grows rapidly as action dimensionality and planning horizon increase.

Trajectory sampling methods evaluate many candidate action sequences without requiring differentiable dynamics. Techniques such as the Cross-Entropy Method (CEM) progressively concentrate samples around promising regions, while Model Predictive Path Integral (MPPI) control uses cost-weighted trajectory perturbations. These approaches allow complex learned world models to participate directly in real-time planning.

When predictive dynamics and objectives are differentiable, trajectory optimization can use gradients to improve action sequences directly. Gradients of predicted reward or cost are propagated backward through imagined state transitions to the actions that generated them. This can provide efficient optimization in smooth planning spaces, although model inaccuracies or poor initialization may lead to undesirable local solutions.

Latent-space planning can substantially reduce the computational burden of world-model-based planning. Instead of predicting complete future images, point clouds, or sensor streams for every candidate, the planner performs rollouts in a compact learned representation. If this latent state preserves geometry, semantics, dynamics, controllability, and safety information, many futures can be evaluated efficiently.

A reward model estimates the immediate desirability of predicted transitions, while a value model summarizes longer-term consequences. The planner can therefore combine rewards accumulated over an explicit rollout with a terminal value estimate (V(s_{t+H})). This reduces the need to simulate every candidate until task completion and connects short predictive horizons with longer-term decision making.

Model Predictive Control (MPC) provides a natural execution framework for this architecture. The planner optimizes actions over a finite horizon but executes only the first action or short segment. New observations are then incorporated, the internal state is updated, and planning begins again. This receding-horizon process continuously corrects prediction and planning errors.

Closed-loop replanning is particularly important because learned world models are never perfectly accurate. Unexpected obstacles, environmental changes, contact errors, disturbances, and actions of other agents can make previously predicted futures obsolete. Frequent observation and replanning allow the agent to remain grounded in the actual physical world rather than committing blindly to an outdated imagined trajectory.

Uncertainty-aware prediction extends the planner beyond deterministic futures. A probabilistic world model may represent several possible outcomes for the same action sequence. The planner can evaluate expected performance together with variance, confidence, probability of constraint violation, worst-case outcomes, or Conditional Value at Risk (CVaR), allowing uncertainty to influence action selection directly.

This capability is essential for safety-critical Physical AI. A trajectory with the highest expected reward may not be desirable if it includes a small probability of collision, instability, or equipment damage. Risk-aware planning can prefer slightly less efficient trajectories when they remain safe across a broader range of plausible futures and provide more predictable physical outcomes.

Safety should nevertheless not depend entirely on learned rewards or predictions. Hard constraints, collision checking, actuator limits, safety filters, emergency stopping, runtime assurance, and verified fallback controllers can surround the learned planner. These mechanisms provide additional protection when the world model encounters unfamiliar conditions or generates inaccurate predictions.

Long-horizon objectives introduce additional challenges because the number of alternatives and accumulated prediction error increase with time. Hierarchical planning addresses this by separating strategic and tactical reasoning. High-level planners may select routes, subgoals, task phases, or learned skills, while lower-level planners optimize detailed trajectories and control commands over shorter horizons.

Temporal abstraction allows one high-level decision to represent many primitive actions. Instead of predicting every motor command across a long mission, the planner may reason using behaviors such as navigate, approach, inspect, grasp, transport, recharge, or wait. World models operating at different temporal scales can predict the consequences of these abstractions with different levels of detail.

Memory extends planning beyond the immediate observation window. Persistent internal state can represent completed subtasks, previous failures, visited locations, object interactions, resource usage, and changes in the environment. This information allows the planner to maintain continuity across long tasks and prevents repeated decisions from being made without knowledge of previous experience.

Active perception can also become part of planning. When uncertainty is high, an action may be valuable because it improves future observations rather than immediately advancing the task. The planner may reposition a sensor, change viewpoint, slow down, or approach cautiously to reduce uncertainty before committing to an action with significant physical consequences.

The world-model-based planner can therefore optimize both control and information acquisition. Actions influence the physical environment while simultaneously changing what the agent will be able to observe. Planning over belief states or uncertainty-aware latent states allows the system to consider how future information may improve subsequent decisions.

Model-Based Reinforcement Learning (MBRL) provides a learning framework around this planning process. Real experience trains the world model, while imagined trajectories support policy improvement, value learning, and planning. Improved behavior generates new real experience, which reveals prediction errors and expands the data available for further world-model refinement.

A learned policy can complement explicit planning by proposing promising candidate actions or producing rapid control in familiar situations. The planner can then concentrate expensive search on uncertain, novel, or strategically important decisions. Conversely, high-quality trajectories discovered through planning can train the policy, creating a complementary relationship between deliberative planning and fast learned behavior.

Hybrid world models can combine learned predictions with known physical structure. Vehicle kinematics, rigid-body dynamics, actuator constraints, collision geometry, or conservation principles may provide reliable components, while neural models learn complex environmental interactions or residual dynamics. Such combinations can improve physical consistency and reduce dependence on purely data-driven prediction.

The complete architecture therefore forms a continuous perception-prediction-evaluation-action loop. Observations update the internal state, the world model imagines candidate futures, the planner evaluates their reward, value, feasibility, uncertainty, and risk, and an optimized action is selected. Physical execution produces new observations that immediately begin the next planning cycle.

A world-model-based planner ultimately turns imagination into controlled physical behavior. Its purpose is not to predict the future perfectly, but to generate sufficiently useful alternative futures to support better decisions. By combining world modeling, trajectory search, value estimation, uncertainty reasoning, hierarchy, memory, safety constraints, and closed-loop replanning, Physical AI can continuously decide what to do next while anticipating what may happen afterward.
