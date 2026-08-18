**Volume 07. World Models for Physical AI**


# Chapter 02. Predictive World Models

##  

## 02.01. Prediction as the Core of World Models

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

Prediction is the central computational function that transforms a world model from a passive representation of the environment into an active model of how the environment may evolve. A Physical AI system must not only estimate what exists at the present moment but also anticipate what is likely to happen next. Prediction therefore connects perception of the current world with reasoning about possible future states.

A world model can be understood as an internal mechanism that estimates transitions from one state of the environment to another. Given a current internal state, the model predicts a future state according to learned dynamics, physical constraints, contextual information, and eventually the actions of the agent. This transition-oriented view distinguishes predictive world modeling from static scene understanding, mapping, or object recognition.

Prediction is particularly important in Physical AI because actions take time to execute. A mobile robot cannot wait until an obstacle has already entered its path before reasoning about avoidance, and a manipulator cannot control an object reliably by considering only its current pose. The system must estimate how objects, agents, surfaces, forces, and its own body will change during the interval between observation, decision, and physical execution.

The predictive process usually begins with observations obtained from cameras, LiDAR, radar, IMUs, proprioceptive sensors, localization systems, or other sensing modalities. These observations are transformed into an internal state representation containing information relevant to future evolution. Prediction then operates on this representation rather than treating every incoming sensor measurement as an independent event, allowing temporal relationships to become part of the modeled world.

Not every observable detail needs to be predicted with equal precision. For intelligent action, the most useful predictions are often those describing task-relevant changes such as object motion, occupancy, traversability, collision risk, contact, agent behavior, or semantic state transitions. A world model therefore benefits from learning representations that preserve predictable and decision-relevant structure while suppressing details that contribute little to future action.

Prediction also provides a mechanism for learning meaningful representations without requiring exhaustive human annotation. When a model is trained to infer missing or future information from previous observations, it must discover regularities that persist across space and time. Repeated exposure to temporal sequences can reveal object permanence, motion patterns, environmental structure, interaction effects, and other latent properties that are difficult to specify manually.

A predictive world model does not necessarily generate future camera images. Prediction can occur in pixel space, geometric space, semantic space, occupancy space, structured state space, or a learned latent representation. For Physical AI, latent and structured predictions are often attractive because they can focus computation on information required for reasoning and control instead of reconstructing every visual detail of the future environment.

The prediction horizon strongly influences what the model must learn. Very short-horizon prediction may primarily capture local motion and immediate state transitions, whereas longer horizons require reasoning about accumulated dynamics, interactions, intentions, and alternative outcomes. As the horizon increases, uncertainty generally grows because small ambiguities in the current state can develop into substantially different future trajectories.

This uncertainty means that prediction should not always be interpreted as producing one exact future. Physical environments frequently permit several plausible outcomes. A pedestrian may continue walking, stop, or change direction; an object may slide or remain stable after contact. A sufficiently expressive world model should therefore represent possible future states and their likelihoods rather than assuming that environmental evolution is perfectly deterministic.

Prediction becomes especially powerful when it is conditioned on action. The relevant question for an autonomous agent is not only "What will happen next?" but also "What will happen if I perform this action?" By modeling the relationship between current state, candidate action, and resulting future state, the world model becomes an internal predictive simulator through which the agent can compare alternative behaviors before committing to them physically.

This ability creates a direct bridge between world modeling and planning. Candidate actions or trajectories can be rolled forward through the predictive model, producing imagined future states that can be evaluated according to goals, safety constraints, rewards, energy consumption, collision probability, or other criteria. Planning can consequently become a process of predicting alternatives, evaluating their consequences, and selecting actions associated with desirable futures.

Prediction also supports closed-loop control because predicted outcomes can continuously be compared with subsequent observations. When the observed environment differs from the predicted environment, the resulting prediction error provides information about inaccuracies in state estimation, dynamics, environmental assumptions, or sensor interpretation. These discrepancies can drive adaptation and help the system refine both its internal representation and its transition model.

In robotics, prediction must account for the dynamics of both the external environment and the embodied agent. Wheel slip, actuator delay, payload variation, terrain properties, contact forces, joint dynamics, and sensor latency can alter the consequences of commands. A useful Physical AI world model therefore predicts not merely external events but the coupled evolution of robot, environment, and interaction between them.

The same principle extends naturally to environments containing other autonomous or intelligent agents. Humans, vehicles, robots, and animals introduce behavior that cannot always be described adequately by simple mechanical extrapolation. Their future states may depend on goals, social interactions, conventions, and responses to the robot itself. Prediction must therefore combine physical dynamics with behavioral and contextual patterns when operating in shared environments.

Predictive models also provide a foundation for temporal memory. The present observation may be incomplete because of occlusion, limited sensor range, noise, or partial observability. By integrating previous observations and predicting how hidden states evolve, the world model can maintain hypotheses about objects or environmental properties that are temporarily invisible. Prediction thus helps preserve continuity of the world beyond what sensors directly observe at each instant.

A major challenge is preventing prediction errors from accumulating over long rollouts. A small mistake in one predicted state can become input to the next prediction and progressively move the imagined trajectory away from reality. Effective world models therefore require temporal consistency, robust representations, uncertainty estimation, corrective observations, and training strategies that expose the model to the consequences of its own prediction errors.

Prediction should consequently be evaluated not only by numerical similarity to future observations but also by usefulness for downstream behavior. A model that produces visually accurate futures may still be poor for control if it misrepresents collision boundaries or object motion. Conversely, a compact latent prediction may be extremely valuable if it preserves the dynamics required for navigation, manipulation, safety assessment, and decision making.

At the system level, prediction converts sensing into anticipation. Perception estimates the current environment, memory preserves relevant past information, and prediction extends this internal state toward possible futures. Planning and control can then operate on those predicted futures rather than reacting exclusively to events after they occur. This transition from reaction to anticipation is one of the defining capabilities enabled by world models.

For Physical AI, prediction ultimately serves as the computational bridge between understanding and intervention. An embodied agent must continuously infer what the world is, estimate how it is changing, anticipate how its own actions may influence that change, and revise its beliefs when reality differs from expectation. A world model becomes useful precisely because prediction allows internal representations to participate directly in this continuous perception--prediction--action loop.

As predictive capability improves, the internal model can support increasingly sophisticated forms of physical reasoning. Short-term state forecasting can develop into multi-step simulation, alternative-future exploration, counterfactual reasoning, risk estimation, and long-horizon planning. In this sense, prediction is not merely one component among many within a world model; it is the mechanism that gives the model temporal meaning and makes imagined futures operationally useful for intelligent action.

예측(Prediction)은 월드 모델(World Model)을 환경(Environment)에 대한 수동적인 표현(Passive Representation)에서 환경이 어떻게 변화할 수 있는지를 능동적으로 추론하는 모델(Active Model)로 전환하는 핵심 계산 기능(Computational Function)이다. 피지컬 AI(Physical AI) 시스템은 현재 순간에 무엇이 존재하는지를 추정하는 것뿐만 아니라 다음에 어떤 일이 발생할 가능성이 있는지도 예상해야 한다. 따라서 예측(Prediction)은 현재 세계에 대한 인식(Perception)과 가능한 미래 상태(Future States)에 대한 추론(Reasoning)을 연결한다.

월드 모델(World Model)은 환경의 한 상태(State)가 다른 상태로 어떻게 전이(Transition)되는지를 추정하는 내부 메커니즘(Internal Mechanism)으로 이해할 수 있다. 현재의 내부 상태(Internal State)가 주어지면 모델은 학습된 동역학(Learned Dynamics), 물리적 제약(Physical Constraints), 맥락 정보(Contextual Information), 그리고 궁극적으로 에이전트(Agent)의 행동(Action)을 기반으로 미래 상태(Future State)를 예측한다. 이러한 전이 중심 관점(Transition-Oriented View)은 예측형 월드 모델링(Predictive World Modeling)을 정적인 장면 이해(Scene Understanding), 매핑(Mapping), 객체 인식(Object Recognition)과 구별한다.

예측(Prediction)은 피지컬 AI(Physical AI)에서 특히 중요하다. 실제 행동(Action)을 실행하는 데에는 시간이 필요하기 때문이다. 이동 로봇(Mobile Robot)은 장애물이 이미 경로에 진입한 이후에야 회피를 판단해서는 안 되며, 매니퓰레이터(Manipulator) 역시 물체의 현재 자세(Pose)만 고려해서는 안정적으로 제어할 수 없다. 시스템은 관측(Observation), 의사결정(Decision), 물리적 실행(Physical Execution) 사이의 시간 동안 객체, 에이전트, 표면, 힘, 그리고 자신의 몸체가 어떻게 변화할지를 추정해야 한다.

예측 과정(Predictive Process)은 일반적으로 카메라(Camera), 라이다(LiDAR), 레이더(Radar), 관성 측정 장치(IMU), 고유수용성 센서(Proprioceptive Sensors), 위치추정 시스템(Localization Systems) 또는 기타 센싱 모달리티(Sensing Modalities)에서 얻어진 관측(Observations)으로 시작한다. 이러한 관측은 미래의 변화에 관련된 정보를 포함하는 내부 상태 표현(Internal State Representation)으로 변환된다. 이후 예측은 각각의 센서 측정값을 독립적인 사건으로 처리하는 대신 이러한 표현을 기반으로 수행되며, 이를 통해 시간적 관계(Temporal Relationships)가 모델링된 세계의 일부가 된다.

관측 가능한 모든 세부 정보를 동일한 정밀도로 예측할 필요는 없다. 지능적 행동(Intelligent Action)에 가장 유용한 예측은 객체 움직임(Object Motion), 점유 상태(Occupancy), 주행 가능성(Traversability), 충돌 위험(Collision Risk), 접촉(Contact), 에이전트 행동(Agent Behavior), 의미적 상태 전이(Semantic State Transitions)처럼 과업(Task)과 관련된 변화를 설명하는 경우가 많다. 따라서 월드 모델(World Model)은 미래 행동에 거의 기여하지 않는 세부 사항을 억제하면서 예측 가능하고 의사결정에 중요한 구조를 보존하는 표현(Representation)을 학습하는 것이 유리하다.

예측(Prediction)은 또한 방대한 인간 라벨링(Human Annotation)을 요구하지 않고 의미 있는 표현(Meaningful Representation)을 학습하는 메커니즘을 제공한다. 모델이 이전 관측으로부터 누락된 정보나 미래 정보를 추론하도록 학습되면 공간과 시간에 걸쳐 지속되는 규칙성(Regularities)을 발견해야 한다. 시간적 시퀀스(Temporal Sequences)에 반복적으로 노출되면서 객체 영속성(Object Permanence), 움직임 패턴(Motion Patterns), 환경 구조(Environmental Structure), 상호작용 효과(Interaction Effects)와 같이 사람이 직접 명시하기 어려운 잠재적 속성(Latent Properties)을 학습할 수 있다.

예측형 월드 모델(Predictive World Model)이 반드시 미래의 카메라 영상을 생성해야 하는 것은 아니다. 예측은 픽셀 공간(Pixel Space), 기하학적 공간(Geometric Space), 의미 공간(Semantic Space), 점유 공간(Occupancy Space), 구조화된 상태 공간(Structured State Space), 또는 학습된 잠재 표현(Learned Latent Representation)에서 수행될 수 있다. 피지컬 AI(Physical AI)에서는 미래 환경의 모든 시각적 세부 사항을 복원하기보다 추론과 제어에 필요한 정보에 계산 자원을 집중할 수 있다는 점에서 잠재 예측(Latent Prediction)과 구조화된 예측(Structured Prediction)이 특히 유용하다.

예측 지평(Prediction Horizon)은 모델이 무엇을 학습해야 하는지에 큰 영향을 준다. 매우 짧은 지평의 예측(Short-Horizon Prediction)은 주로 국소적 움직임(Local Motion)과 즉각적인 상태 전이(State Transition)를 포착하지만, 장기 지평(Long Horizon)은 누적된 동역학(Accumulated Dynamics), 상호작용(Interactions), 의도(Intentions), 대안적 결과(Alternative Outcomes)에 대한 추론을 요구한다. 예측 지평이 길어질수록 현재 상태의 작은 불확실성이 매우 다른 미래 궤적(Future Trajectories)으로 발전할 수 있기 때문에 일반적으로 불확실성(Uncertainty)도 증가한다.

이러한 불확실성(Uncertainty)은 예측을 항상 하나의 정확한 미래를 생성하는 과정으로 해석해서는 안 된다는 것을 의미한다. 물리적 환경(Physical Environment)에서는 여러 개의 미래가 동시에 가능할 수 있다. 보행자(Pedestrian)는 계속 걷거나 멈추거나 방향을 변경할 수 있으며, 물체는 접촉 후 미끄러지거나 현재 위치에 안정적으로 남을 수도 있다. 따라서 충분히 표현력이 높은 월드 모델(World Model)은 환경 변화가 완전히 결정론적(Deterministic)이라고 가정하기보다 가능한 미래 상태와 그 가능성(Likelihood)을 표현해야 한다.

예측(Prediction)은 행동(Action)을 조건으로 사용할 때 특히 강력해진다. 자율 에이전트(Autonomous Agent)에게 중요한 질문은 단순히 "다음에 무엇이 일어날 것인가?"가 아니라 "내가 이 행동을 수행하면 무엇이 일어날 것인가?"이다. 현재 상태(Current State), 후보 행동(Candidate Action), 그리고 그 결과로 발생하는 미래 상태(Future State)의 관계를 모델링함으로써 월드 모델(World Model)은 에이전트가 실제 물리적 행동을 수행하기 전에 여러 대안적 행동을 비교할 수 있는 내부 예측 시뮬레이터(Internal Predictive Simulator)가 된다.

이러한 능력은 월드 모델링(World Modeling)과 계획(Planning)을 직접 연결한다. 후보 행동(Candidate Actions)이나 궤적(Trajectories)을 예측 모델 내부에서 미래 방향으로 전개(Rollout)하여 가상의 미래 상태(Imagined Future States)를 생성하고, 이를 목표(Goals), 안전 제약(Safety Constraints), 보상(Rewards), 에너지 소비(Energy Consumption), 충돌 확률(Collision Probability) 등의 기준으로 평가할 수 있다. 결과적으로 계획은 여러 대안을 예측하고, 그 결과를 평가하며, 바람직한 미래와 연결된 행동을 선택하는 과정이 된다.

예측(Prediction)은 예측된 결과를 이후의 실제 관측(Observation)과 지속적으로 비교할 수 있기 때문에 폐루프 제어(Closed-Loop Control)도 지원한다. 관측된 환경이 예측된 환경과 다르면 그 차이에서 발생하는 예측 오차(Prediction Error)는 상태 추정(State Estimation), 동역학(Dynamics), 환경 가정(Environmental Assumptions), 센서 해석(Sensor Interpretation)의 부정확성에 대한 정보를 제공한다. 이러한 차이는 적응(Adaptation)을 유도하고 시스템이 내부 표현과 전이 모델(Transition Model)을 지속적으로 개선하도록 도울 수 있다.

로보틱스(Robotics)에서 예측은 외부 환경(External Environment)의 동역학뿐만 아니라 몸체를 가진 에이전트(Embodied Agent) 자체의 동역학도 고려해야 한다. 휠 슬립(Wheel Slip), 액추에이터 지연(Actuator Delay), 페이로드 변화(Payload Variation), 지형 특성(Terrain Properties), 접촉력(Contact Forces), 관절 동역학(Joint Dynamics), 센서 지연(Sensor Latency)은 명령의 결과를 변화시킬 수 있다. 따라서 유용한 피지컬 AI 월드 모델(Physical AI World Model)은 외부 사건뿐 아니라 로봇, 환경, 그리고 이들 사이의 상호작용이 결합되어 변화하는 과정까지 예측해야 한다.

동일한 원리는 다른 자율 또는 지능형 에이전트(Intelligent Agents)가 존재하는 환경으로 자연스럽게 확장된다. 인간(Humans), 차량(Vehicles), 로봇(Robots), 동물(Animals)은 단순한 기계적 외삽(Mechanical Extrapolation)만으로 충분히 설명하기 어려운 행동을 보인다. 이들의 미래 상태는 목표(Goals), 사회적 상호작용(Social Interactions), 관습(Conventions), 그리고 로봇 자체에 대한 반응에 따라 달라질 수 있다. 따라서 공유 환경(Shared Environment)에서 동작하는 예측 모델은 물리적 동역학(Physical Dynamics)과 행동적·맥락적 패턴(Behavioral and Contextual Patterns)을 함께 고려해야 한다.

예측 모델(Predictive Model)은 시간적 메모리(Temporal Memory)의 기반도 제공한다. 현재 관측은 가림(Occlusion), 제한된 센서 범위(Limited Sensor Range), 노이즈(Noise), 부분 관측 가능성(Partial Observability) 때문에 불완전할 수 있다. 이전 관측을 통합하고 숨겨진 상태(Hidden States)가 어떻게 변화하는지를 예측함으로써 월드 모델은 일시적으로 보이지 않는 객체나 환경 속성에 대한 가설을 유지할 수 있다. 따라서 예측은 매 순간 센서가 직접 관측하는 범위를 넘어 세계의 연속성(Continuity)을 유지하는 데 기여한다.

주요 과제 중 하나는 장기 롤아웃(Long Rollout) 과정에서 예측 오차(Prediction Error)가 누적되는 것을 방지하는 것이다. 하나의 예측 상태에서 발생한 작은 오류가 다음 예측의 입력으로 사용되면서 가상의 궤적(Imagined Trajectory)을 실제 환경에서 점차 멀어지게 할 수 있다. 따라서 효과적인 월드 모델(World Model)은 시간적 일관성(Temporal Consistency), 강건한 표현(Robust Representation), 불확실성 추정(Uncertainty Estimation), 관측을 통한 보정(Corrective Observations), 그리고 모델 자체의 예측 오류 결과를 학습 과정에서 경험하게 하는 훈련 전략(Training Strategies)을 필요로 한다.

따라서 예측(Prediction)은 미래 관측과의 수치적 유사성(Numerical Similarity)만으로 평가되어서는 안 되며, 후속 행동(Downstream Behavior)에 얼마나 유용한지도 평가해야 한다. 시각적으로 정확한 미래를 생성하는 모델이라도 충돌 경계(Collision Boundaries)나 객체 움직임(Object Motion)을 잘못 표현한다면 제어(Control)에는 부적합할 수 있다. 반대로 간결한 잠재 예측(Latent Prediction)이라도 내비게이션(Navigation), 조작(Manipulation), 안전성 평가(Safety Assessment), 의사결정(Decision Making)에 필요한 동역학을 보존한다면 매우 높은 가치를 가질 수 있다.

시스템 수준(System Level)에서 예측(Prediction)은 센싱(Sensing)을 예상(Anticipation)으로 전환한다. 인식(Perception)은 현재 환경을 추정하고, 메모리(Memory)는 관련된 과거 정보를 보존하며, 예측은 이러한 내부 상태를 가능한 미래로 확장한다. 이후 계획(Planning)과 제어(Control)는 사건이 발생한 이후에만 반응하는 대신 예측된 미래를 기반으로 동작할 수 있다. 이러한 반응(Reaction)에서 예상(Anticipation)으로의 전환은 월드 모델이 제공하는 핵심 능력 중 하나이다.

피지컬 AI(Physical AI)에서 예측(Prediction)은 궁극적으로 이해(Understanding)와 개입(Intervention)을 연결하는 계산적 다리(Computational Bridge)의 역할을 한다. 몸체를 가진 에이전트(Embodied Agent)는 세계가 무엇인지 지속적으로 추론하고, 세계가 어떻게 변화하고 있는지를 추정하며, 자신의 행동이 그 변화를 어떻게 바꿀지를 예상하고, 현실이 예상과 다를 때 자신의 믿음(Belief)을 수정해야 한다. 월드 모델(World Model)은 예측을 통해 내부 표현이 이러한 지속적인 인식--예측--행동 루프(Perception--Prediction--Action Loop)에 직접 참여할 수 있기 때문에 실질적인 가치를 갖는다.

예측 능력(Predictive Capability)이 향상될수록 내부 모델(Internal Model)은 더욱 정교한 형태의 물리적 추론(Physical Reasoning)을 지원할 수 있다. 단기 상태 예측(Short-Term State Forecasting)은 다단계 시뮬레이션(Multi-Step Simulation), 대안적 미래 탐색(Alternative-Future Exploration), 반사실적 추론(Counterfactual Reasoning), 위험 추정(Risk Estimation), 장기 계획(Long-Horizon Planning)으로 발전할 수 있다. 이러한 의미에서 예측은 월드 모델을 구성하는 여러 요소 중 하나에 불과한 것이 아니라, 모델에 시간적 의미(Temporal Meaning)를 부여하고 상상된 미래(Imagined Futures)를 지능적 행동에 실질적으로 활용할 수 있게 만드는 핵심 메커니즘(Core Mechanism)이다.

##  

## 02.02. Next State Prediction

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

Next-state prediction is the most elementary temporal operation of a predictive world model. Given an estimate of the current state, the model attempts to infer the state that will exist at the next relevant time step. Although this appears simple, it establishes the basic transition mechanism from which multi-step forecasting, imagined rollouts, planning, model-based control, and more sophisticated forms of physical reasoning can later be constructed.

The fundamental relationship can be expressed conceptually as a transition from the current state s

t

​

to the next state s

t+1

​

. In an embodied system, this transition usually depends not only on the state itself but also on the action a

t

​

executed by the agent. The predictive model therefore learns a mapping resembling s

t+1

​

=f(s

t

​

,a

t

​

), where the function represents learned knowledge about how states evolve under actions and environmental dynamics.

A state in this formulation does not need to correspond directly to raw sensor measurements. It may contain geometric structure, object properties, occupancy, velocities, semantic information, robot configuration, contact conditions, or learned latent features. The appropriate state representation depends on the task. A navigation system may emphasize free space and motion, while manipulation requires information about object pose, contact, gripper configuration, and local physical interactions.

Next-state prediction differs from simple observation extrapolation because the objective is to capture meaningful state transitions rather than merely reproduce the appearance of the next sensor frame. Predicting the next camera image can be useful, but a Physical AI system often needs information that is more directly connected to behavior. The model may instead predict future occupancy, object motion, robot pose, semantic changes, latent state, or combinations of these representations.

Temporal resolution determines what "next" means. For a high-frequency control model, the next state may occur only milliseconds after the current state, while a navigation-oriented world model may predict hundreds of milliseconds or several seconds ahead. The chosen interval should correspond to the dynamics of the system and the decisions that depend on the prediction. Excessively short intervals may provide little strategic information, whereas long intervals increase uncertainty and transition complexity.

For static parts of the environment, next-state prediction may primarily preserve information across time. Walls, fixed infrastructure, and stable terrain are expected to remain approximately unchanged. Dynamic components require explicit modeling of motion and interaction. Vehicles, pedestrians, manipulators, moving equipment, doors, loose objects, and the robot itself can change position, velocity, orientation, configuration, or semantic condition between consecutive states.

The agent's own action is especially important because Physical AI participates in the transitions it predicts. Steering changes the future pose of a mobile robot, wheel torque affects velocity, and manipulator commands alter joint configurations and contacts. The next state is therefore partly caused by the agent. Action-conditioned prediction allows the model to represent this relationship and provides a foundation for reasoning about the consequences of alternative control commands.

Environmental dynamics also influence the transition independently of commanded action. A robot may command forward motion while wheel slip reduces displacement, an object may continue moving because of momentum, or another agent may enter the scene unexpectedly. A useful next-state predictor must therefore learn both controllable dynamics associated with the robot and external dynamics generated by the surrounding world.

Sensor observations rarely provide a complete description of the true physical state. Occlusion, noise, limited field of view, asynchronous sensing, and ambiguous measurements create partial observability. Consequently, next-state prediction is often performed from an estimated internal state or belief representation that integrates information across previous observations. Memory can preserve evidence about hidden objects and dynamics that cannot be inferred reliably from the current observation alone.

Next-state models can operate directly in observation space, but learned latent spaces often provide a more compact alternative. An encoder transforms observations into a latent state z

t

​

, a dynamics model predicts z

t+1

​

, and an optional decoder reconstructs task-relevant outputs. This architecture allows prediction to concentrate on temporally meaningful structure rather than spending capacity reproducing every texture, illumination variation, or sensor detail that may be irrelevant to action.

The prediction target may also be factorized into several components. Instead of predicting one monolithic state vector, a system can estimate future ego motion, dynamic-object motion, occupancy, semantic state, contact conditions, and other variables through specialized prediction heads. Such decomposition can make the internal model easier to train and evaluate while allowing different physical quantities to use representations and losses appropriate to their characteristics.

Deterministic next-state prediction assumes that the current information identifies essentially one future state. This approximation can work well for short intervals and highly constrained dynamics. Real environments, however, frequently contain uncertainty. Sensor ambiguity, unobserved forces, stochastic interactions, and unpredictable agents can produce multiple plausible next states. Probabilistic models can therefore predict distributions or alternative hypotheses rather than committing prematurely to a single outcome.

Training a next-state model requires temporally ordered experience. Consecutive observations provide pairs of current and future states, while robot logs can additionally provide the actions executed between them. Through repeated exposure to these transitions, the model learns regularities such as motion continuity, action effects, interaction patterns, and environmental persistence. Large quantities of sequential robot, vehicle, simulation, or video data can therefore support predictive learning without requiring every state variable to be manually annotated.

The training objective depends on the predicted representation. Continuous quantities such as position or velocity may use regression losses, categorical semantic states may use classification objectives, and occupancy predictions may require spatial losses. Latent prediction can compare predicted and target embeddings. In practical world models, several objectives can be combined so that geometric, dynamic, semantic, and representation-level consistency are learned simultaneously.

Prediction error provides an important learning signal. After the model estimates the next state, the actual subsequent observation becomes available and can be compared with the prediction. The discrepancy indicates which aspects of the learned dynamics or internal representation were inaccurate. Repeated prediction and correction can progressively improve the model, making next-state prediction a natural component of continual adaptation in embodied systems.

Accurate next-state prediction also supports anomaly detection. If the observed next state differs substantially from what the model expected, the discrepancy may indicate unusual terrain, actuator degradation, unexpected contact, sensor failure, a novel object, or behavior outside the training distribution. Prediction error can therefore serve not only as a training signal but also as evidence that the system has encountered a condition requiring additional caution.

For control, the model can evaluate a candidate action by predicting the state immediately resulting from that action. Multiple candidate commands can be tested internally, and their predicted next states can be evaluated against safety and task objectives. This provides the smallest useful form of model-based planning: imagine one transition, evaluate its consequence, and select an action before physical execution.

A single next-state predictor can also be applied recursively. Once s

t+1

​

has been predicted, it can be treated as the input for predicting s

t+2

​

, and the process can continue toward increasingly distant futures. This transforms one-step prediction into multi-step rollout. However, errors introduced at each transition can accumulate, which makes the quality and stability of the basic next-state model critical for longer-horizon world modeling.

For Physical AI, next-state prediction is therefore more than a narrow forecasting task. It represents the fundamental learned transition operator that connects states across time and actions to consequences. By repeatedly learning what follows from the current physical situation, the system develops an internal approximation of environmental dynamics that can support anticipation, control, planning, adaptation, and increasingly complex reasoning about future physical states.

At its simplest, the process can be viewed as a continuous cycle: observe the environment, construct the current internal state, incorporate the intended action, predict the next state, observe what actually occurs, measure the prediction error, and update the model when necessary. Repeated across large amounts of embodied experience, this cycle provides one of the basic mechanisms through which a Physical AI system can learn how the world changes rather than merely recognize what the world currently contains.

다음 상태 예측(Next-State Prediction)은 예측형 월드 모델(Predictive World Model)의 가장 기본적인 시간적 연산(Temporal Operation)이다. 현재 상태(Current State)에 대한 추정값이 주어지면 모델은 다음의 의미 있는 시간 단계(Time Step)에 존재할 상태를 추론한다. 겉보기에는 단순하지만, 이러한 과정은 이후 다단계 예측(Multi-Step Forecasting), 상상 롤아웃(Imagined Rollouts), 계획(Planning), 모델 기반 제어(Model-Based Control), 그리고 더욱 정교한 물리적 추론(Physical Reasoning)을 구축하기 위한 기본적인 전이 메커니즘(Transition Mechanism)을 형성한다.

기본적인 관계는 현재 상태 s

t

​

에서 다음 상태 s

t+1

​

로의 전이(Transition)로 표현할 수 있다. 체화 시스템(Embodied System)에서 이러한 전이는 일반적으로 상태 자체뿐만 아니라 에이전트(Agent)가 수행한 행동 a

t

​

에도 의존한다. 따라서 예측 모델(Predictive Model)은 s

t+1

​

=f(s

t

​

,a

t

​

)와 유사한 매핑(Mapping)을 학습하며, 여기에서 함수는 행동과 환경 동역학(Environmental Dynamics)에 따라 상태가 어떻게 변화하는지에 대한 학습된 지식을 나타낸다.

이러한 구성에서 상태(State)는 원시 센서 측정값(Raw Sensor Measurements)에 직접 대응할 필요가 없다. 상태에는 기하학적 구조(Geometric Structure), 객체 속성(Object Properties), 점유 상태(Occupancy), 속도(Velocities), 의미 정보(Semantic Information), 로봇 구성(Robot Configuration), 접촉 조건(Contact Conditions), 또는 학습된 잠재 특징(Learned Latent Features)이 포함될 수 있다. 적절한 상태 표현(State Representation)은 과업(Task)에 따라 달라지며, 내비게이션 시스템(Navigation System)은 자유 공간과 움직임을 강조하는 반면 조작(Manipulation)은 객체 자세, 접촉, 그리퍼 구성, 국소적인 물리적 상호작용에 관한 정보를 필요로 한다.

다음 상태 예측(Next-State Prediction)은 단순한 관측 외삽(Observation Extrapolation)과 다르다. 그 목적이 단순히 다음 센서 프레임(Sensor Frame)의 모습을 재현하는 것이 아니라 의미 있는 상태 전이(State Transition)를 포착하는 것이기 때문이다. 다음 카메라 영상(Camera Image)을 예측하는 것도 유용할 수 있지만, 피지컬 AI(Physical AI) 시스템에서는 행동과 더욱 직접적으로 연결된 정보가 필요한 경우가 많다. 따라서 모델은 미래 점유 상태(Future Occupancy), 객체 움직임(Object Motion), 로봇 자세(Robot Pose), 의미적 변화(Semantic Changes), 잠재 상태(Latent State), 또는 이러한 표현의 조합을 예측할 수 있다.

시간 해상도(Temporal Resolution)는 여기에서 "다음(Next)"이 무엇을 의미하는지를 결정한다. 고주파 제어 모델(High-Frequency Control Model)의 다음 상태는 현재 상태로부터 불과 수 밀리초 후일 수 있지만, 내비게이션 중심 월드 모델(Navigation-Oriented World Model)은 수백 밀리초 또는 수 초 이후를 예측할 수 있다. 선택되는 시간 간격은 시스템 동역학(System Dynamics)과 예측을 사용하는 의사결정에 대응해야 한다. 지나치게 짧은 간격은 전략적 정보를 거의 제공하지 못할 수 있으며, 반대로 긴 간격은 불확실성과 상태 전이의 복잡성을 증가시킨다.

환경의 정적인 부분(Static Components)에 대한 다음 상태 예측은 주로 시간에 걸쳐 정보를 유지하는 역할을 할 수 있다. 벽, 고정된 기반 시설, 안정적인 지형은 대체로 변화하지 않을 것으로 예상된다. 반면 동적인 구성 요소(Dynamic Components)는 움직임과 상호작용에 대한 명시적인 모델링이 필요하다. 차량, 보행자, 매니퓰레이터, 이동 장비, 문, 움직일 수 있는 물체, 그리고 로봇 자체는 연속적인 상태 사이에서 위치, 속도, 방향, 구성 또는 의미적 조건(Semantic Condition)이 변화할 수 있다.

에이전트 자신의 행동(Action)은 특히 중요하다. 피지컬 AI(Physical AI)는 자신이 예측하는 상태 전이에 직접 참여하기 때문이다. 조향(Steering)은 이동 로봇의 미래 자세를 변화시키고, 휠 토크(Wheel Torque)는 속도에 영향을 주며, 매니퓰레이터 명령(Manipulator Commands)은 관절 구성과 접촉 상태를 변화시킨다. 따라서 다음 상태는 부분적으로 에이전트에 의해 발생한다. 행동 조건부 예측(Action-Conditioned Prediction)은 이러한 관계를 표현하고 대안적인 제어 명령(Control Commands)의 결과를 추론하기 위한 기반을 제공한다.

환경 동역학(Environmental Dynamics)은 명령된 행동과 독립적으로도 상태 전이에 영향을 준다. 로봇이 전진 명령을 수행하더라도 휠 슬립(Wheel Slip)으로 실제 이동 거리가 감소할 수 있으며, 물체는 관성(Momentum)에 의해 계속 움직이거나 다른 에이전트가 예상하지 못하게 장면에 진입할 수도 있다. 따라서 유용한 다음 상태 예측기(Next-State Predictor)는 로봇과 관련된 제어 가능한 동역학(Controllable Dynamics)과 주변 세계에서 발생하는 외부 동역학(External Dynamics)을 모두 학습해야 한다.

센서 관측(Sensor Observations)은 실제 물리적 상태(True Physical State)를 완전하게 설명하는 경우가 거의 없다. 가림(Occlusion), 노이즈(Noise), 제한된 시야각(Limited Field of View), 비동기 센싱(Asynchronous Sensing), 모호한 측정값(Ambiguous Measurements)은 부분 관측 가능성(Partial Observability)을 발생시킨다. 따라서 다음 상태 예측은 이전 관측의 정보를 통합하는 추정 내부 상태(Estimated Internal State) 또는 신념 표현(Belief Representation)을 기반으로 수행되는 경우가 많다. 메모리(Memory)는 현재 관측만으로 신뢰성 있게 추론할 수 없는 숨겨진 객체와 동역학에 대한 정보를 유지할 수 있다.

다음 상태 모델(Next-State Model)은 관측 공간(Observation Space)에서 직접 작동할 수도 있지만, 학습된 잠재 공간(Learned Latent Space)은 보다 압축된 대안을 제공한다. 인코더(Encoder)는 관측을 잠재 상태 z

t

​

로 변환하고, 동역학 모델(Dynamics Model)은 z

t+1

​

을 예측하며, 선택적인 디코더(Decoder)는 과업과 관련된 출력을 복원한다. 이러한 구조는 행동과 무관할 수 있는 모든 텍스처(Texture), 조명 변화(Illumination Variation), 센서 세부 정보를 재현하는 데 모델 용량을 소비하는 대신 시간적으로 의미 있는 구조에 예측 능력을 집중하도록 한다.

예측 대상(Prediction Target)은 여러 구성 요소로 분해(Factorization)될 수도 있다. 하나의 거대한 상태 벡터(State Vector)를 예측하는 대신 시스템은 미래의 자차 움직임(Ego Motion), 동적 객체 움직임(Dynamic-Object Motion), 점유 상태(Occupancy), 의미 상태(Semantic State), 접촉 조건(Contact Conditions) 및 기타 변수들을 전문화된 예측 헤드(Prediction Heads)를 통해 추정할 수 있다. 이러한 분해는 내부 모델의 학습과 평가를 쉽게 하며 서로 다른 물리량에 각각의 특성에 적합한 표현과 손실 함수(Loss)를 적용할 수 있게 한다.

결정론적 다음 상태 예측(Deterministic Next-State Prediction)은 현재 정보가 본질적으로 하나의 미래 상태를 결정한다고 가정한다. 이러한 근사는 짧은 시간 간격과 강하게 제약된 동역학에서는 효과적일 수 있다. 그러나 실제 환경은 불확실성(Uncertainty)을 포함한다. 센서의 모호성, 관측되지 않은 힘, 확률적 상호작용(Stochastic Interactions), 예측하기 어려운 에이전트는 여러 개의 가능한 다음 상태를 발생시킬 수 있다. 따라서 확률적 모델(Probabilistic Models)은 하나의 결과에 성급하게 고정하는 대신 확률 분포(Distributions) 또는 여러 대안적 가설(Alternative Hypotheses)을 예측할 수 있다.

다음 상태 모델(Next-State Model)을 학습하려면 시간적으로 순서가 있는 경험(Temporally Ordered Experience)이 필요하다. 연속적인 관측은 현재와 미래 상태의 쌍을 제공하며, 로봇 로그(Robot Logs)는 그 사이에 실행된 행동 정보도 추가로 제공할 수 있다. 모델은 이러한 상태 전이에 반복적으로 노출되면서 움직임의 연속성(Motion Continuity), 행동 효과(Action Effects), 상호작용 패턴(Interaction Patterns), 환경 지속성(Environmental Persistence)과 같은 규칙성을 학습한다. 따라서 대규모 로봇, 차량, 시뮬레이션 또는 비디오 시퀀스 데이터는 모든 상태 변수를 사람이 직접 라벨링하지 않아도 예측 학습(Predictive Learning)을 지원할 수 있다.

학습 목적 함수(Training Objective)는 예측되는 표현의 종류에 따라 달라진다. 위치나 속도 같은 연속적인 물리량(Continuous Quantities)에는 회귀 손실(Regression Loss)을 사용할 수 있으며, 범주형 의미 상태(Categorical Semantic States)에는 분류 목적 함수(Classification Objectives)를 적용할 수 있다. 점유 상태 예측에는 공간 손실(Spatial Loss)이 필요할 수 있으며, 잠재 예측(Latent Prediction)은 예측 임베딩(Predicted Embedding)과 목표 임베딩(Target Embedding)을 비교할 수 있다. 실제 월드 모델에서는 여러 목적 함수를 결합하여 기하학적, 동적, 의미적, 표현 수준의 일관성을 동시에 학습할 수 있다.

예측 오차(Prediction Error)는 중요한 학습 신호(Learning Signal)를 제공한다. 모델이 다음 상태를 추정한 이후 실제 후속 관측(Actual Subsequent Observation)이 입력되면 이를 예측 결과와 비교할 수 있다. 두 상태의 차이는 학습된 동역학 또는 내부 표현에서 어떤 부분이 부정확했는지를 나타낸다. 이러한 예측과 보정(Prediction and Correction)을 반복하면 모델을 점진적으로 개선할 수 있으므로 다음 상태 예측은 체화 시스템의 지속적 적응(Continual Adaptation)을 위한 자연스러운 구성 요소가 된다.

정확한 다음 상태 예측(Next-State Prediction)은 이상 탐지(Anomaly Detection)도 지원한다. 실제로 관측된 다음 상태가 모델이 예상한 상태와 크게 다르다면 이러한 차이는 비정상적인 지형, 액추에이터 성능 저하(Actuator Degradation), 예상하지 못한 접촉, 센서 고장(Sensor Failure), 새로운 객체 또는 학습 분포 밖의 행동(Out-of-Distribution Behavior)을 의미할 수 있다. 따라서 예측 오차는 학습 신호뿐만 아니라 시스템이 추가적인 주의를 필요로 하는 상황에 진입했다는 증거로 활용될 수 있다.

제어(Control) 측면에서 모델은 후보 행동(Candidate Action)에 의해 즉시 발생할 상태를 예측함으로써 해당 행동을 평가할 수 있다. 여러 후보 명령(Candidate Commands)을 내부적으로 시험하고 그에 따른 다음 상태를 안전 및 과업 목표(Safety and Task Objectives)에 따라 평가할 수 있다. 이것은 모델 기반 계획(Model-Based Planning)의 가장 작은 유용한 형태를 제공한다. 즉, 하나의 상태 전이를 상상하고 그 결과를 평가한 다음 실제 물리적 실행 이전에 행동을 선택하는 것이다.

하나의 다음 상태 예측기(Next-State Predictor)는 재귀적으로(Recursively) 적용할 수도 있다. s

t+1

​

이 예측되면 이를 s

t+2

​

를 예측하기 위한 입력으로 사용하고, 이러한 과정을 반복하여 점점 더 먼 미래 상태를 생성할 수 있다. 이를 통해 단일 단계 예측(One-Step Prediction)은 다단계 롤아웃(Multi-Step Rollout)으로 확장된다. 그러나 각 상태 전이에서 발생하는 오류가 누적될 수 있으므로 기본적인 다음 상태 모델의 품질과 안정성은 장기 지평 월드 모델링(Long-Horizon World Modeling)에 결정적으로 중요하다.

따라서 피지컬 AI(Physical AI)에서 다음 상태 예측(Next-State Prediction)은 단순한 예측 과제 이상의 의미를 갖는다. 이것은 시간에 걸쳐 상태들을 연결하고 행동을 그 결과와 연결하는 기본적인 학습 전이 연산자(Learned Transition Operator)를 나타낸다. 현재의 물리적 상황 이후에 무엇이 발생하는지를 반복적으로 학습함으로써 시스템은 환경 동역학(Environmental Dynamics)에 대한 내부 근사 모델(Internal Approximation)을 형성하고, 이를 예상(Anticipation), 제어(Control), 계획(Planning), 적응(Adaptation), 그리고 미래의 물리적 상태에 대한 더욱 복잡한 추론에 활용할 수 있다.

가장 단순한 형태에서 이러한 과정은 연속적인 순환 구조(Continuous Cycle)로 이해할 수 있다. 환경을 관측하고, 현재 내부 상태를 구성하며, 의도된 행동(Intended Action)을 반영하고, 다음 상태를 예측한 뒤, 실제로 발생한 결과를 관측하고, 예측 오차를 측정하며, 필요할 경우 모델을 갱신한다. 이러한 순환이 방대한 체화 경험(Embodied Experience)에 걸쳐 반복되면 피지컬 AI 시스템은 현재 세계에 무엇이 존재하는지만 인식하는 것을 넘어 세계가 어떻게 변화하는지를 학습할 수 있게 된다.

##  

## 02.03. Multi Step Future Prediction

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

Multi-step future prediction extends next-state prediction from a single transition into a sequence of anticipated states. Instead of estimating only what will happen immediately after the current moment, the world model predicts how the environment may evolve across multiple future time steps. This capability allows Physical AI systems to reason beyond immediate reactions and consider the longer-term consequences of motion, interaction, and action.

Conceptually, a multi-step prediction produces a sequence such as (s_{t+1}, s_{t+2}, \\ldots, s_{t+H}), where (H) represents the prediction horizon. Each future state describes an estimate of the world at a progressively later time. Depending on the application, these states may represent robot configuration, object motion, occupancy, geometry, semantic conditions, latent features, or combinations of several physical and contextual variables.

One common approach is recursive or autoregressive rollout. The model first predicts (s_{t+1}) from the current state (s_t), then uses the predicted state to estimate (s_{t+2}), continuing until the desired horizon is reached. This approach reuses the same learned transition mechanism repeatedly, making a next-state predictor capable of generating long trajectories without requiring a separate prediction model for every future time step.

When actions influence the future, the rollout must also incorporate an action sequence. The transition can then be represented as (s_{t+k+1}=f(s_{t+k},a_{t+k})). A candidate sequence of steering commands, velocities, joint commands, or other control inputs can be propagated through the world model. The resulting predicted trajectory describes how the agent and environment may evolve if those actions are actually executed.

Recursive prediction creates an important challenge because predicted states gradually replace observed states as inputs. Even a small error in (s_{t+1}) can influence the estimate of (s_{t+2}), and subsequent errors may compound across the rollout. Long-horizon predictions can therefore drift away from physically plausible futures even when the underlying one-step predictor performs accurately on short transitions.

Error accumulation makes temporal consistency a central requirement of multi-step world modeling. Predicted position, velocity, object identity, occupancy, geometry, and semantic state should evolve coherently rather than changing arbitrarily between future steps. Models must learn not only individually accurate states but also trajectories whose temporal evolution remains compatible with the dynamics and structural constraints of the physical environment.

An alternative to recursive prediction is direct multi-horizon prediction. Instead of repeatedly feeding predicted states back into the model, the system predicts several future horizons directly from a shared current representation. Separate outputs may estimate the world after 0.5, 1, 2, or 5 seconds, for example. This can reduce recursive error propagation, although maintaining consistency among independently predicted future horizons becomes a different challenge.

Multi-step prediction does not require the same temporal resolution throughout the entire horizon. Near-term states may be predicted at high frequency because immediate control requires precise timing, while distant states can use coarser intervals. Such hierarchical temporal resolution can reduce computational cost and reflect the fact that exact details become increasingly uncertain as predictions extend farther into the future.

The appropriate prediction horizon depends strongly on the physical task. Collision avoidance may require detailed predictions over the next few seconds, while autonomous navigation may benefit from longer forecasts of traffic, traversability, or route evolution. Manipulation can require precise short-term predictions of contact dynamics combined with longer predictions describing whether a sequence of interactions will ultimately produce the desired object configuration.

As the horizon increases, uncertainty becomes increasingly important. A single near-term future may be relatively predictable, but many different outcomes can become plausible several seconds later. Other agents can change intentions, objects can interact unexpectedly, and small physical disturbances can alter subsequent states. Multi-step models should therefore represent growing uncertainty rather than presenting distant predictions with unjustified confidence.

This uncertainty can be represented through probabilistic trajectories, multiple future hypotheses, stochastic latent variables, ensembles, or distributions over future states. Instead of predicting one trajectory, a model may maintain several possible futures with different probabilities. Such multimodal prediction is especially important when human behavior, traffic interactions, manipulation outcomes, or partially observed environmental dynamics can produce qualitatively different future developments.

The representation used for long rollouts also matters. Pixel-level prediction can become computationally expensive because every future frame contains large amounts of visual detail. Latent-state prediction compresses observations into representations containing information relevant to dynamics and decision making. The model can then roll these latent states forward efficiently and decode only the quantities required for evaluation, planning, or visualization.

Structured representations provide another practical option. Future bird's-eye-view states, occupancy fields, object tracks, robot poses, semantic maps, or contact states can be predicted directly. Such representations emphasize physically relevant variables and allow planners to evaluate future collision risk, free space, object interaction, or goal achievement without requiring complete reconstruction of future sensory observations.

Memory is particularly important for multi-step prediction under partial observability. The current frame may not reveal the velocity of an object, the existence of an occluded obstacle, or the recent behavior of another agent. Historical observations provide information about these hidden variables. A recurrent state, temporal transformer, state-space model, or other memory mechanism can integrate past evidence before generating future rollouts.

Multi-step prediction can also model interactions among multiple entities. The future trajectory of one object may depend on nearby objects, humans, vehicles, robots, or environmental boundaries. Predicting each entity independently can miss these dependencies. Interaction-aware models instead represent relationships among entities so that future states reflect collision avoidance, cooperation, contact, social behavior, and other coupled dynamics.

Physical constraints can help prevent long rollouts from becoming unrealistic. Kinematic limits, acceleration bounds, collision constraints, conservation relationships, contact rules, and known robot dynamics can restrict the space of plausible futures. Combining learned prediction with physical priors can therefore improve stability, particularly when the model must extrapolate beyond situations frequently represented in its training data.

Training for multi-step prediction should expose the model to more than isolated one-step transitions. A model trained only with perfect observed states as inputs may perform poorly when its own imperfect predictions are used during rollout. Multi-step objectives can evaluate several predicted states simultaneously, encouraging the learned dynamics to remain stable and useful across the entire prediction horizon rather than optimizing only immediate accuracy.

Different future steps may also receive different importance during training. Near-term predictions can be weighted strongly because they are more observable and directly relevant to control, while distant predictions may use uncertainty-aware or representation-level objectives. The training design should reflect the intended operational use of the model rather than assuming that every point in the prediction horizon has identical accuracy requirements.

For planning, multi-step prediction effectively provides an internal simulation capability. A planner can propose several candidate action sequences, roll each sequence forward through the world model, and compare the resulting futures. Candidate trajectories can be evaluated according to progress toward a goal, collision probability, stability, energy use, comfort, manipulation success, or other task-specific objectives before an action sequence is selected.

Model predictive control naturally uses this capability. The system predicts several steps into the future, selects a promising action based on the predicted trajectory, executes only the immediate portion of that plan, and then observes the environment again. The prediction is subsequently recomputed using updated information. This repeated replanning limits the damage caused by long-term prediction errors while retaining the benefits of anticipatory reasoning.

Multi-step future prediction therefore changes the role of a world model from estimating local dynamics to imagining extended consequences. It enables an embodied agent to ask not only what will happen next, but how a situation may unfold over time if particular actions, interactions, and environmental changes occur. The quality of these imagined trajectories directly influences the quality of planning and long-horizon decision making.

For Physical AI, the ultimate objective is not to predict every distant detail perfectly. Rather, the model should preserve enough spatial, temporal, semantic, and physical structure to distinguish useful futures from dangerous or ineffective ones. Multi-step future prediction provides the temporal bridge from immediate state transitions to internal simulation, allowing perception and learned dynamics to support anticipation, planning, control, and increasingly sophisticated physical reasoning.

다단계 미래 예측(Multi-Step Future Prediction)은 다음 상태 예측(Next-State Prediction)을 하나의 전이(Transition)에서 연속적인 예상 상태(Sequence of Anticipated States)로 확장한다. 월드 모델(World Model)은 현재 순간 직후에 무엇이 발생할지만 추정하는 것이 아니라 여러 미래 시간 단계(Future Time Steps)에 걸쳐 환경이 어떻게 변화할지를 예측한다. 이러한 능력을 통해 피지컬 AI(Physical AI) 시스템은 즉각적인 반응을 넘어 움직임, 상호작용, 행동이 가져올 장기적인 결과를 고려할 수 있다.

개념적으로 다단계 예측(Multi-Step Prediction)은 s

t+1

​

,s

t+2

​

,...,s

t+H

​

와 같은 시퀀스를 생성하며, 여기서 H는 예측 지평(Prediction Horizon)을 나타낸다. 각각의 미래 상태(Future State)는 점점 더 먼 미래 시점의 세계에 대한 추정치를 나타낸다. 응용 분야에 따라 이러한 상태는 로봇 구성(Robot Configuration), 객체 움직임(Object Motion), 점유 상태(Occupancy), 기하학(Geometry), 의미적 조건(Semantic Conditions), 잠재 특징(Latent Features), 또는 여러 물리적·맥락적 변수의 조합을 표현할 수 있다.

일반적인 접근 방법 중 하나는 재귀적 또는 자기회귀적 롤아웃(Recursive or Autoregressive Rollout)이다. 모델은 먼저 현재 상태 s

t

​

로부터 s

t+1

​

을 예측하고, 이후 예측된 상태를 이용해 s

t+2

​

를 추정하며, 원하는 예측 지평에 도달할 때까지 이 과정을 반복한다. 이러한 접근은 동일한 학습된 전이 메커니즘(Learned Transition Mechanism)을 반복적으로 사용하므로 각각의 미래 시간 단계마다 별도의 예측 모델을 구성하지 않고도 다음 상태 예측기(Next-State Predictor)를 이용해 긴 궤적(Long Trajectory)을 생성할 수 있다.

행동(Action)이 미래에 영향을 주는 경우 롤아웃(Rollout)은 행동 시퀀스(Action Sequence)도 포함해야 한다. 이때 상태 전이는 s

t+k+1

​

=f(s

t+k

​

,a

t+k

​

)로 표현할 수 있다. 조향 명령(Steering Commands), 속도(Velocities), 관절 명령(Joint Commands), 또는 기타 제어 입력(Control Inputs)의 후보 시퀀스를 월드 모델을 통해 미래 방향으로 전개할 수 있다. 그 결과 생성되는 예측 궤적(Predicted Trajectory)은 이러한 행동이 실제로 실행될 경우 에이전트와 환경이 어떻게 변화할지를 나타낸다.

재귀적 예측(Recursive Prediction)은 예측된 상태가 점차 관측된 상태를 대신하여 입력으로 사용되기 때문에 중요한 문제를 발생시킨다. s

t+1

​

에서 발생한 작은 오류도 s

t+2

​

의 추정에 영향을 미칠 수 있으며, 이후의 오류는 롤아웃 전체에서 누적될 수 있다. 따라서 기본적인 단일 단계 예측기(One-Step Predictor)가 짧은 상태 전이에서는 정확하더라도 장기 지평 예측(Long-Horizon Prediction)은 물리적으로 타당한 미래로부터 점차 벗어날 수 있다.

오차 누적(Error Accumulation)은 시간적 일관성(Temporal Consistency)을 다단계 월드 모델링(Multi-Step World Modeling)의 핵심 요구사항으로 만든다. 예측된 위치(Position), 속도(Velocity), 객체 정체성(Object Identity), 점유 상태(Occupancy), 기하학(Geometry), 의미 상태(Semantic State)는 미래 시간 단계 사이에서 임의로 변화하지 않고 일관성 있게 변화해야 한다. 모델은 개별적으로 정확한 상태뿐 아니라 시간에 따른 변화가 물리적 환경의 동역학과 구조적 제약에 부합하는 궤적(Trajectory)을 학습해야 한다.

재귀적 예측의 대안으로 직접 다중 지평 예측(Direct Multi-Horizon Prediction)을 사용할 수 있다. 예측된 상태를 반복적으로 모델에 다시 입력하는 대신 공유된 현재 표현(Shared Current Representation)으로부터 여러 미래 지평을 직접 예측한다. 예를 들어 0.5초, 1초, 2초, 5초 후의 세계를 각각 추정할 수 있다. 이러한 방식은 재귀적 오류 전파(Recursive Error Propagation)를 감소시킬 수 있지만 독립적으로 예측된 여러 미래 지평 사이의 일관성을 유지해야 하는 새로운 문제가 발생한다.

다단계 예측(Multi-Step Prediction)은 전체 예측 지평에 걸쳐 동일한 시간 해상도(Temporal Resolution)를 사용할 필요가 없다. 즉각적인 제어에는 정확한 시간 정보가 필요하기 때문에 가까운 미래 상태는 높은 빈도(High Frequency)로 예측하고, 먼 미래 상태는 더 거친 시간 간격(Coarser Intervals)을 사용할 수 있다. 이러한 계층적 시간 해상도(Hierarchical Temporal Resolution)는 계산 비용을 줄일 수 있으며 예측이 먼 미래로 확장될수록 정확한 세부 사항의 불확실성이 증가한다는 특성도 반영한다.

적절한 예측 지평(Prediction Horizon)은 물리적 과업(Physical Task)에 크게 의존한다. 충돌 회피(Collision Avoidance)는 향후 몇 초에 대한 상세한 예측이 필요할 수 있으며, 자율 내비게이션(Autonomous Navigation)은 교통, 주행 가능성(Traversability), 경로 변화(Route Evolution)에 대한 더 긴 예측을 활용할 수 있다. 조작(Manipulation)은 접촉 동역학(Contact Dynamics)에 대한 정밀한 단기 예측과 일련의 상호작용이 최종적으로 원하는 객체 구성(Object Configuration)을 만들어낼 수 있는지에 대한 장기 예측을 함께 요구할 수 있다.

예측 지평이 길어질수록 불확실성(Uncertainty)은 더욱 중요해진다. 가까운 미래는 비교적 예측 가능할 수 있지만 몇 초 이후에는 여러 결과가 동시에 가능해질 수 있다. 다른 에이전트는 의도(Intentions)를 변경할 수 있고, 객체는 예상하지 못한 방식으로 상호작용할 수 있으며, 작은 물리적 교란(Physical Disturbances)이 이후의 상태를 변화시킬 수 있다. 따라서 다단계 모델(Multi-Step Model)은 먼 미래의 예측에 근거 없는 확신을 부여하기보다 증가하는 불확실성을 표현해야 한다.

이러한 불확실성은 확률적 궤적(Probabilistic Trajectories), 복수의 미래 가설(Multiple Future Hypotheses), 확률적 잠재 변수(Stochastic Latent Variables), 앙상블(Ensembles), 또는 미래 상태에 대한 확률 분포(Distributions)를 통해 표현할 수 있다. 하나의 궤적만 예측하는 대신 모델은 서로 다른 확률을 가진 여러 가능한 미래를 유지할 수 있다. 이러한 다중 모드 예측(Multimodal Prediction)은 인간 행동, 교통 상호작용, 조작 결과 또는 부분적으로 관측된 환경 동역학이 질적으로 서로 다른 미래를 발생시킬 수 있는 경우 특히 중요하다.

장기 롤아웃(Long Rollout)에 사용되는 표현(Representation)도 중요하다. 픽셀 수준 예측(Pixel-Level Prediction)은 각각의 미래 프레임에 방대한 시각적 세부 정보가 포함되기 때문에 계산 비용이 커질 수 있다. 잠재 상태 예측(Latent-State Prediction)은 관측을 동역학과 의사결정에 관련된 정보를 포함하는 표현으로 압축한다. 이후 모델은 이러한 잠재 상태를 효율적으로 미래 방향으로 전개하고 평가, 계획 또는 시각화에 필요한 물리량만 선택적으로 디코딩(Decoding)할 수 있다.

구조화된 표현(Structured Representation)은 또 다른 실용적인 방법을 제공한다. 미래의 조감도(Bird's-Eye View), 점유 필드(Occupancy Fields), 객체 트랙(Object Tracks), 로봇 자세(Robot Poses), 의미 지도(Semantic Maps), 접촉 상태(Contact States) 등을 직접 예측할 수 있다. 이러한 표현은 물리적으로 중요한 변수에 집중하며 미래의 센서 관측 전체를 완전히 복원하지 않고도 계획기(Planner)가 충돌 위험, 자유 공간, 객체 상호작용 또는 목표 달성 여부를 평가할 수 있게 한다.

메모리(Memory)는 부분 관측 가능성(Partial Observability) 상황에서 다단계 예측을 수행할 때 특히 중요하다. 현재 프레임만으로는 객체의 속도, 가려진 장애물의 존재, 다른 에이전트의 최근 행동을 파악하지 못할 수 있다. 과거 관측(Historical Observations)은 이러한 숨겨진 변수에 관한 정보를 제공한다. 순환 상태(Recurrent State), 시간적 트랜스포머(Temporal Transformer), 상태 공간 모델(State-Space Model) 또는 기타 메모리 메커니즘은 미래 롤아웃을 생성하기 전에 과거의 증거를 통합할 수 있다.

다단계 예측(Multi-Step Prediction)은 여러 개체(Entity) 사이의 상호작용도 모델링할 수 있다. 하나의 객체가 앞으로 이동할 궤적은 주변 객체, 인간, 차량, 로봇 또는 환경 경계(Environmental Boundaries)에 의해 영향을 받을 수 있다. 각 개체를 독립적으로 예측하면 이러한 의존 관계를 놓칠 수 있다. 반면 상호작용 인식 모델(Interaction-Aware Model)은 개체 간 관계를 표현하여 미래 상태가 충돌 회피, 협력(Cooperation), 접촉(Contact), 사회적 행동(Social Behavior), 기타 결합된 동역학(Coupled Dynamics)을 반영하도록 한다.

물리적 제약(Physical Constraints)은 장기 롤아웃이 비현실적으로 변화하는 것을 방지하는 데 도움을 줄 수 있다. 운동학적 한계(Kinematic Limits), 가속도 제한(Acceleration Bounds), 충돌 제약(Collision Constraints), 보존 관계(Conservation Relationships), 접촉 규칙(Contact Rules), 알려진 로봇 동역학(Known Robot Dynamics)은 가능한 미래의 범위를 제한한다. 따라서 학습 기반 예측(Learned Prediction)과 물리적 사전 지식(Physical Priors)을 결합하면 특히 학습 데이터에서 충분히 나타나지 않은 상황으로 외삽(Extrapolation)해야 할 때 안정성을 향상시킬 수 있다.

다단계 예측을 위한 학습(Training)은 모델이 단순히 독립된 단일 단계 전이(Isolated One-Step Transitions)만 경험하도록 해서는 안 된다. 완벽하게 관측된 상태만 입력으로 사용하여 학습된 모델은 실제 롤아웃에서 자신의 불완전한 예측값이 입력될 때 성능이 저하될 수 있다. 다단계 목적 함수(Multi-Step Objectives)는 여러 예측 상태를 동시에 평가하여 학습된 동역학이 즉각적인 정확도만 최적화하는 대신 전체 예측 지평에 걸쳐 안정적이고 유용한 상태를 유지하도록 유도할 수 있다.

학습 과정에서는 서로 다른 미래 시간 단계에 서로 다른 중요도를 부여할 수도 있다. 가까운 미래의 예측은 관측 가능성이 높고 제어와 직접적으로 관련되기 때문에 높은 가중치(Weight)를 적용할 수 있으며, 먼 미래의 예측에는 불확실성 인식 목적 함수(Uncertainty-Aware Objectives) 또는 표현 수준 목적 함수(Representation-Level Objectives)를 사용할 수 있다. 따라서 학습 설계(Training Design)는 예측 지평의 모든 지점에 동일한 정확도를 요구하기보다 모델이 실제로 어떻게 사용될 것인지를 반영해야 한다.

계획(Planning)의 관점에서 다단계 예측은 사실상 내부 시뮬레이션(Internal Simulation) 기능을 제공한다. 계획기는 여러 후보 행동 시퀀스(Candidate Action Sequences)를 제안하고 각각을 월드 모델 내부에서 미래 방향으로 롤아웃한 뒤 생성된 미래를 비교할 수 있다. 후보 궤적은 목표까지의 진행 정도, 충돌 확률(Collision Probability), 안정성(Stability), 에너지 사용량(Energy Use), 승차감 또는 동작의 부드러움(Comfort), 조작 성공 가능성(Manipulation Success), 기타 과업별 목적에 따라 평가할 수 있다.

모델 예측 제어(Model Predictive Control)는 이러한 능력을 자연스럽게 활용한다. 시스템은 여러 단계의 미래를 예측하고, 예측된 궤적을 기반으로 유망한 행동을 선택한 다음, 해당 계획의 즉각적인 일부만 실행하고 환경을 다시 관측한다. 이후 갱신된 정보를 이용하여 예측을 다시 계산한다. 이러한 반복적 재계획(Replanning)은 예상적 추론(Anticipatory Reasoning)의 장점을 유지하면서 장기 예측 오류가 실제 행동에 미치는 영향을 제한한다.

따라서 다단계 미래 예측(Multi-Step Future Prediction)은 월드 모델(World Model)의 역할을 국소적인 동역학(Local Dynamics)을 추정하는 수준에서 장기간에 걸친 결과를 상상하는 수준으로 확장한다. 이를 통해 체화 에이전트(Embodied Agent)는 단순히 다음에 무엇이 일어날지를 묻는 것을 넘어 특정한 행동, 상호작용, 환경 변화가 발생했을 때 상황이 시간에 따라 어떻게 전개될지를 추론할 수 있다. 이러한 상상된 궤적(Imagined Trajectories)의 품질은 계획과 장기 의사결정(Long-Horizon Decision Making)의 품질에 직접적인 영향을 미친다.

피지컬 AI(Physical AI)의 궁극적인 목표는 먼 미래의 모든 세부 사항을 완벽하게 예측하는 것이 아니다. 대신 모델은 유용한 미래와 위험하거나 비효율적인 미래를 구별할 수 있을 정도로 충분한 공간적(Spatial), 시간적(Temporal), 의미적(Semantic), 물리적 구조(Physical Structure)를 유지해야 한다. 다단계 미래 예측은 즉각적인 상태 전이에서 내부 시뮬레이션으로 이어지는 시간적 다리(Temporal Bridge)를 제공하며, 이를 통해 인식(Perception)과 학습된 동역학(Learned Dynamics)이 예상(Anticipation), 계획(Planning), 제어(Control), 그리고 더욱 정교한 물리적 추론(Physical Reasoning)을 지원할 수 있게 한다.

##  

## 02.04. Deterministic and Probabilistic Prediction

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

Deterministic and probabilistic prediction represent two fundamental ways in which a world model can describe the future. A deterministic model predicts a specific future state from the current state and action, whereas a probabilistic model represents a distribution of possible future states. The distinction is essential for Physical AI because real environments contain both predictable physical dynamics and uncertainty that cannot always be resolved from available observations.

In deterministic prediction, the transition is commonly expressed as (s_{t+1}=f(s_t,a_t)). Given the same current state (s_t) and action (a_t), the model produces the same predicted next state (s_{t+1}). This formulation is conceptually simple and computationally efficient, making it attractive when dynamics are stable, observations are sufficiently informative, and uncertainty has limited influence on the decision being made.

Many short-term physical transitions can be approximated effectively using deterministic models. Robot joint motion, vehicle kinematics, actuator response, or object displacement over a sufficiently short interval may follow relatively constrained dynamics. When the system state is accurately estimated and external disturbances are small, a single predicted trajectory can provide useful information for immediate control, collision checking, and local planning.

However, deterministic prediction implicitly compresses uncertainty into one outcome. If several futures are compatible with the current observation, the model may produce an average prediction that does not correspond to any realistic outcome. A pedestrian who may move left or right, for example, should not necessarily be represented as moving straight between those alternatives. This limitation becomes increasingly important as prediction horizons grow and behavioral ambiguity accumulates.

Probabilistic prediction addresses this problem by modeling future states as conditional distributions, conceptually written as (p(s_{t+1}\\mid s_t,a_t)). Instead of asking only which state will occur next, the model estimates which states could occur and how plausible they are. The prediction can therefore express uncertainty directly, allowing downstream planning and control to distinguish highly likely futures from rare but potentially dangerous possibilities.

Uncertainty arises from several sources. Sensor noise, occlusion, limited resolution, incomplete observations, unmodeled physical effects, environmental disturbances, and the behavior of other agents can all make future states uncertain. Even with an accurate model, the available information may be insufficient to determine one outcome. Probabilistic prediction treats this ambiguity as part of the world rather than forcing the model to hide it inside a single estimate.

A useful distinction can be made between aleatoric uncertainty and epistemic uncertainty. Aleatoric uncertainty reflects inherent variability or ambiguity in observations and environmental processes, while epistemic uncertainty reflects limitations in the model's knowledge. The latter can become large when the system encounters unfamiliar terrain, objects, interactions, or operating conditions that were poorly represented in its training experience.

Probabilistic models can represent uncertainty in several ways. They may predict parameters of probability distributions, generate multiple samples, maintain ensembles of models, use stochastic latent variables, or explicitly construct several future hypotheses. The appropriate representation depends on the state space and task. Continuous robot motion may use parametric distributions, while complex human or traffic behavior may require multiple distinct trajectory hypotheses.

Multimodality is particularly important because many physical futures cannot be represented adequately by a single Gaussian-like uncertainty region. Another vehicle may turn left, continue straight, or stop; a human may approach the robot or move away. These alternatives represent qualitatively different modes of behavior. A probabilistic world model should preserve such alternatives rather than averaging them into an artificial intermediate future.

The difference between deterministic and probabilistic prediction becomes more pronounced over multiple time steps. A deterministic rollout typically follows one future trajectory, while a probabilistic rollout can expand into a branching set or distribution of trajectories. Each transition introduces additional uncertainty, causing the space of plausible futures to broaden. Long-horizon prediction therefore requires mechanisms for controlling complexity while preserving decision-relevant alternatives.

Not every source of uncertainty deserves equal computational attention. For Physical AI, the objective is usually not to model every possible future detail but to preserve uncertainty that can influence action. Ambiguity near a collision boundary, uncertainty about terrain support, or several plausible human trajectories may be critical. Small uncertainty in irrelevant visual texture may have little importance for navigation or control.

Deterministic and probabilistic approaches are therefore not mutually exclusive. A practical world model can treat predictable components deterministically while modeling uncertain components probabilistically. Robot kinematics may have a relatively narrow predicted distribution, while nearby human motion may require several hypotheses. Such hybrid prediction allows computation to be concentrated where uncertainty has meaningful consequences for planning and safety.

The choice can also vary with prediction horizon. Immediate dynamics may be predicted almost deterministically because little uncertainty has accumulated, while distant futures require increasingly broad distributions. A world model can therefore transition from precise short-term prediction toward probabilistic long-term forecasting. This reflects the natural structure of physical environments, where confidence generally decreases as predictions extend farther beyond current observations.

State representation strongly affects uncertainty modeling. Pixel-space probabilistic prediction can be extremely complex because uncertainty exists over millions of visual variables. Structured representations such as occupancy, object trajectories, semantic states, or robot configurations can make uncertainty easier to interpret. Latent representations provide another alternative by encoding uncertain future dynamics compactly without reconstructing every possible sensory detail.

Training probabilistic predictors requires objectives that reward accurate distributions rather than only minimizing pointwise prediction error. Likelihood-based objectives, distributional losses, latent-variable objectives, or sample-based criteria can encourage the model to assign probability to plausible outcomes. A successful model should avoid both excessive confidence in incorrect predictions and excessively broad uncertainty that provides little useful information for decision making.

Calibration is therefore an important property of probabilistic world models. If a model reports high confidence, its predictions should usually be correct under comparable conditions. When uncertainty is high, the predicted distribution should appropriately reflect the range of outcomes observed in reality. Poor calibration can be dangerous because a planner may interpret inaccurate confidence estimates as reliable evidence when selecting physical actions.

Uncertainty estimation is closely connected to out-of-distribution detection. When a robot encounters an unfamiliar environment or interaction, epistemic uncertainty may increase because the learned model has insufficient experience to predict reliably. This signal can trigger more conservative behavior, additional sensing, slower motion, fallback control, human intervention, or requests for replanning rather than allowing the system to continue with unjustified confidence.

Planning transforms probabilistic prediction into risk-aware decision making. Instead of evaluating candidate actions only according to their most likely outcomes, the planner can consider distributions of possible consequences. An action with excellent expected progress may be rejected if a low-probability branch leads to severe collision or instability. Probability, cost, uncertainty, and consequence severity can therefore be considered together.

In safety-critical Physical AI, this distinction is especially important. Autonomous vehicles, industrial robots, medical robots, and robots operating around humans cannot assume that the most likely future is the only relevant future. Rare events may carry extremely high costs. Probabilistic world models provide information that enables planners and runtime assurance mechanisms to reason explicitly about margins, confidence, and risk.

Deterministic models nevertheless remain valuable because probabilistic prediction introduces computational cost and additional modeling complexity. For fast control loops with well-characterized dynamics, a deterministic model may be sufficient and substantially more efficient. The architecture should therefore match the uncertainty structure of the task rather than adopting probabilistic modeling everywhere merely because it is theoretically more expressive.

A mature Physical AI world model can combine both perspectives dynamically. When observations are clear and dynamics are familiar, prediction can remain concentrated around a narrow set of outcomes. When sensing becomes ambiguous, interactions become complex, or the environment moves outside familiar conditions, the predicted future can broaden into multiple hypotheses. Prediction then becomes adaptive not only in what it predicts but also in how much uncertainty it represents.

Ultimately, deterministic prediction answers the question, "What future does the model expect?" Probabilistic prediction extends this to, "What futures are possible, and how strongly should each be believed?" Physical intelligence requires both capabilities. Reliable action depends on predicting regular physical evolution efficiently while recognizing when the future is ambiguous, uncertain, or insufficiently understood for a single confident prediction.

결정론적 예측(Deterministic Prediction)과 확률적 예측(Probabilistic Prediction)은 월드 모델(World Model)이 미래를 표현하는 두 가지 기본적인 방식이다. 결정론적 모델(Deterministic Model)은 현재 상태와 행동으로부터 특정한 하나의 미래 상태를 예측하는 반면, 확률적 모델(Probabilistic Model)은 가능한 미래 상태들의 분포(Distribution)를 표현한다. 이러한 구분은 실제 환경이 예측 가능한 물리적 동역학과 현재의 관측만으로는 항상 해소할 수 없는 불확실성(Uncertainty)을 모두 포함한다는 점에서 피지컬 AI(Physical AI)에 매우 중요하다.

결정론적 예측(Deterministic Prediction)에서 상태 전이(Transition)는 일반적으로 s

t+1

​

=f(s

t

​

,a

t

​

)로 표현된다. 동일한 현재 상태 s

t

​

와 행동 a

t

​

가 주어지면 모델은 동일한 다음 상태 s

t+1

​

을 예측한다. 이러한 구성은 개념적으로 단순하고 계산 효율성(Computational Efficiency)이 높기 때문에 동역학이 안정적이고 관측 정보가 충분하며 불확실성이 의사결정에 미치는 영향이 제한적인 상황에서 유용하다.

많은 단기 물리적 전이(Short-Term Physical Transitions)는 결정론적 모델(Deterministic Model)을 이용하여 효과적으로 근사할 수 있다. 로봇 관절 움직임(Robot Joint Motion), 차량 운동학(Vehicle Kinematics), 액추에이터 응답(Actuator Response), 또는 충분히 짧은 시간 동안의 객체 변위(Object Displacement)는 비교적 제한된 동역학을 따를 수 있다. 시스템 상태가 정확하게 추정되고 외부 교란이 작다면 하나의 예측 궤적(Predicted Trajectory)만으로도 즉각적인 제어, 충돌 검사(Collision Checking), 국소 계획(Local Planning)에 유용한 정보를 제공할 수 있다.

그러나 결정론적 예측은 본질적으로 불확실성(Uncertainty)을 하나의 결과로 압축한다. 현재 관측과 일치하는 여러 미래가 존재할 경우 모델은 실제로는 존재하지 않는 평균적인 예측(Average Prediction)을 생성할 수 있다. 예를 들어 보행자가 왼쪽 또는 오른쪽으로 이동할 가능성이 있다면 두 대안의 중간 방향으로 이동한다고 표현하는 것이 반드시 적절하지는 않다. 이러한 한계는 예측 지평(Prediction Horizon)이 길어지고 행동의 모호성(Behavioral Ambiguity)이 누적될수록 더욱 중요해진다.

확률적 예측(Probabilistic Prediction)은 미래 상태를 조건부 확률 분포(Conditional Probability Distribution)로 모델링함으로써 이러한 문제를 해결하며, 개념적으로 p(s

t+1

​

∣s

t

​

,a

t

​

)로 표현할 수 있다. 모델은 단순히 어떤 상태가 다음에 발생할 것인지를 예측하는 것이 아니라 어떤 상태들이 발생할 수 있으며 각각이 얼마나 가능성이 높은지를 추정한다. 따라서 불확실성을 직접 표현하여 후속 계획과 제어가 가능성이 높은 미래와 발생 가능성은 낮지만 잠재적으로 위험한 미래를 구별할 수 있도록 한다.

불확실성(Uncertainty)은 다양한 원인에서 발생한다. 센서 노이즈(Sensor Noise), 가림(Occlusion), 제한된 해상도(Limited Resolution), 불완전한 관측(Incomplete Observations), 모델링되지 않은 물리적 효과(Unmodeled Physical Effects), 환경 교란(Environmental Disturbances), 다른 에이전트의 행동 등이 모두 미래 상태를 불확실하게 만들 수 있다. 모델이 정확하더라도 이용 가능한 정보 자체가 하나의 결과를 결정하기에 부족할 수 있으며, 확률적 예측은 이러한 모호성을 하나의 추정값 속에 숨기지 않고 세계 자체의 특성으로 다룬다.

불확실성은 우연적 불확실성(Aleatoric Uncertainty)과 인식론적 불확실성(Epistemic Uncertainty)으로 구분할 수 있다. 우연적 불확실성은 관측과 환경 과정 자체에 존재하는 본질적인 변동성이나 모호성을 나타내며, 인식론적 불확실성은 모델이 보유한 지식의 한계에서 발생한다. 특히 학습 경험에 충분히 포함되지 않았던 새로운 지형, 객체, 상호작용 또는 운용 조건을 시스템이 만났을 때 인식론적 불확실성이 크게 증가할 수 있다.

확률적 모델(Probabilistic Model)은 여러 방법으로 불확실성을 표현할 수 있다. 확률 분포의 매개변수(Distribution Parameters)를 예측하거나, 여러 샘플(Samples)을 생성하거나, 모델 앙상블(Model Ensembles)을 유지하거나, 확률적 잠재 변수(Stochastic Latent Variables)를 사용하거나, 여러 미래 가설(Future Hypotheses)을 명시적으로 구성할 수 있다. 적절한 표현 방법은 상태 공간(State Space)과 과업에 따라 달라지며, 연속적인 로봇 움직임에는 매개변수화된 분포(Parametric Distribution)를 사용할 수 있는 반면 복잡한 인간이나 교통 행동에는 서로 구별되는 여러 궤적 가설(Trajectory Hypotheses)이 필요할 수 있다.

다중 모드성(Multimodality)은 많은 물리적 미래를 하나의 가우시안 형태 불확실성 영역(Gaussian-Like Uncertainty Region)만으로 적절하게 표현할 수 없다는 점에서 특히 중요하다. 다른 차량은 좌회전하거나 직진하거나 정지할 수 있으며, 인간은 로봇에 접근하거나 반대 방향으로 이동할 수 있다. 이러한 대안들은 질적으로 서로 다른 행동 모드(Behavior Modes)를 나타낸다. 따라서 확률적 월드 모델(Probabilistic World Model)은 이들을 인위적인 중간 미래로 평균화하지 않고 서로 다른 대안으로 유지해야 한다.

결정론적 예측과 확률적 예측의 차이는 여러 시간 단계(Multiple Time Steps)에 걸쳐 더욱 분명해진다. 결정론적 롤아웃(Deterministic Rollout)은 일반적으로 하나의 미래 궤적을 따라가지만, 확률적 롤아웃(Probabilistic Rollout)은 분기되는 여러 궤적 또는 궤적 분포로 확장될 수 있다. 각각의 상태 전이는 추가적인 불확실성을 발생시키므로 가능한 미래의 공간은 점차 넓어진다. 따라서 장기 지평 예측(Long-Horizon Prediction)은 의사결정에 중요한 대안들을 보존하면서 이러한 복잡성을 제어하는 메커니즘을 필요로 한다.

모든 불확실성에 동일한 계산 자원(Computational Attention)을 투입할 필요는 없다. 피지컬 AI(Physical AI)의 목표는 일반적으로 가능한 모든 미래의 세부 사항을 모델링하는 것이 아니라 행동에 영향을 줄 수 있는 불확실성을 보존하는 것이다. 충돌 경계(Collision Boundary) 주변의 모호성, 지형 지지력(Terrain Support)에 대한 불확실성, 인간의 여러 가능한 이동 궤적은 매우 중요할 수 있다. 반면 행동과 무관한 시각적 텍스처(Visual Texture)의 작은 불확실성은 내비게이션이나 제어에서 중요성이 낮을 수 있다.

따라서 결정론적 접근(Deterministic Approach)과 확률적 접근(Probabilistic Approach)은 서로 배타적이지 않다. 실제적인 월드 모델은 예측 가능한 구성 요소를 결정론적으로 처리하면서 불확실한 구성 요소는 확률적으로 모델링할 수 있다. 로봇 운동학(Robot Kinematics)은 비교적 좁은 예측 분포를 가질 수 있는 반면 주변 인간의 움직임에는 여러 가설이 필요할 수 있다. 이러한 하이브리드 예측(Hybrid Prediction)은 불확실성이 계획과 안전에 실질적인 영향을 미치는 부분에 계산 자원을 집중할 수 있도록 한다.

선택되는 예측 방식은 예측 지평(Prediction Horizon)에 따라서도 달라질 수 있다. 즉각적인 동역학(Immediate Dynamics)은 불확실성이 거의 누적되지 않았기 때문에 거의 결정론적으로 예측할 수 있지만, 먼 미래는 점점 넓어지는 확률 분포를 필요로 한다. 따라서 월드 모델은 정밀한 단기 예측(Short-Term Prediction)에서 확률적인 장기 예측(Long-Term Forecasting)으로 점진적으로 전환할 수 있다. 이는 현재 관측으로부터 멀어질수록 일반적으로 예측 신뢰도가 감소하는 물리적 환경의 자연스러운 특성을 반영한다.

상태 표현(State Representation)은 불확실성 모델링에 큰 영향을 미친다. 픽셀 공간 확률 예측(Pixel-Space Probabilistic Prediction)은 수백만 개의 시각적 변수에 걸쳐 불확실성이 존재하기 때문에 매우 복잡해질 수 있다. 점유 상태(Occupancy), 객체 궤적(Object Trajectories), 의미 상태(Semantic States), 로봇 구성(Robot Configurations)과 같은 구조화된 표현(Structured Representations)은 불확실성을 보다 쉽게 해석할 수 있도록 한다. 잠재 표현(Latent Representation)은 가능한 모든 센서 세부 사항을 복원하지 않고 불확실한 미래 동역학을 압축하여 표현하는 또 다른 방법을 제공한다.

확률적 예측기(Probabilistic Predictor)를 학습하려면 단순히 점별 예측 오차(Pointwise Prediction Error)를 최소화하는 것이 아니라 정확한 확률 분포를 보상하는 목적 함수(Objective)가 필요하다. 우도 기반 목적 함수(Likelihood-Based Objectives), 분포적 손실(Distributional Losses), 잠재 변수 목적 함수(Latent-Variable Objectives), 샘플 기반 기준(Sample-Based Criteria) 등을 이용하여 모델이 실제로 가능한 결과에 적절한 확률을 할당하도록 할 수 있다. 성공적인 모델은 잘못된 예측에 지나치게 높은 확신을 갖는 것과 의사결정에 거의 도움이 되지 않을 정도로 지나치게 넓은 불확실성을 표현하는 것을 모두 피해야 한다.

따라서 보정(Calibration)은 확률적 월드 모델(Probabilistic World Model)의 중요한 특성이다. 모델이 높은 신뢰도(Confidence)를 보고한다면 유사한 조건에서 해당 예측은 실제로 높은 확률로 정확해야 한다. 불확실성이 높은 경우에는 예측 분포가 현실에서 관측되는 결과의 범위를 적절하게 반영해야 한다. 잘못 보정된 모델(Poorly Calibrated Model)은 계획기가 부정확한 신뢰도 추정치를 신뢰할 수 있는 근거로 해석하여 물리적 행동을 선택할 수 있기 때문에 위험할 수 있다.

불확실성 추정(Uncertainty Estimation)은 분포 외 탐지(Out-of-Distribution Detection)와 밀접하게 연결된다. 로봇이 익숙하지 않은 환경이나 상호작용을 경험하면 학습된 모델이 신뢰성 있게 예측할 충분한 경험을 갖지 못했기 때문에 인식론적 불확실성(Epistemic Uncertainty)이 증가할 수 있다. 이러한 신호는 시스템이 근거 없는 확신을 가지고 계속 행동하는 대신 보다 보수적인 행동, 추가 센싱(Additional Sensing), 감속, 폴백 제어(Fallback Control), 인간 개입(Human Intervention), 또는 재계획(Replanning)을 수행하도록 유도할 수 있다.

계획(Planning)은 확률적 예측을 위험 인식 의사결정(Risk-Aware Decision Making)으로 전환한다. 계획기는 후보 행동을 가장 가능성이 높은 결과만을 기준으로 평가하는 대신 가능한 결과들의 분포를 고려할 수 있다. 기대되는 진행 성능(Expected Progress)이 매우 좋은 행동이라도 낮은 확률의 분기에서 심각한 충돌이나 불안정성이 발생한다면 거부될 수 있다. 따라서 확률(Probability), 비용(Cost), 불확실성(Uncertainty), 결과의 심각도(Consequence Severity)를 함께 고려할 수 있다.

안전 중요 피지컬 AI(Safety-Critical Physical AI)에서는 이러한 구분이 특히 중요하다. 자율주행 차량(Autonomous Vehicles), 산업용 로봇(Industrial Robots), 의료 로봇(Medical Robots), 인간 주변에서 작동하는 로봇은 가장 가능성이 높은 미래만이 유일하게 중요한 미래라고 가정할 수 없다. 발생 가능성이 낮은 사건이라도 비용이나 피해가 매우 클 수 있다. 확률적 월드 모델은 계획기와 런타임 보증 메커니즘(Runtime Assurance Mechanisms)이 안전 여유(Margins), 신뢰도, 위험을 명시적으로 추론할 수 있는 정보를 제공한다.

그럼에도 결정론적 모델(Deterministic Model)은 여전히 중요하다. 확률적 예측은 추가적인 계산 비용(Computational Cost)과 모델링 복잡성(Modeling Complexity)을 발생시키기 때문이다. 동역학이 충분히 잘 알려진 고속 제어 루프(Fast Control Loop)에서는 결정론적 모델만으로도 충분할 수 있으며 훨씬 높은 계산 효율성을 제공할 수 있다. 따라서 이론적으로 표현력이 높다는 이유만으로 모든 영역에 확률적 모델링을 적용하기보다는 과업의 불확실성 구조(Uncertainty Structure)에 적합한 아키텍처를 선택해야 한다.

성숙한 피지컬 AI 월드 모델(Physical AI World Model)은 두 가지 관점을 동적으로 결합할 수 있다. 관측이 명확하고 동역학이 익숙한 상황에서는 예측을 좁은 범위의 결과에 집중할 수 있다. 반대로 센싱이 모호해지고 상호작용이 복잡해지거나 환경이 익숙한 조건에서 벗어나면 예측된 미래를 여러 가설로 확장할 수 있다. 이 경우 예측은 무엇을 예측할 것인지뿐만 아니라 얼마나 많은 불확실성을 표현할 것인지에서도 적응적(Adaptive)이 된다.

궁극적으로 결정론적 예측(Deterministic Prediction)은 "모델이 어떤 미래를 예상하는가?"라는 질문에 답한다. 확률적 예측(Probabilistic Prediction)은 이를 "어떤 미래들이 가능하며 각각을 어느 정도 신뢰해야 하는가?"라는 질문으로 확장한다. 물리적 지능(Physical Intelligence)은 두 능력을 모두 필요로 한다. 신뢰성 있는 행동은 규칙적인 물리적 변화를 효율적으로 예측하는 동시에 미래가 모호하거나 불확실하거나 하나의 확신 있는 예측을 하기에는 충분히 이해되지 않은 상황을 인식할 수 있어야 하기 때문이다.

##  

## 02.05. Autoregressive Prediction

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

Autoregressive prediction is a fundamental mechanism for extending a world model from one-step prediction to sequences of future states. The central idea is simple: the output predicted at one time step becomes part of the input used to predict the next. By repeatedly applying the same predictive process, a model can generate an evolving trajectory of states and simulate how the world may unfold over time.

For a state-based world model, the process can be expressed as (s_{t+1}=f(s_t)), followed by (s_{t+2}=f(\\hat{s}_{t+1})), and continuing recursively toward a prediction horizon (H). The symbol (\\hat{s}) emphasizes that later predictions depend increasingly on previously predicted states rather than directly observed states. This recursive dependency is the defining characteristic of autoregressive future prediction.

In Physical AI, actions must usually be included in the transition. The model can therefore take the form (\\hat{s}\*{t+1}=f(s_t,a_t)), followed by (\\hat{s}\*{t+2}=f(\\hat{s}\*{t+1},a\*{t+1})). Given a sequence of candidate actions, the world model can roll forward repeatedly and estimate the physical consequences associated with that sequence. This turns a learned transition model into an internal simulator for planning and control.

Autoregressive prediction can operate over many forms of state representation. The predicted variable may be an image frame, bird's-eye-view representation, occupancy state, object configuration, semantic feature, robot pose, or learned latent vector. The essential requirement is that the predicted representation contains sufficient information to serve as the context for predicting subsequent states.

Latent autoregressive prediction is particularly attractive for world models because repeatedly generating high-dimensional sensor observations can be computationally expensive. An encoder can transform observations into a compact latent state (z_t), after which a dynamics model predicts (z_{t+1}, z_{t+2}, \\ldots). Planning can then operate directly on latent trajectories, while decoders or task heads extract only the information needed for control, evaluation, or interpretation.

Temporal context can extend beyond the immediately preceding state. Instead of predicting the future solely from (s_t), a model may condition on a sequence such as (s_{t-n},\\ldots,s_t). Recurrent networks, temporal convolution, transformers, and state-space models can summarize this history. Longer context can help infer velocity, acceleration, behavioral trends, hidden states, and other temporal properties that cannot be determined reliably from a single observation.

Autoregressive models are naturally compatible with causal temporal structure. Predictions at time (t+k) depend only on information available from the present and preceding predicted states, not on observations from the unknown future. This causal ordering makes autoregressive modeling suitable for online Physical AI systems, where future sensor measurements are unavailable when a robot must decide what action to execute.

A major advantage of the autoregressive approach is architectural reuse. A model trained to predict a transition can be applied repeatedly to generate predictions over different horizons. The same dynamics function can support short-term control, several-step trajectory evaluation, and longer imagined rollouts. This provides a conceptually unified mechanism for connecting next-state prediction with multi-step future reasoning.

The principal weakness is error accumulation. During the first prediction, the model receives an observed or well-estimated current state. During later steps, however, it receives its own imperfect outputs. Small errors in position, velocity, occupancy, or latent representation can therefore influence subsequent predictions. After many recursive transitions, the predicted trajectory may drift substantially from the physically correct evolution.

This problem is related to the difference between training and inference conditions. During training, the model may receive true historical states when learning each next transition, a strategy often associated with teacher forcing. During autonomous rollout, those true future states are unavailable, so the model must condition on its own predictions. The resulting distribution mismatch can make long autoregressive rollouts significantly less stable than one-step validation performance suggests.

Training strategies can reduce this mismatch by exposing the model to imperfect or self-generated states. Multi-step rollout losses can evaluate predictions several steps into the future rather than optimizing only the immediate next state. Other approaches can gradually replace ground-truth inputs with model-generated predictions during training. The objective is to make the dynamics model robust to the kinds of errors it will encounter during actual recursive inference.

Temporal consistency is equally important. A successful autoregressive rollout should not merely produce individually plausible states; the sequence should represent a coherent evolution of the same world. Objects should maintain identity, trajectories should change smoothly when appropriate, robot motion should respect kinematic limits, and occupancy or semantic structure should evolve consistently with interactions and physical dynamics.

Physical priors can improve autoregressive stability. Known kinematic relationships, actuator constraints, collision rules, contact conditions, conservation principles, or approximate analytical dynamics can restrict unrealistic transitions. A hybrid model can therefore combine learned residual or environmental dynamics with known physical structure, reducing the burden on the neural predictor and helping long rollouts remain within plausible regions of state space.

Uncertainty becomes progressively more important as autoregressive prediction continues. Because each predicted state influences the next, uncertainty should propagate through the rollout rather than disappear after each transition. A probabilistic autoregressive model can represent distributions over future states or generate multiple sampled trajectories, allowing uncertainty to expand naturally as the prediction moves farther from observed evidence.

When the future is multimodal, autoregressive models must avoid collapsing distinct possibilities into a single averaged trajectory. Different samples or latent hypotheses can represent alternative developments such as a pedestrian stopping or continuing, a vehicle turning or proceeding straight, or an object remaining stable or slipping after contact. Each hypothesis can then evolve autoregressively as its own internally consistent future.

Autoregressive prediction is closely related to transformer-based sequence modeling. A transformer can represent states, observations, actions, or multimodal information as temporal tokens and predict subsequent tokens under causal attention. The same general principle used to predict the next element in a sequence can therefore be extended to sequences representing physical states and actions, although the representation must preserve information relevant to physical dynamics.

For robotics, an autoregressive rollout becomes particularly useful when combined with candidate action sequences. A planner can propose several control sequences, predict the resulting state trajectories, and evaluate them according to goal progress, collision risk, stability, energy consumption, or other criteria. The model effectively answers a sequence of conditional questions about what may happen if particular actions are executed over time.

Model predictive control can limit the consequences of autoregressive drift. Instead of trusting a long predicted trajectory and executing the entire action sequence, the controller predicts multiple future steps, selects a plan, executes only the first action or short segment, and observes the world again. The autoregressive rollout is then restarted from an updated real state, repeatedly anchoring prediction to new sensory evidence.

The computational cost of autoregressive inference is another consideration. Because future steps are generated sequentially, prediction of (s_{t+k+1}) generally waits for (s_{t+k}). Long horizons can therefore increase latency, especially when the internal representation or dynamics network is large. Parallel or direct multi-horizon prediction can reduce this sequential dependency, creating an important architectural tradeoff between recursive flexibility and inference speed.

Despite these limitations, autoregressive prediction remains a natural foundation for predictive world models because physical processes themselves evolve sequentially. Current conditions influence subsequent conditions, actions modify those transitions, and newly produced states become the starting point for later evolution. Autoregressive modeling mirrors this temporal structure by repeatedly transforming a representation of the present into representations of progressively more distant futures.

For Physical AI, its importance lies in transforming a local transition model into a mechanism for imagination. A robot can use repeated predictions to explore what may happen before committing to physical action. Combined with memory, action conditioning, uncertainty estimation, physical constraints, and continual replanning, autoregressive prediction provides a practical bridge from next-state learning to trajectory forecasting, internal simulation, and long-horizon decision making.

자기회귀적 예측(Autoregressive Prediction)은 월드 모델(World Model)을 단일 단계 예측(One-Step Prediction)에서 연속적인 미래 상태 시퀀스(Sequence of Future States)로 확장하는 기본적인 메커니즘이다. 핵심 개념은 단순하다. 한 시간 단계에서 예측된 출력이 다음 시간 단계를 예측하기 위한 입력의 일부가 된다. 동일한 예측 과정을 반복적으로 적용함으로써 모델은 시간에 따라 변화하는 상태 궤적(State Trajectory)을 생성하고 세계가 앞으로 어떻게 전개될지를 시뮬레이션할 수 있다.

상태 기반 월드 모델(State-Based World Model)에서 이 과정은 s

t+1

​

=f(s

t

​

)로 표현할 수 있으며, 이후 s

t+2

​

=f(

s

\^

t+1

​

)로 이어지고 예측 지평(Prediction Horizon) H까지 재귀적으로 계속된다. 기호

s

\^

는 미래로 갈수록 예측이 직접 관측된 상태가 아니라 이전 단계에서 예측된 상태에 점점 더 의존한다는 것을 강조한다. 이러한 재귀적 의존성(Recursive Dependency)이 자기회귀적 미래 예측(Autoregressive Future Prediction)의 핵심적인 특징이다.

피지컬 AI(Physical AI)에서는 일반적으로 행동(Action)이 상태 전이에 포함되어야 한다. 따라서 모델은

s

\^

t+1

​

=f(s

t

​

,a

t

​

)의 형태를 취할 수 있으며, 이후

s

\^

t+2

​

=f(

s

\^

t+1

​

,a

t+1

​

)로 이어진다. 후보 행동 시퀀스(Candidate Action Sequence)가 주어지면 월드 모델은 반복적으로 미래 방향으로 롤아웃(Rollout)하여 해당 행동 시퀀스와 관련된 물리적 결과를 추정할 수 있다. 이를 통해 학습된 전이 모델(Learned Transition Model)은 계획과 제어를 위한 내부 시뮬레이터(Internal Simulator)로 전환된다.

자기회귀적 예측(Autoregressive Prediction)은 다양한 형태의 상태 표현(State Representation)에 적용할 수 있다. 예측되는 변수는 이미지 프레임(Image Frame), 조감도 표현(Bird's-Eye-View Representation), 점유 상태(Occupancy State), 객체 구성(Object Configuration), 의미 특징(Semantic Feature), 로봇 자세(Robot Pose), 또는 학습된 잠재 벡터(Learned Latent Vector)가 될 수 있다. 핵심적인 요구사항은 예측된 표현이 이후 상태를 다시 예측하기 위한 맥락(Context)으로 사용될 수 있을 정도로 충분한 정보를 포함하는 것이다.

잠재 자기회귀적 예측(Latent Autoregressive Prediction)은 고차원 센서 관측(High-Dimensional Sensor Observations)을 반복적으로 생성하는 데 많은 계산 비용이 필요하기 때문에 월드 모델에 특히 유용하다. 인코더(Encoder)는 관측을 압축된 잠재 상태 z

t

​

로 변환하고, 이후 동역학 모델(Dynamics Model)은 z

t+1

​

,z

t+2

​

,...를 예측한다. 계획은 잠재 궤적(Latent Trajectory)에서 직접 수행할 수 있으며, 디코더(Decoder)나 과업 헤드(Task Head)는 제어, 평가 또는 해석에 필요한 정보만 추출할 수 있다.

시간적 맥락(Temporal Context)은 바로 직전의 상태보다 더 긴 범위로 확장될 수 있다. 모델은 s

t

​

만을 이용해 미래를 예측하는 대신 s

t−n

​

,...,s

t

​

와 같은 상태 시퀀스를 조건으로 사용할 수 있다. 순환 신경망(Recurrent Network), 시간적 합성곱(Temporal Convolution), 트랜스포머(Transformer), 상태 공간 모델(State-Space Model)은 이러한 과거 정보를 요약할 수 있다. 더 긴 맥락은 단일 관측만으로 신뢰성 있게 결정하기 어려운 속도, 가속도, 행동 추세, 숨겨진 상태 등의 시간적 특성을 추론하는 데 도움을 준다.

자기회귀적 모델(Autoregressive Model)은 인과적 시간 구조(Causal Temporal Structure)와 자연스럽게 호환된다. t+k 시점의 예측은 알 수 없는 미래의 관측이 아니라 현재까지 이용 가능한 정보와 이전에 예측된 상태에만 의존한다. 이러한 인과적 순서(Causal Ordering)는 로봇이 어떤 행동을 실행할지 결정하는 시점에 미래 센서 측정값을 이용할 수 없는 온라인 피지컬 AI(Online Physical AI) 시스템에 자기회귀적 모델링을 적합하게 만든다.

자기회귀적 접근법(Autoregressive Approach)의 주요 장점 중 하나는 아키텍처 재사용(Architectural Reuse)이다. 하나의 상태 전이를 예측하도록 학습된 모델을 반복적으로 적용하여 서로 다른 예측 지평에 대한 미래를 생성할 수 있다. 동일한 동역학 함수(Dynamics Function)가 단기 제어(Short-Term Control), 여러 단계의 궤적 평가(Trajectory Evaluation), 장기 상상 롤아웃(Long Imagined Rollout)을 지원할 수 있다. 이를 통해 다음 상태 예측과 다단계 미래 추론(Multi-Step Future Reasoning)을 하나의 통합된 메커니즘으로 연결할 수 있다.

가장 중요한 약점은 오차 누적(Error Accumulation)이다. 첫 번째 예측에서는 모델이 실제로 관측되었거나 정확하게 추정된 현재 상태를 입력으로 받는다. 그러나 이후 단계에서는 자신의 불완전한 예측 결과를 입력으로 사용한다. 따라서 위치, 속도, 점유 상태, 잠재 표현에서 발생한 작은 오류가 이후 예측에 영향을 미칠 수 있다. 많은 재귀적 전이가 반복되면 예측 궤적이 물리적으로 정확한 변화 과정에서 크게 벗어날 수 있다.

이 문제는 학습 조건(Training Conditions)과 추론 조건(Inference Conditions)의 차이와 관련된다. 학습 과정에서 모델은 각각의 다음 상태 전이를 학습할 때 실제 과거 상태를 입력으로 받을 수 있으며, 이러한 전략은 일반적으로 교사 강요(Teacher Forcing)와 관련된다. 그러나 자율 롤아웃(Autonomous Rollout)에서는 실제 미래 상태를 사용할 수 없으므로 모델이 자신의 예측을 조건으로 사용해야 한다. 이러한 분포 불일치(Distribution Mismatch)로 인해 장기 자기회귀적 롤아웃은 단일 단계 검증 성능(One-Step Validation Performance)이 보여주는 것보다 훨씬 불안정해질 수 있다.

학습 전략(Training Strategy)은 모델을 불완전하거나 스스로 생성한 상태에 노출함으로써 이러한 불일치를 줄일 수 있다. 다단계 롤아웃 손실(Multi-Step Rollout Loss)은 바로 다음 상태만 최적화하는 대신 여러 단계 미래의 예측을 평가할 수 있다. 다른 접근법에서는 학습 과정에서 실제 정답 입력(Ground-Truth Input)을 모델이 생성한 예측으로 점진적으로 대체할 수 있다. 목적은 실제 재귀적 추론 과정에서 발생할 수 있는 종류의 오류에 동역학 모델이 강건하도록 만드는 것이다.

시간적 일관성(Temporal Consistency)도 마찬가지로 중요하다. 성공적인 자기회귀적 롤아웃은 각각의 상태가 개별적으로 그럴듯하게 보이는 것만으로 충분하지 않으며, 전체 시퀀스가 동일한 세계의 일관된 변화 과정을 표현해야 한다. 객체는 정체성(Object Identity)을 유지해야 하고, 궤적은 필요한 경우 부드럽게 변화해야 하며, 로봇 움직임은 운동학적 한계(Kinematic Limits)를 준수하고, 점유 상태나 의미 구조는 상호작용 및 물리적 동역학과 일관되게 변화해야 한다.

물리적 사전 지식(Physical Priors)은 자기회귀적 예측의 안정성을 향상시킬 수 있다. 알려진 운동학적 관계(Kinematic Relationships), 액추에이터 제약(Actuator Constraints), 충돌 규칙(Collision Rules), 접촉 조건(Contact Conditions), 보존 원리(Conservation Principles), 또는 근사적인 해석적 동역학(Analytical Dynamics)을 이용하여 비현실적인 상태 전이를 제한할 수 있다. 따라서 하이브리드 모델(Hybrid Model)은 학습된 잔차 또는 환경 동역학과 알려진 물리적 구조를 결합하여 신경망 예측기의 부담을 줄이고 장기 롤아웃이 타당한 상태 공간 영역을 유지하도록 할 수 있다.

자기회귀적 예측이 계속될수록 불확실성(Uncertainty)은 점점 더 중요해진다. 각각의 예측 상태가 다음 상태에 영향을 주기 때문에 불확실성 역시 매 상태 전이 이후 사라지는 것이 아니라 롤아웃 전체를 따라 전파되어야 한다. 확률적 자기회귀 모델(Probabilistic Autoregressive Model)은 미래 상태에 대한 확률 분포를 표현하거나 여러 개의 샘플 궤적(Sampled Trajectories)을 생성하여 예측이 관측된 증거에서 멀어질수록 불확실성이 자연스럽게 증가하도록 할 수 있다.

미래가 다중 모드(Multimodal)인 경우 자기회귀적 모델은 서로 다른 가능성을 하나의 평균 궤적(Averaged Trajectory)으로 붕괴시키지 않아야 한다. 서로 다른 샘플이나 잠재 가설(Latent Hypotheses)을 통해 보행자가 멈추거나 계속 이동하는 경우, 차량이 회전하거나 직진하는 경우, 물체가 접촉 후 안정적으로 유지되거나 미끄러지는 경우 등의 대안적 미래를 표현할 수 있다. 이후 각각의 가설은 독립적으로 내부 일관성을 유지하는 미래로 자기회귀적으로 전개될 수 있다.

자기회귀적 예측은 트랜스포머 기반 시퀀스 모델링(Transformer-Based Sequence Modeling)과 밀접한 관련이 있다. 트랜스포머는 상태, 관측, 행동 또는 멀티모달 정보(Multimodal Information)를 시간적 토큰(Temporal Tokens)으로 표현하고 인과적 어텐션(Causal Attention)을 이용하여 후속 토큰을 예측할 수 있다. 따라서 시퀀스에서 다음 요소를 예측하는 일반적인 원리를 물리적 상태와 행동을 표현하는 시퀀스로 확장할 수 있지만, 사용되는 표현은 물리적 동역학과 관련된 정보를 보존해야 한다.

로보틱스(Robotics)에서 자기회귀적 롤아웃은 후보 행동 시퀀스(Candidate Action Sequences)와 결합될 때 특히 유용하다. 계획기(Planner)는 여러 제어 시퀀스를 제안하고 그에 따른 상태 궤적을 예측한 뒤 목표 진행도(Goal Progress), 충돌 위험(Collision Risk), 안정성(Stability), 에너지 소비(Energy Consumption) 또는 기타 기준에 따라 평가할 수 있다. 모델은 특정 행동들이 시간에 따라 실행될 경우 어떤 일이 발생할 수 있는지에 관한 연속적인 조건부 질문에 답하는 역할을 한다.

모델 예측 제어(Model Predictive Control)는 자기회귀적 드리프트(Autoregressive Drift)의 영향을 제한할 수 있다. 긴 예측 궤적 전체를 신뢰하고 전체 행동 시퀀스를 한 번에 실행하는 대신 제어기는 여러 미래 단계를 예측하고 계획을 선택한 다음 첫 번째 행동 또는 짧은 구간만 실행한 후 세계를 다시 관측한다. 이후 갱신된 실제 상태에서 자기회귀적 롤아웃을 다시 시작하여 새로운 센서 증거에 예측을 반복적으로 고정(Anchoring)한다.

자기회귀적 추론(Autoregressive Inference)의 계산 비용도 고려해야 한다. 미래 단계가 순차적으로 생성되기 때문에 일반적으로 s

t+k+1

​

의 예측은 s

t+k

​

가 생성될 때까지 기다려야 한다. 따라서 긴 예측 지평에서는 특히 내부 표현이나 동역학 네트워크가 큰 경우 지연 시간(Latency)이 증가할 수 있다. 병렬 예측(Parallel Prediction) 또는 직접 다중 지평 예측(Direct Multi-Horizon Prediction)은 이러한 순차적 의존성을 줄일 수 있으며, 이는 재귀적 유연성(Recursive Flexibility)과 추론 속도(Inference Speed) 사이의 중요한 아키텍처적 절충 관계(Architectural Tradeoff)를 형성한다.

이러한 한계에도 불구하고 자기회귀적 예측(Autoregressive Prediction)은 물리적 과정 자체가 순차적으로 변화한다는 점에서 예측형 월드 모델(Predictive World Model)의 자연스러운 기반이 된다. 현재 조건은 이후의 조건에 영향을 미치고, 행동은 이러한 상태 전이를 변화시키며, 새롭게 생성된 상태는 이후 변화의 출발점이 된다. 자기회귀적 모델링은 현재의 표현을 점점 더 먼 미래의 표현으로 반복적으로 변환함으로써 이러한 시간적 구조(Temporal Structure)를 반영한다.

피지컬 AI(Physical AI)에서 자기회귀적 예측의 중요성은 국소적인 상태 전이 모델(Local Transition Model)을 상상(Imagination)을 위한 메커니즘으로 전환한다는 데 있다. 로봇은 실제 물리적 행동을 실행하기 전에 반복적인 예측을 통해 어떤 일이 발생할 수 있는지를 탐색할 수 있다. 메모리(Memory), 행동 조건화(Action Conditioning), 불확실성 추정(Uncertainty Estimation), 물리적 제약(Physical Constraints), 지속적인 재계획(Continual Replanning)과 결합된 자기회귀적 예측은 다음 상태 학습(Next-State Learning)에서 궤적 예측(Trajectory Forecasting), 내부 시뮬레이션(Internal Simulation), 장기 의사결정(Long-Horizon Decision Making)으로 이어지는 실용적인 연결 고리를 제공한다.

##  

## 02.06. Parallel and Multi Horizon Prediction

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

Parallel and multi-horizon prediction provides an alternative to generating future states strictly one after another. Instead of waiting for the prediction at one time step before estimating the next, a world model can predict several future horizons directly from a shared representation of the present. This architecture is particularly valuable for Physical AI systems that require fast access to both immediate and longer-term future information.

A multi-horizon predictor estimates states such as (s_{t+1}, s_{t+2}, s_{t+5},) and (s_{t+10}) from the current context without necessarily using each intermediate prediction recursively. More generally, the model learns mappings from the current state, history, and actions to multiple future targets. Each output corresponds to a different temporal horizon and can specialize in the information that remains meaningful at that distance into the future.

This differs fundamentally from autoregressive prediction. In an autoregressive rollout, (\\hat{s}\*{t+1}) becomes an input for predicting (\\hat{s}\*{t+2}), creating a sequential dependency between future states. In parallel prediction, multiple future states can be generated simultaneously. The prediction for a distant horizon therefore does not necessarily inherit every numerical error produced at earlier predicted steps.

Reducing recursive error propagation is one of the major motivations for direct multi-horizon prediction. An autoregressive model may accumulate small errors as its own predictions are repeatedly fed back into the dynamics model. A direct predictor can instead estimate a distant state from a representation anchored to actual observations. This does not eliminate prediction error, but it changes how errors develop across the horizon.

Parallel prediction can also reduce inference latency. Sequential autoregressive models must perform repeated model evaluations before reaching a distant future state, whereas a parallel architecture can produce several horizons during one forward computation or through simultaneously evaluated prediction heads. This property is attractive for real-time robots, autonomous vehicles, and other Physical AI platforms operating under strict computational deadlines.

Different horizons naturally contain different types of useful information. Very short-term predictions may require precise velocity, pose, contact, or occupancy estimates for control. Medium-term predictions may emphasize trajectories, interaction patterns, and collision risk. Longer-term predictions may focus more strongly on semantic outcomes, route feasibility, task progress, or broad environmental evolution rather than exact geometric details.

A world model can therefore use horizon-specific prediction heads. A shared encoder or temporal backbone constructs a common representation of the observed environment, while separate heads estimate different future intervals. These heads can share most of the learned representation while adapting their outputs, losses, uncertainty models, or spatial resolution to the requirements of each temporal horizon.

Multi-horizon prediction does not imply that horizons must be uniformly spaced. A system may predict 100 milliseconds, 500 milliseconds, 1 second, 3 seconds, and 5 seconds into the future rather than every fixed interval. Dense prediction can be concentrated near the present, where precise control is required, while sparse prediction can cover the distant future where uncertainty is larger and exact temporal resolution is less useful.

This leads naturally to hierarchical temporal prediction. Fine temporal resolution can represent immediate physical dynamics, while progressively coarser horizons capture longer-term evolution. Such a hierarchy can reduce computational demand and prevent the model from spending excessive capacity on distant details that cannot be predicted reliably. The temporal structure of the model can therefore reflect both physical dynamics and decision-making requirements.

Action conditioning remains essential when the agent influences future states. A multi-horizon model may receive a candidate action sequence and estimate its consequences at several future points simultaneously. For example, a mobile robot can evaluate where it may be after several different time intervals under a proposed velocity profile. A manipulator can similarly estimate intermediate and final object configurations produced by a planned sequence of commands.

Parallel prediction is particularly useful when many candidate actions must be evaluated quickly. If a planner considers multiple trajectories, waiting for long autoregressive rollouts for every candidate can become computationally expensive. Multi-horizon predictors can provide rapid estimates of important future checkpoints, allowing the planner to reject unsafe or ineffective candidates before applying more detailed simulation to the most promising alternatives.

State representation can vary across horizons as well. Near-term predictions may preserve detailed geometry, local occupancy, velocities, and robot configuration, while longer-term outputs may use more abstract latent or semantic representations. There is no requirement that every future horizon describe the world at identical representational detail. The useful representation can become progressively more abstract as temporal distance increases.

Bird's-eye-view and occupancy representations are particularly suitable for multi-horizon prediction in navigation and autonomous mobility. A model can simultaneously estimate future occupancy fields at several time offsets, revealing how free space and dynamic obstacles may evolve. Planners can then reason about not only where obstacles currently exist but also which regions are likely to become occupied as the robot approaches them.

Object-centric multi-horizon prediction can estimate future positions, velocities, orientations, or behavioral modes for tracked entities. Rather than extending each object trajectory recursively one point at a time, the model can predict several future waypoints directly. Interaction-aware architectures can additionally account for relationships among humans, vehicles, robots, and environmental structures when producing these future states.

Uncertainty should generally increase with temporal horizon. A prediction 100 milliseconds into the future can often be relatively concentrated, while a prediction several seconds ahead may contain multiple plausible outcomes. Multi-horizon models can explicitly estimate different uncertainty distributions for each horizon, enabling the system to distinguish precise immediate forecasts from broader and less certain long-term possibilities.

The relationship among independently predicted horizons creates an important consistency problem. If the model predicts one-second and two-second future states separately, the two outputs should still describe a physically coherent evolution. An object predicted to move forward at one second should not appear in an incompatible location at two seconds without a plausible transition. Parallel prediction therefore requires mechanisms that encourage cross-horizon temporal consistency.

Consistency can be encouraged through shared representations, trajectory-level losses, physical constraints, interpolation objectives, or auxiliary transition models connecting predicted horizons. The goal is to obtain the computational advantages of parallel prediction without treating each future time point as an unrelated forecasting problem. A successful multi-horizon model should produce future checkpoints that can be interpreted as parts of one plausible temporal evolution.

Training requires supervision or predictive targets at multiple future offsets. Sequential datasets naturally provide these targets because observations occurring later in the same trajectory can be aligned with the current state. Losses can be computed independently at each horizon and then combined, or the model can use joint objectives that evaluate the entire set of future predictions together.

Loss weighting across horizons is an important design decision. Near-term errors may receive greater weight when accurate control is the primary objective, while long-term predictions may receive objectives emphasizing semantic correctness, uncertainty, or task outcomes. Equal weighting is not always desirable because predictability and operational importance differ substantially across temporal distances.

Parallel and autoregressive prediction can also be combined. A model may directly predict several anchor horizons and use autoregressive transitions between those anchors, or generate a coarse parallel forecast before refining selected trajectories recursively. Such hybrid architectures can balance inference speed, temporal resolution, consistency, and flexibility rather than forcing a system to choose one prediction strategy exclusively.

For model predictive control, multi-horizon outputs provide rapid information about the consequences of candidate actions over the control horizon. The controller can inspect immediate safety, intermediate trajectory quality, and longer-term goal progress simultaneously. After executing a short portion of the selected action, new observations become available and the entire set of future horizons can be predicted again from the updated state.

The central advantage of multi-horizon prediction is therefore not simply parallel computation. It allows the world model to organize future reasoning according to temporal scale. Immediate physical transitions, medium-term interactions, and longer-term outcomes can be represented at resolutions appropriate to their predictability and relevance, providing a richer temporal structure than treating every future step identically.

For Physical AI, parallel and multi-horizon prediction offers a practical bridge between fast reactive control and longer-horizon anticipation. By producing several views of the future simultaneously, the world model can support collision avoidance, trajectory planning, manipulation, risk assessment, and strategic decision making without relying entirely on long sequential rollouts. The result is a temporally structured predictive system that can reason about both what happens next and what may matter later.

병렬 및 다중 지평 예측(Parallel and Multi-Horizon Prediction)은 미래 상태를 반드시 하나씩 순차적으로 생성하는 방식에 대한 대안을 제공한다. 하나의 시간 단계에 대한 예측이 완료될 때까지 기다린 후 다음 상태를 추정하는 대신, 월드 모델(World Model)은 현재의 공유 표현(Shared Representation)으로부터 여러 미래 지평(Future Horizons)을 직접 예측할 수 있다. 이러한 아키텍처는 즉각적인 미래와 장기적인 미래 정보를 모두 빠르게 확보해야 하는 피지컬 AI(Physical AI) 시스템에서 특히 유용하다.

다중 지평 예측기(Multi-Horizon Predictor)는 각각의 중간 예측을 반드시 재귀적으로 사용하지 않고 현재 맥락(Current Context)으로부터 s

t+1

​

,s

t+2

​

,s

t+5

​

,s

t+10

​

과 같은 상태를 추정한다. 보다 일반적으로 모델은 현재 상태(Current State), 과거 정보(History), 행동(Actions)으로부터 여러 미래 목표(Future Targets)로의 매핑을 학습한다. 각각의 출력은 서로 다른 시간적 지평(Temporal Horizon)에 대응하며, 미래의 해당 거리에서 의미 있게 유지되는 정보에 특화될 수 있다.

이러한 방식은 자기회귀적 예측(Autoregressive Prediction)과 근본적으로 다르다. 자기회귀적 롤아웃(Autoregressive Rollout)에서는

s

\^

t+1

​

이

s

\^

t+2

​

를 예측하기 위한 입력이 되면서 미래 상태 사이에 순차적 의존성(Sequential Dependency)이 형성된다. 반면 병렬 예측(Parallel Prediction)에서는 여러 미래 상태를 동시에 생성할 수 있다. 따라서 먼 미래 지평에 대한 예측이 이전 단계의 예측에서 발생한 모든 수치적 오류를 반드시 이어받는 것은 아니다.

재귀적 오류 전파(Recursive Error Propagation)를 감소시키는 것은 직접 다중 지평 예측(Direct Multi-Horizon Prediction)의 주요 목적 중 하나이다. 자기회귀적 모델은 자신의 예측 결과를 동역학 모델(Dynamics Model)에 반복적으로 다시 입력하면서 작은 오류를 누적시킬 수 있다. 반면 직접 예측기(Direct Predictor)는 실제 관측(Actual Observations)에 고정된 표현으로부터 먼 미래 상태를 직접 추정할 수 있다. 이것이 예측 오차 자체를 제거하는 것은 아니지만 예측 지평에 따라 오류가 발생하고 전파되는 방식을 변화시킨다.

병렬 예측(Parallel Prediction)은 추론 지연 시간(Inference Latency)도 감소시킬 수 있다. 순차적인 자기회귀적 모델은 먼 미래 상태에 도달하기 위해 모델을 반복적으로 평가해야 하지만, 병렬 아키텍처는 한 번의 순전파 계산(Forward Computation) 또는 동시에 평가되는 여러 예측 헤드(Prediction Heads)를 통해 여러 미래 지평을 생성할 수 있다. 이러한 특성은 엄격한 계산 시간 제약 아래 동작하는 실시간 로봇(Real-Time Robots), 자율주행 차량(Autonomous Vehicles), 기타 피지컬 AI 플랫폼에 매우 유용하다.

서로 다른 미래 지평에는 자연스럽게 서로 다른 종류의 유용한 정보가 포함된다. 매우 짧은 미래 예측은 제어를 위해 정밀한 속도(Velocity), 자세(Pose), 접촉(Contact), 점유 상태(Occupancy) 추정이 필요할 수 있다. 중기 예측(Medium-Term Prediction)은 궤적(Trajectories), 상호작용 패턴(Interaction Patterns), 충돌 위험(Collision Risk)을 강조할 수 있다. 장기 예측(Long-Term Prediction)은 정확한 기하학적 세부 정보보다 의미적 결과(Semantic Outcomes), 경로 실행 가능성(Route Feasibility), 과업 진행(Task Progress), 광범위한 환경 변화에 더 집중할 수 있다.

따라서 월드 모델(World Model)은 지평별 예측 헤드(Horizon-Specific Prediction Heads)를 사용할 수 있다. 공유 인코더(Shared Encoder) 또는 시간적 백본(Temporal Backbone)이 관측된 환경에 대한 공통 표현을 구성하고, 개별 헤드가 서로 다른 미래 시간 간격을 추정한다. 이러한 헤드는 학습된 표현 대부분을 공유하면서도 각각의 시간 지평에 필요한 출력, 손실 함수(Losses), 불확실성 모델(Uncertainty Models), 공간 해상도(Spatial Resolution)에 맞게 특화될 수 있다.

다중 지평 예측(Multi-Horizon Prediction)이 반드시 균일한 시간 간격을 사용해야 하는 것은 아니다. 시스템은 모든 고정 간격을 예측하는 대신 100밀리초, 500밀리초, 1초, 3초, 5초 이후와 같이 서로 다른 시점을 예측할 수 있다. 정밀한 제어가 필요한 현재 가까운 영역에서는 조밀한 예측(Dense Prediction)을 수행하고, 불확실성이 커지고 정확한 시간 해상도의 유용성이 낮아지는 먼 미래에서는 희소한 예측(Sparse Prediction)을 수행할 수 있다.

이러한 방식은 자연스럽게 계층적 시간 예측(Hierarchical Temporal Prediction)으로 이어진다. 세밀한 시간 해상도(Fine Temporal Resolution)는 즉각적인 물리적 동역학을 표현하고, 점차 거칠어지는 미래 지평은 장기적인 변화를 포착할 수 있다. 이러한 계층 구조는 계산 요구량을 감소시키고 신뢰성 있게 예측할 수 없는 먼 미래의 세부 사항에 모델이 과도한 용량을 소비하는 것을 방지할 수 있다. 따라서 모델의 시간적 구조는 물리적 동역학과 의사결정 요구사항을 동시에 반영할 수 있다.

에이전트가 미래 상태에 영향을 주는 경우 행동 조건화(Action Conditioning)는 여전히 필수적이다. 다중 지평 모델은 후보 행동 시퀀스(Candidate Action Sequence)를 입력받아 여러 미래 시점에서 그 결과를 동시에 추정할 수 있다. 예를 들어 이동 로봇(Mobile Robot)은 제안된 속도 프로파일(Velocity Profile)에 따라 서로 다른 여러 시간 간격 이후에 자신이 어디에 위치할지를 평가할 수 있다. 매니퓰레이터(Manipulator) 역시 계획된 명령 시퀀스가 만들어내는 중간 및 최종 객체 구성(Object Configurations)을 추정할 수 있다.

병렬 예측(Parallel Prediction)은 많은 후보 행동을 빠르게 평가해야 할 때 특히 유용하다. 계획기(Planner)가 여러 궤적을 고려한다면 각각의 후보에 대해 긴 자기회귀적 롤아웃을 기다리는 것은 계산 비용이 매우 클 수 있다. 다중 지평 예측기는 중요한 미래 체크포인트(Future Checkpoints)를 빠르게 추정하여 안전하지 않거나 비효율적인 후보를 먼저 제거하고, 가장 유망한 대안에 대해서만 더욱 상세한 시뮬레이션을 적용할 수 있도록 한다.

상태 표현(State Representation) 역시 미래 지평에 따라 달라질 수 있다. 가까운 미래의 예측은 상세한 기하학(Geometry), 국소 점유 상태(Local Occupancy), 속도, 로봇 구성(Robot Configuration)을 유지하는 반면, 장기 출력은 더욱 추상적인 잠재 표현(Latent Representation)이나 의미적 표현(Semantic Representation)을 사용할 수 있다. 모든 미래 지평에서 세계를 동일한 수준의 세부 정보로 표현해야 할 필요는 없으며, 시간적 거리가 증가함에 따라 유용한 표현도 점차 추상화될 수 있다.

조감도(Bird's-Eye View)와 점유 표현(Occupancy Representation)은 내비게이션 및 자율 이동(Autonomous Mobility)의 다중 지평 예측에 특히 적합하다. 모델은 서로 다른 미래 시간 오프셋(Time Offsets)의 점유 필드(Occupancy Fields)를 동시에 추정하여 자유 공간(Free Space)과 동적 장애물(Dynamic Obstacles)이 어떻게 변화할지를 표현할 수 있다. 이를 통해 계획기는 현재 장애물이 존재하는 위치뿐 아니라 로봇이 접근할 때 어떤 영역이 점유될 가능성이 있는지도 추론할 수 있다.

객체 중심 다중 지평 예측(Object-Centric Multi-Horizon Prediction)은 추적되는 개체(Entity)의 미래 위치, 속도, 방향 또는 행동 모드(Behavioral Modes)를 추정할 수 있다. 각각의 객체 궤적을 한 지점씩 재귀적으로 확장하는 대신 모델은 여러 미래 웨이포인트(Future Waypoints)를 직접 예측할 수 있다. 상호작용 인식 아키텍처(Interaction-Aware Architecture)는 이러한 미래 상태를 생성할 때 인간, 차량, 로봇, 환경 구조 사이의 관계도 추가적으로 고려할 수 있다.

불확실성(Uncertainty)은 일반적으로 시간적 지평이 증가할수록 커져야 한다. 100밀리초 이후의 예측은 비교적 좁은 범위에 집중될 수 있지만, 수 초 이후의 예측에는 여러 가능한 결과가 존재할 수 있다. 다중 지평 모델은 각각의 시간 지평에 대해 서로 다른 불확실성 분포(Uncertainty Distribution)를 명시적으로 추정하여 시스템이 정밀한 즉각적 예측과 더 넓고 불확실한 장기 가능성을 구별할 수 있도록 한다.

독립적으로 예측된 미래 지평 사이의 관계는 중요한 일관성 문제(Consistency Problem)를 발생시킨다. 모델이 1초 후와 2초 후의 미래 상태를 각각 별도로 예측하더라도 두 출력은 물리적으로 일관된 변화 과정을 설명해야 한다. 1초 후 전진한다고 예측된 객체가 타당한 상태 전이 없이 2초 후 전혀 호환되지 않는 위치에 나타나서는 안 된다. 따라서 병렬 예측에는 지평 간 시간적 일관성(Cross-Horizon Temporal Consistency)을 유지하도록 하는 메커니즘이 필요하다.

일관성(Consistency)은 공유 표현(Shared Representations), 궤적 수준 손실(Trajectory-Level Losses), 물리적 제약(Physical Constraints), 보간 목적 함수(Interpolation Objectives), 또는 예측된 미래 지평을 연결하는 보조 전이 모델(Auxiliary Transition Models)을 통해 강화할 수 있다. 목표는 각각의 미래 시점을 서로 독립적인 예측 문제로 취급하지 않으면서 병렬 예측의 계산적 장점을 얻는 것이다. 성공적인 다중 지평 모델은 여러 미래 체크포인트를 하나의 타당한 시간적 변화 과정의 일부로 해석할 수 있도록 생성해야 한다.

학습(Training)에는 여러 미래 시간 오프셋에 대한 지도 신호(Supervision) 또는 예측 목표(Predictive Targets)가 필요하다. 시퀀스 데이터셋(Sequential Dataset)은 동일한 궤적에서 이후에 발생하는 관측을 현재 상태와 정렬할 수 있기 때문에 이러한 목표를 자연스럽게 제공한다. 각각의 시간 지평에 대해 독립적으로 손실을 계산한 후 결합할 수도 있고, 미래 예측 전체를 하나의 집합으로 평가하는 공동 목적 함수(Joint Objectives)를 사용할 수도 있다.

미래 지평에 따른 손실 가중치(Loss Weighting)는 중요한 설계 요소이다. 정확한 제어가 주요 목표라면 단기 예측 오류에 더 높은 가중치를 부여할 수 있으며, 장기 예측에는 의미적 정확성(Semantic Correctness), 불확실성 또는 과업 결과(Task Outcomes)를 강조하는 목적 함수를 사용할 수 있다. 예측 가능성과 실제 운용상의 중요성이 시간적 거리에 따라 크게 달라지므로 모든 미래 지평에 동일한 가중치를 적용하는 것이 항상 바람직한 것은 아니다.

병렬 예측(Parallel Prediction)과 자기회귀적 예측(Autoregressive Prediction)을 결합할 수도 있다. 모델은 여러 기준 미래 지평(Anchor Horizons)을 직접 예측하고 그 사이의 상태를 자기회귀적 전이로 생성하거나, 먼저 거친 병렬 예측(Coarse Parallel Forecast)을 생성한 뒤 선택된 궤적을 재귀적으로 정교화할 수 있다. 이러한 하이브리드 아키텍처(Hybrid Architecture)는 하나의 예측 전략만 선택하는 대신 추론 속도, 시간 해상도, 일관성, 유연성 사이의 균형을 맞출 수 있다.

모델 예측 제어(Model Predictive Control)에서 다중 지평 출력은 제어 지평(Control Horizon) 전체에 걸친 후보 행동의 결과를 빠르게 제공한다. 제어기는 즉각적인 안전성(Immediate Safety), 중간 단계의 궤적 품질(Intermediate Trajectory Quality), 장기적인 목표 진행(Long-Term Goal Progress)을 동시에 확인할 수 있다. 선택된 행동의 짧은 구간을 실행한 후 새로운 관측을 확보하면 갱신된 상태로부터 전체 미래 지평을 다시 예측할 수 있다.

따라서 다중 지평 예측(Multi-Horizon Prediction)의 핵심적인 장점은 단순한 병렬 계산(Parallel Computation)에만 있는 것이 아니다. 월드 모델이 시간적 규모(Temporal Scale)에 따라 미래 추론을 구성할 수 있다는 데 더 큰 의미가 있다. 즉각적인 물리적 상태 전이, 중기적인 상호작용, 장기적인 결과를 각각의 예측 가능성과 중요도에 적합한 해상도로 표현함으로써 모든 미래 단계를 동일하게 취급하는 방식보다 풍부한 시간적 구조(Temporal Structure)를 제공할 수 있다.

피지컬 AI(Physical AI)에서 병렬 및 다중 지평 예측(Parallel and Multi-Horizon Prediction)은 빠른 반응형 제어(Reactive Control)와 장기적인 예상(Long-Horizon Anticipation)을 연결하는 실용적인 다리 역할을 한다. 월드 모델이 여러 미래의 모습을 동시에 생성함으로써 긴 순차적 롤아웃에 전적으로 의존하지 않고도 충돌 회피(Collision Avoidance), 궤적 계획(Trajectory Planning), 조작(Manipulation), 위험 평가(Risk Assessment), 전략적 의사결정(Strategic Decision Making)을 지원할 수 있다. 그 결과 시스템은 바로 다음에 무엇이 발생하는지뿐만 아니라 이후에 무엇이 중요해질 수 있는지도 함께 추론할 수 있는 시간적으로 구조화된 예측 시스템(Temporally Structured Predictive System)으로 발전한다.

##  

## 02.07. State Feature and Semantic Prediction

![](images/image7.png){width="7.268055555555556in" height="7.268055555555556in"}

![](images/image8.png){width="7.268055555555556in" height="7.268055555555556in"}

State feature and semantic prediction extends world modeling beyond forecasting raw observations or geometric motion. Instead of predicting only where objects will move or what the next sensor frame will contain, the model estimates how meaningful properties of the world will evolve. These properties may include object state, motion attributes, affordances, semantic categories, relationships, interaction status, and task-relevant conditions.

A state feature is a compact variable or representation describing an aspect of the current world that is useful for predicting future behavior. Examples include position, orientation, velocity, acceleration, object identity, size, contact state, traversability, visibility, or stability. By predicting how these features change over time, a world model can represent physical evolution without reconstructing every detail contained in raw sensory observations.

Semantic prediction operates at a more abstract level by forecasting changes in the meaning or functional interpretation of a scene. A door may transition from closed to opening to open, a region may change from free to occupied, or an object may change from unreachable to reachable. These transitions describe what the future state means for the agent rather than merely how pixels or coordinates change.

For Physical AI, this distinction is important because intelligent action depends on properties that are not always directly visible. A robot navigating a warehouse does not only need to predict the future coordinates of nearby objects. It may need to determine whether an aisle will remain traversable, whether another robot is yielding, whether a pallet is blocking a route, or whether a human is likely to enter the robot's operational space.

State feature prediction can be represented as a transition from a feature vector x

t

​

to future features x

t+k

​

. The vector may combine continuous quantities such as pose and velocity with discrete properties such as contact or operational state. A learned dynamics model can estimate these future features directly, allowing downstream components to reason about physical conditions without repeatedly interpreting complete future sensor observations.

Semantic states may be represented using categorical labels, structured attributes, embeddings, graphs, or learned latent variables. Object-centric representations can associate semantic properties with individual entities, while scene-level representations describe global conditions. Graph-based models can additionally encode relationships such as near, behind, supporting, approaching, connected, blocking, or interacting, allowing those relationships to evolve through prediction.

Object identity is particularly important for state prediction across time. A useful world model should recognize that an object observed at different moments represents the same persistent entity even when its position, appearance, or visibility changes. Maintaining identity allows the model to associate historical motion, semantic attributes, interactions, and predicted futures with the correct object rather than treating every observation as an unrelated detection.

Feature prediction can separate relatively stable properties from rapidly changing ones. Object category, approximate size, or structural role may remain constant over long periods, while position, velocity, contact, or accessibility may change quickly. A world model can exploit these different temporal characteristics by updating dynamic features frequently while maintaining persistent semantic attributes through memory.

Semantic prediction is closely connected to affordance prediction. An affordance describes what actions an agent can perform with an object or region under the current conditions. A surface may be traversable, an object graspable, a door openable, or a location reachable. Predicting future affordances allows the agent to estimate not only how the environment will change but also how its available action possibilities will change.

This capability becomes especially important during manipulation. A robot may predict that moving its gripper toward an object will change the object from uncontacted to contacted, then to grasped, lifted, transported, and placed. These are semantic state transitions associated with physical interactions. Modeling them provides a task-level description of progress that complements continuous predictions of joint positions, forces, and object trajectories.

Navigation provides another example. Geometric prediction may estimate the future positions of pedestrians and vehicles, while semantic prediction can estimate whether a path will become blocked, whether an intersection will become safe to enter, or whether a region remains navigable. Combining geometric and semantic predictions allows planning to reason simultaneously about precise motion and higher-level operational meaning.

Semantic states can also capture relationships among multiple entities. A human may be approaching a robot, one vehicle may be yielding to another, an object may be supported by a table, or a robot may be carrying a payload. Such relational states often contain information that cannot be represented adequately by independent object features. Predicting future relationships can therefore improve reasoning about interactions and coordinated behavior.

Temporal context is necessary because many semantic states cannot be inferred reliably from a single observation. A person's intention, an object's stability, or whether another robot is yielding may become apparent only through a sequence of observations. Memory mechanisms such as recurrent networks, temporal transformers, or state-space models can integrate historical evidence before predicting future features and semantic transitions.

State feature and semantic prediction can be performed at multiple horizons. Near-term prediction may focus on detailed motion, contact, occupancy, and local interaction states. Medium-term prediction can emphasize trajectories, accessibility, and evolving relationships. Longer-term prediction may become increasingly semantic, estimating task completion, route feasibility, interaction outcomes, or other abstract conditions whose exact geometry is difficult to forecast.

This progression from detailed state features toward abstract semantics provides a natural hierarchy for world modeling. Close to the present, the model can retain precise physical quantities needed for control. Farther into the future, where geometric uncertainty grows, it may preserve higher-level information that remains useful for decision making. The representation can therefore become more abstract as the prediction horizon increases.

Uncertainty must be represented at both feature and semantic levels. The future position of an object may have a continuous uncertainty distribution, while its semantic state may have several categorical possibilities. A door might remain closed or open, a pedestrian might yield or cross, and an object might remain stable or fall. Predicting probabilities over these alternatives allows planning to account for ambiguous future conditions.

Feature and semantic predictions can be generated through a shared backbone with multiple specialized heads. One head may predict future geometry, another motion, another occupancy, another semantic state, and another affordances or relationships. Sharing an internal representation allows these predictions to influence one another while preserving task-specific output structures and training objectives.

Training signals can come from several sources. Geometric and motion features may be derived from tracking, odometry, simulation, or robot state logs, while semantic states may use human labels, automatically generated annotations, task outcomes, or weak supervision. Self-supervised temporal learning can additionally encourage the model to discover predictive features from sequential data without requiring every meaningful property to be manually specified.

Consistency between physical and semantic prediction is critical. A model should not predict that an object is grasped if the predicted gripper and object states are physically separated, nor should it label a path as traversable if predicted occupancy blocks the region. Cross-task consistency constraints can align geometric, dynamic, relational, and semantic outputs so that they describe one coherent future world.

Prediction errors at the semantic level can also provide valuable information. If an object expected to remain stable begins to fall, or a region predicted to remain traversable becomes blocked, the discrepancy indicates that the model misunderstood an interaction or environmental condition. Such errors can trigger replanning, additional sensing, uncertainty increases, or adaptation of the internal world representation.

For planning, semantic predictions provide compact criteria for evaluating candidate futures. Rather than inspecting every predicted sensor value, a planner can reason about states such as safe, blocked, reachable, stable, grasped, completed, or risky. These abstractions reduce the gap between low-level physical prediction and high-level goals, enabling world-model rollouts to be evaluated according to operational meaning.

State feature and semantic prediction therefore forms an important bridge between perception, dynamics, and reasoning. Feature prediction describes how measurable properties evolve, while semantic prediction describes how the meaning, relationships, affordances, and task relevance of those properties change. Together they allow a world model to represent not only what the future may physically look like, but what that future means for an embodied agent.

For Physical AI, this capability supports a transition from forecasting motion toward forecasting situations. The system can anticipate whether objects will become reachable, routes blocked, interactions dangerous, contacts successful, or tasks completed. By combining geometric dynamics with persistent features, relational structure, affordances, semantics, memory, and uncertainty, the world model becomes a richer predictive representation for planning and intelligent physical action.

상태 특징 및 의미 예측(State Feature and Semantic Prediction)은 원시 관측(Raw Observations)이나 기하학적 움직임(Geometric Motion)의 예측을 넘어 월드 모델링(World Modeling)의 범위를 확장한다. 모델은 단순히 객체가 어디로 이동할지 또는 다음 센서 프레임에 무엇이 나타날지만 예측하는 것이 아니라, 세계의 의미 있는 속성들이 어떻게 변화할지를 추정한다. 이러한 속성에는 객체 상태(Object State), 움직임 속성(Motion Attributes), 행동 가능성(Affordances), 의미 범주(Semantic Categories), 관계(Relationships), 상호작용 상태(Interaction Status), 과업 관련 조건(Task-Relevant Conditions) 등이 포함될 수 있다.

상태 특징(State Feature)은 미래 행동을 예측하는 데 유용한 현재 세계의 특정 측면을 설명하는 압축된 변수 또는 표현(Representation)이다. 예를 들면 위치(Position), 방향(Orientation), 속도(Velocity), 가속도(Acceleration), 객체 정체성(Object Identity), 크기(Size), 접촉 상태(Contact State), 주행 가능성(Traversability), 가시성(Visibility), 안정성(Stability) 등이 있다. 이러한 특징이 시간에 따라 어떻게 변화하는지를 예측함으로써 월드 모델은 원시 센서 관측에 포함된 모든 세부 사항을 재구성하지 않고도 물리적 변화를 표현할 수 있다.

의미 예측(Semantic Prediction)은 장면(Scene)의 의미 또는 기능적 해석(Functional Interpretation)이 어떻게 변화할지를 예측함으로써 더욱 추상적인 수준에서 작동한다. 문(Door)은 닫힘(Closed)에서 열리는 중(Opening)을 거쳐 열림(Open) 상태로 전환될 수 있고, 특정 영역은 자유 공간(Free)에서 점유 상태(Occupied)로 변화할 수 있으며, 객체는 도달 불가능(Unreachable) 상태에서 도달 가능(Reachable) 상태로 변화할 수 있다. 이러한 전이는 단순히 픽셀이나 좌표가 어떻게 변화하는지가 아니라 미래 상태가 에이전트에게 무엇을 의미하는지를 설명한다.

피지컬 AI(Physical AI)에서 이러한 구분은 지능적인 행동이 항상 직접적으로 보이는 속성에만 의존하지 않기 때문에 중요하다. 창고를 주행하는 로봇은 주변 객체의 미래 좌표만 예측하면 되는 것이 아니다. 통로가 계속 주행 가능한 상태로 유지될지, 다른 로봇이 양보하고 있는지, 팔레트가 경로를 막고 있는지, 또는 사람이 로봇의 작업 공간(Operational Space)에 진입할 가능성이 있는지를 판단해야 할 수 있다.

상태 특징 예측(State Feature Prediction)은 특징 벡터 x

t

​

에서 미래 특징 x

t+k

​

로의 전이로 표현할 수 있다. 이 벡터는 자세(Pose)와 속도 같은 연속적인 물리량(Continuous Quantities)과 접촉 또는 작동 상태(Operational State) 같은 이산 속성(Discrete Properties)을 함께 포함할 수 있다. 학습된 동역학 모델(Learned Dynamics Model)은 이러한 미래 특징을 직접 추정할 수 있으며, 이를 통해 후속 구성 요소는 전체 미래 센서 관측을 반복적으로 해석하지 않고도 물리적 조건을 추론할 수 있다.

의미 상태(Semantic States)는 범주형 라벨(Categorical Labels), 구조화된 속성(Structured Attributes), 임베딩(Embeddings), 그래프(Graphs), 또는 학습된 잠재 변수(Learned Latent Variables)를 이용해 표현할 수 있다. 객체 중심 표현(Object-Centric Representation)은 개별 개체(Entity)에 의미적 속성을 연결할 수 있으며, 장면 수준 표현(Scene-Level Representation)은 전체적인 조건을 설명한다. 그래프 기반 모델(Graph-Based Model)은 가까움(Near), 뒤에 있음(Behind), 지지함(Supporting), 접근함(Approaching), 연결됨(Connected), 방해함(Blocking), 상호작용함(Interacting)과 같은 관계를 추가로 인코딩하고 이러한 관계의 변화를 예측할 수 있다.

객체 정체성(Object Identity)은 시간에 따른 상태 예측에서 특히 중요하다. 유용한 월드 모델(World Model)은 위치, 외형 또는 가시성이 변화하더라도 서로 다른 시점에서 관측된 객체가 동일하게 지속되는 개체(Persistent Entity)임을 인식해야 한다. 정체성을 유지하면 모델은 모든 관측을 서로 무관한 탐지 결과로 처리하는 대신 과거의 움직임, 의미적 속성, 상호작용, 예측된 미래를 올바른 객체와 연결할 수 있다.

특징 예측(Feature Prediction)은 비교적 안정적인 속성과 빠르게 변화하는 속성을 구분할 수 있다. 객체 범주(Object Category), 대략적인 크기, 구조적 역할(Structural Role)은 오랜 시간 동안 일정하게 유지될 수 있지만 위치, 속도, 접촉, 접근 가능성(Accessibility)은 빠르게 변화할 수 있다. 월드 모델은 이러한 서로 다른 시간적 특성을 활용하여 동적 특징(Dynamic Features)은 자주 갱신하고 지속적인 의미 속성(Persistent Semantic Attributes)은 메모리(Memory)를 통해 유지할 수 있다.

의미 예측(Semantic Prediction)은 행동 가능성 예측(Affordance Prediction)과 밀접하게 연결된다. 행동 가능성(Affordance)은 현재 조건에서 에이전트가 객체나 영역에 대해 어떤 행동을 수행할 수 있는지를 나타낸다. 표면은 주행 가능(Traversable)할 수 있고, 객체는 파지 가능(Graspable)할 수 있으며, 문은 열 수 있는 상태(Openable), 위치는 도달 가능(Reachable)할 수 있다. 미래 행동 가능성을 예측하면 에이전트는 환경이 어떻게 변화할지뿐만 아니라 자신이 사용할 수 있는 행동 가능성이 어떻게 변화할지도 추정할 수 있다.

이러한 능력은 조작(Manipulation) 과정에서 특히 중요해진다. 로봇은 그리퍼(Gripper)를 객체 방향으로 이동시킴으로써 객체 상태가 비접촉(Uncontacted)에서 접촉(Contacted), 파지(Grasped), 들어 올림(Lifted), 운반(Transported), 배치(Placed) 상태로 변화할 것이라고 예측할 수 있다. 이러한 변화는 물리적 상호작용과 연결된 의미적 상태 전이(Semantic State Transitions)이다. 이를 모델링하면 관절 위치, 힘, 객체 궤적과 같은 연속적 예측을 보완하는 과업 수준(Task-Level)의 진행 상태를 표현할 수 있다.

내비게이션(Navigation)은 또 다른 예를 제공한다. 기하학적 예측(Geometric Prediction)은 보행자와 차량의 미래 위치를 추정할 수 있는 반면, 의미 예측은 경로가 차단될지, 교차로에 진입해도 안전한 상태가 될지, 또는 특정 영역이 계속 주행 가능한지를 추정할 수 있다. 기하학적 예측과 의미 예측을 결합하면 계획(Planning)은 정밀한 움직임과 보다 높은 수준의 운용적 의미(Operational Meaning)를 동시에 추론할 수 있다.

의미 상태(Semantic State)는 여러 개체 사이의 관계도 표현할 수 있다. 사람이 로봇에 접근하고 있거나, 한 차량이 다른 차량에 양보하고 있거나, 객체가 테이블에 의해 지지되고 있거나, 로봇이 페이로드(Payload)를 운반하고 있을 수 있다. 이러한 관계 상태(Relational States)는 각각의 객체 특징을 독립적으로 표현하는 것만으로는 충분히 설명하기 어려운 정보를 포함하는 경우가 많다. 따라서 미래 관계를 예측하면 상호작용과 협력 행동(Coordinated Behavior)에 대한 추론 능력을 향상시킬 수 있다.

많은 의미 상태를 단일 관측만으로 신뢰성 있게 추론할 수 없기 때문에 시간적 맥락(Temporal Context)이 필요하다. 사람의 의도(Intention), 객체의 안정성, 또는 다른 로봇이 양보하고 있는지는 일련의 관측을 통해서만 명확해질 수 있다. 순환 신경망(Recurrent Networks), 시간적 트랜스포머(Temporal Transformers), 상태 공간 모델(State-Space Models)과 같은 메모리 메커니즘은 미래 특징과 의미적 전이를 예측하기 전에 과거의 증거를 통합할 수 있다.

상태 특징 및 의미 예측(State Feature and Semantic Prediction)은 여러 예측 지평(Multiple Horizons)에서 수행될 수 있다. 단기 예측(Near-Term Prediction)은 상세한 움직임, 접촉, 점유 상태, 국소적인 상호작용 상태에 집중할 수 있다. 중기 예측(Medium-Term Prediction)은 궤적, 접근 가능성, 변화하는 관계를 강조할 수 있다. 장기 예측(Long-Term Prediction)은 정확한 기하학적 구조를 예측하기 어려워짐에 따라 과업 완료(Task Completion), 경로 실행 가능성(Route Feasibility), 상호작용 결과(Interaction Outcomes) 또는 기타 추상적인 조건을 더욱 중요하게 다룰 수 있다.

상세한 상태 특징에서 추상적인 의미(Semantics)로 진행하는 이러한 구조는 월드 모델링을 위한 자연스러운 계층 구조(Hierarchy)를 제공한다. 현재와 가까운 시점에서는 제어에 필요한 정밀한 물리량을 유지할 수 있다. 반면 미래로 멀어질수록 기하학적 불확실성(Geometric Uncertainty)이 증가하므로 의사결정에 여전히 유용한 상위 수준의 정보를 유지할 수 있다. 따라서 예측 지평이 증가할수록 표현은 점차 추상적으로 변화할 수 있다.

불확실성(Uncertainty)은 특징 수준과 의미 수준 모두에서 표현되어야 한다. 객체의 미래 위치는 연속적인 불확실성 분포(Continuous Uncertainty Distribution)를 가질 수 있는 반면, 의미 상태는 여러 범주형 가능성(Categorical Possibilities)을 가질 수 있다. 문은 닫힌 상태를 유지하거나 열릴 수 있고, 보행자는 양보하거나 횡단할 수 있으며, 객체는 안정적으로 유지되거나 넘어질 수 있다. 이러한 대안들의 확률을 예측하면 계획기가 모호한 미래 조건을 고려할 수 있다.

특징 및 의미 예측은 공유 백본(Shared Backbone)과 여러 전문화된 헤드(Specialized Heads)를 통해 생성할 수 있다. 하나의 헤드는 미래 기하학을 예측하고, 다른 헤드는 움직임, 점유 상태, 의미 상태를 예측하며, 또 다른 헤드는 행동 가능성이나 관계를 예측할 수 있다. 내부 표현을 공유하면 이러한 예측들이 서로 영향을 주면서도 각각의 과업에 적합한 출력 구조(Output Structure)와 학습 목적 함수(Training Objective)를 유지할 수 있다.

학습 신호(Training Signals)는 여러 출처에서 얻을 수 있다. 기하학적 특징과 움직임 특징은 추적(Tracking), 오도메트리(Odometry), 시뮬레이션(Simulation), 로봇 상태 로그(Robot State Logs)에서 얻을 수 있으며, 의미 상태는 인간 라벨(Human Labels), 자동 생성 주석(Automatically Generated Annotations), 과업 결과(Task Outcomes), 약한 지도 학습(Weak Supervision)을 활용할 수 있다. 자기지도 시간 학습(Self-Supervised Temporal Learning)을 이용하면 모든 의미 있는 속성을 사람이 직접 지정하지 않고도 시퀀스 데이터에서 예측 가능한 특징을 발견하도록 모델을 학습할 수 있다.

물리적 예측과 의미 예측 사이의 일관성(Consistency)은 매우 중요하다. 예측된 그리퍼와 객체가 물리적으로 떨어져 있는데 객체가 파지되었다고 예측해서는 안 되며, 예측된 점유 상태가 특정 영역을 막고 있는데 해당 경로를 주행 가능하다고 판단해서도 안 된다. 교차 과업 일관성 제약(Cross-Task Consistency Constraints)은 기하학적, 동적, 관계적, 의미적 출력을 정렬하여 모두 하나의 일관된 미래 세계를 설명하도록 할 수 있다.

의미 수준에서 발생하는 예측 오차(Prediction Error) 역시 중요한 정보를 제공할 수 있다. 안정적으로 유지될 것으로 예상했던 객체가 넘어지기 시작하거나 주행 가능한 상태로 유지될 것으로 예측했던 영역이 차단된다면, 이러한 차이는 모델이 상호작용 또는 환경 조건을 잘못 이해했다는 것을 의미한다. 이러한 오류는 재계획(Replanning), 추가 센싱(Additional Sensing), 불확실성 증가, 또는 내부 월드 표현(Internal World Representation)의 적응을 유발할 수 있다.

계획(Planning)에서 의미 예측은 후보 미래를 평가하기 위한 압축된 기준을 제공한다. 계획기는 모든 예측 센서 값을 직접 검사하는 대신 안전(Safe), 차단(Blocked), 도달 가능(Reachable), 안정(Stable), 파지됨(Grasped), 완료(Completed), 위험(Risky)과 같은 상태를 중심으로 추론할 수 있다. 이러한 추상화는 저수준 물리적 예측(Low-Level Physical Prediction)과 고수준 목표(High-Level Goals) 사이의 간격을 줄여 월드 모델 롤아웃을 운용적 의미에 따라 평가할 수 있게 한다.

따라서 상태 특징 및 의미 예측(State Feature and Semantic Prediction)은 인식(Perception), 동역학(Dynamics), 추론(Reasoning)을 연결하는 중요한 다리를 형성한다. 특징 예측(Feature Prediction)은 측정 가능한 속성이 어떻게 변화하는지를 설명하고, 의미 예측(Semantic Prediction)은 이러한 속성의 의미, 관계, 행동 가능성, 과업 관련성이 어떻게 변화하는지를 설명한다. 두 가지를 결합하면 월드 모델은 미래가 물리적으로 어떤 모습일지만 표현하는 것이 아니라 그 미래가 체화 에이전트(Embodied Agent)에게 무엇을 의미하는지도 표현할 수 있다.

피지컬 AI(Physical AI)에서 이러한 능력은 움직임 예측(Motion Forecasting)에서 상황 예측(Situation Forecasting)으로의 전환을 지원한다. 시스템은 객체가 도달 가능한 상태가 될지, 경로가 차단될지, 상호작용이 위험해질지, 접촉이 성공할지, 과업이 완료될지를 사전에 예상할 수 있다. 기하학적 동역학(Geometric Dynamics)에 지속적인 특징(Persistent Features), 관계 구조(Relational Structure), 행동 가능성(Affordances), 의미(Semantics), 메모리(Memory), 불확실성(Uncertainty)을 결합함으로써 월드 모델은 계획과 지능적인 물리적 행동(Intelligent Physical Action)을 위한 더욱 풍부한 예측 표현(Predictive Representation)으로 발전한다.

##  

## 02.08. Temporal Consistency and Error Accumulation

![](images/image9.png){width="7.268055555555556in" height="7.268055555555556in"}

Temporal consistency is the requirement that predicted states form a coherent evolution of the same world across time. A world model should not merely generate individually plausible future states; those states must also agree with one another. Objects should preserve identity, motion should evolve continuously when appropriate, physical relationships should remain compatible, and semantic changes should follow plausible temporal transitions.

This requirement becomes especially important when prediction extends beyond the immediate next state. A model may produce an accurate estimate at (t+1), yet increasingly inconsistent states at (t+2, t+3,\\ldots,t+H). Long-horizon world modeling therefore depends not only on local prediction accuracy but also on whether the sequence preserves meaningful spatial, physical, semantic, and causal relationships throughout the rollout.

Error accumulation occurs when small prediction errors at earlier steps influence later predictions. In an autoregressive model, a predicted state (\\hat{s}\*{t+1}) becomes an input for estimating (\\hat{s}\*{t+2}), which then influences (\\hat{s}\*{t+3}). The process can be expressed recursively as (\\hat{s}\*{t+k+1}=f(\\hat{s}\*{t+k},a\*{t+k})), allowing inaccuracies to propagate and potentially grow with prediction horizon.

The accumulated error may appear in many forms. Position estimates can gradually drift, velocity can become unrealistic, object boundaries may deform, identities can switch, occupancy predictions can become inconsistent, and semantic states may change without physical justification. Individually small deviations can interact with one another, eventually producing a predicted future that no longer represents a physically plausible continuation of the observed world.

Autoregressive prediction is particularly vulnerable because inference conditions differ from ideal training conditions. During training, a model may receive correct observed states at each step, while during deployment it must increasingly operate on its own imperfect predictions. This train--inference mismatch means that errors rarely encountered as inputs during training can become common during long rollouts, causing the model to move into unfamiliar regions of state space.

Temporal consistency is broader than numerical smoothness. A trajectory can change smoothly while still violating physical or semantic constraints. A robot might move smoothly through a wall, an object could remain visually stable while losing its supporting surface, or a model might label an object as grasped without predicted contact. Consistency therefore requires agreement among geometry, dynamics, relationships, semantics, and physical constraints.

Object permanence provides an important example. Once an entity has been detected and assigned an identity, its predicted future should normally preserve that identity even when it becomes partially occluded or temporarily invisible. If the model repeatedly creates and deletes objects or exchanges their identities during prediction, downstream planning can misunderstand trajectories, interactions, and collision risks despite apparently reasonable frame-level predictions.

Motion consistency requires position, velocity, acceleration, and orientation to evolve compatibly. Predicted displacement should correspond approximately to velocity over the relevant interval, acceleration should respect feasible dynamics, and abrupt changes should occur only when supported by interactions or control inputs. Such relationships provide structure that can constrain predictions beyond simple similarity to future observations.

Physical consistency adds constraints derived from embodiment and environmental dynamics. Robot states should respect kinematic and dynamic limits, rigid objects should not arbitrarily change shape, collisions should influence subsequent motion, and contact relationships should evolve according to plausible interaction. Known physics does not need to describe every detail perfectly, but it can restrict obviously impossible futures generated by a learned model.

Semantic consistency operates at a higher level. State transitions such as closed to opening to open, uncontacted to contacted to grasped, or free to occupied to blocked should follow plausible sequences. Semantic predictions should also remain compatible with lower-level physical states. This coupling prevents the world model from generating a geometrically plausible future whose task-level interpretation contradicts the predicted physical configuration.

Errors can accumulate even in non-autoregressive multi-horizon models. Directly predicting several horizons avoids repeatedly feeding predictions back as inputs, but independently estimated horizons can disagree. A model might predict one trajectory at one second and an incompatible state at three seconds. Parallel prediction therefore exchanges recursive error propagation for a cross-horizon consistency problem that must be addressed explicitly.

Several complementary strategies can improve temporal consistency. Multi-step training can optimize predictions across an entire rollout rather than only the next state. Consistency losses can penalize incompatible motion or semantic transitions. Physical constraints can restrict impossible states, while shared temporal representations can encourage different horizons to describe the same evolving world. No single mechanism is sufficient for every type of inconsistency.

Multi-step rollout loss is particularly important because it exposes the consequences of early errors during training. Instead of minimizing only (L(\\hat{s}\*{t+1},s\*{t+1})), the objective can include errors at several horizons, such as (\\sum_{k=1}\^{H} w_k L(\\hat{s}\*{t+k},s\*{t+k})). The model is therefore encouraged to learn transitions that remain stable when repeatedly applied rather than transitions that are accurate only for one isolated step.

Training can also expose the predictor to its own generated states. If a model always receives perfect ground-truth history, it may never learn how to recover from small deviations. Scheduled sampling or related approaches can gradually introduce predicted states as inputs during training. The model then learns to operate under conditions closer to those encountered during autonomous rollout and can become more robust to accumulated deviations.

Latent-state design strongly influences long-term stability. A representation that preserves every unpredictable visual detail may amplify irrelevant errors, while a compact latent state focused on persistent geometry, dynamics, objects, and semantics can provide a more stable prediction space. The objective is not simply maximum compression but preservation of the variables necessary for coherent future evolution and downstream decision making.

Uncertainty estimation provides another defense against error accumulation. As predictions extend farther from observations, the model should recognize that confidence is decreasing. Instead of treating an increasingly uncertain trajectory as exact, it can represent distributions or multiple hypotheses. Planning can then account for uncertainty, avoid overcommitting to unreliable distant predictions, and request new observations before critical decisions.

Periodic observation updates are especially powerful because real sensor information can re-anchor the internal model. A robot does not normally need to execute an entire long-horizon prediction open-loop. It can predict, act briefly, observe again, correct its internal state, and generate a new rollout. This closed-loop process repeatedly prevents accumulated model error from becoming detached from the physical environment.

Model predictive control uses precisely this principle. The world model predicts several future steps, the controller selects an action based on those predictions, but only the immediate action or short segment is executed. New sensor measurements then replace uncertain predicted states with updated estimates. Receding-horizon replanning therefore combines long enough prediction for anticipation with frequent correction from reality.

Hierarchical prediction can further limit error growth. Detailed high-frequency prediction can be restricted to the near future, while longer horizons use coarser or more semantic representations. Exact object coordinates may become unreliable after several seconds, yet predictions such as route blocked, object reachable, or task likely to succeed may remain useful. Abstraction can therefore preserve decision-relevant information even when fine geometric accuracy deteriorates.

Parallel and autoregressive prediction can also be combined to improve stability. Direct multi-horizon predictions can provide anchor states that reduce unrestricted recursive drift, while autoregressive prediction can generate detailed transitions between those anchors. Cross-checking the two forms of prediction can reveal disagreement and provide a signal that uncertainty is increasing or the internal dynamics model requires correction.

Temporal consistency should be evaluated with more than frame-level accuracy metrics. Useful evaluation can examine trajectory drift, identity preservation, physical constraint violations, semantic transition validity, cross-horizon agreement, uncertainty calibration, and downstream planning performance. A model that achieves low visual prediction error but produces unstable trajectories may be less useful for Physical AI than a simpler model with coherent dynamics.

Error accumulation is ultimately unavoidable to some degree because future prediction operates with incomplete information. The goal is therefore not to eliminate every deviation but to prevent errors from growing unnoticed into confident and physically misleading futures. Robust world models should detect uncertainty, preserve structural constraints, recover from imperfect states, and repeatedly incorporate new evidence as the physical world evolves.

For Physical AI, temporal consistency determines whether imagined futures can be trusted sufficiently for action. A useful world model must preserve the continuity of entities, dynamics, relationships, and semantics while recognizing that uncertainty increases with prediction horizon. Multi-step training, physical constraints, stable representations, uncertainty modeling, observation correction, and continual replanning together transform long-horizon prediction from uncontrolled extrapolation into disciplined predictive reasoning.

시간적 일관성(Temporal Consistency)은 예측된 상태들이 시간에 걸쳐 동일한 세계의 일관된 변화 과정을 형성해야 한다는 요구사항이다. 월드 모델(World Model)은 각각 개별적으로 그럴듯한 미래 상태를 생성하는 것만으로는 충분하지 않으며, 이러한 상태들이 서로 일치해야 한다. 객체는 정체성(Object Identity)을 유지해야 하고, 움직임은 적절한 경우 연속적으로 변화해야 하며, 물리적 관계(Physical Relationships)는 서로 호환되어야 하고, 의미적 변화(Semantic Changes)는 타당한 시간적 전이(Temporal Transitions)를 따라야 한다.

이러한 요구사항은 예측이 바로 다음 상태를 넘어 확장될 때 특히 중요해진다. 모델이 (t+1)에서는 정확한 추정치를 생성하더라도 (t+2, t+3,\\ldots,t+H)로 진행하면서 점차 일관되지 않은 상태를 생성할 수 있다. 따라서 장기 지평 월드 모델링(Long-Horizon World Modeling)은 국소적인 예측 정확도(Local Prediction Accuracy)뿐만 아니라 롤아웃(Rollout) 전체에서 의미 있는 공간적, 물리적, 의미적, 인과적 관계가 유지되는지에도 의존한다.

오차 누적(Error Accumulation)은 초기 단계에서 발생한 작은 예측 오류가 이후의 예측에 영향을 미칠 때 발생한다. 자기회귀적 모델(Autoregressive Model)에서는 예측 상태 (\\hat{s}\*{t+1})이 (\\hat{s}\*{t+2})를 추정하기 위한 입력이 되고, 이것이 다시 (\\hat{s}\*{t+3})에 영향을 미친다. 이러한 과정은 (\\hat{s}\*{t+k+1}=f(\\hat{s}\*{t+k},a\*{t+k}))와 같이 재귀적으로 표현할 수 있으며, 부정확성이 예측 지평(Prediction Horizon)에 따라 전파되고 잠재적으로 증가할 수 있다.

누적된 오차(Accumulated Error)는 다양한 형태로 나타날 수 있다. 위치 추정(Position Estimation)은 점차 드리프트(Drift)할 수 있고, 속도는 비현실적으로 변할 수 있으며, 객체 경계(Object Boundaries)가 변형되거나 정체성이 서로 바뀔 수 있다. 또한 점유 예측(Occupancy Prediction)이 일관성을 잃거나 의미 상태(Semantic State)가 물리적 근거 없이 변화할 수 있다. 개별적으로는 작은 편차라도 서로 영향을 주면서 결국 관측된 세계의 물리적으로 타당한 연속 상태를 더 이상 나타내지 못하는 미래를 생성할 수 있다.

자기회귀적 예측(Autoregressive Prediction)은 추론 조건(Inference Conditions)이 이상적인 학습 조건(Training Conditions)과 다르기 때문에 이러한 문제에 특히 취약하다. 학습 중에는 각 단계에서 정확하게 관측된 상태를 입력으로 받을 수 있지만, 실제 운용에서는 점점 자신의 불완전한 예측을 기반으로 작동해야 한다. 이러한 학습-추론 불일치(Train--Inference Mismatch)로 인해 학습 과정에서는 입력으로 거의 경험하지 못했던 오류가 장기 롤아웃에서는 빈번하게 나타나고, 모델이 익숙하지 않은 상태 공간(State Space)의 영역으로 이동할 수 있다.

시간적 일관성(Temporal Consistency)은 단순한 수치적 부드러움(Numerical Smoothness)보다 더 넓은 개념이다. 궤적이 부드럽게 변화하더라도 물리적 또는 의미적 제약(Physical or Semantic Constraints)을 위반할 수 있다. 로봇이 벽을 부드럽게 통과하거나, 객체가 시각적으로 안정된 상태를 유지하면서 지지면(Supporting Surface)을 잃거나, 예측된 접촉 없이 객체를 파지했다고 모델이 판단할 수도 있다. 따라서 일관성은 기하학(Geometry), 동역학(Dynamics), 관계(Relationships), 의미(Semantics), 물리적 제약 사이의 일치를 필요로 한다.

객체 영속성(Object Permanence)은 중요한 예를 제공한다. 하나의 개체(Entity)가 탐지되어 정체성을 부여받았다면 부분적으로 가려지거나 일시적으로 보이지 않더라도 예측된 미래에서는 일반적으로 동일한 정체성이 유지되어야 한다. 모델이 예측 과정에서 객체를 반복적으로 생성하고 삭제하거나 객체들의 정체성을 서로 바꾼다면, 프레임 수준의 예측이 겉보기에 합리적이더라도 후속 계획(Downstream Planning)은 궤적, 상호작용, 충돌 위험(Collision Risk)을 잘못 이해할 수 있다.

움직임 일관성(Motion Consistency)은 위치(Position), 속도(Velocity), 가속도(Acceleration), 방향(Orientation)이 서로 호환되도록 변화해야 한다는 것을 의미한다. 예측된 변위(Displacement)는 해당 시간 간격의 속도와 대략적으로 일치해야 하며, 가속도는 실현 가능한 동역학(Feasible Dynamics)의 범위를 준수해야 한다. 또한 급격한 변화는 상호작용이나 제어 입력(Control Inputs)에 의해 뒷받침되는 경우에만 발생해야 한다. 이러한 관계는 미래 관측과의 단순한 유사성을 넘어 예측을 제한하는 구조를 제공한다.

물리적 일관성(Physical Consistency)은 체화(Embodiment)와 환경 동역학(Environmental Dynamics)에서 유래하는 제약을 추가한다. 로봇 상태는 운동학적 및 동역학적 한계(Kinematic and Dynamic Limits)를 준수해야 하고, 강체(Rigid Object)는 임의로 형태가 변해서는 안 되며, 충돌은 이후의 움직임에 영향을 미쳐야 하고, 접촉 관계(Contact Relationships)는 타당한 상호작용에 따라 변화해야 한다. 알려진 물리 법칙이 모든 세부 사항을 완벽하게 설명할 필요는 없지만 학습 모델이 명백하게 불가능한 미래를 생성하는 것을 제한할 수 있다.

의미적 일관성(Semantic Consistency)은 보다 높은 수준에서 작동한다. 닫힘(Closed)에서 열리는 중(Opening)을 거쳐 열림(Open)으로 변화하거나, 비접촉(Uncontacted)에서 접촉(Contacted)을 거쳐 파지(Grasped)로 변화하거나, 자유 공간(Free)에서 점유(Occupied)를 거쳐 차단(Blocked) 상태로 변화하는 것과 같은 상태 전이는 타당한 순서를 따라야 한다. 또한 의미적 예측은 저수준 물리 상태(Low-Level Physical States)와 일치해야 한다. 이러한 결합은 월드 모델이 기하학적으로는 타당하지만 과업 수준의 해석(Task-Level Interpretation)이 예측된 물리적 구성과 모순되는 미래를 생성하는 것을 방지한다.

오차는 비자기회귀적 다중 지평 모델(Non-Autoregressive Multi-Horizon Model)에서도 누적되거나 나타날 수 있다. 여러 미래 지평을 직접 예측하면 예측 결과를 반복적으로 입력으로 사용하는 문제는 피할 수 있지만, 독립적으로 추정된 미래 지평들이 서로 일치하지 않을 수 있다. 예를 들어 모델이 1초 후에는 하나의 궤적을 예측하면서 3초 후에는 그와 호환되지 않는 상태를 예측할 수 있다. 따라서 병렬 예측(Parallel Prediction)은 재귀적 오류 전파 문제를 줄이는 대신 지평 간 일관성(Cross-Horizon Consistency) 문제를 명시적으로 해결해야 한다.

시간적 일관성을 향상시키기 위해 여러 상호보완적인 전략을 사용할 수 있다. 다단계 학습(Multi-Step Training)은 다음 상태만이 아니라 전체 롤아웃에 걸쳐 예측을 최적화할 수 있다. 일관성 손실(Consistency Losses)은 서로 호환되지 않는 움직임이나 의미적 전이를 페널티로 처리할 수 있다. 물리적 제약은 불가능한 상태를 제한하고, 공유 시간 표현(Shared Temporal Representations)은 서로 다른 미래 지평이 동일하게 변화하는 세계를 설명하도록 유도할 수 있다. 하나의 메커니즘만으로 모든 종류의 불일치를 해결하기는 어렵다.

다단계 롤아웃 손실(Multi-Step Rollout Loss)은 학습 과정에서 초기 오류가 이후에 미치는 영향을 직접 노출한다는 점에서 특히 중요하다. 단순히 (L(\\hat{s}\*{t+1},s\*{t+1}))만 최소화하는 대신 목적 함수(Objective)는 (\\sum_{k=1}\^{H} w_k L(\\hat{s}\*{t+k},s\*{t+k}))와 같이 여러 미래 지평에서 발생하는 오류를 포함할 수 있다. 이를 통해 모델은 하나의 독립적인 상태 전이에서만 정확한 모델이 아니라 반복적으로 적용되더라도 안정적인 상태 전이를 학습하도록 유도된다.

학습 과정에서 예측기가 자신이 생성한 상태를 직접 경험하도록 할 수도 있다. 모델이 항상 완벽한 실제 정답 이력(Ground-Truth History)만 입력받는다면 작은 편차에서 어떻게 회복해야 하는지를 학습하지 못할 수 있다. 예정 샘플링(Scheduled Sampling) 또는 관련 접근법은 학습 중 예측된 상태를 점진적으로 입력으로 도입할 수 있다. 이를 통해 모델은 실제 자율 롤아웃에서 경험하는 조건과 더욱 유사한 환경에서 작동하는 방법을 학습하고 누적 편차에 대한 강건성(Robustness)을 향상시킬 수 있다.

잠재 상태 설계(Latent-State Design)는 장기 안정성(Long-Term Stability)에 큰 영향을 미친다. 예측하기 어려운 모든 시각적 세부 사항을 보존하는 표현은 중요하지 않은 오류까지 증폭시킬 수 있지만, 지속적인 기하학, 동역학, 객체, 의미 정보에 집중하는 압축된 잠재 상태(Compact Latent State)는 더욱 안정적인 예측 공간을 제공할 수 있다. 목표는 단순히 최대한 압축하는 것이 아니라 일관된 미래 변화와 후속 의사결정에 필요한 변수들을 보존하는 것이다.

불확실성 추정(Uncertainty Estimation)은 오차 누적에 대응하는 또 다른 방어 수단을 제공한다. 예측이 실제 관측으로부터 멀어질수록 모델은 자신의 신뢰도가 감소하고 있음을 인식해야 한다. 점점 불확실해지는 하나의 궤적을 정확한 미래처럼 취급하는 대신 확률 분포(Distributions) 또는 여러 가설(Multiple Hypotheses)을 표현할 수 있다. 이를 통해 계획기는 불확실성을 고려하고 신뢰하기 어려운 먼 미래 예측에 지나치게 의존하지 않으며 중요한 의사결정을 내리기 전에 새로운 관측을 요구할 수 있다.

주기적인 관측 갱신(Periodic Observation Updates)은 실제 센서 정보가 내부 모델을 다시 현실에 고정(Re-Anchor)할 수 있기 때문에 특히 강력하다. 일반적으로 로봇은 장기 예측 전체를 개방 루프(Open Loop) 방식으로 실행할 필요가 없다. 예측하고, 짧게 행동하고, 다시 관측한 다음 내부 상태를 수정하고 새로운 롤아웃을 생성할 수 있다. 이러한 폐루프 과정(Closed-Loop Process)을 반복하면 누적된 모델 오류가 실제 물리적 환경에서 완전히 분리되는 것을 방지할 수 있다.

모델 예측 제어(Model Predictive Control)는 바로 이러한 원리를 사용한다. 월드 모델은 여러 미래 단계를 예측하고, 제어기는 이러한 예측을 기반으로 행동을 선택하지만 즉각적인 행동 또는 짧은 구간만 실제로 실행한다. 이후 새로운 센서 측정값이 불확실한 예측 상태를 갱신된 추정값으로 대체한다. 따라서 이동 지평 재계획(Receding-Horizon Replanning)은 미래를 예상할 수 있을 정도로 충분히 긴 예측과 현실로부터의 빈번한 보정을 결합한다.

계층적 예측(Hierarchical Prediction)은 오류 증가를 추가적으로 제한할 수 있다. 상세한 고주파 예측(High-Frequency Prediction)은 가까운 미래에 제한하고, 더 긴 미래 지평에서는 거친 표현이나 보다 의미적인 표현을 사용할 수 있다. 정확한 객체 좌표는 몇 초 후부터 신뢰성이 떨어질 수 있지만 경로 차단(Route Blocked), 객체 도달 가능(Object Reachable), 과업 성공 가능(Task Likely to Succeed)과 같은 예측은 여전히 유용할 수 있다. 따라서 추상화(Abstraction)는 정밀한 기하학적 정확도가 감소하더라도 의사결정에 중요한 정보를 보존할 수 있다.

병렬 예측(Parallel Prediction)과 자기회귀적 예측(Autoregressive Prediction)을 결합하여 안정성을 향상시킬 수도 있다. 직접 다중 지평 예측(Direct Multi-Horizon Prediction)은 제한되지 않은 재귀적 드리프트를 줄이는 기준 상태(Anchor States)를 제공하고, 자기회귀적 예측은 이러한 기준 상태 사이의 세부적인 상태 전이를 생성할 수 있다. 두 가지 예측 형태를 교차 검증(Cross-Checking)하면 불일치를 발견하고 불확실성이 증가하거나 내부 동역학 모델(Internal Dynamics Model)의 수정이 필요하다는 신호를 얻을 수 있다.

시간적 일관성은 단순한 프레임 수준 정확도(Frame-Level Accuracy) 지표만으로 평가해서는 안 된다. 유용한 평가는 궤적 드리프트(Trajectory Drift), 정체성 유지(Identity Preservation), 물리적 제약 위반(Physical Constraint Violations), 의미적 전이의 타당성(Semantic Transition Validity), 지평 간 일치(Cross-Horizon Agreement), 불확실성 보정(Uncertainty Calibration), 후속 계획 성능(Downstream Planning Performance)을 함께 검토할 수 있다. 시각적 예측 오류가 낮더라도 불안정한 궤적을 생성하는 모델은 일관된 동역학을 제공하는 더 단순한 모델보다 피지컬 AI에 덜 유용할 수 있다.

미래 예측은 불완전한 정보(Incomplete Information)를 기반으로 수행되므로 어느 정도의 오차 누적은 궁극적으로 피할 수 없다. 따라서 목표는 모든 편차를 완전히 제거하는 것이 아니라 오류가 감지되지 않은 채 증가하여 높은 신뢰도를 가진 물리적으로 잘못된 미래로 발전하는 것을 방지하는 것이다. 강건한 월드 모델(Robust World Model)은 불확실성을 감지하고, 구조적 제약(Structural Constraints)을 유지하며, 불완전한 상태에서 회복하고, 물리적 세계가 변화함에 따라 새로운 증거를 반복적으로 통합할 수 있어야 한다.

피지컬 AI(Physical AI)에서 시간적 일관성(Temporal Consistency)은 상상된 미래(Imagined Futures)를 실제 행동에 활용할 수 있을 정도로 신뢰할 수 있는지를 결정한다. 유용한 월드 모델은 예측 지평이 증가함에 따라 불확실성이 커진다는 사실을 인식하면서 개체(Entity), 동역학(Dynamics), 관계(Relationships), 의미(Semantics)의 연속성을 유지해야 한다. 다단계 학습(Multi-Step Training), 물리적 제약(Physical Constraints), 안정적인 표현(Stable Representations), 불확실성 모델링(Uncertainty Modeling), 관측 보정(Observation Correction), 지속적인 재계획(Continual Replanning)을 결합함으로써 장기 지평 예측을 통제되지 않은 외삽(Uncontrolled Extrapolation)에서 체계적인 예측 추론(Disciplined Predictive Reasoning)으로 발전시킬 수 있다.

##  

## 02.09. Training Objectives for Predictive Models

![](images/image10.png){width="7.268055555555556in" height="7.268055555555556in"}

Training objectives determine what a predictive world model learns to preserve about the future. A model does not automatically discover the representation most useful for Physical AI simply by observing temporal data. The loss function defines which prediction errors matter, which structures should remain stable, and which aspects of future states deserve model capacity. Objective design therefore shapes the internal world representation as strongly as the architecture itself.

The simplest objective compares a predicted next state (\\hat{s}\*{t+1}) with the observed target (s\*{t+1}). A generic formulation can be written as (L=L(\\hat{s}\*{t+1},s\*{t+1})). Although conceptually straightforward, the meaning of this loss depends strongly on the predicted state representation. Images, geometry, occupancy, motion, semantic attributes, and latent features require different measures of similarity and different assumptions about prediction quality.

Regression objectives are commonly used for continuous physical quantities such as position, orientation, velocity, acceleration, force, depth, or joint configuration. Mean squared error and related distance measures encourage numerical agreement between predicted and observed values. However, minimizing average numerical error may be insufficient when several physically different futures are possible, because the resulting prediction can converge toward an unrealistic average state.

Classification objectives are appropriate when the future state contains discrete semantic variables. A predictive model may estimate whether a region will be free or occupied, whether an object will remain stable, whether contact will occur, or whether a manipulation stage will succeed. Cross-entropy and related losses can train probabilities over such categories, connecting future prediction with semantic and task-level interpretation.

Spatial prediction requires objectives that preserve geometric organization. Future occupancy grids, bird's-eye-view representations, depth fields, segmentation maps, or voxel structures contain relationships among neighboring locations that independent scalar losses may not capture adequately. Spatial losses can emphasize boundaries, occupied regions, geometric consistency, or safety-critical areas where small localization errors have significant consequences for planning.

Motion objectives can explicitly supervise displacement, velocity, acceleration, optical flow, scene flow, or object trajectories. Predicting these quantities separately can help a world model learn dynamic structure rather than infer motion indirectly from reconstructed observations. Motion consistency losses can additionally constrain predicted position and velocity to agree across time, reducing physically inconsistent trajectories during long rollouts.

Pixel reconstruction is one possible objective for visual predictive models. The model predicts a future image and compares it with the actual future frame. This provides dense supervision without requiring manual labels, but pixel-level accuracy can allocate excessive capacity to texture, lighting, and other details that may have little relevance to action. For Physical AI, reconstruction is often more useful when combined with objectives focused on geometry, dynamics, and semantics.

Latent prediction avoids reconstructing every sensory detail by predicting future representations in feature space. An encoder maps observations into latent states (z_t), and the predictive model estimates (\\hat{z}\*{t+k}) corresponding to a future target representation (z\*{t+k}). The objective encourages temporal predictability in the learned representation while allowing irrelevant visual variation to be discarded, provided the latent space retains information required for downstream behavior.

Representation learning objectives must also prevent trivial solutions. If both the predicted and target representations collapse to nearly identical constants, prediction loss may become small without learning meaningful world structure. Contrastive learning, variance regularization, stop-gradient mechanisms, reconstruction constraints, or carefully designed target networks can help maintain informative latent representations while preserving their temporal predictability.

Multi-step objectives extend training beyond immediate next-state accuracy. Instead of optimizing only one transition, the model can minimize losses over a horizon (H), conceptually written as (L_{\\text{multi}}=\\sum_{k=1}\^{H}w_kL(\\hat{s}\*{t+k},s\*{t+k})). This exposes the model to the consequences of recursive errors and encourages dynamics that remain stable and useful across longer imagined rollouts.

The weights (w_k) determine how strongly different temporal horizons influence learning. Near-term predictions may receive greater weight because they are more reliable and directly relevant to control, while distant horizons may emphasize coarse structure or semantic outcomes. Alternatively, a task requiring anticipation may assign substantial importance to longer horizons. Horizon weighting therefore connects the training objective to the intended temporal behavior of the system.

Temporal consistency objectives encourage neighboring predictions to describe one coherent evolution. These losses can penalize abrupt identity changes, incompatible motion, inconsistent occupancy, or physically unsupported semantic transitions. Cross-horizon consistency can also constrain directly predicted future states so that predictions at one, two, and several seconds describe compatible points along the same possible future rather than independent guesses.

Physical consistency objectives introduce knowledge about embodiment and environmental dynamics. Kinematic limits, acceleration bounds, rigid-body assumptions, collision constraints, contact relationships, or approximate equations of motion can become penalties or regularizers. Such objectives do not require the learned model to reproduce an exact analytical simulator, but they discourage predictions that violate basic properties of the physical system.

Action-conditioned objectives ensure that predicted futures respond correctly to control inputs. If two candidate actions should produce different outcomes, the learned representation must preserve that distinction. Training can therefore compare predicted state transitions under observed actions, emphasizing controllable changes. This is essential when the world model will later be used to simulate alternative actions for planning or model predictive control.

Probabilistic objectives are required when a single future target cannot adequately represent uncertainty. Likelihood-based losses can train predicted distributions, while stochastic latent-variable models can learn distributions over possible trajectories. The objective should reward probability assigned to plausible futures without encouraging either unjustified confidence or excessively broad uncertainty that becomes useless for downstream decisions.

Calibration objectives can further align predicted confidence with empirical accuracy. A model that assigns 90 percent confidence to an event should, under comparable conditions, be correct approximately at that rate. Well-calibrated uncertainty is particularly important for safety-critical Physical AI because planning may use confidence estimates to determine margins, reduce speed, request additional sensing, or reject risky actions.

Multimodal objectives are necessary when several qualitatively different futures are possible. Human motion, traffic behavior, contact outcomes, and object interactions frequently produce branching possibilities. Training should allow the model to preserve distinct hypotheses rather than averaging them. Mixture distributions, multiple trajectory predictions, stochastic samples, or diversity-promoting objectives can represent alternative futures while maintaining their relative plausibility.

Semantic and affordance objectives connect prediction to the operational meaning of future states. The model can be trained to predict whether an object will become graspable, whether a path will remain traversable, whether a contact will succeed, or whether a task stage will be completed. Such objectives encourage representations that preserve information directly relevant to action rather than only reproducing observable appearance.

Task-oriented objectives can go further by evaluating whether predicted representations support successful decisions. A latent world model may not need to reconstruct the environment perfectly if its predictions allow a planner to select safe and effective actions. Auxiliary losses for value, reward, goal progress, collision risk, or task success can therefore shape the predictive representation toward variables that matter for control and long-horizon reasoning.

Self-supervised objectives are especially valuable because sequential sensor data naturally provides future targets. Cameras, LiDAR, proprioception, robot states, and actions collected during operation create temporal supervision without requiring every state variable to be manually labeled. The future itself becomes a learning signal, allowing large volumes of embodied experience to contribute to representation and dynamics learning.

Weakly supervised and partially labeled data can complement self-supervision. Some trajectories may contain semantic labels, task outcomes, object identities, or interaction annotations while most contain only raw temporal observations. Combining dense self-supervised prediction with sparse semantic supervision allows the model to exploit large datasets while aligning learned features with concepts useful for planning and physical reasoning.

A practical world model usually combines several objectives rather than relying on one loss. A total objective may take the form (L=\\lambda_1L_{\\text{state}}+\\lambda_2L_{\\text{motion}}+\\lambda_3L_{\\text{semantic}}+\\lambda_4L_{\\text{consistency}}+\\lambda_5L_{\\text{uncertainty}}+\\lambda_6L_{\\text{task}}). The coefficients determine the balance among accurate physical prediction, stable representation, semantic understanding, uncertainty awareness, and operational usefulness.

Balancing these objectives is itself a major learning problem. If reconstruction dominates, the model may focus excessively on appearance. If semantic losses dominate, fine physical dynamics may be lost. If consistency constraints are too strong, genuine abrupt events may be suppressed. Objective weights, schedules, normalization, and adaptive balancing methods must therefore reflect the data, architecture, prediction horizon, and intended Physical AI application.

Training objectives should ultimately be evaluated by more than loss values on held-out data. A predictive model should be judged by whether its rollouts remain stable, uncertainty is calibrated, physical and semantic states remain coherent, and downstream planning improves. Low prediction error is valuable only when the information preserved by the model supports reliable decisions in the physical environment.

For Physical AI, objective design defines what the world model learns to care about. Effective training combines future-state accuracy with temporal consistency, physical plausibility, semantic relevance, uncertainty representation, and task utility. By coordinating these signals across multiple horizons and representations, predictive learning can transform raw embodied experience into an internal model capable of anticipation, simulation, planning, and intelligent physical action.

학습 목적 함수(Training Objectives)는 예측형 월드 모델(Predictive World Model)이 미래에 관해 무엇을 보존하도록 학습할지를 결정한다. 모델은 시간적 데이터(Temporal Data)를 관측하는 것만으로 피지컬 AI(Physical AI)에 가장 유용한 표현(Representation)을 자동으로 발견하는 것은 아니다. 손실 함수(Loss Function)는 어떤 예측 오류가 중요한지, 어떤 구조가 안정적으로 유지되어야 하는지, 미래 상태의 어떤 측면에 모델 용량(Model Capacity)을 할당해야 하는지를 정의한다. 따라서 목적 함수 설계(Objective Design)는 아키텍처 자체만큼이나 내부 월드 표현(Internal World Representation)의 형성에 중요한 영향을 미친다.

가장 단순한 목적 함수(Objective)는 예측된 다음 상태 (\\hat{s}\*{t+1})과 실제 관측된 목표 상태 (s\*{t+1})을 비교한다. 일반적인 형태는 (L=L(\\hat{s}\*{t+1},s\*{t+1}))로 표현할 수 있다. 개념적으로는 단순하지만 이 손실의 의미는 예측되는 상태 표현(State Representation)에 따라 크게 달라진다. 이미지(Image), 기하학(Geometry), 점유 상태(Occupancy), 움직임(Motion), 의미적 속성(Semantic Attributes), 잠재 특징(Latent Features)은 각각 서로 다른 유사도 측정 방식과 예측 품질에 대한 서로 다른 가정을 필요로 한다.

회귀 목적 함수(Regression Objectives)는 위치(Position), 방향(Orientation), 속도(Velocity), 가속도(Acceleration), 힘(Force), 깊이(Depth), 관절 구성(Joint Configuration)과 같은 연속적인 물리량(Continuous Physical Quantities)에 일반적으로 사용된다. 평균 제곱 오차(Mean Squared Error)와 관련 거리 측정 방식은 예측값과 관측값 사이의 수치적 일치를 유도한다. 그러나 물리적으로 서로 다른 여러 미래가 가능할 경우 평균적인 수치 오차만 최소화하면 실제로는 존재하지 않는 비현실적인 평균 상태로 예측이 수렴할 수 있다.

분류 목적 함수(Classification Objectives)는 미래 상태가 이산적인 의미 변수(Discrete Semantic Variables)를 포함할 때 적합하다. 예측 모델은 특정 영역이 자유 공간(Free)으로 유지될지 점유 상태(Occupied)가 될지, 객체가 안정적인 상태를 유지할지, 접촉(Contact)이 발생할지, 또는 조작 단계(Manipulation Stage)가 성공할지를 추정할 수 있다. 교차 엔트로피(Cross-Entropy)와 관련 손실 함수는 이러한 범주에 대한 확률을 학습하여 미래 예측을 의미적 및 과업 수준 해석(Task-Level Interpretation)과 연결할 수 있다.

공간 예측(Spatial Prediction)에는 기하학적 구조(Geometric Organization)를 보존하는 목적 함수가 필요하다. 미래 점유 격자(Future Occupancy Grids), 조감도 표현(Bird's-Eye-View Representations), 깊이 필드(Depth Fields), 분할 지도(Segmentation Maps), 복셀 구조(Voxel Structures)는 서로 인접한 위치 사이의 관계를 포함하며, 독립적인 스칼라 손실만으로는 이러한 관계를 충분히 포착하지 못할 수 있다. 공간 손실(Spatial Losses)은 경계(Boundaries), 점유 영역(Occupied Regions), 기하학적 일관성(Geometric Consistency), 또는 작은 위치 오차도 계획에 큰 영향을 미칠 수 있는 안전 중요 영역(Safety-Critical Areas)을 강조할 수 있다.

움직임 목적 함수(Motion Objectives)는 변위(Displacement), 속도, 가속도, 옵티컬 플로우(Optical Flow), 장면 흐름(Scene Flow), 객체 궤적(Object Trajectories)을 명시적으로 지도할 수 있다. 이러한 물리량을 별도로 예측하면 월드 모델이 재구성된 관측으로부터 움직임을 간접적으로 추론하는 대신 동적 구조(Dynamic Structure)를 직접 학습하도록 할 수 있다. 움직임 일관성 손실(Motion Consistency Losses)은 예측된 위치와 속도가 시간에 걸쳐 서로 일치하도록 추가적으로 제한하여 장기 롤아웃(Long Rollout)에서 물리적으로 일관되지 않은 궤적을 감소시킬 수 있다.

픽셀 재구성(Pixel Reconstruction)은 시각적 예측 모델(Visual Predictive Model)에서 사용할 수 있는 하나의 목적 함수이다. 모델은 미래 이미지를 예측하고 이를 실제 미래 프레임(Future Frame)과 비교한다. 이러한 방식은 수동 라벨(Manual Labels) 없이 밀집된 지도 신호(Dense Supervision)를 제공하지만, 픽셀 수준 정확도(Pixel-Level Accuracy)는 행동과 거의 관련이 없는 텍스처(Texture), 조명(Lighting), 기타 세부 사항에 지나치게 많은 모델 용량을 할당할 수 있다. 피지컬 AI에서는 재구성 목적을 기하학, 동역학, 의미 정보에 집중하는 목적 함수와 결합할 때 더욱 유용한 경우가 많다.

잠재 예측(Latent Prediction)은 모든 센서 세부 사항을 재구성하는 대신 특징 공간(Feature Space)에서 미래 표현을 예측한다. 인코더(Encoder)는 관측을 잠재 상태 (z_t)로 변환하고, 예측 모델은 미래 목표 표현 (z_{t+k})에 대응하는 (\\hat{z}_{t+k})를 추정한다. 목적 함수는 학습된 표현이 시간적으로 예측 가능한 구조를 갖도록 유도하면서, 후속 행동에 필요한 정보를 잠재 공간에 유지하는 조건 아래 중요하지 않은 시각적 변동(Visual Variation)을 제거할 수 있도록 한다.

표현 학습 목적 함수(Representation Learning Objectives)는 자명한 해(Trivial Solutions)도 방지해야 한다. 예측 표현과 목표 표현이 거의 동일한 상수로 붕괴(Collapse)한다면 의미 있는 세계 구조를 학습하지 않고도 예측 손실이 작아질 수 있다. 대조 학습(Contrastive Learning), 분산 정규화(Variance Regularization), 그래디언트 차단(Stop-Gradient) 메커니즘, 재구성 제약(Reconstruction Constraints), 신중하게 설계된 목표 네트워크(Target Networks)는 잠재 표현의 시간적 예측 가능성을 유지하면서도 충분한 정보를 보존하도록 도울 수 있다.

다단계 목적 함수(Multi-Step Objectives)는 학습을 즉각적인 다음 상태의 정확도를 넘어 확장한다. 하나의 상태 전이만 최적화하는 대신 모델은 예측 지평 (H) 전체의 손실을 최소화할 수 있으며, 개념적으로 (L_{\\text{multi}}=\\sum_{k=1}\^{H}w_kL(\\hat{s}\*{t+k},s\*{t+k}))로 표현할 수 있다. 이를 통해 모델은 재귀적 오류(Recursive Errors)의 영향을 학습 과정에서 경험하고 더 긴 상상 롤아웃(Imagined Rollouts)에 걸쳐 안정적이고 유용하게 유지되는 동역학을 학습할 수 있다.

가중치 (w_k)는 서로 다른 시간적 지평(Temporal Horizons)이 학습에 얼마나 강하게 영향을 미치는지를 결정한다. 단기 예측(Near-Term Prediction)은 더 신뢰할 수 있고 제어와 직접적으로 관련되기 때문에 높은 가중치를 받을 수 있으며, 먼 미래의 예측은 거친 구조(Coarse Structure)나 의미적 결과(Semantic Outcomes)를 더욱 강조할 수 있다. 반대로 미래 상황에 대한 예상(Anticipation)이 중요한 과업에서는 장기 지평에 상당한 중요도를 부여할 수도 있다. 따라서 지평 가중치(Horizon Weighting)는 학습 목적 함수를 시스템이 의도하는 시간적 행동과 연결한다.

시간적 일관성 목적 함수(Temporal Consistency Objectives)는 인접한 예측들이 하나의 일관된 변화 과정을 설명하도록 유도한다. 이러한 손실은 갑작스러운 객체 정체성 변화(Identity Changes), 호환되지 않는 움직임, 일관되지 않은 점유 상태 또는 물리적 근거가 없는 의미적 전이(Semantic Transitions)에 페널티를 부여할 수 있다. 지평 간 일관성(Cross-Horizon Consistency)은 직접 예측된 여러 미래 상태가 서로 독립적인 추측이 아니라 동일한 가능한 미래의 서로 다른 시점을 나타내도록 제한할 수도 있다.

물리적 일관성 목적 함수(Physical Consistency Objectives)는 체화(Embodiment)와 환경 동역학(Environmental Dynamics)에 관한 지식을 학습 과정에 도입한다. 운동학적 한계(Kinematic Limits), 가속도 제한(Acceleration Bounds), 강체 가정(Rigid-Body Assumptions), 충돌 제약(Collision Constraints), 접촉 관계(Contact Relationships), 근사적인 운동 방정식(Equations of Motion)을 페널티 또는 정규화 항(Regularizers)으로 사용할 수 있다. 이러한 목적은 학습 모델이 정확한 해석적 시뮬레이터(Analytical Simulator)를 그대로 재현하도록 요구하는 것이 아니라 물리 시스템의 기본적인 특성을 위반하는 예측을 억제한다.

행동 조건부 목적 함수(Action-Conditioned Objectives)는 예측된 미래가 제어 입력(Control Inputs)에 올바르게 반응하도록 보장한다. 두 개의 후보 행동(Candidate Actions)이 서로 다른 결과를 만들어야 한다면 학습된 표현 역시 이러한 차이를 보존해야 한다. 따라서 학습 과정에서는 실제로 관측된 행동에 따른 상태 전이를 비교하여 제어 가능한 변화(Controllable Changes)를 강조할 수 있다. 이는 월드 모델이 이후 계획(Planning)이나 모델 예측 제어(Model Predictive Control)를 위해 대안적 행동을 시뮬레이션하는 데 사용될 경우 필수적이다.

하나의 미래 목표만으로 불확실성(Uncertainty)을 충분히 표현할 수 없는 경우에는 확률적 목적 함수(Probabilistic Objectives)가 필요하다. 우도 기반 손실(Likelihood-Based Losses)은 예측된 확률 분포를 학습할 수 있으며, 확률적 잠재 변수 모델(Stochastic Latent-Variable Models)은 가능한 궤적들의 분포를 학습할 수 있다. 목적 함수는 실제로 가능한 미래에 높은 확률을 부여하면서도 근거 없는 과도한 확신이나 후속 의사결정에 거의 도움이 되지 않을 정도로 지나치게 넓은 불확실성을 방지해야 한다.

보정 목적 함수(Calibration Objectives)는 예측된 신뢰도(Confidence)를 경험적으로 관측되는 정확도와 더욱 일치시킬 수 있다. 모델이 어떤 사건에 90퍼센트의 신뢰도를 부여한다면 유사한 조건에서 실제로도 대략 그 정도의 비율로 정확해야 한다. 잘 보정된 불확실성(Well-Calibrated Uncertainty)은 계획기가 신뢰도 추정을 이용하여 안전 여유(Margins)를 결정하거나, 속도를 낮추거나, 추가 센싱(Additional Sensing)을 요청하거나, 위험한 행동을 거부할 수 있기 때문에 안전 중요 피지컬 AI(Safety-Critical Physical AI)에서 특히 중요하다.

질적으로 서로 다른 여러 미래가 가능한 경우에는 다중 모드 목적 함수(Multimodal Objectives)가 필요하다. 인간의 움직임, 교통 행동(Traffic Behavior), 접촉 결과(Contact Outcomes), 객체 상호작용은 빈번하게 여러 방향으로 분기되는 가능성을 만든다. 학습은 이러한 미래들을 하나의 평균값으로 합치는 대신 서로 구별되는 가설(Distinct Hypotheses)로 유지할 수 있어야 한다. 혼합 분포(Mixture Distributions), 다중 궤적 예측(Multiple Trajectory Predictions), 확률적 샘플(Stochastic Samples), 다양성 촉진 목적 함수(Diversity-Promoting Objectives)를 통해 상대적인 가능성을 유지하면서 대안적인 미래를 표현할 수 있다.

의미 및 행동 가능성 목적 함수(Semantic and Affordance Objectives)는 예측을 미래 상태의 운용적 의미(Operational Meaning)와 연결한다. 모델은 객체가 파지 가능(Graspable) 상태가 될지, 경로가 계속 주행 가능(Traversable)할지, 접촉이 성공할지, 또는 과업 단계가 완료될지를 예측하도록 학습할 수 있다. 이러한 목적 함수는 단순히 관측되는 외형을 재현하는 것보다 실제 행동과 직접적으로 관련된 정보를 표현에 보존하도록 유도한다.

과업 지향 목적 함수(Task-Oriented Objectives)는 예측된 표현이 성공적인 의사결정(Decision Making)을 지원하는지를 직접 평가하는 수준으로 확장될 수 있다. 잠재 월드 모델(Latent World Model)은 예측을 이용하여 계획기가 안전하고 효과적인 행동을 선택할 수 있다면 환경을 완벽하게 재구성할 필요가 없을 수 있다. 따라서 가치(Value), 보상(Reward), 목표 진행도(Goal Progress), 충돌 위험(Collision Risk), 과업 성공(Task Success)을 위한 보조 손실(Auxiliary Losses)을 사용하여 제어와 장기 추론에 중요한 변수 중심으로 예측 표현을 형성할 수 있다.

자기지도 목적 함수(Self-Supervised Objectives)는 순차적인 센서 데이터(Sequential Sensor Data)가 자연스럽게 미래 목표를 제공한다는 점에서 특히 중요하다. 카메라(Camera), 라이다(LiDAR), 고유수용감각(Proprioception), 로봇 상태(Robot States), 행동(Actions)으로부터 운용 중 수집된 데이터는 모든 상태 변수를 사람이 직접 라벨링하지 않더라도 시간적 지도 신호(Temporal Supervision)를 제공한다. 미래 자체가 학습 신호가 되므로 대규모 체화 경험(Embodied Experience)을 표현 및 동역학 학습(Representation and Dynamics Learning)에 활용할 수 있다.

약한 지도 학습(Weakly Supervised Learning)과 부분 라벨 데이터(Partially Labeled Data)는 자기지도 학습(Self-Supervision)을 보완할 수 있다. 일부 궤적에는 의미 라벨(Semantic Labels), 과업 결과, 객체 정체성 또는 상호작용 주석(Interaction Annotations)이 포함될 수 있지만 대부분의 데이터에는 원시 시간 관측만 존재할 수 있다. 밀집된 자기지도 예측(Dense Self-Supervised Prediction)과 희소한 의미 지도(Sparse Semantic Supervision)를 결합하면 대규모 데이터셋을 활용하면서 학습된 특징을 계획과 물리적 추론에 유용한 개념과 정렬할 수 있다.

실용적인 월드 모델(World Model)은 일반적으로 하나의 손실 함수에만 의존하지 않고 여러 목적 함수를 결합한다. 전체 목적 함수는 (L=\\lambda_1L_{\\text{state}}+\\lambda_2L_{\\text{motion}}+\\lambda_3L_{\\text{semantic}}+\\lambda_4L_{\\text{consistency}}+\\lambda_5L_{\\text{uncertainty}}+\\lambda_6L_{\\text{task}})와 같이 표현할 수 있다. 각 계수는 정확한 물리적 예측, 안정적인 표현, 의미적 이해(Semantic Understanding), 불확실성 인식(Uncertainty Awareness), 운용적 유용성(Operational Usefulness) 사이의 균형을 결정한다.

이러한 목적 함수들의 균형을 조절하는 것 자체가 중요한 학습 문제이다. 재구성(Reconstruction)이 지나치게 지배적이면 모델은 외형에 과도하게 집중할 수 있고, 의미적 손실이 지나치게 강하면 세밀한 물리적 동역학을 잃을 수 있다. 일관성 제약(Consistency Constraints)이 너무 강하면 실제로 발생하는 급격한 사건까지 억제될 수 있다. 따라서 목적 함수 가중치(Objective Weights), 스케줄(Schedules), 정규화(Normalization), 적응형 균형 조정 방법(Adaptive Balancing Methods)은 데이터, 아키텍처, 예측 지평, 피지컬 AI 응용 목적을 반영해야 한다.

학습 목적 함수는 궁극적으로 검증 데이터(Held-Out Data)의 손실값만으로 평가해서는 안 된다. 예측형 모델은 롤아웃이 안정적으로 유지되는지, 불확실성이 적절하게 보정되는지, 물리적 상태와 의미 상태가 일관성을 유지하는지, 그리고 후속 계획(Downstream Planning)의 성능이 향상되는지를 기준으로 평가해야 한다. 낮은 예측 오차는 모델이 보존한 정보가 실제 물리적 환경에서 신뢰할 수 있는 의사결정을 지원할 때 비로소 실질적인 가치를 갖는다.

피지컬 AI(Physical AI)에서 목적 함수 설계(Objective Design)는 월드 모델이 무엇을 중요하게 학습할지를 정의한다. 효과적인 학습은 미래 상태 정확도(Future-State Accuracy)를 시간적 일관성(Temporal Consistency), 물리적 타당성(Physical Plausibility), 의미적 관련성(Semantic Relevance), 불확실성 표현(Uncertainty Representation), 과업 유용성(Task Utility)과 결합한다. 이러한 학습 신호를 여러 예측 지평과 표현 수준에 걸쳐 조정함으로써 예측 학습(Predictive Learning)은 원시 체화 경험을 예상(Anticipation), 시뮬레이션(Simulation), 계획(Planning), 지능적인 물리적 행동(Intelligent Physical Action)이 가능한 내부 모델(Internal Model)로 변환할 수 있다.

##  

## 02.10. Multi Step Predictive Model [w/Code]

![](images/image11.png){width="7.268055555555556in" height="7.268055555555556in"}

A multi-step predictive model extends learned dynamics from immediate transition prediction into structured reasoning over sequences of future states. Rather than estimating only (s_{t+1}), it predicts a horizon (s_{t+1},s_{t+2},\\ldots,s_{t+H}). This capability transforms a local dynamics predictor into a practical world model that can anticipate trajectories, interactions, risks, and consequences before physical actions are executed.

The model begins with an internal representation of the present. Observations from cameras, LiDAR, proprioception, maps, or other sensors can be encoded into a state (s_t) or latent state (z_t). Historical observations may also be integrated to estimate motion and hidden conditions. The resulting representation should contain enough information about geometry, dynamics, objects, semantics, and agent state to support prediction across the intended horizon.

When the agent can influence the environment, future prediction must be conditioned on actions. A transition model can be expressed as (\\hat{s}\*{t+k+1}=f(\\hat{s}\*{t+k},a_{t+k})). Given a candidate action sequence (a_t,\\ldots,a_{t+H-1}), the model predicts the corresponding future evolution. It therefore estimates not merely what may happen naturally, but what may happen if the agent performs a particular sequence of physical actions.

One implementation is autoregressive prediction, in which each predicted state becomes the input for the next transition. This provides a flexible mechanism for generating trajectories of arbitrary length using a shared dynamics model. However, recursive prediction also introduces error accumulation because inaccuracies in early predicted states influence later predictions. Long-horizon stability therefore becomes a central design requirement.

A second implementation predicts multiple future horizons directly or in parallel. The model can estimate states at selected future offsets from a common present representation without recursively traversing every intermediate step. Direct prediction reduces sequential inference latency and recursive error propagation, although independently generated horizons must still satisfy temporal and physical consistency.

Practical multi-step models can combine both approaches. Parallel prediction may establish anchor states at several future horizons, while autoregressive transitions provide detailed intermediate evolution. Such hybrid architectures can exploit the speed and stability of direct prediction together with the temporal flexibility of recursive rollout. The appropriate balance depends on control frequency, computational resources, and prediction horizon.

Temporal resolution need not remain constant across the rollout. Near-term prediction may operate at high frequency to represent precise motion, contact, and collision risk, whereas longer horizons may use increasingly coarse intervals. This hierarchical temporal structure concentrates computation where precision matters most and avoids demanding unrealistic geometric accuracy from distant predictions whose uncertainty is inherently larger.

Representational detail can similarly change with temporal distance. Near the present, the model may preserve position, velocity, occupancy, object pose, and contact information. At longer horizons, semantic states such as reachable, blocked, stable, safe, or task completed may become more useful than exact coordinates. Multi-step prediction can therefore evolve from detailed physical forecasting toward increasingly abstract situation forecasting.

Latent-state prediction is particularly suitable for this architecture. Instead of reconstructing complete future sensor observations at every step, the model rolls compact latent states forward through learned dynamics. These states can preserve decision-relevant information while discarding unpredictable visual details. Specialized prediction heads can decode geometry, motion, occupancy, semantics, uncertainty, reward, or other quantities only when they are required.

Object-centric representations offer another useful structure. Rather than representing the entire environment as one undifferentiated vector, the model can maintain persistent entities with attributes such as identity, pose, velocity, semantic category, and interaction state. Multi-step prediction then estimates how these entities and their relationships evolve, improving reasoning about collisions, cooperation, manipulation, and other interactions.

Relational modeling becomes increasingly important when multiple entities influence one another. A pedestrian trajectory may depend on robot motion, one vehicle may react to another, and an object may move because it contacts a manipulator. Graph-based or attention-based interaction models can represent these dependencies, allowing predicted futures to reflect coupled dynamics rather than treating every object as an independent trajectory.

Partial observability requires memory. A single current observation may not reveal object velocity, hidden obstacles, contact history, or another agent's behavioral trend. Recurrent networks, temporal transformers, state-space models, or persistent latent memories can integrate previous observations before prediction begins. The resulting internal state provides a richer initial condition for long-horizon rollout.

Uncertainty must propagate through the multi-step model because confidence normally decreases as predictions extend farther from observed evidence. Near-term states may have narrow uncertainty, while distant states may support several plausible outcomes. Probabilistic prediction can represent distributions, stochastic latent states, ensembles, or multiple trajectory hypotheses rather than presenting one distant future as certain.

Multimodal prediction is essential when future evolution can branch qualitatively. A pedestrian may stop or cross, another robot may yield or continue, and a manipulated object may remain stable or slip. A useful multi-step model preserves these alternatives as distinct hypotheses and propagates each into a coherent future. Planning can then evaluate both likely outcomes and lower-probability but safety-critical possibilities.

Temporal consistency constrains the entire predicted sequence. Object identities should persist, motion should evolve compatibly with velocity and acceleration, semantic transitions should follow plausible sequences, and relationships should not change without explanation. The objective is not merely to generate plausible states independently, but to produce a trajectory representing one physically and causally coherent evolution of the world.

Physical constraints can further stabilize long rollouts. Robot kinematics, acceleration limits, rigid-body assumptions, collision rules, contact constraints, and approximate analytical dynamics can restrict impossible transitions. Learned models can focus on complex environmental effects and residual dynamics while known physical structure provides boundaries within which predictions should remain plausible.

Training should therefore optimize more than one-step prediction accuracy. A multi-step objective can be expressed as (L_{\\text{multi}}=\\sum_{k=1}\^{H}w_kL(\\hat{s}\*{t+k},s\*{t+k})), where the weights (w_k) determine the importance of different horizons. Training across multiple steps exposes the model to the consequences of prediction errors and encourages transitions that remain stable when repeatedly applied.

The training process should also account for the difference between ground-truth inputs and predicted inputs. A model trained exclusively with correct historical states may become unstable when its own imperfect predictions are used during deployment. Rollout training, scheduled sampling, or related techniques can expose the predictor to self-generated states, helping it learn how to recover from small deviations rather than amplifying them.

Multiple losses can supervise different aspects of the predicted future. Regression losses can train pose and motion, spatial objectives can supervise occupancy and geometry, classification losses can train semantic states, and probabilistic objectives can model uncertainty. Consistency, physical, affordance, reward, and task-oriented losses can be added so that the internal representation remains useful for both prediction and decision making.

Sequential experience naturally supports self-supervised training because future observations provide prediction targets. Large quantities of robot trajectories, driving sequences, manipulation episodes, simulation data, and multimodal sensor logs can therefore train predictive dynamics without complete manual labeling. Weak semantic labels and task outcomes can supplement this signal and align learned states with operationally meaningful concepts.

The multi-step model becomes an internal simulator when connected to a planner. Several candidate action sequences can be proposed and propagated through the predictive model. Their resulting futures can then be compared according to collision risk, goal progress, stability, energy use, traversability, manipulation success, or other objectives. Prediction thereby becomes a mechanism for evaluating actions before committing to them physically.

Model predictive control provides a practical closed-loop implementation. The model predicts a finite future horizon, the planner selects an action sequence, and the robot executes only the first action or short portion. New observations are then collected, the internal state is corrected, and prediction begins again. Receding-horizon operation repeatedly anchors imagined futures to reality and limits uncontrolled accumulation of prediction error.

Prediction horizon should be selected according to decision requirements rather than maximized without purpose. Very short horizons may provide insufficient anticipation, while excessively long horizons can consume computation and produce highly uncertain states with little operational value. An effective model predicts far enough to reveal consequences relevant to current decisions while preserving sufficient accuracy and uncertainty awareness.

Evaluation must therefore consider rollout quality rather than only one-step loss. Important criteria include trajectory drift, identity preservation, physical constraint violations, semantic consistency, uncertainty calibration, cross-horizon agreement, computational latency, and downstream planning performance. A model with slightly higher local error may be more useful if its long-term predictions remain coherent and produce safer decisions.

A multi-step predictive model ultimately connects perception, memory, dynamics, uncertainty, and action within one temporal reasoning system. It converts the current estimated state into multiple possible future evolutions, evaluates how candidate actions modify those futures, and repeatedly corrects prediction using new observations. This creates the predictive foundation required for anticipation rather than purely reactive behavior.

For Physical AI, the purpose of multi-step prediction is not perfect reconstruction of an unknowable distant future. Its purpose is to preserve enough physical, spatial, relational, semantic, and uncertainty information to distinguish safe and useful action sequences from dangerous or ineffective ones. In this role, the multi-step predictive model becomes the computational bridge from learned world dynamics to imagination, planning, control, and intelligent physical behavior.

다단계 예측 모델(Multi-Step Predictive Model)은 학습된 동역학(Learned Dynamics)을 즉각적인 상태 전이 예측(Immediate Transition Prediction)에서 미래 상태 시퀀스에 대한 구조화된 추론(Structured Reasoning)으로 확장한다. 단순히 (s_{t+1})만 추정하는 것이 아니라 (s_{t+1},s_{t+2},\\ldots,s_{t+H})의 지평(Horizon)을 예측한다. 이러한 능력은 국소 동역학 예측기(Local Dynamics Predictor)를 실제 물리적 행동이 실행되기 전에 궤적(Trajectories), 상호작용(Interactions), 위험(Risks), 결과(Consequences)를 예상할 수 있는 실용적인 월드 모델(World Model)로 전환한다.

모델은 현재에 대한 내부 표현(Internal Representation)에서 시작한다. 카메라(Camera), 라이다(LiDAR), 고유수용감각(Proprioception), 지도(Maps), 기타 센서의 관측을 상태 (s_t) 또는 잠재 상태(Latent State) (z_t)로 인코딩할 수 있다. 움직임과 숨겨진 조건(Hidden Conditions)을 추정하기 위해 과거 관측도 통합할 수 있다. 이렇게 생성된 표현은 의도한 예측 지평 전체를 지원할 수 있도록 기하학(Geometry), 동역학(Dynamics), 객체(Objects), 의미(Semantics), 에이전트 상태(Agent State)에 관한 충분한 정보를 포함해야 한다.

에이전트가 환경에 영향을 미칠 수 있는 경우 미래 예측은 행동(Action)을 조건으로 해야 한다. 전이 모델(Transition Model)은 (\\hat{s}\*{t+k+1}=f(\\hat{s}\*{t+k},a_{t+k}))로 표현할 수 있다. 후보 행동 시퀀스(Candidate Action Sequence) (a_t,\\ldots,a_{t+H-1})가 주어지면 모델은 이에 대응하는 미래 변화를 예측한다. 따라서 모델은 단순히 자연적으로 어떤 일이 발생할지를 추정하는 것이 아니라 에이전트가 특정한 물리적 행동 시퀀스를 수행할 경우 어떤 일이 발생할지를 추정한다.

하나의 구현 방식은 자기회귀적 예측(Autoregressive Prediction)으로, 각각의 예측 상태가 다음 상태 전이를 위한 입력이 된다. 이 방식은 하나의 공유 동역학 모델(Shared Dynamics Model)을 사용하여 임의 길이의 궤적을 생성할 수 있는 유연한 메커니즘을 제공한다. 그러나 재귀적 예측(Recursive Prediction)은 초기 예측 상태의 부정확성이 이후 예측에 영향을 주기 때문에 오차 누적(Error Accumulation) 문제를 발생시킨다. 따라서 장기 지평 안정성(Long-Horizon Stability)이 핵심적인 설계 요구사항이 된다.

두 번째 구현 방식은 여러 미래 지평(Future Horizons)을 직접 또는 병렬로 예측하는 것이다. 모델은 모든 중간 단계를 재귀적으로 통과하지 않고도 공통된 현재 표현(Common Present Representation)으로부터 선택된 미래 시간 오프셋(Future Time Offsets)의 상태를 추정할 수 있다. 직접 예측(Direct Prediction)은 순차적 추론 지연(Sequential Inference Latency)과 재귀적 오류 전파(Recursive Error Propagation)를 줄일 수 있지만, 독립적으로 생성된 미래 지평들은 여전히 시간적 및 물리적 일관성(Temporal and Physical Consistency)을 만족해야 한다.

실용적인 다단계 모델(Multi-Step Model)은 두 접근법을 결합할 수 있다. 병렬 예측(Parallel Prediction)은 여러 미래 지평에 기준 상태(Anchor States)를 설정하고, 자기회귀적 전이(Autoregressive Transitions)는 그 사이의 세부적인 변화를 생성할 수 있다. 이러한 하이브리드 아키텍처(Hybrid Architecture)는 직접 예측의 속도와 안정성, 재귀적 롤아웃(Recursive Rollout)의 시간적 유연성을 함께 활용할 수 있다. 적절한 균형은 제어 주파수(Control Frequency), 계산 자원(Computational Resources), 예측 지평에 따라 달라진다.

시간 해상도(Temporal Resolution)는 전체 롤아웃에서 일정하게 유지될 필요가 없다. 단기 예측(Near-Term Prediction)은 정밀한 움직임, 접촉(Contact), 충돌 위험(Collision Risk)을 표현하기 위해 높은 주파수로 수행할 수 있지만, 장기 지평에서는 점차 더 거친 시간 간격(Coarser Intervals)을 사용할 수 있다. 이러한 계층적 시간 구조(Hierarchical Temporal Structure)는 정밀도가 가장 중요한 영역에 계산 자원을 집중하고, 본질적으로 불확실성이 더 큰 먼 미래에 비현실적인 기하학적 정확도를 요구하는 것을 방지한다.

표현의 세부 수준(Representational Detail)도 시간적 거리에 따라 변화할 수 있다. 현재에 가까운 시점에서는 위치(Position), 속도(Velocity), 점유 상태(Occupancy), 객체 자세(Object Pose), 접촉 정보를 유지할 수 있다. 더 긴 지평에서는 도달 가능(Reachable), 차단(Blocked), 안정(Stable), 안전(Safe), 과업 완료(Task Completed)와 같은 의미 상태(Semantic States)가 정확한 좌표보다 더 유용할 수 있다. 따라서 다단계 예측은 상세한 물리적 예측에서 점차 추상적인 상황 예측(Situation Forecasting)으로 발전할 수 있다.

잠재 상태 예측(Latent-State Prediction)은 이러한 아키텍처에 특히 적합하다. 모델은 모든 단계에서 완전한 미래 센서 관측을 재구성하는 대신 압축된 잠재 상태(Compact Latent States)를 학습된 동역학을 통해 미래로 전개한다. 이러한 상태는 예측하기 어려운 시각적 세부 사항을 제거하면서 의사결정 관련 정보(Decision-Relevant Information)를 보존할 수 있다. 전문화된 예측 헤드(Specialized Prediction Heads)는 필요한 경우에만 기하학, 움직임, 점유 상태, 의미, 불확실성, 보상(Reward) 또는 기타 물리량을 디코딩할 수 있다.

객체 중심 표현(Object-Centric Representations)은 또 다른 유용한 구조를 제공한다. 전체 환경을 하나의 구분되지 않은 벡터로 표현하는 대신 모델은 정체성(Identity), 자세, 속도, 의미 범주(Semantic Category), 상호작용 상태(Interaction State)와 같은 속성을 가진 지속적인 개체(Persistent Entities)를 유지할 수 있다. 다단계 예측은 이러한 개체와 그 관계가 어떻게 변화하는지를 추정하여 충돌, 협력(Cooperation), 조작(Manipulation), 기타 상호작용에 대한 추론 능력을 향상시킨다.

여러 개체가 서로 영향을 주는 경우 관계 모델링(Relational Modeling)은 더욱 중요해진다. 보행자의 궤적은 로봇의 움직임에 따라 달라질 수 있고, 한 차량은 다른 차량의 행동에 반응할 수 있으며, 객체는 매니퓰레이터(Manipulator)와 접촉하여 움직일 수 있다. 그래프 기반(Graph-Based) 또는 어텐션 기반 상호작용 모델(Attention-Based Interaction Model)은 이러한 의존성을 표현하여 각각의 객체를 독립적인 궤적으로 취급하는 대신 결합된 동역학(Coupled Dynamics)을 미래 예측에 반영할 수 있다.

부분 관측 가능성(Partial Observability)은 메모리(Memory)를 필요로 한다. 하나의 현재 관측만으로는 객체 속도, 숨겨진 장애물(Hidden Obstacles), 접촉 이력(Contact History), 다른 에이전트의 행동 추세(Behavioral Trend)를 파악하지 못할 수 있다. 순환 신경망(Recurrent Networks), 시간적 트랜스포머(Temporal Transformers), 상태 공간 모델(State-Space Models), 지속적인 잠재 메모리(Persistent Latent Memories)는 예측을 시작하기 전에 이전 관측들을 통합할 수 있다. 이렇게 형성된 내부 상태는 장기 지평 롤아웃을 위한 더욱 풍부한 초기 조건(Initial Condition)을 제공한다.

예측이 관측된 증거에서 멀어질수록 일반적으로 신뢰도가 감소하기 때문에 불확실성(Uncertainty)은 다단계 모델 전체를 통해 전파되어야 한다. 단기 상태는 좁은 불확실성 범위를 가질 수 있지만 먼 미래 상태에는 여러 가능한 결과가 존재할 수 있다. 확률적 예측(Probabilistic Prediction)은 하나의 먼 미래를 확정된 것으로 제시하는 대신 확률 분포(Distributions), 확률적 잠재 상태(Stochastic Latent States), 앙상블(Ensembles), 다중 궤적 가설(Multiple Trajectory Hypotheses)을 표현할 수 있다.

미래 변화가 질적으로 여러 방향으로 분기될 수 있는 경우 다중 모드 예측(Multimodal Prediction)이 필수적이다. 보행자는 멈추거나 횡단할 수 있고, 다른 로봇은 양보하거나 계속 이동할 수 있으며, 조작되는 객체는 안정적으로 유지되거나 미끄러질 수 있다. 유용한 다단계 모델은 이러한 대안들을 서로 구별되는 가설(Distinct Hypotheses)로 유지하고 각각을 일관된 미래로 전개한다. 계획기는 이를 통해 가능성이 높은 결과뿐 아니라 확률은 낮지만 안전에 중요한 가능성도 평가할 수 있다.

시간적 일관성(Temporal Consistency)은 예측된 전체 시퀀스를 제한한다. 객체의 정체성은 지속되어야 하고, 움직임은 속도와 가속도에 부합하도록 변화해야 하며, 의미적 전이(Semantic Transitions)는 타당한 순서를 따라야 하고, 관계는 설명 가능한 원인 없이 변화해서는 안 된다. 목표는 각각 독립적으로 그럴듯한 상태를 생성하는 것이 아니라 하나의 물리적이고 인과적으로 일관된 세계 변화(Physically and Causally Coherent Evolution)를 나타내는 궤적을 생성하는 것이다.

물리적 제약(Physical Constraints)은 장기 롤아웃을 더욱 안정화할 수 있다. 로봇 운동학(Robot Kinematics), 가속도 한계(Acceleration Limits), 강체 가정(Rigid-Body Assumptions), 충돌 규칙(Collision Rules), 접촉 제약(Contact Constraints), 근사적인 해석적 동역학(Analytical Dynamics)을 이용하여 불가능한 상태 전이를 제한할 수 있다. 학습 모델은 복잡한 환경 효과와 잔차 동역학(Residual Dynamics)에 집중하고, 알려진 물리적 구조는 예측이 타당한 범위 안에 머물도록 경계를 제공할 수 있다.

따라서 학습(Training)은 단일 단계 예측 정확도(One-Step Prediction Accuracy) 이상을 최적화해야 한다. 다단계 목적 함수(Multi-Step Objective)는 (L_{\\text{multi}}=\\sum_{k=1}\^{H}w_kL(\\hat{s}\*{t+k},s\*{t+k}))로 표현할 수 있으며, 가중치 (w_k)는 서로 다른 미래 지평의 중요도를 결정한다. 여러 단계에 걸친 학습은 모델이 예측 오류의 결과를 직접 경험하도록 하고 반복적으로 적용되더라도 안정성을 유지하는 상태 전이를 학습하도록 유도한다.

학습 과정은 실제 정답 입력(Ground-Truth Inputs)과 예측 입력(Predicted Inputs)의 차이도 고려해야 한다. 정확한 과거 상태만을 이용해 학습된 모델은 실제 운용에서 자신의 불완전한 예측이 입력으로 사용될 때 불안정해질 수 있다. 롤아웃 학습(Rollout Training), 예정 샘플링(Scheduled Sampling), 또는 관련 기법을 통해 예측기가 자신이 생성한 상태를 경험하도록 하면 작은 편차를 증폭시키는 대신 그 상태에서 회복하는 방법을 학습하는 데 도움이 된다.

여러 손실 함수(Losses)를 이용하여 예측된 미래의 서로 다른 측면을 지도할 수 있다. 회귀 손실(Regression Losses)은 자세와 움직임을 학습하고, 공간 목적 함수(Spatial Objectives)는 점유 상태와 기하학을 지도하며, 분류 손실(Classification Losses)은 의미 상태를 학습하고, 확률적 목적 함수(Probabilistic Objectives)는 불확실성을 모델링할 수 있다. 또한 일관성, 물리적 제약, 행동 가능성(Affordance), 보상, 과업 지향 손실(Task-Oriented Losses)을 추가하여 내부 표현이 예측과 의사결정 모두에 유용하도록 만들 수 있다.

순차적 경험(Sequential Experience)은 미래 관측 자체가 예측 목표를 제공하기 때문에 자연스럽게 자기지도 학습(Self-Supervised Training)을 지원한다. 대규모 로봇 궤적(Robot Trajectories), 주행 시퀀스(Driving Sequences), 조작 에피소드(Manipulation Episodes), 시뮬레이션 데이터(Simulation Data), 멀티모달 센서 로그(Multimodal Sensor Logs)를 완전한 수동 라벨링 없이 예측 동역학 학습에 활용할 수 있다. 약한 의미 라벨(Weak Semantic Labels)과 과업 결과를 추가하면 학습된 상태를 운용적으로 의미 있는 개념과 정렬할 수 있다.

다단계 모델은 계획기(Planner)와 연결될 때 내부 시뮬레이터(Internal Simulator)가 된다. 여러 후보 행동 시퀀스를 제안하고 예측 모델을 통해 미래로 전개할 수 있다. 그 결과 생성된 미래들을 충돌 위험, 목표 진행도(Goal Progress), 안정성(Stability), 에너지 사용(Energy Use), 주행 가능성(Traversability), 조작 성공(Manipulation Success), 기타 목적에 따라 비교할 수 있다. 이를 통해 예측은 실제 행동을 실행하기 전에 행동의 결과를 평가하는 메커니즘으로 발전한다.

모델 예측 제어(Model Predictive Control)는 실용적인 폐루프 구현(Closed-Loop Implementation)을 제공한다. 모델은 유한한 미래 지평을 예측하고, 계획기는 행동 시퀀스를 선택하며, 로봇은 첫 번째 행동 또는 짧은 구간만 실행한다. 이후 새로운 관측을 수집하고 내부 상태를 보정한 다음 다시 예측을 시작한다. 이러한 이동 지평 운용(Receding-Horizon Operation)은 상상된 미래를 반복적으로 현실에 고정하여 예측 오류가 통제되지 않은 상태로 누적되는 것을 제한한다.

예측 지평(Prediction Horizon)은 목적 없이 최대화하기보다 의사결정 요구사항에 따라 선택해야 한다. 지나치게 짧은 지평은 충분한 예상 능력을 제공하지 못할 수 있으며, 지나치게 긴 지평은 계산 자원을 소비하면서 운용적 가치가 낮고 불확실성이 매우 큰 상태를 생성할 수 있다. 효과적인 모델은 현재 의사결정에 중요한 결과를 파악할 수 있을 만큼 충분히 먼 미래를 예측하면서 적절한 정확도와 불확실성 인식(Uncertainty Awareness)을 유지해야 한다.

따라서 평가는 단일 단계 손실(One-Step Loss)만이 아니라 롤아웃 품질(Rollout Quality)을 고려해야 한다. 중요한 평가 기준에는 궤적 드리프트(Trajectory Drift), 정체성 유지(Identity Preservation), 물리적 제약 위반(Physical Constraint Violations), 의미적 일관성(Semantic Consistency), 불확실성 보정(Uncertainty Calibration), 지평 간 일치(Cross-Horizon Agreement), 계산 지연(Computational Latency), 후속 계획 성능(Downstream Planning Performance)이 포함된다. 국소적인 오차가 약간 크더라도 장기 예측이 일관성을 유지하고 더 안전한 의사결정을 가능하게 한다면 실제 피지컬 AI 시스템에서는 더욱 유용할 수 있다.

다단계 예측 모델(Multi-Step Predictive Model)은 궁극적으로 인식(Perception), 메모리(Memory), 동역학(Dynamics), 불확실성(Uncertainty), 행동(Action)을 하나의 시간적 추론 시스템(Temporal Reasoning System) 안에서 연결한다. 현재의 추정 상태를 여러 가능한 미래 변화로 변환하고, 후보 행동이 이러한 미래를 어떻게 변화시키는지 평가하며, 새로운 관측을 이용하여 예측을 반복적으로 수정한다. 이를 통해 단순한 반응형 행동(Reactive Behavior)을 넘어 예상(Anticipation)을 가능하게 하는 예측 기반을 형성한다.

피지컬 AI(Physical AI)에서 다단계 예측의 목적은 알 수 없는 먼 미래를 완벽하게 재구성하는 것이 아니다. 핵심 목적은 안전하고 유용한 행동 시퀀스와 위험하거나 비효율적인 행동 시퀀스를 구별할 수 있도록 충분한 물리적, 공간적, 관계적, 의미적 정보와 불확실성 정보를 보존하는 것이다. 이러한 역할에서 다단계 예측 모델은 학습된 월드 동역학(Learned World Dynamics)을 상상(Imagination), 계획(Planning), 제어(Control), 지능적인 물리적 행동(Intelligent Physical Behavior)으로 연결하는 계산적 가교(Computational Bridge)가 된다.
