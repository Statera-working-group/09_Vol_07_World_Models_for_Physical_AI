**Volume 07. World Models for Physical AI**

# Chapter 15. World Model to Foundation Model Strategy

## 15.01. From Task Specific to Foundation World Models

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

초기의 로봇공학(Robotics)용 월드 모델(World Model)은 일반적으로 좁게 정의된 작업(Task), 환경(Environment), 센서 구성(Sensor Configuration), 그리고 체화 형태(Embodiment)를 중심으로 설계되었습니다. 내비게이션(Navigation) 모델은 지역 점유(Local Occupancy)를 예측하고, 조작(Manipulation) 모델은 파지(Grasp) 이후의 객체 움직임을 추정할 수 있습니다. 이러한 전문화(Specialization)는 특정 운용 영역에서 뛰어난 성능을 제공하지만, 학습된 표현(Representation)은 원래 작업에 필요한 물리 세계의 일부 특성만 포착하는 경우가 많습니다.

파운데이션 월드 모델(Foundation World Model)은 보다 광범위한 목표를 추구합니다. 하나의 제어기(Controller)나 하나의 로봇에 필요한 동역학(Dynamics)만 학습하는 대신, 객체(Object), 기하학(Geometry), 운동(Motion), 상호작용(Interaction), 인과성(Causality), 불확실성(Uncertainty), 시간적 변화(Temporal Evolution)에 대한 재사용 가능한 표현을 획득하고자 합니다. 이러한 표현은 다양한 물리 환경과 작업에서 지각(Perception), 예측(Prediction), 계획(Planning), 제어(Control), 추론(Reasoning), 적응(Adaptation)을 지원할 수 있습니다.

이러한 전환은 월드 지식(World Knowledge)을 작업 특화 출력(Task-Specific Output)으로부터 분리하는 것에서 시작됩니다. 기존 파이프라인(Pipeline)에서는 지각 특징(Perception Feature)이 특정 예측이나 제어 목표를 직접 최적화하도록 학습될 수 있습니다. 반면 파운데이션 지향 아키텍처(Foundation-Oriented Architecture)는 다양한 목표에 유용한 정보를 보존하는 공유 잠재 상태(Shared Latent State)를 학습합니다. 이후 내비게이션, 조작, 충돌 예측(Collision Prediction), 주행 가능성 추정(Traversability Estimation), 상호작용 추론(Interaction Reasoning) 등이 공통 표현(Common Representation) 위에 구축된 특화 헤드(Specialized Head)를 통해 수행될 수 있습니다.

물리 환경(Physical Environment)은 매우 큰 다양성을 포함하므로 규모(Scale)는 중요합니다. 창고에서만 학습된 모델은 특정 바닥 질감, 객체 배치 또는 움직임 패턴을 특정 결과와 연관시킬 수 있습니다. 공장, 가정, 도로, 야외 지형, 연구실, 시뮬레이션 환경(Simulated Environment) 전반에서 학습하면 물리 상태가 어떻게 변화하는지를 결정하는 보다 일반적인 규칙성(Regularity)을 모델이 발견하도록 유도할 수 있습니다. 목표는 단순히 더 많은 데이터가 아니라 물리적 변화 요인에 대한 더욱 폭넓은 범위(Coverage)를 확보하는 것입니다.

멀티태스크 학습(Multitask Learning)은 파운데이션 능력(Foundation Capability)을 향한 또 다른 경로를 제공합니다. 하나의 공유 모델(Shared Model)은 미래 상태 예측(Future-State Prediction), 점유 추정(Occupancy Estimation), 객체 운동(Object Motion), 의미 이해(Semantic Understanding), 행동 효과(Action Effect), 접촉 사건(Contact Event), 기타 물리적 속성을 동시에 학습할 수 있습니다. 각각의 목표는 내부 표현을 서로 다른 방식으로 제약하며, 이들의 결합은 하나의 좁은 벤치마크(Benchmark)나 로봇 행동에만 적합한 특징이 아니라 지속적으로 유효한 구조를 잠재 공간(Latent Space)에 포착하도록 유도합니다.

파운데이션 월드 모델은 물리적 지능(Physical Intelligence)이 단순한 수동 관찰이 아니라 개입(Intervention)에 의존하기 때문에 행동(Action)도 표현해야 합니다. 모델은 자연적으로 발생할 가능성이 높은 변화와 에이전트(Agent)가 가속, 회전, 파지, 밀기, 열기, 들어 올리기 또는 놓기와 같은 행동을 수행했을 때 발생할 변화를 구분해야 합니다. 따라서 행동 조건부 예측(Action-Conditioned Prediction)은 일반적인 예측 모델을 실제 물리적 실행 이전에 여러 대안적 미래(Alternative Future)를 비교할 수 있는 내부 시뮬레이터(Internal Simulator)로 변화시킵니다.

모델의 범위가 확장될수록 시간적 추상화(Temporal Abstraction)는 더욱 중요해집니다. 저수준 동역학(Low-Level Dynamics)은 바퀴 운동, 접촉, 관절 움직임, 단기 객체 변위와 같은 빠른 변화를 설명하는 반면, 고수준 동역학(High-Level Dynamics)은 방에 진입하거나 조작 단계를 완료하거나 내비게이션 목표에 도달하는 것과 같은 사건을 설명합니다. 파운데이션 월드 모델은 즉각적인 물리적 결과가 장기적인 행동 예측(Long-Horizon Behavioral Prediction)과 일관성을 유지하도록 이러한 서로 다른 시간 척도(Temporal Scale)를 연결해야 합니다.

일반화(Generalization)를 위해서는 보편적인 물리 구조(Universal Physical Structure)를 체화 특화 특성(Embodiment-Specific Characteristics)과 분리하는 것도 필요합니다. 바퀴형 로봇(Wheeled Robot), 4족 보행 로봇(Quadruped), 매니퓰레이터(Manipulator), 휴머노이드(Humanoid), 비행 로봇(Aerial Robot)은 서로 다른 행동 공간(Action Space)과 제약 조건을 가지지만, 자유 공간(Free Space), 장애물(Obstacle), 지지(Support), 충돌(Collision), 운동, 객체 영속성(Object Permanence), 원인과 결과(Cause and Effect)와 같은 많은 공통 개념이 지배하는 세계에서 작동합니다. 공유 표현은 이러한 공통 속성을 인코딩(Encoding)하고, 체화 특화 모듈(Embodiment-Specific Module)은 각 플랫폼이 세계에 어떤 영향을 미칠 수 있는지를 표현할 수 있습니다.

멀티모달 센싱(Multimodal Sensing)은 특화 모델에서 일반적인 물리 표현(General Physical Representation)으로의 전환을 더욱 강화합니다. 카메라(Camera)는 외형과 의미 정보를 제공하고, 라이다(LiDAR)와 깊이 센서(Depth Sensor)는 기하학 정보를 제공하며, 레이더(Radar)는 열악한 가시성에서도 움직임 정보를 포착합니다. 고유수용성 신호(Proprioceptive Signal)는 에이전트 자체의 상태를 설명하며, 언어(Language)는 개념적 정보와 작업 맥락(Task Context)을 추가할 수 있습니다. 파운데이션 모델은 각각의 모달리티(Modality)를 독립적인 예측 문제로 처리하기보다 이러한 신호들을 일관된 상태(Coherent State)로 통합해야 합니다.

그 결과로 만들어지는 표현이 관측 가능한 모든 세부 사항을 복원할 필요는 없습니다. 피지컬 AI(Physical AI)에서는 미래의 상호작용(Future Interaction)에 필요한 정보를 얼마나 잘 보존하는지가 더욱 중요합니다. 따라서 월드 모델은 질감(Texture)이나 시각적으로 중요하지 않은 세부 정보를 압축하면서도 기하학, 객체 정체성(Object Identity), 운동, 행동유도성(Affordance), 접촉 관계(Contact Relationship), 불확실성, 행동 결과(Action Consequence)를 유지할 수 있습니다. 이러한 예측적 추상화(Predictive Abstraction)는 유용한 내부 모델과 단순히 감각 관측(Sensory Observation)을 재현하는 시스템을 구별합니다.

자기지도 학습(Self-Supervised Learning)은 로봇 및 비디오 데이터(Video Data)의 시간적 구조 자체가 풍부한 감독 신호(Supervision Signal)를 포함하고 있기 때문에 이러한 전환에 특히 적합합니다. 미래 관측(Future Observation), 마스킹 영역(Masked Region), 교차 모달 대응(Cross-Modal Correspondence), 상태 전이(State Transition), 행동 결과는 광범위한 수작업 어노테이션(Manual Annotation) 없이 학습 신호를 제공할 수 있습니다. 따라서 실제 환경과 시뮬레이션에서 수집된 대규모 궤적(Trajectory)은 특정 다운스트림 작업(Downstream Task)이 결정되기 전부터 재사용 가능한 물리 표현을 학습하기 위한 훈련 데이터가 될 수 있습니다.

시뮬레이션(Simulation)은 희귀 사건(Rare Event), 다양한 환경, 통제된 개입(Controlled Intervention), 대규모 궤적을 모델에 제공하여 이러한 학습 과정을 확장할 수 있습니다. 이후 실제 세계 데이터(Real-World Data)는 학습된 동역학을 실제 센서 특성과 물리적 행동에 연결합니다. 파운데이션 전략(Foundation Strategy)은 시뮬레이션과 현실을 서로 분리된 영역으로 취급하는 대신 두 영역을 결합하면서, 표현의 어떤 부분이 안정적으로 유지되고 어떤 동역학이 실제 배치 환경(Deployment Environment)에 맞게 적응되어야 하는지를 학습할 수 있습니다.

일반성(Generality)이 증가할수록 불확실성(Uncertainty)은 더욱 중요해집니다. 작업 특화 모델은 상대적으로 제한된 운용 분포(Operating Distribution)를 중심으로 최적화할 수 있지만, 파운데이션 모델은 익숙하지 않은 객체, 환경, 행동, 체화 형태를 마주할 것으로 예상됩니다. 따라서 모델은 예측된 미래뿐 아니라 해당 예측에 대한 신뢰도(Confidence)도 표현해야 합니다. 불확실하거나 분포 외 상태(Out-of-Distribution State)를 인식하면 다운스트림 플래너(Downstream Planner)가 속도를 낮추거나, 추가 정보를 수집하거나, 더 안전한 행동을 선택하거나, 폴백 메커니즘(Fallback Mechanism)을 호출할 수 있습니다.

실용적인 아키텍처(Practical Architecture)는 대규모 사전학습 월드 모델 백본(Pretrained World-Model Backbone)과 경량 작업 특화 구성요소(Task-Specific Component)를 결합할 수 있습니다. 백본(Backbone)은 대규모 경험으로부터 공간적(Spatial), 시간적(Temporal), 의미적(Semantic), 물리적(Physical), 인과적(Causal) 구조를 학습하고, 작업 헤드(Task Head)는 이러한 지식을 점유 예측, 내비게이션, 조작, 위험 추정(Risk Estimation), 제어 등의 응용에 특화합니다. 이러한 구성은 비용이 높은 일반 표현 학습(General Representation Learning)을 공유하면서 개별 작업에 대한 적응 비용을 상대적으로 낮추는 파운데이션 모델 원칙을 반영합니다.

따라서 파운데이션 월드 모델(Foundation World Model)로의 전환은 단순히 파라미터 수(Parameter Count)를 증가시키는 것을 의미하지 않습니다. 이는 하나의 예측 문제를 해결하는 모델에서 물리 환경이 어떻게 구성되고, 어떻게 변화하며, 행동이 어떻게 환경을 변화시키는지에 관한 재사용 가능한 지식(Reusable Knowledge)을 획득하는 모델로 목적 자체가 변화하는 것을 의미합니다. 작업 특화 동역학(Task-Specific Dynamics)에서 멀티태스크(Multitask), 멀티모달(Multimodal), 다중 환경(Multi-Environment), 그리고 궁극적으로 교차 체화 학습(Cross-Embodiment Learning)으로 발전하는 과정은 범용 물리 월드 모델(General Physical World Model)을 향한 개념적 연결고리를 형성합니다.

## 15.02. Large Scale World Model Pretraining

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

대규모 월드 모델 사전학습(Large-Scale World Model Pretraining)은 개별 로봇 작업에 특화하기 전에 환경(Environment), 동역학(Dynamics), 객체(Object), 상호작용(Interaction), 행동 결과(Action Consequence)에 대한 재사용 가능한 표현(Reusable Representation)을 학습함으로써 파운데이션 모델 패러다임(Foundation-Model Paradigm)을 물리 지능(Physical Intelligence)으로 확장합니다. 각 응용마다 새로운 동역학 모델을 학습하는 대신, 충분히 광범위하게 사전학습된 모델은 내비게이션(Navigation), 조작(Manipulation), 이동(Locomotion), 계획(Planning), 제어(Control) 시스템에 적용할 수 있는 공통 예측 백본(Common Predictive Backbone)을 제공할 수 있습니다.

이러한 접근법의 핵심 자원은 단순히 거대한 데이터셋(Dataset)이 아니라 다양한 물리적 경험(Physical Experience)의 집합입니다. 학습 데이터에는 로봇 궤적(Robot Trajectory), 자율주행 시퀀스(Autonomous Driving Sequence), 인간 비디오(Human Video), 조작 시연(Manipulation Demonstration), 시뮬레이션 롤아웃(Simulation Rollout), 원격조작 기록(Teleoperation Record), 멀티모달 센서 스트림(Multimodal Sensor Stream) 등이 포함될 수 있습니다. 환경, 객체, 행동, 시점, 운용 조건의 다양성은 단일 데이터셋의 특정 조건을 넘어 활용할 수 있는 일반적인 규칙성을 모델이 발견하도록 합니다.

시간적 데이터(Temporal Data)는 월드 모델 사전학습을 기존의 정적 표현 학습(Static Representation Learning)과 구별합니다. 개별 이미지는 외형과 기하학(Geometry)에 관한 정보를 제공하지만, 시퀀스(Sequence)는 상태가 어떻게 변화하는지를 보여줍니다. 시간에 따른 전이(Transition)를 관찰함으로써 모델은 운동(Motion), 지속성(Persistence), 상호작용, 접촉(Contact), 가림(Occlusion), 변형(Deformation), 장기적인 사건 구조(Event Structure)를 학습할 수 있습니다. 행동 정보가 존재하면 개입(Intervention)과 그 결과로 발생하는 물리 상태 변화 사이의 관계도 학습할 수 있습니다.

따라서 대규모 사전학습에는 이질적인 관측(Heterogeneous Observation)을 통합할 수 있는 표현이 필요합니다. 카메라(Camera)는 RGB 비디오를 제공하고, 라이다(LiDAR)는 3차원 구조를 표현하며, 레이더(Radar)는 속도 정보를 제공할 수 있고, 관성 측정 장치(IMU)나 관절 센서(Joint Sensor)는 자차 운동(Ego-Motion)과 고유수용감각(Proprioception)을 표현할 수 있습니다. 각 모달리티(Modality)가 반드시 동일한 인코더(Encoder)를 사용할 필요는 없지만, 최종 표현은 공간적, 시간적, 의미적, 물리적 관계를 공동으로 모델링할 수 있는 일관된 내부 상태(Coherent Internal State)를 지원해야 합니다.

자기지도 학습(Self-Supervised Learning)은 대부분의 물리 데이터에 사람이 작성한 레이블(Label)이 존재하지 않기 때문에 이러한 규모의 학습을 실용적으로 가능하게 합니다. 모델은 미래 잠재 상태(Future Latent State)를 예측하거나, 마스킹된 정보(Masked Information)를 복원하거나, 서로 다른 시점 또는 모달리티 사이의 표현을 정렬하거나, 시간 순서를 추정하거나, 관측된 행동의 결과를 예측하면서 학습할 수 있습니다. 따라서 물리 세계 자체가 상당 부분 감독 신호(Supervision Signal)를 제공하며, 방대한 센서 및 궤적 데이터를 광범위한 수작업 어노테이션(Manual Annotation) 없이 표현 학습에 활용할 수 있습니다.

잠재 표현 공간(Latent Representation Space)에서의 예측은 사전학습에 필요한 계산 부담을 크게 줄일 수 있습니다. 모든 미래 프레임의 모든 픽셀(Pixel)을 복원하면 모델이 물리적 추론에 필수적이지 않은 질감(Texture), 조명(Lighting), 기타 세부 정보에 많은 용량을 할당할 수 있습니다. 반면 잠재 예측 목표(Latent Predictive Objective)는 객체 정체성(Object Identity), 기하학, 운동, 상호작용, 상태 전이와 같은 지속적인 구조를 강조하면서 예측하기 어렵거나 작업과 관련성이 낮은 감각적 세부 사항을 억제할 수 있습니다.

그러나 세부적인 관측 정보가 중요한 경우에는 생성형 목표(Generative Objective)도 유용합니다. 미래 비디오 생성(Future Video Generation), 점유 복원(Occupancy Reconstruction), 깊이 예측(Depth Prediction), 멀티모달 복원(Multimodal Reconstruction)은 가능한 미래에 대한 풍부한 정보를 모델이 유지하도록 할 수 있습니다. 따라서 대규모 시스템은 하나의 학습 신호에만 의존하기보다 잠재 예측(Latent Prediction), 생성(Generation), 대조 학습(Contrastive Learning), 복원(Reconstruction), 행동 조건부(Action-Conditioned) 목표를 결합할 수 있으며, 이들의 균형에 따라 사전학습 표현에 나타나는 물리 정보의 종류가 결정됩니다.

행동 조건부 사전학습(Action-Conditioned Pretraining)은 관측만으로는 제어 가능한 동역학(Controllable Dynamics)을 완전히 파악할 수 없기 때문에 피지컬 AI(Physical AI)에서 특히 중요합니다. 궤적에 조향 명령(Steering Command), 속도, 관절 명령(Joint Command), 힘(Force), 그리퍼 동작(Gripper Action) 등의 개입 정보가 포함되면 모델은 서로 다른 행동이 미래 상태에 어떠한 영향을 주는지를 학습할 수 있습니다. 이를 통해 로봇은 실제 환경에서 하나의 행동을 실행하기 전에 여러 후보 행동 시퀀스(Candidate Action Sequence)를 내부적으로 상상하고 평가하는 반사실적 예측(Counterfactual Prediction)을 수행할 수 있습니다.

시뮬레이션(Simulation)은 이러한 행동 중심 경험(Action-Rich Experience)을 확장하는 중요한 수단입니다. 하드웨어를 손상시키거나 사람을 위험에 빠뜨리거나 막대한 실제 운용 시간을 소비하지 않고도 수백만 번의 통제된 상호작용(Controlled Interaction)을 생성할 수 있습니다. 질량(Mass), 마찰(Friction), 조명, 지형(Terrain), 객체 구성(Object Configuration), 센서 노이즈(Sensor Noise), 액추에이터 동작(Actuator Behavior) 등의 파라미터(Parameter)를 체계적으로 변화시켜 실제 환경에서 드물거나 수집하기 어려운 조합까지 사전학습 모델에 경험시킬 수 있습니다.

그러나 시뮬레이션 환경은 실제 물리 시스템을 완벽하게 재현할 수 없기 때문에 실제 세계 데이터(Real-World Data)는 여전히 필수적입니다. 센서 아티팩트(Sensor Artifact), 액추에이터 지연(Actuator Delay), 기계적 마모(Mechanical Wear), 모델링되지 않은 접촉(Unmodeled Contact), 환경 변화, 인간 행동 등은 시뮬레이션이 완전히 포착하지 못하는 차이를 발생시킵니다. 따라서 대규모 사전학습은 시뮬레이션 궤적과 실제 궤적을 혼합하여 시뮬레이션으로 범위와 통제된 다양성을 확보하고, 실제 경험을 통해 표현과 전이 동역학(Transition Dynamics)을 실제 배치 조건에 연결할 수 있습니다.

데이터셋의 규모가 증가할수록 데이터 품질(Data Quality)은 더욱 중요해집니다. 반복되거나 손상되었거나 동기화가 불량하거나 지나치게 중복된 궤적은 학습 연산량(Training Compute)을 소비하면서도 모델 성능을 그만큼 향상시키지 못할 수 있습니다. 따라서 효과적인 사전학습에는 의미 있는 다양성을 보존하는 데이터 큐레이션(Data Curation), 동기화(Synchronization), 필터링(Filtering), 균형 조정(Balancing), 샘플링 전략(Sampling Strategy)이 필요합니다. 희귀한 상호작용, 실패 사례(Failure), 비정상적인 지형, 어려운 조명 조건, 안전 중요 상황(Safety-Critical Situation)은 자연 발생 빈도보다 더 높은 비중으로 포함될 필요가 있습니다.

스케일링(Scaling)은 모델 용량(Model Capacity)과 계산 자원(Computational Resource)에도 적용됩니다. 더 큰 아키텍처는 객체, 모달리티, 시간 범위, 환경 사이의 더욱 복잡한 관계를 표현할 수 있지만, 단순히 파라미터 수를 증가시키는 것만으로 더 우수한 월드 모델이 보장되지는 않습니다. 모델 규모는 충분한 데이터 다양성, 효과적인 학습 목표, 시간적 맥락(Temporal Context), 최적화(Optimization)와 함께 확장되어야 합니다. 중요한 스케일링 목표는 모델 크기 자체가 아니라 표현이 포착하는 재사용 가능한 물리 구조(Reusable Physical Structure)의 양입니다.

긴 시간적 맥락(Long Temporal Context)은 특별한 도전 과제를 제시합니다. 물리적 행동에는 접촉과 액추에이터 응답처럼 빠른 사건뿐만 아니라 내비게이션, 작업 진행(Task Progression), 인간과의 상호작용처럼 느린 과정도 포함됩니다. 긴 궤적의 모든 관측을 동일한 시간 해상도(Temporal Resolution)로 처리하면 계산 비용이 크게 증가합니다. 계층적 표현(Hierarchical Representation), 시간적 추상화(Temporal Abstraction), 메모리 메커니즘(Memory Mechanism), 압축된 잠재 상태(Compressed Latent State)는 사전학습 월드 모델이 즉각적인 동역학과 장기적인 환경 변화를 연결하도록 할 수 있습니다.

사전학습은 또한 물리 세계를 결정론적(Deterministic)으로만 표현하기보다 불확실성(Uncertainty)을 경험하도록 해야 합니다. 불완전한 관측, 확률적 상호작용(Stochastic Interaction), 숨겨진 변수(Hidden Variable), 다른 에이전트의 행동 때문에 여러 미래가 동시에 가능할 수 있습니다. 가능한 미래에 대한 분포(Distribution)를 학습하면 모델은 서로 양립할 수 없는 결과를 평균화하는 대신 모호성(Ambiguity)을 표현할 수 있습니다. 이러한 능력은 사전학습된 모델이 이후 계획, 충돌 회피(Collision Avoidance), 위험 민감 의사결정(Risk-Sensitive Decision Making)에 사용될 때 특히 중요합니다.

사전학습 이후 학습된 월드 표현(World Representation)은 작업 특화 헤드(Task-Specific Head), 미세조정(Fine-Tuning), 프롬프팅(Prompting), 조건화(Conditioning), 경량 적응 모듈(Lightweight Adaptation Module)을 통해 개별 작업에 적응할 수 있습니다. 내비게이션 시스템은 주행 가능성(Traversability)과 미래 점유(Future Occupancy)를 추출하고, 조작 시스템은 동일한 기반 지식을 객체 상호작용과 접촉 예측(Contact Prediction)에 활용할 수 있습니다. 경제적·공학적 이점은 각 로봇 응용마다 물리 지식을 처음부터 다시 구축하지 않고 비용이 높은 사전학습 결과를 여러 다운스트림 시스템(Downstream System)에서 재사용할 수 있다는 점에 있습니다.

따라서 대규모 월드 모델 사전학습(Large-Scale World Model Pretraining)의 궁극적인 목표는 이질적인 물리 경험을 전이 가능한 예측 지식(Transferable Predictive Knowledge)으로 변환하는 것입니다. 실제 및 시뮬레이션 데이터, 다양한 센서, 여러 환경, 시간적 시퀀스, 행동 조건부 상호작용이 결합되어 물리 상태가 어떻게 구성되고 어떻게 변화하는지를 모델에 학습시킵니다. 이러한 사전학습 지식은 멀티태스크(Multi-Task), 다중 환경(Multi-Environment), 그리고 궁극적으로 교차 체화(Cross-Embodiment) 월드 모델로 확장하기 위한 기반을 형성하며, 점차 범용화되는 피지컬 AI를 지원하는 확장 가능한 토대가 됩니다.

## 15.03. Multi Task and Multi Environment Pretraining

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

멀티태스크 및 다중 환경 사전학습(Multi-Task and Multi-Environment Pretraining)은 월드 모델(World Model)을 단일 로봇 응용의 가정에서 벗어나도록 확장합니다. 하나의 창고에서 내비게이션(Navigation)만 학습하거나 하나의 작업대에서 조작(Manipulation)만 학습하는 대신, 모델은 사전학습(Pretraining) 과정에서 다양한 목표와 운용 영역(Operating Domain)을 경험합니다. 이러한 다양성은 내부 표현(Internal Representation)이 하나의 작업, 장면 또는 배치 구성에만 유용한 상관관계가 아니라 재사용 가능한 물리 구조(Reusable Physical Structure)를 포착하도록 유도합니다.

멀티태스크 사전학습(Multi-Task Pretraining)은 동일한 모델을 서로 다른 예측 및 상호작용 목표에 노출시킵니다. 여기에는 미래 상태 예측(Future-State Prediction), 점유 추정(Occupancy Estimation), 객체 운동(Object Motion), 깊이(Depth), 의미 구조(Semantic Structure), 접촉 예측(Contact Prediction), 주행 가능성(Traversability), 행동 결과(Action Consequence), 보상 관련 신호(Reward-Related Signal) 등이 포함될 수 있습니다. 각각의 목표는 환경의 서로 다른 속성을 강조하며, 이들의 결합은 공유 표현(Shared Representation)이 다양한 형태의 물리적 추론(Physical Reasoning)에 필요한 정보를 보존하도록 유도합니다.

핵심적인 아키텍처 원칙(Architectural Principle)은 공유 월드 표현(Shared World Representation)과 작업 의존적 출력(Task-Dependent Output)을 결합하는 것입니다. 멀티모달 관측(Multimodal Observation)은 먼저 기하학(Geometry), 객체(Object), 운동(Motion), 의미(Semantics), 에이전트 상태(Agent State)를 표현하는 공통 잠재 상태(Common Latent State)로 인코딩될 수 있습니다. 이후 공유 동역학 모듈(Shared Dynamics Module)이 이 상태의 변화를 예측하고, 특화 헤드(Specialized Head)가 개별 작업에 필요한 정보를 디코딩합니다. 따라서 하나의 목표에서 학습된 지식이 다른 목표에서 사용하는 표현을 향상시킬 수 있습니다.

다중 환경 사전학습(Multi-Environment Pretraining)은 두 번째 다양성 차원을 도입합니다. 피지컬 AI(Physical AI) 시스템은 궁극적으로 창고, 공장, 사무실, 가정, 도로, 건설 현장, 농경지 또는 비정형 야외 지형(Unstructured Outdoor Terrain)에서 운용될 수 있습니다. 이러한 다양한 환경에 걸친 학습은 월드 모델이 하나의 장면 분포(Scene Distribution)를 현실 자체로 간주하는 것을 방지합니다. 대신 어떤 환경적 속성이 안정적으로 유지되고 어떤 속성이 맥락(Context)에 따라 변화하는지를 발견해야 합니다.

이러한 불변 구조(Invariant Structure)와 환경 특화 구조(Environment-Specific Structure)의 구분은 일반화(Generalization)에 핵심적입니다. 자유 공간(Free Space), 충돌(Collision), 지지(Support), 객체 영속성(Object Persistence), 운동, 원인과 결과(Cause and Effect) 같은 개념은 시각적 외형이 크게 달라지더라도 여러 영역에서 의미를 유지할 수 있습니다. 반면 바닥 재질, 조명, 날씨, 객체 범주, 지형 기하학(Terrain Geometry), 교통 패턴, 인간 활동은 달라질 수 있으므로 표현은 공통적인 물리 원리를 유지하면서 지역적인 차이도 수용해야 합니다.

작업(Task)과 환경(Environment)의 다양성은 서로 독립적인 학습 차원을 형성하는 것이 아니라 상호작용합니다. 창고에서의 내비게이션, 야외에서의 내비게이션, 공장에서의 조작, 가정에서의 조작은 서로 다른 물리적 제약 조건의 조합을 모델에 제공합니다. 충분히 다양한 학습 매트릭스(Training Matrix)는 동일한 개념을 여러 조건에서 경험하도록 합니다. 이를 통해 모델은 본질적인 물리적 관계(Essential Physical Relationship)를 특정 데이터셋이나 응용에 우연히 존재하는 상관관계(Accidental Correlation)와 분리할 수 있습니다.

따라서 균형 잡힌 샘플링(Balanced Sampling)이 매우 중요합니다. 대부분의 학습 궤적(Training Trajectory)이 하나의 환경이나 작업에서 제공된다면 데이터셋이 아무리 크더라도 모델은 강한 편향(Bias)을 가질 수 있습니다. 사전학습 파이프라인(Pretraining Pipeline)은 작업, 환경, 상호작용 유형, 난이도, 희귀 사건(Rare Event)의 균형을 조정하여 지배적인 데이터셋이 규모는 작지만 유용한 데이터 소스를 압도하지 않도록 할 수 있습니다. 또한 실패(Failure), 비정상적 상호작용, 어려운 지형, 안전 중요 상황(Safety-Critical Situation)처럼 학습 가치가 높은 사례를 강조할 수 있습니다.

학습 목표(Training Objective)는 누락된 레이블(Missing Label)과 이질적인 데이터(Heterogeneous Data)도 수용해야 합니다. 일부 궤적에는 행동(Action)이 포함될 수 있지만 다른 데이터에는 비디오(Video)만 존재할 수 있으며, 특정 데이터셋에는 깊이, 라이다(LiDAR), 언어(Language), 의미 레이블(Semantic Label), 고유수용감각(Proprioception)이 제공될 수도 있습니다. 불완전한 데이터를 버리는 대신 멀티모달 월드 모델(Multimodal World Model)은 각 샘플에서 사용 가능한 정보에 적합한 학습 목표를 적용할 수 있습니다. 자기지도 예측(Self-Supervised Prediction)은 이러한 이질적인 데이터 소스를 연결하는 공통 학습 메커니즘을 제공합니다.

행동 조건부 학습(Action-Conditioned Learning)은 작업이 서로 다를 때 특히 중요한 가치를 가집니다. 자율주행(Driving), 모바일 내비게이션(Mobile Navigation), 조작, 이동(Locomotion)은 매우 다른 제어 공간(Control Space)을 사용하지만, 모두 물리 세계에서 상태 전이(State Transition)를 발생시킵니다. 행동과 그 결과 상태 사이의 관계를 학습함으로써 모델은 보다 일반적인 개입(Intervention)의 개념을 형성할 수 있습니다. 작업 특화 행동 인코더(Task-Specific Action Encoder)는 서로 다른 명령 구조를 공유 예측 동역학 모델(Shared Predictive Dynamics Model)과 상호작용할 수 있는 표현으로 변환할 수 있습니다.

시간적 다양성(Temporal Diversity)도 마찬가지로 중요합니다. 일부 작업은 접촉(Contact)이나 액추에이터 응답(Actuator Response)에 대해 밀리초 수준의 민감도를 요구하는 반면, 다른 작업은 수초 또는 수분에 걸쳐 변화하는 사건에 의존합니다. 따라서 멀티태스크 사전학습은 하나의 예측 시간 범위(Prediction Horizon)만 가정하지 않고 여러 시간 척도(Temporal Scale)를 표현해야 합니다. 단기 동역학(Short-Horizon Dynamics)은 안정화와 충돌 회피(Collision Avoidance)를 지원하고, 장기 표현(Long-Horizon Representation)은 내비게이션 진행, 상호작용 시퀀스, 작업 완료(Task Completion)를 설명할 수 있습니다.

다중 환경 데이터는 모델을 서로 다른 불확실성 영역(Uncertainty Regime)에도 노출시킵니다. 구조화된 공장 환경은 비교적 예측 가능한 기하학과 움직임을 제공하지만, 야외 환경에는 변화하는 지형, 날씨, 식생(Vegetation), 충분히 관측되지 않은 영역이 존재할 수 있습니다. 사람이 존재하는 환경은 추가적인 행동 불확실성(Behavioral Uncertainty)을 발생시킵니다. 이러한 조건을 함께 학습하면 모델은 신뢰도(Confidence)를 맥락과 연관시키고 현재 상황이 익숙한 경험과 달라 예측의 신뢰성이 낮아지는 시점을 인식할 수 있습니다.

시뮬레이션(Simulation)은 작업-환경 학습 매트릭스(Task-Environment Training Matrix)를 효율적으로 확장할 수 있습니다. 동일한 로봇이 수천 개의 절차적으로 생성된 장면(Procedurally Generated Scene)에서 다양한 작업을 수행하도록 하면서 물리 파라미터(Physics Parameter), 센서 특성, 객체, 지형, 외란(Disturbance)을 변화시킬 수 있습니다. 또한 실제 환경에서 재현하기 어렵거나 위험한 개입과 실패를 체계적으로 생성할 수 있습니다. 이후 실제 세계 궤적(Real-World Trajectory)은 공유 모델이 시뮬레이션에만 존재하는 규칙성에 의존하지 않도록 현실에 기반을 제공하는 역할을 합니다.

이 전략의 중요한 결과 중 하나는 긍정적 전이(Positive Transfer)입니다. 객체 운동을 학습하면 조작 예측이 향상될 수 있으며, 점유와 기하학을 학습하면 내비게이션과 충돌 추론(Collision Reasoning)에 도움이 될 수 있습니다. 그러나 서로 다른 목표가 경쟁하거나 환경마다 상충하는 표현을 요구하면 부정적 전이(Negative Transfer)도 발생할 수 있습니다. 충분한 모델 용량(Model Capacity), 모듈형 구성요소(Modular Component), 작업 조건화(Task Conditioning), 혼합 메커니즘(Mixture Mechanism), 신중하게 설계된 손실 함수(Loss)는 모든 작업에 동일한 내부 특징을 강제하지 않으면서 공유 지식을 유지하는 데 도움을 줄 수 있습니다.

따라서 평가는 학습 데이터셋 전반의 평균 성능만 측정해서는 안 됩니다. 유용한 사전학습 월드 모델은 알려진 작업과 환경의 새로운 조합(Unseen Combination)으로 전이할 수 있어야 하며, 이상적으로는 학습 과정에 포함되지 않았던 환경이나 목표에도 적용될 수 있어야 합니다. 분포 변화(Distribution Shift), 제한된 적응 데이터(Limited Adaptation Data), 센서 변화, 새로운 객체 구성(Novel Object Configuration)에서의 성능을 평가하면 모델이 재사용 가능한 물리 구조를 학습했는지 아니면 단순히 많은 영역을 암기했는지를 판단할 수 있습니다.

사전학습 이후에는 경량 헤드(Lightweight Head), 어댑터(Adapter), 조건화 신호(Conditioning Signal), 선택적 미세조정(Selective Fine-Tuning)을 통해 작업 적응(Task Adaptation)을 수행할 수 있습니다. 기하학, 동역학, 의미, 상호작용 지식, 불확실성 표현(Uncertainty Representation)의 상당 부분이 이미 공유 백본(Shared Backbone)에 존재하므로 새로운 응용에는 훨씬 적은 작업 특화 데이터(Task-Specific Data)만 필요할 수 있습니다. 이를 통해 사전학습은 독립된 모델들의 집합이 아니라 여러 로봇 시스템을 지원하는 공통 물리 지식 인프라(Common Physical Knowledge Infrastructure)로 전환됩니다.

따라서 멀티태스크 및 다중 환경 사전학습(Multi-Task and Multi-Environment Pretraining)은 대규모 월드 모델 학습에서 파운데이션 수준의 물리 지능(Foundation-Level Physical Intelligence)으로 발전하는 중요한 단계입니다. 다양한 목표와 다양한 운용 영역을 결합함으로써 모델은 작업과 환경이 달라져도 지속적으로 유용한 요소를 찾아내도록 요구받습니다. 이렇게 형성된 공유 표현은 이후의 교차 체화 학습(Cross-Embodiment Learning)을 위한 기반이 되며, 월드 지식(World Knowledge)이 로봇이 무엇을 수행하는지와 어디에서 운용되는지를 넘어 서로 다른 종류의 로봇 자체에까지 일반화되는 다음 단계로 연결됩니다.

## 15.04. Cross Embodiment World Models

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

교차 체화 월드 모델(Cross-Embodiment World Model)은 파운데이션 월드 모델(Foundation World Model)의 개념을 개별 로봇 플랫폼을 넘어 확장합니다. 기존 모델은 바퀴형 모바일 로봇(Wheeled Mobile Robot), 매니퓰레이터(Manipulator), 4족 보행 로봇(Quadruped), 휴머노이드(Humanoid), 비행 로봇(Aerial Robot)과 같은 하나의 체화 형태(Embodiment)를 중심으로 학습되는 경우가 많습니다. 반면 교차 체화 모델링(Cross-Embodiment Modeling)은 에이전트의 형태(Morphology), 센서, 액추에이터(Actuator), 운동학(Kinematics), 동역학(Dynamics), 행동 공간(Action Space)이 달라져도 유용성을 유지할 수 있는 물리 세계의 표현을 학습하는 것을 목표로 합니다.

이러한 접근의 동기는 물리 세계(World)와 그 안에서 행동하는 에이전트(Agent)를 구분하는 데서 출발합니다. 로봇은 매우 다른 신체 구조를 가질 수 있지만, 객체는 공간을 점유하고, 표면은 지지(Support)를 제공하며, 장애물은 움직임을 제한하고, 접촉(Contact)은 힘을 전달하며, 행동은 상태 전이(State Transition)를 발생시킨다는 공통된 물리 개념을 경험합니다. 재사용 가능한 월드 모델(Reusable World Model)은 이러한 공유 구조를 특정 로봇 하나의 기계적 구성에 불필요하게 종속시키지 않고 포착해야 합니다.

그러나 모든 로봇은 서로 다른 방식으로 세계를 관측하고 변화시키므로 체화 형태는 여전히 중요합니다. 모바일 로봇(Mobile Robot)은 평면 공간을 이동하고, 매니퓰레이터는 관절 운동(Articulated Motion)을 통해 객체를 변화시키며, 4족 보행 로봇은 반복적인 발 접촉(Foot Contact)을 통해 환경과 상호작용하고, 드론(Drone)은 3차원 공간을 자유롭게 이동합니다. 따라서 월드 표현(World Representation)은 공유하면서 체화 특화 정보(Embodiment-Specific Information)를 통해 센싱 기하학(Sensing Geometry), 도달 가능한 상태, 행동 능력, 물리적 제약, 상호작용 메커니즘을 표현할 수 있습니다.

유용한 아키텍처(Architecture)는 공유 월드 상태(Shared World State)와 체화 상태(Embodiment State)를 분리합니다. 공유 구성요소는 기하학(Geometry), 객체, 의미(Semantics), 운동(Motion), 점유(Occupancy), 접촉 관계(Contact Relationship), 환경 동역학(Environmental Dynamics)을 인코딩할 수 있습니다. 체화 표현(Embodiment Representation)은 형태, 관절 구성(Joint Configuration), 크기, 센서 배치, 액추에이터 특성, 운동학적 한계(Kinematic Limit), 이동 방식(Mobility Type)을 인코딩할 수 있습니다. 이후 두 표현을 함께 조건화(Conditioning)하여 현재 로봇의 능력에 맞게 공통 물리 지식을 해석하고 미래를 예측합니다.

행동 표현(Action Representation)은 핵심적인 도전 과제 중 하나입니다. 조향 명령(Steering Command), 바퀴 속도(Wheel Velocity), 관절 토크(Joint Torque), 말단장치 목표(End-Effector Target), 발 궤적(Foot Trajectory), 추력 명령(Thrust Command)을 하나의 고정된 행동 벡터(Action Vector)로 직접 표현하기는 어렵습니다. 따라서 교차 체화 모델은 플랫폼 특화 제어(Platform-Specific Control)를 보다 전이 가능한 물리적 개입(Physical Intervention)의 표현으로 변환하면서도 각 체화 형태가 자신의 상태와 주변 환경을 실제로 어떻게 변화시키는지 예측하는 데 필요한 세부 정보를 유지해야 합니다.

한 가지 접근법은 행동을 의도된 물리적 효과(Intended Physical Effect)를 통해 표현하는 것입니다. 명령을 단순한 모터 값(Motor Value)으로 취급하는 대신 변위(Displacement), 힘(Force), 접촉 변화(Contact Change), 객체 운동(Object Motion), 원하는 상태 전이(Desired State Transition) 등으로 표현할 수 있습니다. 이러한 추상화(Abstraction)는 외형적으로 서로 다른 행동 사이의 유사성을 드러낼 수 있습니다. 모바일 베이스(Mobile Base)가 객체를 향해 이동하는 것과 매니퓰레이터가 말단장치를 동일한 객체 쪽으로 이동하는 것은 서로 다른 액추에이터를 사용하지만 의미 있는 공간적·상호작용 관계를 공유합니다.

교차 체화 학습(Cross-Embodiment Learning)은 다양한 학습 경험도 필요로 합니다. 데이터는 이상적으로 여러 로봇 형태, 센서 구성, 작업, 환경, 상호작용 방식을 포함해야 합니다. 특히 서로 다른 체화 형태가 동일한 물리 구조의 상호보완적인 측면을 보여줄 수 있으므로 공유 상황(Shared Situation)은 높은 가치를 가집니다. 매니퓰레이터는 풍부한 접촉 상호작용(Contact Interaction)을 제공하고, 모바일 로봇은 대규모 공간 경험(Spatial Experience)을 제공하며, 4족 보행 로봇은 지형, 지지, 균형(Balance), 반복 접촉 동역학에 관한 정보를 제공합니다.

멀티모달 표현(Multimodal Representation)은 이러한 이질적인 플랫폼을 연결하는 데 도움을 줍니다. 카메라(Camera), 깊이 센서(Depth Sensor), 라이다(LiDAR), 힘 센서(Force Sensor), 관성 측정 장치(IMU), 관절 상태(Joint State), 언어(Language)는 로봇마다 서로 다른 조합으로 사용될 수 있습니다. 모달리티 특화 인코더(Modality-Specific Encoder)는 사용 가능한 관측을 공유 잠재 월드 표현(Shared Latent World Representation)으로 변환하고, 모달리티 누락 학습(Missing-Modality Training)은 특정 센서 구성에 대한 의존성을 낮출 수 있습니다. 목표는 동일한 센서 입력을 요구하는 것이 아니라 근본적인 물리 상황에 대해 호환 가능한 표현을 만드는 것입니다.

표준화된 공간 표현(Canonical Spatial Representation)은 체화 형태 사이를 연결하는 또 다른 다리가 될 수 있습니다. 3차원 장면 표현(3D Scene Representation), 점유 필드(Occupancy Field), 객체 중심 상태(Object-Centric State) 또는 다른 에이전트 독립적 좌표계(Agent-Independent Coordinate System)를 사용하면 로봇 자체의 구성과 분리하여 환경을 표현할 수 있습니다. 이후 체화 특화 변환(Embodiment-Specific Transformation)을 통해 이러한 공통 공간 표현을 실제 계획과 제어에 필요한 로컬 센서 좌표계(Local Sensor Frame), 바디 좌표계(Body Frame), 조작 가능 영역(Manipulability Region), 도달 가능 영역(Reachable Area), 충돌 기하학(Collision Geometry)과 연결할 수 있습니다.

동역학 모델(Dynamics Model)은 환경 동역학(Environmental Dynamics)과 체화 동역학(Embodiment Dynamics)을 구분해야 합니다. 객체 운동, 중력(Gravity), 지지 관계, 여러 형태의 충돌은 주로 외부 세계에 속하지만, 가속 한계, 관절 응답, 균형, 조향 거동(Steering Behavior), 액추에이터 지연(Actuator Delay)은 플랫폼에 크게 의존합니다. 이러한 구성요소를 분해(Factorization)하면 전이 가능한 환경 지식을 재사용하면서 더 작은 체화 의존적 모듈(Embodiment-Dependent Module)을 통해 특정 로봇이 해당 동역학에 어떻게 참여하는지를 학습할 수 있습니다.

시뮬레이션(Simulation)은 다양한 로봇 형태를 통제된 조건에서 생성하고 운용할 수 있기 때문에 교차 체화 사전학습(Cross-Embodiment Pretraining)에 특히 유용합니다. 크기, 질량, 관절 구조, 바퀴 구성, 센서 위치, 액추에이터 특성을 체계적으로 변화시킬 수 있습니다. 이러한 형태 무작위화(Morphological Randomization)는 모델을 몇 개의 고정된 로봇에만 노출시키는 대신 연속적으로 변화하는 체화 형태를 경험하게 하여 어떤 관계가 보편적이고 어떤 관계가 체화 파라미터(Embodiment Parameter)에 따라 조건화되어야 하는지를 학습하도록 합니다.

실제 로봇은 시뮬레이션으로 완전히 재현하기 어려운 특성을 가지므로 실제 세계 기반화(Real-World Grounding)는 여전히 필요합니다. 기계적 순응성(Mechanical Compliance), 백래시(Backlash), 바퀴 미끄러짐(Wheel Slip), 액추에이터 포화(Actuator Saturation), 센서 정렬 오차(Sensor Misalignment), 통신 지연, 마모(Wear), 복잡한 접촉 거동은 플랫폼마다 다르게 나타날 수 있습니다. 따라서 새로운 로봇에서 얻은 제한적인 실제 궤적을 이용하여 체화 특화 동역학을 식별하면서 다른 로봇과 시뮬레이션에서 학습한 광범위한 환경 표현은 그대로 유지할 수 있습니다.

주요 목표 중 하나는 이전에 경험하지 못한 체화 형태에 대한 제로샷 전이(Zero-Shot Transfer) 또는 퓨샷 전이(Few-Shot Transfer)입니다. 강력한 교차 체화 월드 모델은 새로운 로봇이 도입될 때마다 전체 모델을 처음부터 다시 학습할 필요가 없어야 합니다. 새로운 로봇의 형태, 센서, 운동학과 상대적으로 적은 양의 상호작용 데이터가 주어지면 모델은 해당 플랫폼에 맞게 예측을 적응시킬 수 있어야 합니다. 이때 필요한 새로운 경험의 양은 공유 표현(Shared Representation)의 품질을 평가하는 중요한 척도가 됩니다.

그러나 전이(Transfer)는 물리적 능력의 차이를 반드시 존중해야 합니다. 어떤 객체를 이동시킬 수 있다는 지식이 모든 로봇이 해당 객체를 이동시킬 수 있다는 것을 의미하지 않으며, 드론이 통과할 수 있는 경로가 바퀴형 플랫폼에는 불가능할 수도 있습니다. 따라서 교차 체화 일반화(Cross-Embodiment Generalization)는 체화 제약을 제거해서는 안 됩니다. 월드에 대한 공유 지식과 함께 도달 가능성(Reachability), 이동 능력(Mobility), 페이로드(Payload), 접촉, 안정성(Stability), 센싱(Sensing) 등 플랫폼 특화 한계를 명시적으로 추론해야 합니다.

따라서 평가는 공유 예측(Shared Prediction)과 체화 조건부 행동(Embodiment-Conditioned Behavior)을 모두 측정해야 합니다. 모델이 서로 다른 로봇에서 공통적인 장면 동역학(Scene Dynamics)을 이해하는지, 서로 다른 행동에 따른 결과를 구별하여 예측하는지, 학습하지 않은 형태(Unseen Morphology)로 전이할 수 있는지, 제한된 데이터만으로 적응할 수 있는지를 평가할 수 있습니다. 또한 센서 구성, 크기, 페이로드 또는 액추에이터 특성이 사전학습에서 경험한 조건과 달라지는 상황에서도 성능을 시험해야 합니다.

궁극적으로 교차 체화 월드 모델(Cross-Embodiment World Model)은 이질적인 로봇 경험을 공유 물리 지식(Shared Physical Knowledge)으로 변환합니다. 모바일 로봇, 매니퓰레이터, 4족 보행 로봇, 휴머노이드, 비행 시스템마다 독립적인 모델을 유지하는 대신 공통 예측 파운데이션(Common Predictive Foundation)이 세계를 표현하고, 특화된 체화 인터페이스(Embodiment Interface)가 각 기계가 세계를 어떻게 감지하고 행동하는지를 설명할 수 있습니다. 이는 멀티태스크 및 다중 환경 사전학습(Multi-Task and Multi-Environment Pretraining)에서 로봇 간 공유 월드 표현(Shared World Representation Across Robots)과 더욱 범용적인 피지컬 AI(Physical AI)로 발전하기 위한 핵심적인 연결고리를 제공합니다.

## 15.05. Shared World Representation Across Robots

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

로봇 간 공유 월드 표현(Shared World Representation Across Robots)은 물리 환경(Physical Environment)을 다양한 로봇 플랫폼이 이해하고 재사용할 수 있는 형태로 인코딩(Encoding)하는 것을 목표로 합니다. 각 로봇이 완전히 독립적인 내부 모델(Internal Model)을 구축하도록 하는 대신, 이기종 시스템(Heterogeneous System)은 자신의 관측을 기하학(Geometry), 객체(Object), 의미(Semantics), 운동(Motion), 점유(Occupancy), 상호작용(Interaction), 불확실성(Uncertainty)에 대한 호환 가능한 표현으로 변환할 수 있습니다. 이를 통해 지각(Perception)과 로봇 특화 행동(Robot-Specific Behavior) 사이에 공통 지식 계층(Common Knowledge Layer)을 형성할 수 있습니다.

핵심 원칙은 월드 상태(World State)와 로봇 상태(Robot State)를 구분하는 것입니다. 객체 위치(Object Location), 자유 공간(Free Space), 표면 기하학(Surface Geometry), 동적 장애물(Dynamic Obstacle), 의미적 정체성(Semantic Identity), 물리적 관계(Physical Relationship)와 같은 환경 속성은 특정 기계와 독립적으로 표현할 수 있습니다. 반면 로봇의 자세(Pose), 크기, 관절(Joint), 페이로드(Payload), 도달 가능성(Reachability), 센서 배치(Sensor Placement), 이동 제약(Mobility Constraint)과 같은 로봇 특화 속성은 별도로 표현한 뒤 필요할 때 공유 월드 상태와 연결할 수 있습니다.

이러한 분리를 통해 이기종 로봇(Heterogeneous Robot)은 동일한 환경을 자신의 능력에 따라 다르게 해석할 수 있습니다. 폭이 좁은 모바일 로봇(Mobile Robot)은 특정 통로를 주행 가능(Traversable)하다고 판단할 수 있지만, 더 큰 플랫폼은 동일한 통로에 접근할 수 없다고 판단할 수 있습니다. 매니퓰레이터(Manipulator)는 객체를 파지 가능성(Graspability)의 관점에서 해석할 수 있는 반면, 드론(Drone)은 주로 장애물로 판단할 수 있습니다. 결과적인 행동유도성(Affordance)과 행동(Action)이 달라지더라도 기반이 되는 월드 표현은 공통으로 유지될 수 있습니다.

따라서 공간적 일관성(Spatial Consistency)은 기본적인 요구사항입니다. 서로 다른 시점(Viewpoint), 센서, 로봇에서 수집된 관측은 서로 호환되는 물리적 위치와 개체(Entity)를 참조해야 합니다. 공유 좌표계(Shared Coordinate System), 3차원 장면 표현(3D Scene Representation), 조감도 구조(Bird's-Eye-View Structure), 점유 필드(Occupancy Field), 객체 중심 맵(Object-Centric Map), 학습된 잠재 공간 표현(Learned Latent Spatial Representation)은 이러한 공통 기준을 제공할 수 있습니다. 로봇 특화 변환(Robot-Specific Transformation)은 로컬 센서 좌표계와 바디 좌표계(Body Frame)를 공유 표현에 연결합니다.

로봇이 공유된 개체에 대해 호환 가능한 의미를 부여해야 하므로 의미적 일관성(Semantic Consistency) 역시 중요합니다. 한 로봇이 어떤 구조물을 문(Door)으로 식별했다면 다른 로봇도 카메라 시점이나 센서 구성이 다르더라도 자신의 관측을 동일한 의미 개념(Semantic Concept)과 연관시킬 수 있어야 합니다. 따라서 객체 정체성(Object Identity), 범주(Category), 속성(Attribute), 기능적 역할(Functional Role), 관계(Relationship)는 개별 지각 파이프라인의 일시적인 출력이 아니라 공유 표현의 지속적인 구성요소가 될 수 있습니다.

유용한 공유 표현은 시간적 특성(Temporal Property)도 가져야 합니다. 사람의 이동, 객체 조작, 문의 개폐, 차량 이동, 로봇 자체의 행동으로 인해 물리 환경은 지속적으로 변화합니다. 표현은 지속적인 구조(Persistent Structure)와 동적 상태(Dynamic State)를 모두 유지하여 서로 다른 시간에 수집된 관측이 기존 정보를 단순히 덮어쓰는 대신 월드 상태를 갱신하도록 해야 합니다. 시간적 메모리(Temporal Memory)는 안정적인 월드 지식과 일시적인 사건(Transient Event)을 구분하고 미래 환경 상태(Future Environmental State)의 예측을 지원할 수 있습니다.

멀티모달 융합(Multimodal Fusion)은 서로 다른 센싱 시스템을 가진 로봇들이 동일한 모델에 정보를 제공할 수 있도록 합니다. 한 플랫폼은 RGB 카메라와 라이다(LiDAR)를 사용하고, 다른 플랫폼은 깊이 카메라(Depth Camera)와 촉각 센싱(Tactile Sensing)을 사용하며, 또 다른 플랫폼은 레이더(Radar), 관성 측정 장치(IMU), 고유수용감각(Proprioceptive Information)을 제공할 수 있습니다. 모달리티 특화 인코더(Modality-Specific Encoder)는 이러한 이질적인 측정값을 호환 가능한 잠재 특징(Latent Feature)으로 변환하여 동일한 하드웨어를 요구하지 않으면서 상호보완적인 관측이 공통 표현을 향상시키도록 할 수 있습니다.

서로 다른 로봇의 관측은 동일한 신뢰성을 갖지 않으므로 불확실성(Uncertainty)도 공유 정보와 함께 표현되어야 합니다. 센서 노이즈(Sensor Noise), 가림(Occlusion), 위치추정 오차(Localization Error), 환경 변화, 제한된 시야(Viewpoint)는 서로 충돌하는 추정값을 발생시킬 수 있습니다. 모든 측정값을 하나의 결정론적 상태(Deterministic State)로 강제하는 대신 표현은 신뢰도(Confidence)와 불확실성을 유지할 수 있습니다. 새로운 관측은 그 신뢰성과 시간적 관련성(Temporal Relevance)에 따라 기존 믿음(Belief)을 강화하거나 수정하거나 반박할 수 있습니다.

공유 표현(Shared Representation)이 반드시 하나의 컴퓨터에 저장되는 단일 중앙집중형 맵(Centralized Map)을 의미하는 것은 아닙니다. 이 개념은 중앙집중형(Centralized), 분산형(Distributed), 계층형(Hierarchical), 하이브리드 아키텍처(Hybrid Architecture)를 모두 지원할 수 있습니다. 개별 로봇은 로컬 월드 상태(Local World State)를 유지하면서 선택된 특징, 객체 정보, 점유 업데이트(Occupancy Update), 압축 잠재 표현(Compressed Latent Representation)을 교환할 수 있습니다. 플릿 수준 모델(Fleet-Level Model)은 지속적인 지식을 통합하고, 로컬 모델은 실시간 지각과 제어에 필요한 고주파 정보(High-Frequency Information)를 유지할 수 있습니다.

통신 제약(Communication Constraint)은 어떤 정보를 공유해야 하는지에 큰 영향을 미칩니다. 원시 카메라와 라이다 스트림(Raw Camera and LiDAR Stream)은 풍부한 정보를 포함하지만 상당한 대역폭(Bandwidth)을 요구하는 반면, 압축된 의미 객체(Semantic Object), 점유 업데이트, 잠재 특징 또는 기존 월드 상태의 변화량은 더욱 효율적으로 전송할 수 있습니다. 따라서 실용적인 시스템은 의사결정에 필요한 물리 정보를 보존하면서 중복 데이터를 줄일 수 있는 표현이 필요하며, 이를 통해 간헐적 통신(Intermittent Communication)이나 제한된 대역폭 환경에서도 협업이 가능해집니다.

표현은 공유 환경 지식(Shared Environmental Knowledge)과 체화 조건부 행동유도성(Embodiment-Conditioned Affordance)도 구분해야 합니다. 계단, 좁은 통로, 무거운 객체, 높은 플랫폼은 이를 관측하는 로봇과 독립적으로 존재하지만, 해당 대상이 주행 가능(Traversable), 도달 가능(Reachable), 운반 가능(Liftable), 안전(Safe)한지는 체화 형태(Embodiment)에 따라 달라집니다. 공유 계층은 물리적 속성을 기술하고, 로봇 특화 추론(Robot-Specific Reasoning)은 이러한 속성을 형태(Morphology), 페이로드, 운동학(Kinematics), 안정성(Stability), 이동 제약과 결합할 수 있습니다.

이러한 표현을 학습하려면 여러 로봇이 동일하거나 유사한 환경을 관측한 데이터가 유용합니다. 교차 시점 및 교차 로봇 대응(Cross-View and Cross-Robot Correspondence)은 서로 다른 인코더가 공통 객체와 장소에 대해 호환 가능한 표현을 생성하도록 유도할 수 있습니다. 예측 목표(Predictive Objective)를 통해 어떤 로봇이 관측을 제공했는지와 관계없이 공유 잠재 상태(Shared Latent State)가 미래 상태 예측을 지원하도록 요구할 수도 있습니다. 이를 통해 플랫폼 특화 센서 외형보다 근본적인 월드 동역학(World Dynamics)을 기술하는 표현을 학습할 수 있습니다.

공유 월드 표현은 각 플랫폼이 모든 상황을 직접 경험하지 않더라도 로봇 사이의 지식 전이(Knowledge Transfer)를 가능하게 합니다. 한 로봇이 차단된 통로(Blocked Corridor), 미끄러운 영역(Slippery Region), 변경된 객체 위치 또는 새로운 장애물을 발견하면 해당 정보를 동일한 환경에서 운용되는 다른 로봇이 활용할 수 있습니다. 더 큰 규모에서는 축적된 경험이 지형(Terrain), 객체 상호작용, 환경 동역학, 반복적으로 발생하는 위험(Recurring Hazard)에 관한 재사용 가능한 사전 지식(Reusable Prior)을 제공할 수 있습니다.

그러나 월드는 정적이지 않기 때문에 공유 지식은 지속적으로 적응할 수 있어야 합니다. 환경 배치가 변경되거나, 임시 장애물이 사라지거나, 운용 조건이 변화하면 기존 정보가 오래된 정보(Outdated Information)가 될 수 있습니다. 따라서 표현에는 시간적 유효성(Temporal Validity), 갱신(Update), 망각(Forgetting), 충돌 해결(Conflict Resolution), 버전 일관성(Version Consistency)을 처리하는 메커니즘이 필요합니다. 월드 상태는 영구적으로 고정된 사실의 맵이 아니라 분산된 관측(Distributed Observation)을 통해 지속적으로 변화하는 믿음(Evolving Belief)으로 다루어져야 합니다.

평가(Evaluation)는 서로 다른 로봇이 호환 가능한 표현을 생성하는지뿐만 아니라 한 플랫폼이 획득한 정보가 다른 플랫폼의 예측이나 의사결정(Decision Making)을 실제로 향상시키는지도 검증해야 합니다. 주요 평가 항목에는 교차 로봇 위치추정(Cross-Robot Localization), 객체 대응(Object Correspondence), 공유 점유 일관성(Shared Occupancy Consistency), 동적 예측의 전이(Transfer of Dynamic Prediction), 센서 누락에 대한 강건성(Robustness), 새로운 체화 형태에 대한 적응(Adaptation)이 포함될 수 있습니다. 통신 효율성(Communication Efficiency)과 전이된 지식의 실질적인 유용성도 중요한 시스템 수준의 평가 지표입니다.

따라서 로봇 간 공유 월드 표현(Shared World Representation Across Robots)은 교차 체화 모델링(Cross-Embodiment Modeling)과 범용 로봇 파운데이션 모델(General Robot Foundation Model)을 연결하는 정보적 가교(Informational Bridge)를 제공합니다. 이기종 로봇은 각자의 센서, 신체 구조, 제어기(Controller), 운용 제약을 유지하면서 물리 환경에 대한 공통 예측 표현(Common Predictive Representation)을 활용할 수 있습니다. 여러 플랫폼의 경험이 지속적으로 축적되면 이러한 공유 표현은 재사용 가능한 물리적 메모리(Physical Memory)와 지식으로 발전하여 피지컬 AI(Physical AI) 시스템 전반에서 더욱 일반적인 지각, 예측, 계획(Planning), 행동(Action)을 지원할 수 있습니다.

## 15.06. World Models and Robot Foundation Models

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

월드 모델(World Model)과 로봇 파운데이션 모델(Robot Foundation Model)은 범용 피지컬 AI(General Physical AI)의 상호보완적인 측면을 다룹니다. 월드 모델은 물리 환경(Physical Environment)이 어떻게 표현되고 그 상태가 어떻게 변화할 수 있는지를 학습하는 반면, 로봇 파운데이션 모델은 다양한 로봇 작업(Task), 환경(Environment), 체화 형태(Embodiment)에 걸쳐 재사용 가능한 능력을 제공하는 것을 목표로 합니다. 두 모델의 통합은 세계에 대한 예측적 이해(Predictive Understanding)를 범용적인 지각(Perception), 추론(Reasoning), 계획(Planning), 행동(Action)과 연결합니다.

로봇 파운데이션 모델은 로봇 지능(Robotic Intelligence)을 위한 광범위하게 사전학습된 계산 기반(Computational Foundation)으로 볼 수 있습니다. 내비게이션(Navigation), 조작(Manipulation), 이동(Locomotion), 상호작용(Interaction) 등의 행동을 위해 각각 별도의 모델을 구축하는 대신, 대규모 사전학습(Large-Scale Pretraining)을 통해 여러 응용에 적응할 수 있는 표현과 능력을 생성합니다. 이러한 모델은 비전(Vision), 언어(Language), 고유수용감각(Proprioception), 행동, 시연(Demonstration), 로봇 궤적(Robot Trajectory)을 공통 학습 아키텍처(Common Learning Architecture) 안에 통합할 수 있습니다.

월드 모델은 이러한 파운데이션에 특히 중요한 요소인 물리 동역학(Physical Dynamics)의 내부 표현(Internal Representation)을 제공합니다. 객체를 인식하거나 언어 명령을 이해하는 것만으로는 로봇이 밀기, 파지(Grasp), 가속, 회전 또는 환경과 접촉했을 때 어떤 일이 발생할지를 설명할 수 없습니다. 예측 월드 모델(Predictive World Model)은 상태 전이(State Transition)와 행동 결과(Action Consequence)를 표현하여 로봇 지능이 현재 관측에만 반응하는 것이 아니라 가능한 미래(Possible Future)를 추론하도록 합니다.

따라서 두 모델 유형은 서로 다르지만 중첩되는 수준에서 작동합니다. 로봇 파운데이션 모델은 의미 지식(Semantic Knowledge), 작업 이해(Task Understanding), 전이 가능한 기술(Transferable Skill), 행동 생성(Action Generation)을 제공할 수 있으며, 월드 모델은 공간적(Spatial), 시간적(Temporal), 물리적(Physical), 인과적(Causal) 구조를 제공합니다. 이들이 연결되면 의미적 추론(Semantic Reasoning)을 예측된 물리적 결과와 연결할 수 있습니다. 로봇은 무엇을 달성해야 하는지를 해석하는 동시에 후보 행동이 물리적으로 실행 가능한지와 어떤 결과를 만들어낼지를 추정할 수 있습니다.

공유 잠재 표현(Shared Latent Representation)은 이러한 능력 사이의 인터페이스(Interface)를 형성할 수 있습니다. 카메라(Camera), 깊이 센서(Depth Sensor), 라이다(LiDAR), 고유수용감각, 힘 센싱(Force Sensing), 언어로부터 얻은 멀티모달 관측(Multimodal Observation)을 구조화되거나 학습된 월드 상태(World State)로 인코딩할 수 있습니다. 동역학 모델(Dynamics Model)은 이 상태가 시간에 따라 어떻게 변화하는지를 예측하고, 파운데이션 모델 구성요소는 해당 표현을 작업 해석, 추론, 정책 생성(Policy Generation), 계획에 활용합니다. 예측과 행동 선택(Action Selection) 사이에서 정보가 반복적으로 순환할 수 있습니다.

이러한 통합은 상상-평가-행동(Imagine-Evaluate-Act) 과정을 지원합니다. 목표(Goal)가 주어지면 로봇 파운데이션 모델은 후보 행동(Candidate Action)이나 고수준 계획(High-Level Plan)을 생성할 수 있습니다. 월드 모델은 이러한 후보들을 내부적으로 롤아웃(Rollout)하여 미래 상태, 상호작용, 위험(Risk), 목표를 향한 진행 정도를 추정합니다. 이후 후보 미래(Candidate Future)를 평가함으로써 시스템은 학습된 행동 패턴뿐 아니라 현재 물리 상황에서 예측되는 결과를 기반으로 행동을 선택할 수 있습니다.

이러한 아키텍처는 순수한 반응형 정책(Reactive Policy)에 대한 의존성을 줄일 수 있습니다. 엔드투엔드 정책(End-to-End Policy)은 배치 조건(Deployment Condition)이 학습 분포와 유사한 경우 우수하게 작동할 수 있지만, 예상하지 못한 장애물, 객체 구성, 실패 또는 상호작용에서는 대안적 미래(Alternative Future)를 명시적으로 고려해야 할 수 있습니다. 월드 모델은 되돌리기 어렵거나 비용이 크거나 안전하지 않은 행동을 실행하기 전에 파운데이션 모델이 여러 가능성을 시험할 수 있는 예측 작업공간(Predictive Workspace)을 제공합니다.

월드 모델은 로봇 파운데이션 모델의 데이터 효율성(Data Efficiency)도 향상시킬 수 있습니다. 실제 로봇 상호작용에는 하드웨어 운용 시간, 인간 감독(Human Supervision), 안전 절차, 유지보수, 물리적 초기화(Physical Reset)가 필요하므로 비용이 높습니다. 충분히 정확한 월드 모델이 학습되면 정책 학습(Policy Learning)과 계획의 일부를 상상된 궤적(Imagined Trajectory)을 통해 수행할 수 있습니다. 이러한 합성 경험(Synthetic Experience)이 실제 데이터를 완전히 대체할 수는 없지만 수집된 물리적 경험에서 얻을 수 있는 학습 가치를 증가시킬 수 있습니다.

반대로 로봇 파운데이션 모델은 더욱 풍부한 의미적 및 작업 맥락(Semantic and Task Context)을 제공하여 월드 모델을 강화할 수 있습니다. 순수한 기하학적 동역학 모델(Geometric Dynamics Model)은 접촉 후 객체가 움직인다는 사실은 예측할 수 있지만 그 객체의 기능적 역할(Functional Role)이나 왜 그 움직임이 중요한지는 이해하지 못할 수 있습니다. 대규모 비전, 언어, 로봇 데이터에서 학습된 의미 표현(Semantic Representation)은 객체, 관계, 의도(Intent), 작업 관련성(Task Relevance)을 식별하여 지능적 행동에 중요한 정보에 월드 모델의 예측을 집중시킬 수 있습니다.

언어(Language)는 특히 유용한 연결고리를 제공할 수 있습니다. 객체 이동, 컨테이너 열기, 제한 구역 회피, 물품 전달과 같은 명령은 원시 모터 명령(Raw Motor Command)이 아니라 원하는 월드 상태의 변화(Desired World-State Change)를 설명합니다. 파운데이션 모델은 이러한 목표를 의미적으로 해석하고, 월드 모델은 목표 달성에 필요한 물리적 상태 전이를 평가할 수 있습니다. 이를 통해 추상적 의도(Abstract Intent)를 기하학, 동역학, 행동유도성(Affordance), 제약 조건(Constraint), 예측된 행동 결과와 연결할 수 있습니다.

여러 작업과 환경에 걸쳐 학습할 경우 이러한 결합은 더욱 강력해집니다. 내비게이션 궤적은 공간 구조(Spatial Structure)와 이동 능력(Mobility)을 학습시키고, 조작 데이터는 접촉과 객체 상호작용을 제공하며, 이동 데이터는 지지(Support)와 지형 동역학(Terrain Dynamics)을 제공하고, 인간 또는 로봇 비디오는 광범위한 시각적 경험을 제공합니다. 공통 사전학습 아키텍처(Common Pretrained Architecture)는 이러한 경험을 통합하여 의미 지식, 물리적 예측, 행동 능력(Action Competence)이 서로 분리된 능력으로 남지 않고 함께 향상되도록 할 수 있습니다.

교차 체화 학습(Cross-Embodiment Learning)은 이러한 관계를 더욱 확장합니다. 서로 다른 로봇은 서로 다른 저수준 행동(Low-Level Action)을 필요로 하지만 객체, 기하학, 운동(Motion), 인과성(Causality), 환경 변화에 관한 상당한 지식을 공유할 수 있습니다. 월드 모델은 물리적 상황에 대한 체화 독립적 표현(Embodiment-Independent Representation)을 제공하고, 로봇 파운데이션 모델 구성요소는 형태(Morphology), 운동학(Kinematics), 센서, 페이로드(Payload), 도달 가능성(Reachability) 등의 체화 특화 제약(Embodiment-Specific Constraint)에 따라 계획과 제어를 조건화할 수 있습니다.

월드 모델의 예측이 파운데이션 모델의 행동에 영향을 미치는 경우 불확실성(Uncertainty)은 필수적입니다. 로봇은 예측 신뢰성이 높은 익숙한 상황과 상상된 미래의 불확실성이 높은 새로운 조건을 구별해야 합니다. 예측 분포(Predictive Distribution), 신뢰도 추정(Confidence Estimation), 신규성 탐지(Novelty Detection), 앙상블(Ensemble) 등을 통해 플래너(Planner)나 정책에 불확실성을 전달할 수 있습니다. 그러면 파운데이션 모델은 불확실한 예측을 맹목적으로 따르는 대신 보수적인 행동을 선택하거나, 추가 관측을 수집하거나, 도움을 요청하거나, 폴백 행동(Fallback Behavior)을 사용할 수 있습니다.

학습은 표현 학습(Representation Learning), 미래 예측(Future Prediction), 행동 조건화(Action Conditioning), 복원(Reconstruction), 언어 정렬(Language Alignment), 모방 학습(Imitation), 제어 목표(Control Objective)의 조합을 중심으로 구성할 수 있습니다. 모든 데이터셋이 모든 신호를 포함할 필요는 없습니다. 비디오는 시각 동역학(Visual Dynamics)을 학습하고, 로봇 궤적은 행동 결과를 학습하며, 언어는 의미 구조를 제공하고, 시뮬레이션(Simulation)은 통제된 물리적 상호작용을 생성할 수 있습니다. 공동 또는 단계적 사전학습(Joint or Staged Pretraining)을 통해 이러한 데이터 소스를 점진적으로 연결하여 재사용 가능한 물리 지능(Reusable Physical Intelligence)을 구축할 수 있습니다.

배치(Deployment)에서는 로봇에 따라 서로 다른 계산 분할(Computational Partition)을 사용할 수 있습니다. 대규모 사전학습과 광범위한 상상 롤아웃(Imagined Rollout)은 강력한 컴퓨팅 인프라(Compute Infrastructure)에서 수행하고, 압축된 표현(Compact Representation), 예측 모듈(Predictive Module), 정책 또는 작업 헤드(Task Head)는 엣지 하드웨어(Edge Hardware)에서 실행할 수 있습니다. 계층적 설계(Hierarchical Design)를 통해 빠른 로컬 제어(Fast Local Control)와 상대적으로 느린 예측 추론(Predictive Reasoning)을 분리할 수도 있습니다. 따라서 모든 제어 주기(Control Cycle)마다 파운데이션 모델의 모든 구성요소를 최대 규모로 실행할 필요는 없습니다.

평가(Evaluation)는 단순히 두 개의 대규모 모델을 결합했는지가 아니라 이러한 통합이 실제로 물리 지능을 향상시키는지를 검증해야 합니다. 관련 능력에는 예측 정확도(Prediction Accuracy), 계획 성공률(Planning Success), 학습하지 않은 환경에 대한 적응(Adaptation), 장기 작업 완료(Long-Horizon Task Completion), 데이터 효율성, 불확실성 보정(Uncertainty Calibration), 분포 변화(Distribution Shift)에 대한 강건성(Robustness)이 포함됩니다. 또한 월드 모델의 예측이 실제 행동 선택을 향상시키는지, 파운데이션 모델의 의미 정보가 다운스트림 행동(Downstream Behavior)에 더 유용한 예측을 가능하게 하는지도 평가해야 합니다.

궁극적으로 월드 모델(World Model)과 로봇 파운데이션 모델(Robot Foundation Model)은 물리 세계를 이해하고, 세계가 어떻게 변화할지를 예측하며, 원하는 결과를 만들어내는 행동을 선택할 수 있는 재사용 가능한 지능(Reusable Intelligence)이라는 공통 목표로 수렴합니다. 월드 모델은 예측 가능한 물리 구조(Predictive Physical Structure)를 제공하고, 로봇 파운데이션 모델은 광범위한 의미적, 추론적, 행동적 능력(Semantic, Reasoning, and Behavioral Capability)을 제공합니다. 두 모델의 통합은 다양한 피지컬 AI 응용 전반에서 지각하고, 상상하고, 추론하고, 계획하고, 적응하고, 행동할 수 있는 범용 로봇 시스템(General-Purpose Robotic System)을 향한 중요한 아키텍처 단계가 됩니다.

## 15.07. World Models and Vision Language Action Models

![](images/image7.png){width="7.268055555555556in" height="7.268055555555556in"}

비전-언어-행동 모델(Vision-Language-Action Model)은 시각적 지각(Visual Perception)과 언어 이해(Language Understanding)를 로봇 행동(Robotic Action)에 직접 연결하여 범용 로봇 행동(General-Purpose Robot Behavior)을 위한 강력한 프레임워크를 제공합니다. 월드 모델(World Model)은 물리 환경(Physical Environment)이 시간에 따라 어떻게 변화하는지를 표현하는 상호보완적 능력을 추가합니다. 두 모델을 통합하면 로봇은 자신이 무엇을 보고 무엇을 수행하도록 요청받았는지를 이해할 뿐만 아니라, 실행하기 전에 가능한 행동의 물리적 결과(Physical Consequence)를 예측할 수 있습니다.

비전-언어-행동 모델(Vision-Language-Action Model), 즉 VLA는 일반적으로 시각적 관측(Visual Observation)과 언어 명령(Language Instruction)을 함께 입력받아 행동 또는 행동 표현(Action Representation)을 생성합니다. 대규모 사전학습(Large-Scale Pretraining)을 통해 이러한 모델은 다양한 데이터에서 객체, 장면(Scene), 명령, 작업(Task), 행동 사이의 관계를 학습할 수 있습니다. 이는 인간의 의도(Human Intent)에서 로봇 행동으로 이어지는 의미적 경로(Semantic Pathway)를 형성하지만, 직접적인 행동 생성만으로는 각각의 후보 행동 이후 세계가 어떻게 변화할지를 예측하는 명시적인 메커니즘을 반드시 제공하는 것은 아닙니다.

월드 모델은 이러한 예측 구성요소(Predictive Component)를 제공합니다. 현재 상태(Current State)와 가능한 행동이 주어지면 미래 상태(Future State), 객체 운동(Object Motion), 접촉 사건(Contact Event), 점유 변화(Occupancy Change), 환경 상호작용(Environmental Interaction), 기타 결과를 추정합니다. 관측과 언어를 하나의 행동으로 직접 매핑하는 대신, 통합 시스템은 여러 개의 가능한 행동을 생성하고 월드 모델을 이용하여 각각의 결과를 상상할 수 있습니다. 따라서 예측(Prediction)은 이해(Understanding)와 실행(Execution) 사이의 중간 추론 과정(Intermediate Reasoning Process)이 됩니다.

이러한 통합은 공유 잠재 월드 표현(Shared Latent World Representation)을 중심으로 구성할 수 있습니다. 시각적 관측은 기하학(Geometry), 객체(Object), 의미(Semantics), 운동(Motion), 공간적 관계(Spatial Relationship)의 표현으로 인코딩되고, 언어는 목표(Goal), 제약 조건(Constraint), 작업 맥락(Task Context)을 지정합니다. 행동 표현은 가능한 개입(Intervention)을 기술합니다. 월드 모델은 이러한 공유 공간에서 상태 전이(State Transition)를 예측함으로써 비전(Vision), 언어(Language), 행동(Action), 물리 동역학(Physical Dynamics)이 서로 분리된 처리 흐름으로 남지 않고 공통 표현을 통해 상호작용하도록 합니다.

많은 로봇 명령은 물리 세계에 요구되는 변화를 표현하기 때문에 언어는 특히 유용합니다. 객체를 테이블 위에 놓기, 서랍 열기, 출입구 통과하기, 사람 피하기와 같은 명령은 정확한 액추에이터 명령(Actuator Command)이 아니라 목표와 제약 조건을 지정합니다. VLA 모델은 이러한 명령을 후보 행동(Candidate Behavior)으로 변환하고, 월드 모델은 예측된 상태 전이가 실제로 의도된 의미적 목표(Semantic Goal)를 만족시키는지를 평가할 수 있습니다.

시각 정보(Visual Information)는 이러한 명령을 현재 환경과 연결하는 데 필요한 기반화(Grounding)를 제공합니다. 객체의 위치를 파악하고, 관계를 이해하고, 장애물을 식별하며, 관련 상태 변화를 탐지해야 합니다. 월드 모델은 현재 존재하는 것뿐만 아니라 상호작용 이후 무엇이 존재할 수 있는지를 표현함으로써 이러한 시각적 기반화를 시간적으로 확장합니다. 그 결과 현재 지각(Current Perception), 의도된 미래 상태(Intended Future State), 그리고 두 상태 사이를 연결하는 행동 시퀀스(Action Sequence)를 하나의 표현으로 연결할 수 있습니다.

행동 조건화(Action Conditioning)는 VLA 정책(VLA Policy)과 예측 동역학(Predictive Dynamics)을 연결하는 핵심적인 연결고리를 형성합니다. 동일한 시각적 장면이라도 로봇이 기다리거나, 이동하거나, 파지(Grasp)하거나, 밀거나, 회전시키거나, 객체를 놓는지에 따라 서로 다른 방식으로 변화할 수 있습니다. 월드 모델은 후보 행동을 조건으로 이러한 대안적 미래(Alternative Future)를 추정합니다. 이후 VLA 구성요소는 예측 결과를 언어로 정의된 목표와 비교하고 요청된 작업에 가장 적합한 결과를 만들어낼 행동을 선택할 수 있습니다.

이를 통해 상상-평가-행동 루프(Imagine-Evaluate-Act Loop)가 형성됩니다. VLA 모델은 후보 행동 또는 짧은 행동 시퀀스를 제안하고, 월드 모델은 이를 미래로 롤아웃(Rollout)하며, 평가기(Evaluator)는 예상되는 작업 진행(Task Progress), 물리적 실행 가능성(Physical Feasibility), 안전성(Safety), 비용(Cost), 불확실성(Uncertainty)을 평가합니다. 가장 적절한 후보를 실행한 후 새로운 관측으로 월드 상태를 갱신하고 이 과정을 반복합니다. 이러한 폐루프 추론(Closed-Loop Reasoning)은 학습된 정책의 유연성과 변화하는 물리 조건에 대한 명시적 예측을 결합합니다.

장기 작업(Long-Horizon Task)은 이러한 통합으로부터 특히 큰 이점을 얻을 수 있습니다. 다른 방에서 객체를 가져오는 명령에는 내비게이션(Navigation), 장애물 회피(Obstacle Avoidance), 위치추정(Localization), 접근(Reaching), 파지, 운반, 배치(Placement)가 필요할 수 있습니다. 긴 저수준 행동 시퀀스를 직접 예측하면 오차가 누적될 수 있습니다. 월드 모델은 예측된 중간 상태(Intermediate State)를 유지하고 관측이 변화할 때마다 VLA 시스템이 반복적으로 재계획(Re-Planning)하도록 하여 고수준 의미 목표와 물리적으로 기반화된 짧은 행동 구간을 연결할 수 있습니다.

월드 모델은 VLA 시스템에 반사실적 추론(Counterfactual Reasoning)도 제공할 수 있습니다. 로봇은 다른 파지 방법을 선택하거나, 다른 방향에서 객체에 접근하거나, 장애물을 우회하거나, 상호작용을 지연했을 때 어떤 일이 발생할지를 추정할 수 있습니다. 이러한 반사실적 미래(Counterfactual Future)는 실제로 실행할 필요가 없습니다. 내부 평가를 통해 비효율적이거나, 불안정하거나, 위험하거나, 명령을 만족시킬 가능성이 낮은 행동을 제거함으로써 실제 환경에서 비용이 높은 시행착오(Trial and Error)를 줄일 수 있습니다.

상상된 미래가 항상 신뢰할 수 있는 것은 아니므로 불확실성(Uncertainty)은 필수적입니다. 가려진 객체(Occluded Object), 익숙하지 않은 환경, 모호한 명령(Ambiguous Instruction), 새로운 상호작용, 충분히 모델링되지 않은 동역학은 예측 불확실성을 증가시킬 수 있습니다. 통합 시스템은 이러한 불확실성을 행동 선택 과정에 전달해야 합니다. 신뢰도가 낮을 경우 VLA 모델은 정보 수집 행동(Information-Gathering Action)을 선택하거나, 속도를 낮추거나, 다른 시점에서 다시 관측하거나, 보수적인 대안을 선택하거나, 불확실한 계획을 실행하는 대신 인간에게 명확한 지시를 요청할 수 있습니다.

VLA 표현(VLA Representation)이 월드 모델링을 향상시킬 수도 있기 때문에 두 모델의 관계는 양방향(Bidirectional)입니다. 비전-언어 사전학습(Vision-Language Pretraining)은 로봇 궤적만으로 학습하기 어려운 객체, 활동(Activity), 관계, 기능적 개념(Functional Concept)에 관한 의미 지식을 제공합니다. 언어는 현재 작업에서 장면의 어떤 부분이 중요한지를 식별할 수 있으므로 월드 모델이 관측 가능한 모든 세부 사항을 동일하게 처리하는 대신 관련 객체, 상호작용, 제약 조건, 가능한 상태 변화에 예측 능력을 집중하도록 도울 수 있습니다.

학습에는 인터넷 규모의 비전-언어 데이터(Internet-Scale Vision-Language Data)와 로봇 시연(Robot Demonstration), 행동 궤적(Action Trajectory), 인간 비디오(Human Video), 시뮬레이션(Simulation), 멀티모달 센서 시퀀스(Multimodal Sensor Sequence)를 결합할 수 있습니다. 비전-언어 데이터는 의미적 폭(Semantic Breadth)을 제공하고, 로봇 및 시뮬레이션 데이터는 물리적으로 기반화된 상태 전이와 행동 결과를 제공합니다. 표현 학습(Representation Learning), 언어 정렬(Language Alignment), 미래 예측(Future Prediction), 행동 예측(Action Prediction), 모방 학습(Imitation), 마스킹 모델링(Masked Modeling), 행동 조건부 동역학(Action-Conditioned Dynamics) 등의 목표가 통합 아키텍처에 상호보완적인 감독 신호를 제공할 수 있습니다.

교차 체화 학습(Cross-Embodiment Training)은 의미적 의도(Semantic Intent)를 로봇 특화 실행(Robot-Specific Execution)과 더욱 명확하게 분리할 수 있습니다. 객체를 이동하라는 명령은 모바일 매니퓰레이터(Mobile Manipulator), 휴머노이드(Humanoid), 기타 실행 가능한 플랫폼에 공통으로 적용될 수 있지만 각각의 모터 명령은 서로 다릅니다. 공유 월드 모델은 객체와 원하는 물리적 변화를 표현하고, 체화 조건부 VLA 구성요소(Embodiment-Conditioned VLA Component)는 이러한 변화를 각 로봇의 형태(Morphology), 도달 가능성(Reachability), 센서, 운동학(Kinematics), 제어 인터페이스(Control Interface)에 적합한 행동으로 변환합니다.

배치(Deployment)에서는 계층적 계산(Hierarchical Computation)을 이용하여 추론 품질과 실시간 제약(Real-Time Constraint) 사이의 균형을 맞출 수 있습니다. 고수준 언어 해석(High-Level Language Interpretation), 작업 분해(Task Decomposition), 장기 월드 모델 롤아웃(Longer World-Model Rollout)은 상대적으로 느린 주기로 수행하고, 단기 예측(Short-Horizon Prediction)과 제어는 로봇 가까이에서 빠르게 실행할 수 있습니다. 이러한 분리를 통해 모든 저수준 제어 업데이트마다 전체 파운데이션 규모의 아키텍처를 실행하지 않으면서도 비용이 높은 예측적 추론(Predictive Reasoning)을 행동 결정에 활용할 수 있습니다.

평가(Evaluation)는 월드 모델이 VLA 행동을 실제로 더욱 물리적으로 기반화하고 신뢰성 있게 만드는지를 측정해야 합니다. 관련 평가에는 명령 수행 성공률(Instruction-Following Success), 행동 예측(Action Prediction), 미래 상태 정확도(Future-State Accuracy), 장기 작업 완료(Long-Horizon Completion), 예상하지 못한 변화로부터의 복구(Recovery), 반사실적 선택(Counterfactual Selection), 불확실성 보정(Uncertainty Calibration), 새로운 환경 또는 체화 형태에 대한 일반화(Generalization)가 포함됩니다. 핵심적인 질문은 물리적 결과에 대한 내부 상상(Imagined Physical Consequence)이 단순한 비전-언어-행동 직접 매핑보다 더 나은 의사결정을 가능하게 하는가입니다.

따라서 월드 모델(World Model)과 비전-언어-행동 모델(Vision-Language-Action Model)은 점차 범용화되는 로봇 지능을 위한 두 가지 상호보완적인 기반을 제공합니다. VLA 모델은 지각과 언어를 행동에 연결하고, 월드 모델은 현재 상태와 행동을 가능한 미래(Possible Future)에 연결합니다. 두 모델을 통합하면 시스템은 명령을 이해하고, 물리적 상황을 지각하며, 여러 대안적 결과를 상상하고, 위험과 목표 진행 정도를 평가하며, 물리적으로 기반화된 행동(Grounded Action)을 선택할 수 있습니다. 이는 적응 가능하고 범용적인 피지컬 AI(Physical AI)를 향한 중요한 발전 경로를 형성합니다.

## 15.08. World Models for Physical Reasoning

![](images/image8.png){width="7.268055555555556in" height="7.268055555555556in"}

물리적 추론(Physical Reasoning)은 지능형 시스템이 환경에 무엇이 존재하는지를 이해하는 것뿐만 아니라, 물리적 개체(Physical Entity)가 어떻게 상호작용하고, 움직이며, 서로를 제약하고, 행동(Action)에 반응하는지를 이해하는 것을 요구합니다. 월드 모델(World Model)은 상태(State)를 표현하고 시간에 따른 전이(Transition)를 예측함으로써 이러한 능력을 제공합니다. 피지컬 AI(Physical AI)에서 이는 지각(Perception)을 현재 상태의 인식에서 앞으로 무엇이 발생할 수 있으며 특정 결과가 왜 발생하는지를 추론하는 능력으로 확장합니다.

물리 세계(Physical World)는 위치(Position), 방향(Orientation), 기하학(Geometry), 속도(Velocity), 질량(Mass), 지지(Support), 접촉(Contact), 기능적 관계(Functional Relationship)와 같은 속성을 가진 상호작용하는 개체들의 집합으로 표현할 수 있습니다. 월드 모델은 관측을 서로 관련 없는 픽셀이나 센서 측정값으로 처리하는 대신 구조화된 상태(Structured State) 또는 잠재 상태(Latent State)로 구성할 수 있습니다. 물리적 추론은 이러한 표현을 기반으로 관계를 추론하고, 변화를 예측하며, 장래의 행동에 어떤 장면 요소가 중요한지를 판단합니다.

공간적 추론(Spatial Reasoning)은 이러한 능력의 기본적인 토대를 형성합니다. 로봇은 자유 공간(Free Space), 포함 관계(Containment), 근접성(Proximity), 상대 위치(Relative Position), 가시성(Visibility), 도달 가능성(Reachability), 충돌 관계(Collision Relationship)를 이해해야 합니다. 이러한 속성은 경로의 주행 가능성(Traversability), 객체의 접근 가능성, 행동의 기하학적 실행 가능성(Geometric Feasibility)을 결정합니다. 월드 모델은 시간에 따라 공간 관계를 유지하여 객체가 이동하거나, 관측이 가려지거나, 로봇의 시점(Viewpoint)이 변경되더라도 일관된 추론을 가능하게 합니다.

시간적 추론(Temporal Reasoning)은 이러한 표현을 정적인 기하학에서 변화하는 과정으로 확장합니다. 물리적 사건(Physical Event)에는 순서(Order), 지속 시간(Duration), 의존 관계(Dependency)가 존재합니다. 객체는 들어 올리기 전에 먼저 파지(Grasp)되어야 하고, 로봇이 통과하기 전에 문이 열려야 하며, 충돌을 피하려면 충돌이 발생하기 전에 제동(Braking)이 시작되어야 합니다. 예측 상태 전이(Predictive State Transition)는 현재 조건을 중간 상태 및 미래 상태와 연결하여 개별 관측이 아니라 일련의 시퀀스(Sequence)에 대한 추론을 지원합니다.

상호작용 추론(Interaction Reasoning)은 개체들이 접촉과 힘(Force)을 통해 서로에게 어떤 영향을 미치는지를 다룹니다. 객체를 밀면 병진(Translation)하거나 회전(Rotation)할 수 있고, 객체를 파지하면 로봇과 객체 사이의 관계가 변화하며, 불안정한 지형을 밟으면 지지 상태와 균형(Balance)이 달라질 수 있습니다. 유용한 월드 모델은 모든 물리량을 정확하게 해석적으로 시뮬레이션하지 않더라도 이러한 상호작용 패턴을 포착해야 합니다. 학습된 표현(Learned Representation)은 지각, 계획(Planning), 제어(Control)에 가장 중요한 결과를 근사할 수 있습니다.

인과적 추론(Causal Reasoning)은 상관관계(Correlation)와 개입(Intervention)을 구분함으로써 또 다른 추론 계층을 추가합니다. 두 객체가 함께 움직이는 것을 관측하는 것만으로는 어떤 행동이 그 변화를 발생시켰는지를 반드시 설명할 수 없습니다. 행동 조건부 월드 모델(Action-Conditioned World Model)은 자연적으로 발생할 것으로 예상되는 변화와 로봇의 개입 이후 발생할 수 있는 변화를 비교할 수 있습니다. 이는 원인과 결과(Cause and Effect)를 추론하는 기반을 제공하고, 서로 다른 행동이 현재의 물리 상태를 어떻게 의도적으로 변화시킬 수 있는지를 시스템이 판단하도록 합니다.

반사실적 추론(Counterfactual Reasoning)은 이러한 예측 구조에서 자연스럽게 이어집니다. 로봇은 행동하기 전에 오른쪽 대신 왼쪽으로 이동하거나, 다른 방향에서 파지하거나, 더 작은 힘을 적용하거나, 움직이는 장애물이 지나갈 때까지 기다리는 것과 같은 대안을 고려할 수 있습니다. 월드 모델은 이러한 대안에 대한 예측 결과(Predicted Outcome)를 생성하여 시스템이 내부적으로 여러 가능성을 비교할 수 있도록 합니다. 따라서 물리적 추론은 단순히 반응을 선택하는 것이 아니라 여러 미래(Future)를 평가하는 과정으로 발전합니다.

로봇은 완전한 세계를 관측하는 경우가 거의 없으므로 객체 영속성(Object Permanence)과 숨겨진 상태 추론(Hidden-State Inference) 역시 필수적입니다. 객체는 장애물 뒤로 사라질 수 있고, 내부 메커니즘은 보이지 않을 수 있으며, 센서 범위가 불완전할 수도 있습니다. 월드 모델은 이전 관측과 학습된 동역학(Learned Dynamics)을 기반으로 관측되지 않은 개체와 상태에 대한 잠재적 믿음(Latent Belief)을 유지할 수 있습니다. 새로운 증거가 나타나면 최신 관측만으로 전체 장면을 다시 구성하는 대신 이러한 믿음을 갱신할 수 있습니다.

행동유도성 추론(Affordance Reasoning)은 물리적 속성을 가능한 행동과 연결합니다. 표면은 물체를 올려놓을 수 있는 지지를 제공하고, 손잡이는 당기는 행동을 가능하게 하며, 개구부(Opening)는 통과를 허용하고, 객체는 특정 방향에서 파지 가능할 수 있습니다. 행동유도성(Affordance)은 행동하는 로봇의 능력에 따라 달라지므로 순수하게 객체만의 속성은 아닙니다. 월드 모델은 환경 표현(Environment Representation)과 체화 정보(Embodiment Information)를 결합하여 특정 플랫폼에서 어떤 상호작용이 실행 가능한지를 예측할 수 있습니다.

복잡한 장면에서는 여러 관계가 동시에 결과에 영향을 미치기 때문에 조합적 추론(Compositional Reasoning)이 중요해집니다. 하나의 객체를 이동하면 다른 객체가 드러날 수 있고, 컨테이너(Container)를 열면 내부 내용물에 접근할 수 있으며, 지지 상태를 변경하면 쌓여 있는 객체가 불안정해질 수 있습니다. 객체, 관계, 행동, 전이를 조합적으로 표현하면 가능한 모든 물리 상황을 학습 데이터에서 직접 경험하지 않더라도 단순한 상호작용에서 학습한 지식을 새로운 조합에 대한 추론에 활용할 수 있습니다.

물리적 추론은 여러 공간적·시간적 척도(Spatial and Temporal Scale)에 걸쳐 작동해야 합니다. 접촉, 균형, 장애물 회피, 액추에이터 응답(Actuator Response)에는 빠른 추론이 필요할 수 있지만, 내비게이션(Navigation), 조작 시퀀스(Manipulation Sequence), 장기 작업(Long-Horizon Task)에는 상대적으로 느리고 장기적인 추론이 필요합니다. 계층적 월드 모델(Hierarchical World Model)은 세부적인 로컬 동역학(Local Dynamics)과 추상적인 사건 및 작업 상태(Task State)를 함께 표현하여 모든 미래 순간을 동일한 해상도로 예측할 필요성을 줄이면서 이러한 서로 다른 척도를 연결할 수 있습니다.

물리적 예측은 거의 항상 완벽하지 않으므로 불확실성(Uncertainty)은 기본적인 요소입니다. 마찰(Friction)을 알 수 없거나, 객체가 부분적으로만 관측되거나, 사람이 예측하기 어렵게 행동하거나, 학습된 동역학이 익숙하지 않은 상황을 만날 수 있습니다. 따라서 추론 시스템은 여러 개의 가능한 미래(Plausible Future) 또는 예측 결과에 대한 신뢰도(Confidence)를 표현해야 합니다. 불확실성 인식 월드 모델(Uncertainty-Aware World Model)은 플래너(Planner)가 강건한 행동과 현재 증거가 충분히 뒷받침하지 못하는 가정에 성공 여부가 의존하는 행동을 구별하도록 합니다.

물리적 추론은 학습된 동역학과 명시적인 물리 사전지식(Physical Prior)을 결합할 수도 있습니다. 기하학, 운동학적 제약(Kinematic Constraint), 보존 원리(Conservation Principle), 접촉 구조(Contact Structure), 알려진 로봇의 한계는 예측을 제약할 수 있으며, 학습된 구성요소는 해석적으로 모델링하기 어려운 복잡한 효과를 포착할 수 있습니다. 이러한 하이브리드 추론(Hybrid Reasoning)은 모델이 모든 물리적 관계를 경험만으로 처음부터 다시 발견해야 하는 부담을 줄여 일관성과 데이터 효율성(Data Efficiency)을 향상시킬 수 있습니다.

언어(Language)와 의미 지식(Semantic Knowledge)은 목표와 관련 개체를 식별함으로써 물리적 추론을 안내할 수 있습니다. 깨지기 쉬운 객체를 안정적인 표면에 안전하게 놓으라는 명령에는 궁극적으로 물리적 상태와 결과에 기반화(Grounding)되어야 하는 개념들이 포함됩니다. 의미 모델(Semantic Model)은 무엇이 중요한지를 식별하고, 월드 모델은 지지, 도달 가능성, 운동(Motion), 충돌 위험(Collision Risk), 가능한 미래 상태를 평가할 수 있습니다. 이를 통해 추상적 추론(Abstract Reasoning)을 물리적으로 실행 가능한 행동과 연결할 수 있습니다.

물리적 추론의 학습에는 단순한 정적 인식(Static Recognition)이 아니라 의미 있는 상태 변화를 포함하는 경험이 필요합니다. 로봇 궤적(Robot Trajectory), 조작 시연(Manipulation Demonstration), 내비게이션 시퀀스(Navigation Sequence), 인간 비디오(Human Video), 시뮬레이션 롤아웃(Simulation Rollout), 멀티모달 센서 데이터(Multimodal Sensor Data)는 모델을 시간적·인과적 구조(Temporal and Causal Structure)에 노출시킵니다. 자기지도 미래 예측(Self-Supervised Future Prediction)과 행동 조건부 학습(Action-Conditioned Learning)은 이러한 시퀀스에서 직접 감독 신호(Supervision Signal)를 추출할 수 있으며, 시뮬레이션은 개입, 실패, 희귀한 물리적 구성을 체계적으로 생성할 수 있습니다.

평가(Evaluation)는 모델이 암기된 궤적을 넘어 추론할 수 있는지를 검증해야 합니다. 유용한 벤치마크(Benchmark)는 학습하지 않은 객체 배치(Unseen Object Arrangement), 새로운 행동 조합(Novel Action Combination), 가림(Occlusion), 변화된 물리적 속성, 다단계 상호작용(Multi-Step Interaction), 반사실적 질문(Counterfactual Question), 분포 변화(Distribution Shift)를 포함해야 합니다. 성공 여부는 예측 정확도만으로 측정해서는 안 되며, 학습된 물리 표현이 계획, 적응(Adaptation), 안전성(Safety), 여러 개의 상호 의존적인 상태 전이를 필요로 하는 작업의 완료 성능을 실제로 향상시키는지도 평가해야 합니다.

궁극적으로 물리적 추론을 위한 월드 모델(World Model for Physical Reasoning)은 피지컬 AI가 지각, 동역학, 인과성(Causality), 행동유도성, 불확실성, 행동을 연결할 수 있는 내부 계산 공간(Internal Computational Space)을 제공합니다. 로봇은 각각의 관측에 직접 반응하는 대신 세계에 대한 믿음(Belief)을 유지하고, 숨겨진 상태를 추론하며, 다양한 개입을 상상하고, 대안적 미래를 비교하며, 새로운 증거가 들어오면 자신의 예측을 수정할 수 있습니다. 이러한 예측적 추론 능력(Predictive Reasoning Capability)은 더욱 자율적이고 범용적인 물리 지능(General Physical Intelligence)을 구축하기 위한 핵심 기반을 형성합니다.

## 15.09. World Model Pretraining and Task Heads

![](images/image9.png){width="7.268055555555556in" height="7.268055555555556in"}

월드 모델 사전학습(World Model Pretraining)은 일반적인 물리 구조(General Physical Structure)를 학습하는 비용이 높은 과정과, 이러한 지식을 개별 로봇 작업에 적응시키는 상대적으로 가벼운 과정을 분리합니다. 공유 사전학습 백본(Shared Pretrained Backbone)은 광범위한 경험으로부터 기하학(Geometry), 객체(Object), 운동(Motion), 상호작용(Interaction), 시간적 동역학(Temporal Dynamics), 불확실성(Uncertainty)의 표현을 학습합니다. 이후 작업 헤드(Task Head)는 이러한 재사용 가능한 표현을 내비게이션(Navigation), 조작(Manipulation), 예측(Prediction), 계획(Planning), 제어(Control)에 필요한 출력으로 변환합니다.

핵심 개념은 최종 출력이 서로 다르더라도 많은 로봇 작업이 동일한 기반 물리 정보(Underlying Physical Information)에 의존한다는 것입니다. 충돌 회피(Collision Avoidance)에는 기하학과 운동이 필요하고, 조작에는 객체와 접촉 관계(Contact Relationship)가 필요하며, 내비게이션에는 자유 공간(Free Space)과 주행 가능성(Traversability)이 필요합니다. 이러한 속성을 각각 독립적으로 다시 학습하는 대신 사전학습된 월드 모델은 이를 하나의 공통 잠재 표현(Common Latent Representation)에 인코딩하고, 여러 작업 특화 구성요소(Task-Specific Component)가 이후 이를 재사용할 수 있습니다.

사전학습(Pretraining)은 이질적인 관측(Heterogeneous Observation)을 잠재 월드 상태(Latent World State)로 변환하는 것에서 시작됩니다. 카메라(Camera), 깊이 센서(Depth Sensor), 라이다(LiDAR), 레이더(Radar), 고유수용감각(Proprioception), 힘 센싱(Force Sensing) 등의 모달리티(Modality)는 정보가 융합되기 전에 서로 다른 인코더(Encoder)를 사용할 수 있습니다. 생성되는 표현은 단순히 원시 감각 입력(Raw Sensory Input)을 재현하기보다 환경의 안정적이고 예측 가능한 속성을 보존해야 합니다. 이러한 잠재 상태는 대규모 사전학습과 다운스트림 특화(Downstream Specialization)를 연결하는 공유 정보 인터페이스(Shared Informational Interface)가 됩니다.

동역학 구성요소(Dynamics Component)는 잠재 상태가 시간에 따라 어떻게 변화하는지를 학습함으로써 표현을 시간축으로 확장합니다. 현재 상태, 시간적 맥락(Temporal Context), 그리고 필요한 경우 행동(Action)이 주어지면 모델은 미래 잠재 상태(Future Latent State) 또는 가능한 미래에 대한 분포(Distribution)를 예측합니다. 학습 목표에는 미래 상태 예측(Future-State Prediction), 마스킹 모델링(Masked Modeling), 복원(Reconstruction), 멀티모달 정렬(Multimodal Alignment), 점유 예측(Occupancy Prediction), 행동 조건부 전이(Action-Conditioned Transition)가 포함될 수 있습니다. 이러한 목표들은 백본이 재사용 가능한 공간적·시간적 규칙성을 포착하도록 유도합니다.

사전학습 이후 작업 헤드(Task Head)는 공유 월드 상태에 대한 특화된 해석(Specialized Interpretation)을 제공합니다. 점유 헤드(Occupancy Head)는 공간의 특정 영역이 비어 있는지 또는 점유되어 있는지를 추정할 수 있고, 운동 헤드(Motion Head)는 동적 객체의 궤적(Trajectory)을 예측할 수 있습니다. 의미 헤드(Semantic Head)는 객체나 영역을 분류하고, 주행 가능성 헤드(Traversability Head)는 특정 로봇이 어디로 이동할 수 있는지를 판단할 수 있습니다. 이러한 출력은 서로 크게 다르지만 모두 동일한 사전학습 환경 표현에 의존할 수 있습니다.

작업 헤드는 보다 고수준의 물리적 추론(Physical Reasoning)도 지원할 수 있습니다. 충돌 위험 헤드(Collision-Risk Head)는 미래의 위험을 추정하고, 행동유도성 헤드(Affordance Head)는 가능한 상호작용을 식별하며, 가치 또는 보상 헤드(Value or Reward Head)는 목표를 향한 진행 정도를 평가할 수 있습니다. 계획 구성요소(Planning Component)는 후보 행동을 비교할 때 이러한 예측을 질의할 수 있습니다. 따라서 사전학습된 월드 모델은 공통 예측 기반(Common Predictive Substrate)으로 작동하고, 각각의 헤드는 특정 의사결정에 적합한 형태로 월드 모델의 지식을 노출합니다.

백본(Backbone)과 헤드(Head)의 구분이 항상 절대적인 것은 아닙니다. 일부 응용에서는 사전학습된 파라미터(Parameter)의 대부분을 동결(Freeze)하고 작은 출력 모듈(Output Module)만 학습할 수 있으며, 다른 응용에서는 작업 헤드와 함께 선택된 계층을 미세조정(Fine-Tuning)할 수 있습니다. 어댑터 모듈(Adapter Module), 저랭크 업데이트(Low-Rank Update), 프롬프트(Prompt), 조건화 토큰(Conditioning Token), 혼합 메커니즘(Mixture Mechanism)은 그 중간 전략을 제공할 수 있습니다. 적절한 방법은 작업의 신규성(Task Novelty), 사용 가능한 데이터, 계산 제약(Compute Constraint), 필요한 특화 수준에 따라 달라집니다.

다운스트림 데이터(Downstream Data)가 제한적인 경우 백본 동결(Backbone Freezing)은 매력적인 방법입니다. 일반 표현을 변경하지 않기 때문에 비교적 작은 작업 데이터셋으로 경량 헤드(Lightweight Head)를 학습하면서 기존에 학습된 물리 지식을 손상시키지 않을 수 있습니다. 또한 계산량을 줄이고 동일한 백본 위에 여러 작업 헤드를 배치하기 쉽게 만듭니다. 그러나 새로운 작업이 사전학습 과정에서 충분히 보존되지 않은 물리 정보를 요구한다면 성능에 한계가 발생할 수 있습니다.

미세조정(Fine-Tuning)은 표현 자체를 변화시킬 수 있으므로 더 높은 적응성(Adaptability)을 제공합니다. 특이한 지형(Unusual Terrain)에서 운용되거나, 변형 가능한 객체(Deformable Object)를 조작하거나, 새로운 센서 구성을 사용하는 로봇은 사전학습에서 강조된 특징과 다른 특징을 필요로 할 수 있습니다. 선택적 미세조정(Selective Fine-Tuning)은 광범위하게 유용한 지식을 보호하면서 월드 모델의 관련 부분을 적응시킬 수 있습니다. 이 과정에서는 파국적 망각(Catastrophic Forgetting)이나 작은 다운스트림 데이터셋에 대한 과도한 특화를 방지하기 위한 신중한 최적화가 필요합니다.

멀티헤드 학습(Multi-Head Learning)은 작업 사이의 관계를 더욱 적극적으로 활용할 수 있습니다. 점유, 깊이(Depth), 의미, 운동, 접촉(Contact), 위험(Risk) 예측은 서로 보완적인 방식으로 표현을 제약합니다. 여러 헤드를 공동으로 학습하면 각 목표가 공통 물리 구조를 강화하는 경우 백본의 품질을 향상시킬 수 있습니다. 반면 서로 호환되지 않는 목표는 부정적 전이(Negative Transfer)를 발생시킬 수 있으므로 손실 균형 조정(Loss Balancing), 작업 조건화(Task Conditioning), 모듈형 라우팅(Modular Routing), 부분적으로 분리된 표현 등을 통해 한 작업이 다른 작업의 성능을 저하시키지 않도록 해야 합니다.

작업 헤드는 체화 독립적(Embodiment-Independent)이거나 체화 조건부(Embodiment-Conditioned)일 수 있습니다. 객체 정체성(Object Identity)과 일반적인 장면 기하학(Scene Geometry)은 여러 로봇이 공유할 수 있지만, 주행 가능성, 도달 가능성(Reachability), 안정성(Stability), 파지 가능성(Graspability), 페이로드 실행 가능성(Payload Feasibility)은 행동하는 플랫폼에 따라 달라집니다. 따라서 크기, 형태(Morphology), 운동학(Kinematics), 센서 배치(Sensor Placement), 액추에이터 한계(Actuator Limit)와 같은 체화 정보를 특정 헤드에 조건으로 제공하면서 기반 환경 표현은 이기종 로봇(Heterogeneous Robot) 전반에서 광범위하게 재사용할 수 있습니다.

모듈형 백본-헤드 아키텍처(Modular Backbone-and-Head Architecture)는 서로 다른 시간 해상도(Temporal Resolution)도 지원할 수 있습니다. 빠른 헤드는 충돌 위험, 로컬 점유(Local Occupancy), 접촉, 단기 운동(Short-Horizon Motion)을 높은 빈도로 추정하고, 느린 헤드는 작업 진행(Task Progress), 장기 예측(Long-Horizon Prediction), 의미적 사건(Semantic Event)을 추론할 수 있습니다. 두 유형 모두 동일한 월드 모델에서 생성된 표현에 접근할 수 있습니다. 이를 통해 모든 예측을 동일한 주기로 실행하지 않고 각 작업의 시간적 요구에 따라 계산 자원을 할당할 수 있습니다.

불확실성(Uncertainty)은 사전학습 표현에서 다운스트림 헤드까지 전달되어야 합니다. 기반 월드 상태가 충분히 관측되지 않았거나 학습 분포(Training Distribution)를 벗어난 경우에도 작업 예측 자체는 겉보기에 정밀하게 나타날 수 있습니다. 신뢰도 추정(Confidence Estimate), 예측 분포(Predictive Distribution), 앙상블(Ensemble), 불확실성 인식 잠재 상태(Uncertainty-Aware Latent State)를 활용하면 헤드가 신뢰할 수 있는 지식과 불확실한 추론을 구분하는 데 도움이 됩니다. 이후 계획 및 제어 시스템은 불확실한 월드 모델 상태에 의존하는 다운스트림 예측에 대해 보다 보수적으로 대응할 수 있습니다.

작업 헤드 적응(Task-Head Adaptation)은 다운스트림 학습이 원시 관측에서 시작하는 대신 이미 구조화된 물리 지식(Structured Physical Knowledge)에서 시작되므로 데이터 효율성(Data Efficiency)을 크게 향상시킬 수 있습니다. 새로운 작업에서는 객체, 기하학, 운동, 시간 구조를 처음부터 다시 학습하는 대신 기존 개념을 어떻게 해석해야 하는지를 보여주는 사례만 필요할 수 있습니다. 로봇 응용이 증가할수록 이러한 특성은 더욱 중요해지며, 대규모 사전학습 비용을 여러 특화 능력(Specialized Capability)에 걸쳐 분산하여 활용할 수 있습니다.

동일한 아키텍처는 지속적인 확장(Continual Expansion)도 지원합니다. 새로운 요구사항이 발생할 때 전체 시스템을 다시 구축하지 않고 새로운 작업 헤드를 추가할 수 있습니다. 예를 들어 로봇 플릿(Robot Fleet)은 초기에는 점유, 내비게이션, 충돌 헤드를 사용하고 이후 조작, 이상 탐지(Anomaly Detection), 상호작용 예측(Interaction Prediction), 검사(Inspection) 능력을 추가할 수 있습니다. 공유 표현이 충분히 일반적이라면 이러한 추가 기능은 독립적인 학습 프로젝트가 아니라 기존 물리 지식 파운데이션(Physical Knowledge Foundation)의 확장이 됩니다.

평가(Evaluation)는 사전학습된 백본의 품질과 개별 작업 헤드의 품질을 구분해야 합니다. 선형 프로빙(Linear Probing), 동결 백본 평가(Frozen-Backbone Evaluation), 퓨샷 적응(Few-Shot Adaptation), 전체 미세조정(Full Fine-Tuning), 학습하지 않은 환경으로의 전이(Transfer)를 통해 표현 내부에 이미 얼마나 많은 유용한 정보가 포함되어 있는지를 확인할 수 있습니다. 이후 다운스트림 작업 성능을 통해 특화 헤드가 현실적인 데이터 및 계산 제약 조건에서 이러한 지식을 얼마나 효과적으로 추출하고 적응시키는지를 측정해야 합니다.

따라서 월드 모델 사전학습과 작업 헤드(World Model Pretraining and Task Heads)는 일반적인 물리 지식(General Physical Knowledge)과 응용 특화 지능(Application-Specific Intelligence)을 서로 다른 수준에서 학습하는 확장 가능한 피지컬 AI(Physical AI) 아키텍처를 구축합니다. 대규모 사전학습은 재사용 가능한 예측 백본(Reusable Predictive Backbone)을 생성하고, 경량 또는 선택적으로 적응된 작업 헤드는 잠재 지식을 작업 관련 출력(Task-Relevant Output)으로 변환합니다. 이러한 분리는 물리 세계를 매번 처음부터 다시 학습하지 않고도 효율적인 전이(Transfer), 모듈형 확장(Modular Expansion), 멀티태스크 운용(Multi-Task Operation), 점진적 특화(Progressive Specialization)를 가능하게 합니다.

## 15.10. Path to General Physical World Models

![](images/image10.png){width="7.268055555555556in" height="7.268055555555556in"}

일반적인 물리 월드 모델(General Physical World Model)은 단순히 특정 작업에 특화된 예측 모델(Task-Specific Predictive Model)의 규모를 확대한다고 해서 만들어지는 것은 아닙니다. 이는 모델이 재사용 가능한 물리 지식(Reusable Physical Knowledge)을 작업(Task), 환경(Environment), 체화 형태(Embodiment)에 특화된 정보와 점진적으로 분리해 나가는 과정에서 형성됩니다. 이 장의 구조는 이러한 발전 과정을 따라 파운데이션 월드 모델(Foundation World Model) 사전학습에서 시작하여 다양한 로봇, 작업, 환경, 물리적 추론을 지원할 수 있는 공유 예측 시스템(Shared Predictive System)으로 발전하는 경로를 보여줍니다.

첫 번째 요구사항은 물리 세계(Physical World)에 대한 충분히 일반적인 내부 표현(Internal Representation)입니다. 모델은 단순한 시각적 외형(Visual Appearance)을 넘어 기하학(Geometry), 객체(Object), 공간적 관계(Spatial Relationship), 운동(Motion), 상호작용(Interaction), 시간적 상태(Temporal State), 행동유도성(Affordance), 불확실성(Uncertainty)을 표현해야 합니다. 초기의 월드 모델(World Model) 접근법은 BEV(BEV), 점유(Occupancy), 비디오(Video), 잠재 동역학(Latent Dynamics)과 같은 특정 표현에 집중할 수 있지만, 일반적인 모델은 이러한 관점을 서로 연결하여 기반이 되는 물리 상태(Underlying Physical State)에 대한 재사용 가능한 표현을 만들어야 합니다.

대규모 사전학습(Large-Scale Pretraining)은 이러한 일반화(Generalization)의 기반을 제공합니다. 하나의 로봇과 하나의 작업으로부터만 학습하는 대신, 모델은 다양한 관측(Observation), 궤적(Trajectory), 시연(Demonstration), 비디오, 시뮬레이션(Simulation), 멀티모달 센서 데이터(Multimodal Sensor Data)를 흡수할 수 있습니다. 카메라(Camera), 라이다(LiDAR), 레이더(Radar), IMU, 고유수용감각(Proprioception), 언어(Language), 행동(Action) 정보는 물리 현실(Physical Reality)의 서로 다른 측면을 모델에 노출시킵니다. 목표는 단순히 데이터셋의 크기를 증가시키는 것이 아니라 서로 다른 데이터 소스에서도 지속적으로 의미를 유지하는 규칙성(Regularity)을 학습된 표현에 포함시키는 것입니다.

이후 멀티태스크 및 다중 환경 사전학습(Multi-Task and Multi-Environment Pretraining)은 모델이 일반적인 물리 구조(General Physical Structure)와 지역적 상관관계(Local Correlation)를 구분하도록 합니다. 내비게이션(Navigation), 조작(Manipulation), 이동(Locomotion), 상호작용(Interaction), 충돌 회피(Collision Avoidance), 예측(Prediction)은 서로 다른 출력을 필요로 할 수 있지만 공간, 운동, 접촉(Contact), 지지(Support), 객체, 인과성(Causality)과 같은 개념을 공유합니다. 창고, 공장, 도로, 가정, 야외 지형 및 기타 다양한 환경에서 학습하면 모델은 무엇이 불변(Invariant)으로 유지되고 무엇이 변화하는 시각적·물리적 맥락에 따라 달라지는지를 식별할 수 있습니다.

다음 단계는 교차 체화 학습(Cross-Embodiment Learning)입니다. 일반적인 물리 월드 모델은 관측하거나 행동하는 기계가 항상 동일한 로봇이라고 가정해서는 안 됩니다. 바퀴형 로봇(Wheeled Robot), 매니퓰레이터(Manipulator), 4족 보행 로봇(Quadruped), 휴머노이드(Humanoid), 드론(Drone) 및 기타 플랫폼은 서로 다른 센서, 형태(Morphology), 운동학(Kinematics), 행동 공간(Action Space)을 통해 세계를 경험합니다. 따라서 모델은 공유 월드 상태(Shared World State)와 체화 특화 능력(Embodiment-Specific Capability)을 분리하여 공통 물리 지식이 각 로봇의 제약 조건에 맞게 해석될 수 있도록 해야 합니다.

공유 월드 표현(Shared World Representation)은 이러한 체화 형태 사이를 연결하는 가교 역할을 합니다. 서로 다른 로봇은 자신의 관측을 객체, 기하학, 점유(Occupancy), 의미(Semantics), 운동, 상호작용, 불확실성에 대한 호환 가능한 표현으로 변환할 수 있습니다. 이 표현은 센서 구성이나 관측 시점(Viewpoint)이 달라지더라도 유용성을 유지해야 합니다. 이후 로봇 특화 정보(Robot-Specific Information)를 통해 도달 가능성(Reachability), 주행 가능성(Traversability), 안정성(Stability), 파지 가능성(Graspability), 페이로드 실행 가능성(Payload Feasibility) 등의 행동유도성을 판단할 수 있으며, 각 플랫폼마다 기반 환경 표현을 다시 구축할 필요가 없습니다.

로봇 파운데이션 모델(Robot Foundation Model) 및 비전-언어-행동 모델(Vision-Language-Action Model)과의 통합은 월드 모델을 예측에서 범용 지능(General-Purpose Intelligence)으로 확장합니다. 파운데이션 모델은 의미 지식(Semantic Knowledge), 작업 이해(Task Understanding), 언어 기반화(Language Grounding), 전이 가능한 행동 능력(Transferable Behavioral Capability)을 제공하고, 월드 모델은 예측 가능한 물리 구조(Predictive Physical Structure)를 제공합니다. 이들의 결합을 통해 로봇은 목표를 해석하고, 현재 상황을 이해하며, 가능한 미래를 상상하고, 결과를 평가하고, 물리 환경에 기반화된 행동을 선택할 수 있습니다.

물리적 추론(Physical Reasoning)은 이러한 구성요소를 연결하는 핵심 능력이 됩니다. 일반적인 월드 모델은 공간적(Spatial), 시간적(Temporal), 상호작용(Interaction), 인과적(Causal), 반사실적(Counterfactual), 조합적(Compositional), 행동유도성(Affordance) 추론을 지원해야 합니다. 관측이 불완전할 때 숨겨진 상태(Hidden State)를 추론하고, 행동이 환경을 어떻게 변화시키는지를 예측하며, 실행 전에 여러 대안적 미래(Alternative Future)를 비교할 수 있어야 합니다. 또한 불확실성(Uncertainty)은 이러한 추론 과정의 일부로 유지되어야 하며, 이를 통해 시스템은 신뢰할 수 있는 예측과 추가 관측 또는 보수적인 행동이 필요한 상황을 구분할 수 있습니다.

사전학습과 작업 헤드(Pretraining and Task Heads)는 이러한 아키텍처를 확장하기 위한 실용적인 메커니즘을 제공합니다. 공유 백본(Shared Backbone)은 일반적인 물리 구조를 한 번 학습하고, 특화된 헤드(Specialized Head)는 점유, 깊이(Depth), 의미, 운동, 주행 가능성, 행동유도성, 위험(Risk), 보상(Reward), 계획, 제어를 위한 정보를 추출합니다. 일부 응용에서는 백본을 동결하고 경량 헤드(Lightweight Head)만 학습할 수 있으며, 다른 응용에서는 표현을 선택적으로 미세조정(Selective Fine-Tuning)하거나 적응(Adaptation)시킬 수 있습니다. 이러한 분리는 물리 세계를 매번 처음부터 다시 학습하지 않고도 새로운 능력을 추가할 수 있도록 합니다.

일반화로 가는 과정에서는 지속적인 적응(Continual Adaptation)과 전이(Transfer) 역시 필요합니다. 월드 모델은 새로운 환경, 객체, 로봇, 센서, 상호작용 패턴을 경험하면서 기존에 학습한 지식을 보존하는 동시에 지속적으로 개선되어야 합니다. 시뮬레이션은 광범위한 경험과 통제된 물리적 변화를 제공할 수 있으며, 실제 세계 데이터(Real-World Data)는 남아 있는 동역학 차이와 체화 특화 효과를 보정할 수 있습니다. 퓨샷 적응(Few-Shot Adaptation), 불확실성 인식 학습(Uncertainty-Aware Learning), 지속적인 모델 업데이트(Continuous Model Update)는 운용 조건이 변화하더라도 공유 표현을 계속 유용하게 유지하도록 합니다.

궁극적으로 일반적인 물리 월드 모델은 고립된 예측이 아니라 폐루프 과정(Closed-Loop Process)을 지원해야 합니다. 시스템은 환경을 지각하고, 내부 월드 상태(Internal World State)를 유지하며, 가능한 미래를 예측하고, 행동을 평가하고, 불확실성 아래에서 계획하고, 행동하며, 새로운 관측을 다음 예측 주기에 반영합니다. 이는 이 로드맵에서 발전해 온 표현(Representation), 예측(Prediction), 멀티모달 융합(Multimodal Fusion), 행동 조건화(Action Conditioning), 인과적 추론(Causal Reasoning), 물리 기반 모델링(Physics-Informed Modeling), 계획, Sim2Real 적응, 파운데이션 모델 전이를 하나의 연속적인 시스템으로 연결합니다.

최종적인 목표는 하나의 범용 로봇 정책(Universal Robot Policy)이 아니라 재사용 가능한 물리 지능 기반(Reusable Physical Intelligence Substrate)을 구축하는 것입니다. 이러한 모델은 작업, 환경, 체화 형태, 모달리티 전반에 걸쳐 공통의 예측 지식(Common Predictive Knowledge)을 제공하면서도 특화된 구성요소(Specialized Component)가 해당 지식을 특정 운용 요구사항에 맞게 적응할 수 있도록 합니다. 작업 특화 모델(Task-Specific Model)에서 일반적인 물리 월드 모델(General Physical World Model)로의 발전은 고립된 행동을 학습하는 단계에서 벗어나, 피지컬 AI(Physical AI) 시스템 전반에서 지각, 예측, 추론, 계획, 적응, 행동을 지속적으로 지원할 수 있는 물리 현실(Physical Reality)의 내부 모델(Internal Model)을 구축하는 단계로의 전환을 의미합니다.
