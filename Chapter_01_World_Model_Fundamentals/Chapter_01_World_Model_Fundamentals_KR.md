**Volume 07. World Models for Physical AI**

# Chapter 01. World Model Fundamentals

## 01.01. Definition of a World Model

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

월드 모델(World Model)은 지능형 에이전트(Intelligent Agent)가 환경(Environment)에 대해 알고 있는 정보를 체계화하고, 그 환경이 앞으로 어떻게 변화할지를 예상하기 위해 사용하는 내부 계산 표현(Internal Computational Representation)이다. 에이전트는 들어오는 각각의 센서 측정값에 독립적으로 반응하는 대신, 객체(Object), 기하 구조(Geometry), 움직임(Motion), 관계(Relationship), 그리고 미래 행동에 영향을 미칠 수 있는 조건을 포함하는 물리적 세계(Physical World)의 중요한 측면을 요약한 내부 상태(Internal State)를 유지한다.

피지컬 AI(Physical AI)에서 월드 모델(World Model)은 단순히 장면(Scene)을 정적으로 묘사하는 것 이상의 의미를 가진다. 월드 모델은 시간에 따라 변화하고 외부 사건(External Event)과 에이전트 자신의 행동(Action)에 의해 영향을 받는 세계를 표현한다. 따라서 로봇(Robot)은 현재 주변에 무엇이 존재하는지만 이해하는 것이 아니라, 객체가 어떻게 움직일 수 있는지, 물리적 상호작용(Physical Interaction)이 어떻게 전개될 수 있는지, 자신의 이동이나 조작이 환경 상태를 어떻게 변화시킬 수 있는지도 이해해야 한다.

관측(Observation)과 세계 상태(World State)는 개념적으로 구분할 필요가 있다. 카메라(Camera), 라이다(LiDAR), 레이더(Radar), 마이크(Microphone), 촉각 센서(Tactile Sensor), 관성 센서(Inertial Sensor), 고유수용성 측정(Proprioceptive Measurement)은 관측 정보를 제공하지만, 이러한 측정값은 불완전하고 종종 잡음(Noise)을 포함한다. 월드 모델은 이러한 관측을 구조화된 표현(Structured Representation) 또는 잠재 내부 표현(Latent Internal Representation)으로 변환하여 관측 가능한 감각 증거를 만들어낸 근본적인 상태를 포착하려 한다.

이러한 구분이 중요한 이유는 지능형 시스템(Intelligent System)이 완전한 물리적 환경을 직접 관측하는 경우가 거의 없기 때문이다. 객체는 가려질 수 있고, 센서는 일시적으로 고장 날 수 있으며, 속도(Velocity), 마찰(Friction), 의도(Intent), 미래 움직임(Future Motion)과 같은 중요한 속성은 즉시 측정되지 않을 수 있다. 월드 모델은 이전 관측, 축적된 기억(Memory), 물리적 제약조건(Physical Constraint), 그리고 환경에서 학습한 규칙성을 이용하여 이러한 숨겨진 정보(Hidden Information)를 추론할 수 있도록 한다.

가장 단순한 형태에서 월드 모델(World Model)은 현재 상태(Current State)를 추정하고 그 상태가 어떻게 변화하는지를 예측하는 메커니즘(Mechanism)으로 볼 수 있다. 현재 내부 상태를 (s_t), 행동을 (a_t), 다음 상태를 (s_{t+1})이라고 표현한다면, 모델은 이들 사이의 상태 전이 관계(State Transition Relationship)를 학습하거나 표현하려 한다. 피지컬 AI(Physical AI)에서 이러한 관계는 실제 세계에서 움직임을 실행하기 전에 그 움직임의 결과를 추론하는 기반을 제공한다.

내부 상태(Internal State)가 현실의 모든 물리적 세부 사항을 재현할 필요는 없다. 유용한 월드 모델(World Model)은 지각(Perception), 예측(Prediction), 의사결정(Decision Making), 계획(Planning), 제어(Control)에 필요한 정보를 보존하면서 불필요한 복잡성은 제거한다. 예를 들어 자율이동로봇(Autonomous Mobile Robot)은 주변 환경의 모든 시각적 질감이나 미세한 물리적 속성을 명시적으로 모델링하지 않더라도 자유 공간(Free Space), 장애물(Obstacle), 지형(Terrain), 이동 객체(Dynamic Object), 주행 가능성(Traversability), 충돌 가능성(Collision)을 정확하게 파악할 필요가 있다.

따라서 월드 모델(World Model)은 서로 다른 추상화 수준(Level of Abstraction)으로 존재할 수 있다. 일부 모델은 위치(Position), 속도(Velocity), 점유(Occupancy), 깊이(Depth), 객체 경계(Object Boundary), 3차원 구조(Three-Dimensional Structure)와 같은 명시적인 기하학적 정보를 표현한다. 다른 모델은 객체 범주(Object Category), 기능 영역(Functional Region), 인간 활동(Human Activity), 작업 관련 관계(Task-Relevant Relationship)와 같은 의미론적 개념(Semantic Concept)을 표현한다. 현대의 학습 시스템은 환경의 많은 정보를 개별 차원의 물리적 의미를 직접 해석하기 어려운 잠재 표현(Latent Representation)에 인코딩할 수도 있다.

월드 모델(World Model)은 공간적 정보(Spatial Information), 시간적 정보(Temporal Information), 의미론적 정보(Semantic Information), 물리적 정보(Physical Information)가 통합될 때 특히 강력해진다. 공간적 정보는 객체가 어디에 위치하고 어떻게 배치되어 있는지를 설명하며, 시간적 정보는 상태가 어떻게 변화하는지를 나타낸다. 의미론적 정보는 객체가 무엇이며 어떤 역할을 수행하는지를 설명하고, 물리적 정보는 움직임(Motion), 접촉(Contact), 질량(Mass), 기하 구조(Geometry), 마찰(Friction), 운동학적 실행 가능성(Kinematic Feasibility)과 같은 특성을 통해 가능한 상호작용을 제한한다.

따라서 예측(Prediction)은 실용적인 월드 모델(World Model)을 정의하는 핵심 능력 중 하나이다. 현재 상태와 최근 이력(History)이 주어지면 모델은 가능한 미래 상태(Future State)를 추정할 수 있다. 여기에 행동(Action)이 포함되면 서로 다른 후보 행동(Candidate Behavior)에 대응하는 여러 미래를 예측할 수 있다. 에이전트는 실제 물리적 행동을 실행하기 전에 왼쪽으로 이동하기, 감속하기, 객체 잡기, 보행자를 기다리기, 다른 경로 선택하기와 같은 여러 대안을 내부적으로 평가할 수 있다.

가능한 미래(Possible Future)를 생성하거나 추정하는 이러한 능력은 월드 모델링(World Modeling)과 계획(Planning)을 연결한다. 에이전트는 단순한 자극-반응 행동(Stimulus-Response Behavior)에 의존하는 대신 자신의 내부 모델을 후보 행동을 정신적으로 시뮬레이션하는 계산 환경(Computational Environment)으로 사용할 수 있다. 따라서 계획은 가능한 행동을 상상하고, 그 결과를 예측하고, 결과를 평가한 뒤, 현재 목표(Objective)와 제약조건(Constraint)을 가장 잘 만족하는 행동을 선택하는 과정으로 이해할 수 있다.

월드 모델(World Model)은 현실을 완전하게 재현하는 시뮬레이터(Simulator)와 동일하지 않다. 시뮬레이터는 사전에 정의되거나 학습된 규칙에 따라 환경의 행동을 재현하려는 반면, 월드 모델은 주로 유용한 추론(Inference)과 행동(Action)을 위해 최적화된 에이전트 중심 표현(Agent-Centered Representation)이다. 피지컬 AI 시스템(Physical AI System)의 요구사항에 따라 명시적 물리학(Explicit Physics), 학습된 동역학(Learned Dynamics), 확률적 예측(Probabilistic Prediction), 신경망 잠재 상태(Neural Latent State), 기호적 구조(Symbolic Structure), 또는 이들의 조합을 포함할 수 있다.

마찬가지로 월드 모델(World Model)은 지도(Map)와 동일하지 않다. 지도는 주로 공간 구조(Spatial Structure)를 설명하지만, 월드 모델은 추가적으로 동적 객체(Dynamic Object), 시간적 변화(Temporal Evolution), 숨겨진 상태(Hidden State), 불확실성(Uncertainty), 행동의 결과(Action Consequence), 의미론적 관계(Semantic Relationship), 물리적 상호작용(Physical Interaction)을 표현할 수 있다. 지도는 월드 모델의 한 구성 요소가 될 수 있지만, 변화하는 환경에서 작동하는 자율 에이전트(Autonomous Agent)는 물리적 세계의 변화에 따라 지속적으로 갱신될 수 있는 내부 표현을 필요로 한다.

기억(Memory) 역시 월드 모델링(World Modeling)과 밀접하게 연결된다. 현재의 관측만으로 실제 환경 상태를 결정하기에는 정보가 부족한 경우가 많기 때문이다. 몇 초 또는 몇 분 전에 수집한 정보도 더 이상 보이지 않더라도 여전히 중요할 수 있다. 월드 모델은 시간에 따른 관측을 통합함으로써 객체 영속성(Object Permanence)을 유지하고, 궤적(Trajectory)을 추정하며, 공간적 맥락(Spatial Context)을 보존하고, 변화를 추론하며, 일시적인 센서 관측 소실과 실제 환경 변화를 구별할 수 있다.

불확실성(Uncertainty)은 현실적인 월드 모델(World Model)의 또 다른 기본 특성이다. 자율 에이전트의 관점에서 물리적 미래는 거의 항상 완전히 결정적이지 않다. 보행자는 여러 방향 중 하나를 선택할 수 있고, 지형의 특성이 불확실할 수 있으며, 센서 측정값에는 잡음이 포함될 수 있다. 고급 월드 모델은 하나의 미래만 표현하는 대신 확률 분포(Probability Distribution) 또는 여러 개의 가능한 미래(Multiple Plausible Futures)를 표현함으로써 계획 시스템이 예상 결과뿐만 아니라 관련된 위험(Risk)까지 고려하도록 할 수 있다.

월드 모델(World Model)의 학습은 지도학습(Supervised Learning), 약지도학습(Weakly Supervised Learning), 자기지도학습(Self-Supervised Learning), 강화학습 기반 접근법(Reinforcement-Based Approach), 또는 이들을 결합한 하이브리드 접근법(Hybrid Approach)을 통해 이루어질 수 있다. 특히 대규모 비라벨 시계열 감각 데이터(Unlabeled Sensory Sequence)는 유용하다. 이전 관측을 이용하여 이후 상태를 예측할 수 있기 때문에 시간 데이터 자체가 자연스러운 학습 신호(Learning Signal)를 제공한다. 반복적인 물리적 상호작용을 통해 모델은 움직임, 지속성(Persistence), 기하 구조, 인과성(Causality), 행동에 따른 환경 변화의 규칙성을 점진적으로 학습할 수 있다.

로보틱스(Robotics)에서는 에이전트 자신의 신체(Body)도 모델링된 세계 안에 표현되어야 한다. 관절 위치(Joint Position), 속도(Velocity), 액추에이터 상태(Actuator State), 바퀴 움직임(Wheel Motion), 접촉 상태(Contact Condition), 배터리 또는 자원 제약(Resource Constraint), 그리고 기타 고유수용성 정보(Proprioceptive Information)는 외부 환경 상태와 상호작용한다. 따라서 의미 있는 예측을 위해서는 체화된 에이전트(Embodied Agent)와 주변 환경이 함께 어떻게 변화하는지를 이해해야 하며, 로봇 모델링과 환경 모델링 사이의 경계는 의도적으로 유연할 필요가 있다.

필요한 세계 표현(World Representation)은 체화(Embodiment)와 작업(Task)에 따라 크게 달라진다. 자율주행차(Autonomous Vehicle)는 도로, 차선, 교통 참여자(Traffic Participant), 점유(Occupancy), 움직임, 충돌 위험을 중요하게 다룬다. 매니퓰레이터(Manipulator)는 객체 자세(Object Pose), 접촉, 파지 가능성(Graspability), 기하 구조, 힘의 상호작용(Force Interaction)을 중요하게 다룬다. 4족 보행 로봇(Quadruped Robot)은 지형 형상(Terrain Geometry), 발판 안정성(Foothold Stability), 몸체 동역학(Body Dynamics), 주행 가능성(Traversability)을 중요하게 다룰 수 있다. 범용 피지컬 AI(General Physical AI)는 궁극적으로 다양한 체화 형태와 환경을 지원할 수 있는 유연한 표현을 필요로 한다.

월드 모델(World Model)은 지각(Perception)과 지능(Intelligence)을 연결하는 역할도 한다. 지각은 원시 감각 신호(Raw Sensory Signal)를 유용한 정보로 변환하지만, 월드 모델링은 그 정보를 지속적인 내부 구조(Persistent Internal Structure)로 조직한다. 추론(Reasoning)은 이 구조를 기반으로 수행되고, 예측(Prediction)은 이를 가능한 미래로 확장하며, 계획(Planning)은 그러한 미래 가운데 적절한 것을 탐색하고, 제어(Control)는 선택된 계획을 실제 물리적 행동으로 변환한다. 따라서 월드 모델은 지각--예측--계획--행동(Perception--Prediction--Planning--Action) 순환 구조의 중심에 위치한다.

이러한 관점에서 월드 모델(World Model)의 품질은 단순히 복원 정확도(Reconstruction Accuracy)나 시각적 사실성(Visual Realism)만으로 평가해서는 안 된다. 모델이 인상적인 이미지를 생성하더라도 안전한 행동에 필요한 정보를 보존하지 못한다면 좋은 월드 모델이라고 보기 어렵다. 반대로 압축된 잠재 표현(Compact Latent Representation)은 직접 해석하기 어려울 수 있지만 충돌, 주행 가능성, 객체 움직임, 행동 결과를 매우 정확하게 예측할 수 있다. 피지컬 AI에서는 외형적 사실성보다 예측, 계획, 제어에 얼마나 유용한지가 궁극적으로 더 중요하다.

충분한 능력을 갖춘 월드 모델(World Model)은 체화된 에이전트(Embodied Agent)와 물리적 현실(Physical Reality) 사이에서 내부 예측 인터페이스(Internal Predictive Interface)로 기능한다. 월드 모델은 경험을 상태(State)로 압축하고, 즉각적인 관측 범위를 넘어 정보를 유지하며, 상황이 어떻게 변화할 수 있는지를 예측하고, 행동이 그러한 상황을 어떻게 변화시킬지를 추정한다. 이러한 의미에서 월드 모델링은 피지컬 AI를 단순한 반응형 센서 처리(Reactive Sensor Processing)에서 벗어나 무엇이 존재하는지, 다음에 무엇이 일어날 수 있는지, 그리고 이에 대해 에이전트가 무엇을 해야 하는지를 추론할 수 있는 예측적 지능(Anticipatory Intelligence)으로 발전시키는 핵심 기반이다.

## 01.02. Agent Environment and Internal Model

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

지능형 물리 시스템(Intelligent Physical System)은 서로 밀접하게 연결된 세 가지 요소, 즉 에이전트(Agent), 환경(Environment), 그리고 에이전트가 유지하는 내부 모델(Internal Model)을 통해 이해할 수 있다. 에이전트는 환경을 지각하고 행동하는 주체이며, 환경은 이러한 행동이 실제 결과를 만들어내는 외부 세계이다. 내부 모델은 에이전트가 관측을 해석하고, 지식을 유지하며, 환경의 변화를 예상할 수 있도록 하는 계산 구조(Computational Structure)이다.

피지컬 AI(Physical AI)에서 에이전트(Agent)는 세계와 분리되어 존재하는 추상적인 의사결정 과정(Decision-Making Process)이 아니다. 에이전트는 센서(Sensor), 액추에이터(Actuator), 물리적 크기, 이동 능력, 계산 자원(Computational Resource), 기계적 능력(Mechanical Capability)에 의해 무엇을 관측하고 어떤 행동을 수행할 수 있는지가 결정되는 체화된 시스템(Embodied System)이다. 따라서 이동 로봇(Mobile Robot), 매니퓰레이터(Manipulator), 자율주행차(Autonomous Vehicle), 4족 보행 로봇(Quadruped), 휴머노이드(Humanoid), 비행 로봇(Aerial Robot)은 각각의 체화 형태가 서로 다른 감지와 행동 가능성을 제공하기 때문에 동일한 환경도 서로 다르게 경험한다.

환경(Environment)은 에이전트 외부에 존재하면서 에이전트의 관측, 의사결정 또는 행동에 영향을 줄 수 있는 모든 것을 포함한다. 여기에는 벽, 도로, 선반, 건물, 지형과 같은 정적 구조(Static Structure)뿐만 아니라 사람, 차량, 동물, 기계, 다른 로봇과 같은 동적 개체(Dynamic Entity)도 포함된다. 조명, 날씨, 표면 특성, 가시성, 마찰, 통신 가용성과 같은 환경 조건(Environmental Condition) 역시 에이전트가 물리적 세계를 얼마나 안정적으로 지각하고 상호작용할 수 있는지에 영향을 미칠 수 있다.

에이전트(Agent)와 환경(Environment)의 상호작용은 연속적인 폐루프(Closed Loop)를 형성한다. 환경은 센서에 의해 측정되어 관측(Observation)으로 변환되는 물리적 신호를 생성한다. 에이전트는 이러한 관측을 처리하고 내부 표현(Internal Representation)을 갱신하며, 행동(Action)을 선택하고 액추에이터에 명령을 전달한다. 그 결과 발생한 물리적 행동은 환경이나 그 안에 존재하는 에이전트의 상태 또는 양쪽 모두를 변화시키며, 새로운 관측을 생성하여 다음 순환 과정을 시작한다.

에이전트(Agent)는 일반적으로 환경의 실제 상태(True Environmental State)에 직접 접근할 수 없다. 대신 카메라(Camera), 라이다(LiDAR), 레이더(Radar), 관성 센서(Inertial Sensor), 마이크(Microphone), 촉각 장치(Tactile Device), 엔코더(Encoder), 힘 센서(Force Sensor) 및 기타 감지 시스템을 통해 부분적인 관측(Partial Observation)을 얻는다. 모든 센서는 범위, 해상도, 잡음, 가림(Occlusion), 지연시간(Latency), 작동 조건과 관련된 한계를 가진다. 따라서 에이전트는 현재의 측정값이 세계를 완전하게 설명한다고 가정하는 대신 현실에 대한 추정치(Estimate)를 구성해야 한다.

내부 모델(Internal Model)은 이러한 현실에 대한 추정된 설명을 제공한다. 내부 모델은 현재 이용 가능한 관측을 이전 상태(Previous State), 축적된 경험(Accumulated Experience), 학습된 표현(Learned Representation), 그리고 세계가 어떻게 변화하는지에 관한 가정과 통합한다. 즉각적인 센서 시야에서 사라진 정보가 반드시 내부 모델에서도 사라지는 것은 아니다. 예를 들어 차량 뒤에 일시적으로 가려진 보행자는 시각적 측정이 잠시 사라졌더라도 계속 존재할 가능성이 있다는 근거에 따라 내부 모델에 유지될 수 있다.

이러한 능력은 관측(Observation)과 세계에 대한 믿음(Belief) 사이에 근본적인 구분을 만든다. 관측은 센서가 현재 측정하고 있는 것을 나타내는 반면, 내부 상태(Internal State)는 에이전트가 현재 환경에서 중요하다고 판단하고 있는 내용을 표현한다. 내부 상태에는 직접 관측된 값뿐만 아니라 추론된 숨겨진 변수(Hidden Variable), 기억된 정보, 예측된 움직임, 의미론적 속성(Semantic Property), 불확실성 추정(Uncertainty Estimate), 그리고 하나의 센서 측정만으로는 얻을 수 없는 개체 간 관계가 포함될 수 있다.

내부 모델(Internal Model)은 에이전트 자신도 표현해야 한다. 물리적 상호작용(Physical Interaction)은 환경의 상태와 체화된 시스템(Embodied System)의 상태 사이 관계에 따라 결정되기 때문이다. 로봇의 위치, 방향, 속도, 관절 구성(Joint Configuration), 액추에이터 상태, 접촉 상태(Contact State), 사용 가능한 에너지, 페이로드(Payload), 기계적 한계(Mechanical Limit)는 어떤 행동이 실행 가능한지를 결정할 수 있다. 따라서 효과적인 월드 모델링(World Modeling)은 주변 세계에 관한 외수용성 정보(Exteroceptive Information)와 에이전트 자신의 물리적 상태를 설명하는 고유수용성 정보(Proprioceptive Information)를 결합한다.

에이전트(Agent)와 환경(Environment)의 경계는 개념적으로 유용하지만 실제 작동에서는 동적으로 변화할 수 있다. 로봇이 객체를 운반하거나, 장비를 견인하거나, 도구를 조작하면 에이전트의 실질적인 물리적 특성이 달라진다. 파지된 객체는 처음에는 환경의 일부였지만 일시적으로 제어 시스템(Controlled System)의 일부가 될 수 있다. 따라서 고급 피지컬 AI(Physical AI)는 개별 객체만 모델링하는 것이 아니라 신체, 도구, 페이로드, 주변 구조물, 다른 에이전트 사이에서 변화하는 관계까지 모델링해야 한다.

행동(Action)은 에이전트(Agent)와 내부 모델(Internal Model)을 연결하는 또 다른 핵심 요소이다. 모델은 환경이 현재 어떻게 보이는지만 설명하는 것이 아니라 서로 다른 행동이 환경을 어떻게 변화시킬 수 있는지도 추정해야 한다. 전진하면 장애물에 대한 로봇의 상대적 위치가 달라지고, 회전하면 센서의 시점(Viewpoint)이 변하며, 힘을 가하면 객체가 움직일 수 있다. 가속하면 미래의 정지 거리(Stopping Distance)가 달라진다. 따라서 내부 모델의 상태 전이(State Transition)가 후보 행동(Candidate Action)을 조건으로 할 때 제어(Control)에 유용해진다.

이러한 행동 조건부 관점(Action-Conditioned Perspective)은 반사실적 추론(Counterfactual Reasoning)을 가능하게 한다. 명령을 실제로 실행하기 전에 에이전트는 오른쪽 대신 왼쪽으로 회전하면 어떻게 되는지, 제동하는 대신 가속하면 어떻게 되는지, 다른 방향에서 객체를 파지하면 어떻게 되는지와 같은 가상적인 질문을 평가할 수 있다. 내부 모델은 모든 가능성을 물리적으로 직접 실행하지 않고도 대안 행동과 그 결과를 비교할 수 있는 계산 공간(Computational Space)을 제공하여 위험을 줄이고 계획 효율성을 향상시킨다.

시간(Time) 역시 중요하다. 에이전트--환경 상호작용(Agent--Environment Interaction)은 본질적으로 순차적(Sequential)이기 때문이다. 현재 관측의 의미는 이전의 관측과 행동에 따라 달라지는 경우가 많다. 하나의 이미지는 객체가 어디에 있는지를 보여줄 수 있지만, 연속된 이미지 시퀀스(Image Sequence)는 객체의 속도와 이동 방향을 보여줄 수 있다. 내부 모델은 시간 정보를 유지함으로써 움직임을 추정하고, 지속적으로 존재하는 개체를 인식하며, 변화를 감지하고, 이동 객체의 움직임과 자기 운동(Ego-Motion)을 구별하며, 미래 시간 구간에서 환경이 어떻게 변화할지를 예측할 수 있다.

내부 모델(Internal Model)은 명시적(Explicit), 잠재적(Latent), 또는 하이브리드(Hybrid) 형태일 수 있다. 명시적 표현(Explicit Representation)에는 지도(Map), 점유 격자(Occupancy Grid), 객체 목록(Object List), 자세(Pose), 속도, 의미론적 라벨(Semantic Label), 기하 구조(Geometric Structure)와 같이 의미를 직접 해석할 수 있는 정보가 포함될 수 있다. 잠재 모델(Latent Model)은 예측이나 제어에 최적화된 학습 특징 공간(Learned Feature Space)에 중요한 정보를 인코딩한다. 하이브리드 시스템(Hybrid System)은 해석 가능한 물리적 값과 학습된 잠재 표현을 결합하여 공학적으로 설계된 구조와 데이터 기반 학습(Data-Driven Learning)이 동일한 예측 과정에 기여하도록 할 수 있다.

어떠한 내부 모델(Internal Model)도 완벽한 정확도로 전체 물리적 세계를 표현할 수는 없다. 따라서 에이전트는 불확실성(Uncertainty)을 표현하고 자신의 믿음(Belief)을 지속적으로 수정할 수 있는 메커니즘을 필요로 한다. 새로운 관측은 이전 예측을 확인할 수도 있고 잘못되었음을 보여줄 수도 있다. 따라서 내부 상태는 지속적인 예측(Prediction)과 수정(Correction) 과정을 통해 갱신되어야 하며, 이를 통해 객체가 예상과 다르게 움직이거나 환경 조건이 변하거나 기존 가정이 더 이상 유효하지 않을 때 모델이 적응할 수 있다.

에이전트(Agent), 환경(Environment), 내부 모델(Internal Model) 사이의 관계는 어떤 정보를 유지해야 하는지도 결정한다. 내비게이션(Navigation)을 위한 월드 모델은 자유 공간(Free Space), 장애물, 지형, 이동 에이전트, 주행 가능성(Traversability)을 중요하게 다룰 수 있는 반면, 조작(Manipulation)을 위한 모델은 객체 자세(Object Pose), 기하 구조, 접촉, 파지 가능성(Graspability), 힘(Force)을 중요하게 다룰 수 있다. 따라서 내부 표현은 에이전트의 체화 형태, 목표, 행동, 필요한 예측 시간 범위(Prediction Horizon)에 대한 유용성을 기준으로 정보를 보존해야 한다.

따라서 동일한 물리적 환경에서 작동하는 서로 다른 에이전트는 서로 다른 내부 모델(Internal Model)을 구성할 수 있다. 자율주행차(Autonomous Vehicle)는 차선, 교통 참여자, 도로 경계, 예측 궤적(Predicted Trajectory)을 표현할 수 있는 반면, 배송 로봇(Delivery Robot)은 보도, 경사로, 문, 보행자, 주행 가능한 표면을 중요하게 다룰 수 있다. 동일한 장면을 관측하는 매니퓰레이터(Manipulator)는 접근 가능한 객체, 파지 구성(Grasp Configuration), 충돌 기하 구조(Collision Geometry), 접촉 관계에 집중할 수 있다. 따라서 세계 표현(World Representation)은 본질적으로 행동 능력(Action Capability)과 연결된다.

다중 에이전트 환경(Multi-Agent Environment)에서는 내부 모델(Internal Model)이 제어 대상 에이전트와 독립적으로 행동하는 다른 개체를 추가적으로 구별해야 한다. 다른 로봇, 차량 또는 사람은 각각 자신의 상태, 목표, 가능한 행동을 가지므로 미래 상태를 제어 대상 에이전트의 명령만으로 결정할 수 없다. 따라서 월드 모델(World Model)은 자기 행동으로 발생하는 상태 전이(Self-Induced State Transition)의 예측과 외부에서 발생하는 변화 및 여러 에이전트 사이의 상호작용에 대한 예측을 결합해야 한다.

학습(Learning)은 반복적인 에이전트--환경 상호작용(Agent--Environment Interaction)을 통해 내부 모델(Internal Model)을 개선함으로써 이러한 관계를 강화한다. 센서 시퀀스(Sensor Sequence)는 장면이 어떻게 변화하는지를 보여주며, 행동 시퀀스(Action Sequence)는 에이전트가 그러한 변화에 어떻게 영향을 미치는지를 보여준다. 예측 오차(Prediction Error)는 표현과 동역학(Dynamics)을 갱신하는 학습 신호를 제공한다. 시간이 지나면서 축적된 상호작용 데이터는 움직임, 객체 지속성(Object Persistence), 물리적 제약, 행동 결과, 반복되는 환경 행동 패턴의 규칙성을 모델이 학습하도록 할 수 있다.

내부 모델(Internal Model)은 궁극적으로 감지(Sensing)와 행동(Action)을 연결하는 정보적 가교(Information Bridge) 역할을 한다. 환경에서 들어온 원시 관측(Raw Observation)은 추정된 내부 상태(Estimated Internal State)로 변환되고, 기억(Memory) 및 학습된 동역학(Learned Dynamics)과 결합된다. 이후 후보 행동에 따른 가능한 미래 상태(Possible Future State)를 예측할 수 있으며, 계획 및 의사결정 시스템은 이를 이용해 여러 대안을 평가한다. 선택된 행동은 물리적 신체를 통해 다시 환경에 전달되면서 지각--모델--예측--행동(Perception--Model--Prediction--Action) 순환 구조를 완성한다.

물리적 지능(Physical Intelligence)은 지각, 모델링 또는 제어 가운데 어느 하나가 독립적으로 뛰어나다고 해서 형성되는 것이 아니라 이들 사이의 지속적인 관계가 얼마나 효과적으로 작동하는지에 따라 나타난다. 에이전트는 환경을 반복적으로 관측하고, 내부 모델(Internal Model)을 갱신하며, 미래 변화를 예상하고, 자신의 체화된 신체(Embodied Body)를 통해 행동하며, 그 결과로부터 학습해야 한다. 따라서 강력한 월드 모델(World Model)은 물리적 현실(Physical Reality)에 대한 에이전트의 지속적으로 진화하는 내부 인터페이스(Internal Interface)로 기능하며, 센서가 현재 감지하는 정보뿐만 아니라 에이전트가 무엇을 믿고, 기억하고, 예측하며, 물리적으로 변화시킬 수 있는지를 기반으로 행동하도록 한다.

## 01.03. State Observation Action and Transition

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

월드 모델(World Model)은 상태(State), 관측(Observation), 행동(Action), 전이(Transition)라는 네 가지 기본 개념을 통해 설명할 수 있다. 이들은 지능형 에이전트(Intelligent Agent)가 물리적 환경(Physical Environment)을 어떻게 표현하고 시간에 따른 변화를 어떻게 추론하는지를 설명하는 간결한 언어를 제공한다. 상태는 세계의 조건을, 관측은 에이전트가 감지할 수 있는 것을, 행동은 에이전트가 수행할 수 있는 것을, 전이는 하나의 상태가 다른 상태로 어떻게 변화하는지를 설명한다.

일반적으로 (s_t)로 표현되는 상태(State)는 시간 (t)에서 세계와 에이전트에 관한 중요한 정보를 나타낸다. 작업(Task)에 따라 상태에는 위치(Position), 방향(Orientation), 속도(Velocity), 객체 정체성(Object Identity), 점유(Occupancy), 지형 특성(Terrain Property), 로봇 관절 구성(Robot Joint Configuration), 접촉 상태(Contact Condition) 또는 기타 변수가 포함될 수 있다. 유용한 상태가 현실 전체를 완벽하게 재현할 필요는 없으며, 예측(Prediction), 계획(Planning), 제어(Control)에 필요한 정보를 보존하면 된다.

이동 로봇(Mobile Robot)의 경우 상태에는 로봇의 자세(Pose)와 속도뿐만 아니라 주변 장애물, 주행 가능한 영역(Traversable Region), 이동 객체(Moving Object), 그리고 이들의 추정 움직임(Estimated Motion)이 포함될 수 있다. 반면 매니퓰레이터(Manipulator)의 경우에는 관절 상태(Joint State), 말단장치 자세(End-Effector Pose), 객체 기하 구조(Object Geometry), 접촉(Contact), 파지 관계(Grasp Relationship)가 더욱 중요할 수 있다. 따라서 상태 표현(State Representation)은 서로 다른 물리적 에이전트가 자신의 행동 결과를 예측하기 위해 서로 다른 정보를 필요로 하기 때문에 작업과 체화 형태(Embodiment)에 따라 달라진다.

실제 물리적 상태(True Physical State)는 일반적으로 에이전트가 직접 이용할 수 없다. 대신 센서는 흔히 (o_t)로 표현되는 관측(Observation)을 생성한다. 관측에는 카메라 이미지(Camera Image), 라이다 포인트 클라우드(LiDAR Point Cloud), 레이더 반사 신호(Radar Return), 관성측정장치 측정값(IMU Measurement), 촉각 신호(Tactile Signal), 관절 엔코더(Joint Encoder), 힘 측정(Force Measurement), 또는 여러 모달리티(Modality)의 조합이 포함될 수 있다. 관측은 세계 자체가 아니라 세계에 관한 증거(Evidence)이므로 이 두 개념을 혼동하면 취약한 모델이 만들어질 수 있다.

관측(Observation)은 센서 범위(Sensor Range), 시야각(Field of View), 해상도(Resolution), 잡음(Noise), 지연시간(Latency), 가림(Occlusion), 환경 조건(Environmental Condition)에 의해 제한된다. 카메라는 벽 뒤에 가려진 객체를 직접 관측할 수 없으며, 라이다 측정값은 특정 표면이나 기상 조건에서 희소하거나 성능이 저하될 수 있다. 따라서 에이전트는 현재 관측을 이전 관측, 행동, 기억(Memory), 학습된 환경 규칙성(Learned Environmental Regularity)과 결합하여 불완전한 측정값으로부터 유용한 내부 상태(Internal State)를 추론해야 한다.

이러한 관계는 상태 (s_t)와 관측 (o_t)를 연결하는 관측 모델(Observation Model)을 통해 개념적으로 표현할 수 있다. 물리적 상태는 측정 가능한 감각적 결과(Sensory Consequence)를 발생시키며, 지각 시스템(Perception System)은 이러한 결과로부터 해당 상태에 관한 정보를 추론한다. 학습 기반 월드 모델(Learned World Model)에서는 인코더(Encoder)가 고차원 관측(High-Dimensional Observation)을 압축된 잠재 상태(Latent State) (z_t)로 변환하여 원시 센서 공간(Raw Sensor Space)이 아닌 표현 공간(Representation Space)에서 예측이 수행되도록 할 수 있다.

일반적으로 (a_t)로 표현되는 행동(Action)은 에이전트가 수행하는 개입(Intervention)을 의미한다. 행동에는 바퀴 속도 명령(Wheel Velocity Command), 조향각(Steering Angle), 가속(Acceleration), 제동(Braking), 관절 토크(Joint Torque), 목표 위치(Target Position), 그리퍼 명령(Gripper Command), 추력(Thrust), 또는 웨이포인트(Waypoint)를 향해 이동하는 것과 같은 상위 수준 명령(High-Level Command)이 포함될 수 있다. 행동 공간(Action Space)의 형태는 체화 구조, 액추에이터 아키텍처(Actuator Architecture), 제어 계층(Control Hierarchy), 월드 모델이 작동하는 시간 해상도(Temporal Resolution)에 따라 달라진다.

행동(Action)은 미래 상태(Future State)에 인과적으로 영향을 미칠 수 있다는 점에서 관측(Observation)과 근본적으로 다르다. 센서 측정은 환경에 관한 정보를 제공하지만, 액추에이터 명령(Actuator Command)은 환경을 변화시키려 한다. 로봇이 가속하거나 회전하고, 객체를 밀거나, 그리퍼를 닫거나, 지형에 발을 디디면 행동에 의해 이후의 물리적 조건이 변화한다. 이러한 인과적 연결(Causal Connection)을 모델링하는 것은 계획과 제어를 지원하는 월드 모델의 핵심 요소이다.

전이(Transition)는 세계가 상태 (s_t)에서 상태 (s_{t+1})로 어떻게 변화하는지를 설명한다. 행동 조건부 모델(Action-Conditioned Model)에서 이 관계는 개념적으로 (s_{t+1}=f(s_t,a_t))로 표현할 수 있으며, 여기서 전이 함수(Transition Function) (f)는 중요한 동역학(Dynamics)을 포착한다. 보다 현실적인 시스템에서는 불확실성, 외란(Disturbance), 숨겨진 변수(Hidden Variable), 다른 에이전트의 행동 때문에 동일한 현재 상태와 행동에서도 서로 다른 미래 결과가 발생할 수 있으므로 이를 확률적으로 표현할 수 있다.

전이 모델(Transition Model)은 제어 대상 에이전트가 발생시키는 변화뿐만 아니라 환경에서 독립적으로 발생하는 변화도 포착해야 한다. 차량은 조향과 가속 명령에 의해 움직이지만 보행자와 다른 차량 역시 자신의 행동에 따라 이동한다. 바람은 비행 로봇(Aerial Robot)에 영향을 미칠 수 있고, 지형은 바퀴 미끄러짐(Wheel Slip)에 영향을 줄 수 있으며, 객체는 중력(Gravity)에 의해 떨어질 수 있다. 따라서 세계 동역학(World Dynamics)은 제어 가능한 과정, 외부 과정, 부분적으로 예측할 수 없는 과정을 함께 포함한다.

상태 전이(State Transition)는 물리적 세계에서는 연속적으로 발생하지만 계산 모델(Computational Model)은 일반적으로 이를 이산적인 시간 단계(Time Step)로 나누어 처리한다. 각 단계에서 에이전트는 추정 상태(Estimated State)를 유지하고, 행동을 실행하거나 고려하며, 그 결과로 나타날 다음 상태를 예측한다. 이 연산을 반복하면 (s_t, s_{t+1}, s_{t+2}, \\ldots)와 같은 롤아웃(Rollout)이 생성되며, 이를 통해 월드 모델은 즉각적인 미래를 넘어 예측 시간 범위(Prediction Horizon)에 걸친 가능한 궤적(Trajectory)을 검토할 수 있다.

다단계 예측(Multi-Step Prediction)은 작은 전이 오차(Transition Error)가 누적될 수 있다는 중요한 문제를 발생시킨다. 약간 부정확한 속도 추정은 한 단계 앞에서는 작은 오차만 만들지만 여러 단계를 예측한 이후에는 큰 위치 오차로 확대될 수 있다. 따라서 장기 예측 월드 모델링(Long-Horizon World Modeling)에는 시간적 일관성(Temporal Consistency), 강건한 상태 표현(Robust State Representation), 불확실성 추정(Uncertainty Estimation), 기억, 그리고 예측된 미래가 관측된 현실에서 멀어질수록 오차가 통제 불가능하게 증가하는 것을 방지하는 메커니즘이 필요하다.

상태--행동--전이(State--Action--Transition) 관계는 반사실적 예측(Counterfactual Prediction)을 가능하게 한다. 동일한 추정 상태에서 에이전트는 여러 후보 행동(Candidate Action)을 평가하고 서로 다른 예측 미래(Predicted Future)를 얻을 수 있다. 이동 로봇은 직진을 계속하거나 감속하거나 방향을 변경하는 경우를 비교할 수 있고, 매니퓰레이터는 서로 다른 파지 궤적(Grasp Trajectory)을 비교할 수 있다. 이를 통해 월드 모델은 행동을 실제로 실행하기 전에 계산적으로 시험할 수 있는 내부 예측 환경(Internal Predictive Environment)이 된다.

관측(Observation)은 다시 예측(Prediction)과 현실(Reality) 사이의 순환 구조를 완성한다. 행동을 실행한 이후 새로운 센서 측정은 실제 결과 상태에 관한 증거를 제공한다. 예측된 상태(Predicted State)는 새롭게 추론된 상태와 비교될 수 있으며, 그 차이는 예측 오차(Prediction Error)가 된다. 이 오차를 이용해 현재 내부 추정값을 수정할 수 있으며, 학습 과정에서는 표현 또는 전이 모델을 개선하여 이후의 예측 정확도를 높일 수 있다.

따라서 전체 과정은 단방향 파이프라인(One-Way Pipeline)이 아니라 반복되는 순환 과정(Recurring Cycle)으로 이해할 수 있다. 에이전트는 환경을 관측하고 현재 상태를 추정하며, 행동을 선택하고, 상태 전이를 예측하며, 행동을 실행하고, 새로운 관측을 받은 후 내부 상태를 갱신한다. 이러한 순환 과정은 지각(Perception), 월드 모델링(World Modeling), 예측, 의사결정(Decision Making), 제어를 지속적으로 연결하면서 변화하는 물리적 현실과 에이전트의 내부 표현을 동기화한다.

부분 관측 환경(Partially Observable Environment)에서는 추정 상태(Estimated State)가 현재 관측 이상의 정보를 포함해야 한다. 장애물 뒤로 일시적으로 사라진 사람도 계속 표현해야 할 수 있으며, 로봇은 센서 시야에서 벗어난 지형이나 객체를 기억해야 할 수 있다. 따라서 과거 관측(Historical Observation)과 이전 행동(Previous Action)을 믿음 상태(Belief State) 또는 잠재 기억(Latent Memory)에 통합하여 미래 예측에 필요한 정보를 요약할 수 있다.

상태(State)는 하나의 확정적인 추정값 대신 불확실성(Uncertainty)을 포함할 수도 있다. 로봇은 자신의 정확한 위치, 객체의 속도, 표면 마찰(Surface Friction), 다른 에이전트의 의도(Intent), 또는 가려진 영역에 장애물이 존재하는지 여부를 확신하지 못할 수 있다. 확률적 상태 표현(Probabilistic State Representation)을 사용하면 전이 모델이 이러한 불확실성을 미래로 전파하여 하나의 결정론적 궤적(Deterministic Trajectory)이 반드시 발생한다고 가정하는 대신 여러 개의 가능한 미래 상태(Plausible Future State)를 생성할 수 있다.

피지컬 AI(Physical AI)에서 상태 표현(State Representation)은 외부 환경 조건과 에이전트 자신의 신체 사이의 관계도 포함해야 한다. 로봇 속도, 관절 구성, 페이로드(Payload), 접촉, 에너지 상태(Energy State), 액추에이터 한계(Actuator Limit), 기타 고유수용성 변수(Proprioceptive Variable)는 가능한 상태 전이에 영향을 미친다. 동일한 명령이라도 지형, 페이로드, 배터리 상태, 기계적 구성, 접촉 상태에 따라 서로 다른 결과를 만들어낼 수 있으므로 신뢰할 수 있는 물리적 예측을 위해서는 체화 상태 정보(Embodied State Information)가 필수적이다.

따라서 네 가지 개념은 서로 밀접하게 결합되어 있다. 관측(Observation)은 상태(State)를 추정하는 데 사용되는 증거를 제공하고, 행동(Action)은 에이전트가 세계에 개입할 수 있는 능력을 표현하며, 전이(Transition)는 행동과 외부 동역학에 따라 상태가 어떻게 변화하는지를 설명하고, 이후의 관측은 실제로 어떤 일이 발생했는지를 보여준다. 월드 모델(World Model)은 이러한 관계를 학습하거나 표현함으로써 에이전트가 단순히 현재를 인식하는 수준에서 벗어나 물리적 세계가 어떻게 변화할지를 예상하도록 한다.

이러한 구성은 더욱 발전된 월드 모델 아키텍처(World Model Architecture)의 기반도 제공한다. 잠재 동역학 모델(Latent Dynamics Model)은 관측을 예측 가능한 상태로 압축하고, 행동 조건부 모델(Action-Conditioned Model)은 제어 명령을 명시적으로 포함하며, 확률적 모델(Probabilistic Model)은 불확실한 전이를 표현하고, 계획 시스템(Planning System)은 서로 다른 행동에 대해 모델을 반복적으로 미래로 롤아웃한다. 아키텍처의 차이에도 불구하고 이러한 시스템은 상태를 표현하고 관측과 행동을 이용하여 시간에 따른 전이를 이해한다는 동일한 기본 문제를 다룬다.

결과적으로 상태(State), 관측(Observation), 행동(Action), 전이(Transition)는 체화된 에이전트(Embodied Agent)와 환경(Environment) 사이에서 이루어지는 예측적 상호작용(Predictive Interaction)의 기본 문법을 구성한다. 이들은 감각적 증거가 어떻게 내부 추정으로 변환되는지, 물리적 개입이 가능한 미래를 어떻게 변화시키는지, 그리고 새로운 증거가 기존의 믿음을 어떻게 수정하는지를 설명한다. 이러한 요소 사이에 신뢰할 수 있는 관계를 구축하는 것은 적응적(Adaptive), 예측적(Predictive), 자율적(Autonomous) 피지컬 AI를 지원할 수 있는 월드 모델을 구현하기 위한 가장 기본적인 요구사항 중 하나이다.

## 01.04. Partial Observability and Belief State

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

피지컬 AI(Physical AI) 시스템은 거의 언제나 세계의 완전한 상태(Complete State)에 직접 접근할 수 없다. 센서는 환경의 제한된 부분만 관측하고, 측정값에는 잡음(Noise)이 포함되며, 객체는 가려질 수 있고, 많은 중요한 물리적 속성은 직접 측정할 수 없다. 이러한 조건을 부분 관측 가능성(Partial Observability)이라고 하며, 복잡한 물리적 환경에서 신뢰성 있게 작동하는 월드 모델(World Model)을 위해 내부 상태 추정(Internal State Estimation)은 필수적인 요구사항이 된다.

부분 관측 가능성(Partial Observability)이란 현재의 관측(Current Observation)만으로 환경의 실제 상태(True State)를 유일하게 결정할 수 없다는 의미이다. 서로 다른 두 가지 물리적 상황이 유사한 센서 측정값을 만들어낼 수 있으며, 중요한 정보가 센서의 시야(Field of View) 밖에 존재할 수도 있다. 예를 들어 로봇이 교차로에 진입할 때 현재 보이는 영역은 비어 있을 수 있지만, 장애물 뒤에 가려진 차량이 접근하고 있을 수도 있다. 따라서 현재 보이는 것이 실제로 존재하는 모든 것과 반드시 동일한 것은 아니다.

센서의 한계(Sensor Limitation)는 겉보기에 단순한 환경에서도 부분 관측 가능성(Partial Observability)을 발생시킨다. 카메라(Camera)는 조명, 가림(Occlusion), 모션 블러(Motion Blur), 제한된 시야각의 영향을 받는다. 라이다(LiDAR)는 기하학적 측정값을 제공하지만 고체 장애물을 통과하여 관측할 수 없으며 측정 결과가 희소할 수 있다. 레이더(Radar), 촉각 센싱(Tactile Sensing), 마이크(Microphone), 관성측정장치(IMU), 고유수용성 센서(Proprioceptive Sensor)는 각각 현실의 서로 다른 측면을 관측한다. 일반적으로 하나의 센싱 모달리티(Sensing Modality)만으로는 물리적 세계를 완전하게 설명할 수 없다.

일부 중요한 변수는 단순히 센서 범위 밖에 있는 것이 아니라 본질적으로 숨겨진 상태(Hidden State)이다. 표면 마찰(Surface Friction), 객체 질량(Object Mass), 기계적 유연성(Mechanical Compliance), 인간의 의도(Human Intention), 액추에이터 성능 저하(Actuator Degradation), 다른 에이전트의 미래 행동(Future Behavior)은 직접 관측하기 어려울 수 있다. 월드 모델(World Model)은 시간에 따라 나타나는 효과로부터 이러한 특성을 추론해야 한다. 예를 들어 로봇은 바퀴 미끄러짐(Wheel Slip)을 통해 마찰을 추정하거나, 힘을 가했을 때 객체가 반응하는 방식으로부터 질량을 추론할 수 있다.

이러한 이유로 피지컬 AI(Physical AI) 시스템은 현재 관측을 넘어서는 내부 추정(Internal Estimate)을 필요로 한다. 이러한 추정은 일반적으로 믿음 상태(Belief State)라고 한다. 믿음 상태는 현재 순간에 센서가 감지한 내용만 표현하는 것이 아니라, 관측(Observation), 이전 행동(Previous Action), 기억(Memory), 학습된 동역학(Learned Dynamics), 그리고 아직 알려지지 않은 정보에 대한 불확실성(Uncertainty)을 바탕으로 에이전트가 현재 세계의 중요한 측면에 대해 무엇을 믿고 있는지를 요약한다.

개념적으로 믿음 상태(Belief State)는 시간 (t)에서 가능한 상태 (s)에 대한 에이전트의 믿음을 나타내는 분포 (b_t(s))로 표현할 수 있다. 불확실성이 낮으면 이 분포는 좁은 상태 범위에 집중될 수 있다. 반대로 관측이 모호하거나 정보가 누락된 경우 분포는 더 넓어지거나 다봉형(Multimodal)이 될 수 있으며, 이는 현재 이용 가능한 증거를 고려할 때 여러 가지 서로 다른 물리적 상황이 여전히 가능하다는 것을 나타낸다.

모든 실용적인 월드 모델(World Model)이 명시적인 수학적 확률 분포(Mathematical Probability Distribution)를 유지해야 하는 것은 아니다. 신경망 시스템(Neural System)은 순환 은닉 상태(Recurrent Hidden State), 잠재 표현(Latent Representation), 시간적 토큰(Temporal Token), 기억 특징(Memory Feature) 내부에 믿음 상태를 암묵적으로 인코딩할 수 있다. 중요한 것은 내부 표현이 불완전한 관측에서도 추론하는 데 필요한 정보를 보존하는 것이다. 따라서 확률을 명시적으로 계산하지 않더라도 결정론적 특징 벡터(Deterministic Feature Vector)가 근사적인 믿음 표현(Approximate Belief Representation)의 역할을 할 수 있다.

믿음 형성(Belief Formation)은 과거 이력(History)에 크게 의존한다. 보행자가 횡단보도를 향해 걷는 것이 관측된 후 주차된 차량 뒤로 가려졌다고 가정해 보자. 순수한 반응형 지각 시스템(Reactive Perception System)은 시각적 증거가 사라지는 순간 보행자를 놓칠 수 있다. 그러나 시간적 기억(Temporal Memory)을 갖춘 월드 모델은 보행자가 여전히 존재한다는 가설을 유지하고, 가려진 상태에서의 가능한 이동 궤적을 추정하며, 보행자가 곧 로봇의 이동 경로에 다시 나타날 가능성을 유지할 수 있다.

이전 행동(Previous Action) 역시 중요하다. 현재 상황이 어떻게 형성되었는지를 설명하는 데 도움을 주기 때문이다. 로봇이 방금 회전하거나 가속하거나 객체를 조작하거나 문을 열었다면 이러한 행동은 이후 관측을 해석하는 방식에 영향을 준다. 따라서 믿음 상태 추정(Belief-State Estimation)은 수동적인 센서 측정의 연속만 사용하는 것이 아니라 상호작용 이력(Interaction History)을 이용한다. 에이전트 자신의 개입(Intervention)은 자신의 상태와 주변 환경의 동역학에 관한 정보를 동시에 제공한다.

믿음 갱신(Belief Updating)은 예측(Prediction)과 수정(Correction)이 교대로 반복되는 과정으로 이해할 수 있다. 먼저 월드 모델(World Model)은 동역학과 에이전트가 수행한 행동을 바탕으로 현재 믿음이 어떻게 변화할지를 예측한다. 새로운 관측이 들어오면 해당 관측이 가능한 상태들과 얼마나 일치하는지를 기준으로 예측된 믿음을 수정한다. 이러한 예측--관측--수정(Predict--Observe--Correct)의 반복 과정은 완전하게 관측할 수 없는 세계에서도 내부 모델이 현실과 지속적으로 동기화되도록 한다.

따라서 기억(Memory)은 부분 관측 가능성(Partial Observability)에서 추론하기 위한 핵심 구성 요소이다. 단기 기억(Short-Term Memory)은 최근의 움직임, 센서 이력, 행동 맥락(Action Context)을 유지할 수 있으며, 장기 기억(Long-Term Memory)은 지도(Map), 객체 위치(Object Location), 환경 특성(Environmental Property), 반복적으로 나타나는 패턴을 보존할 수 있다. 효과적인 기억은 과거의 모든 관측을 단순히 저장하는 것이 아니라 현재 상태를 추정하고 미래의 물리적 변화를 예측하는 데 여전히 유용한 정보로 과거 이력을 압축한다.

객체 영속성(Object Permanence)은 이러한 요구사항을 명확하게 보여주는 사례이다. 물리적 객체는 일반적으로 센서 시야(Field of View)를 벗어나더라도 계속 존재한다. 따라서 강력한 월드 모델(World Model)은 관측에서 사라지는 것과 현실에서 사라지는 것을 구분해야 한다. 지속적인 객체 가설(Persistent Object Hypothesis)을 유지함으로써 자율 시스템은 가려진 차량, 장애물 뒤의 사람, 컨테이너 내부의 객체, 또는 현재 카메라나 라이다 범위에서 일시적으로 벗어난 장비에 대해 추론할 수 있다.

부분 관측 가능성(Partial Observability)은 모호성(Ambiguity)도 발생시킨다. 멀리 있는 센서 반사 신호가 여러 종류의 객체 가운데 하나일 수 있고, 가려진 영역에 장애물이 존재할 수도 있고 자유 공간(Free Space)일 수도 있으며, 다른 에이전트가 여러 가지 가능한 의도(Intention)를 가질 수도 있다. 믿음 상태(Belief State)는 하나의 해석을 성급하게 확정하는 대신 서로 경쟁하는 여러 가설(Competing Hypothesis)을 유지할 수 있다. 이후 추가적인 증거가 확보되면 새로운 관측을 통해 모호성을 줄이고 일치하지 않는 가설을 제거할 수 있다.

이러한 불확실성(Uncertainty)은 에이전트가 미래 상태(Future State)를 예측해야 할 때 특히 중요해진다. 현재 믿음에 존재하는 불확실성은 전이 모델(Transition Model)을 통해 전파되어 미래 궤적과 결과에 대한 불확실성을 만들어낸다. 다른 차량의 위치나 의도가 불확실하다면 그 차량의 미래 움직임에 대한 예측도 불확실해진다. 따라서 장기 예측(Long-Horizon Prediction)은 현재의 모호성과 상태 전이의 불확실성이 시간에 따라 누적되면서 일반적으로 미래로 갈수록 불확실성이 증가한다.

계획(Planning)에서는 하나의 추정 상태(Single Estimated State)보다 믿음 상태(Belief State)가 더 유용한 경우가 많다. 행동을 선택할 때 에이전트가 알지 못하는 것까지 고려해야 하기 때문이다. 가려진 모퉁이에 접근하는 로봇은 현재 장애물이 보이지 않더라도 자신의 믿음 상태가 숨겨진 위험(Hidden Hazard)에 일정한 가능성을 부여하고 있다면 속도를 줄일 수 있다. 따라서 안전한 계획(Safe Planning)은 관측되지 않은 영역을 비어 있거나 안전하다는 증거로 간주하는 대신 불확실성 자체를 행동 결정에 활용할 수 있는 정보(Actionable Information)로 취급한다.

행동(Action)은 불확실성을 줄이기 위한 목적으로 선택될 수도 있다. 로봇은 가려진 영역을 확인하기 위해 시점(Viewpoint)을 변경하거나, 객체에 더 가까이 이동하거나, 센서를 회전시키거나, 표면을 접촉하거나, 물리적 특성을 파악하기 위해 작은 조작을 수행할 수 있다. 이러한 행동은 흔히 능동 지각(Active Perception) 또는 정보 수집(Information Gathering)이라고 한다. 에이전트는 외부 작업을 달성하기 위해서만 행동하는 것이 아니라 더욱 중요한 결정을 내리기 전에 세계 상태에 대한 자신의 믿음을 개선하기 위해서도 행동한다.

멀티모달 센싱(Multimodal Sensing)은 서로 다른 센서가 상호보완적인 증거(Complementary Evidence)를 제공하기 때문에 부분 관측 가능성(Partial Observability)을 줄일 수 있다. 카메라는 의미론적 정보와 외형 정보를 제공하고, 라이다는 기하 구조(Geometry)를 제공하며, 레이더는 가시성이 좋지 않은 조건에서도 움직임을 감지할 수 있고, 고유수용성 정보(Proprioception)는 로봇 자신의 움직임을 설명할 수 있다. 센서 융합(Sensor Fusion)이 불확실성을 완전히 제거하지는 못하지만 동일한 물리적 상황의 서로 다른 측면을 제한하는 관측들을 결합함으로써 더욱 강력한 믿음 상태를 구성할 수 있다.

믿음 상태(Belief State)는 동적인 다중 에이전트 환경(Dynamic Multi-Agent Environment)에서 특히 중요하다. 사람, 차량, 다른 로봇은 숨겨진 목표(Hidden Goal)를 가지고 독립적인 의사결정을 수행할 수 있다. 이들의 내부 의도는 일반적으로 직접 관측할 수 없으므로 월드 모델(World Model)은 움직임, 상호작용 이력, 상황적 맥락(Context), 행동을 통해 이를 추론해야 한다. 서로 다른 가능한 의도가 크게 다른 궤적과 위험을 만들어낼 수 있으므로 여러 미래 가설(Future Hypothesis)을 동시에 유지해야 할 수도 있다.

학습 기반 월드 모델(Learned World Model)에서 시간적 아키텍처(Temporal Architecture)는 믿음과 유사한 표현을 구성하기 위한 여러 메커니즘을 제공한다. 순환 신경망(Recurrent Network)은 은닉 상태(Hidden State)를 유지할 수 있고, 상태 공간 모델(State-Space Model)은 잠재 변수(Latent Variable)를 재귀적으로 갱신할 수 있으며, 트랜스포머(Transformer)는 관측 및 행동 이력 전체의 정보를 통합할 수 있다. 아키텍처가 무엇이든 목표는 유사하다. 과거의 증거를 숨겨진 상태를 추정하고 다음에 무엇이 발생할지를 예측하는 데 유용한 내부 상태로 압축하는 것이다.

믿음 상태(Belief State)의 품질은 궁극적으로 예측(Prediction)과 행동(Action)에 얼마나 유용한지를 기준으로 평가해야 한다. 내부 표현은 에이전트가 중요한 숨겨진 정보를 유지하고, 모호성을 정량화하며, 위험을 예상하고, 불완전한 센싱 환경에서도 강건한 행동(Robust Action)을 선택하도록 지원할 때 가치가 있다. 관측되지 않은 모든 세부 사항을 완벽하게 복원하는 것은 가능하지도 않고 반드시 필요하지도 않다. 대신 모델은 물리적 작업에 필요한 수준에서 불확실성과 숨겨진 정보를 보존해야 한다.

따라서 부분 관측 가능성(Partial Observability)은 월드 모델(World Model)이 해결해야 하는 근본적인 질문 자체를 변화시킨다. 문제는 단순히 "에이전트가 지금 무엇을 보고 있는가?"가 아니라 "지금까지 관측하고, 기억하고, 수행한 모든 것을 고려할 때 현재 어떤 세계 상태들이 가능한가?"가 된다. 믿음 상태(Belief State)는 이 질문에 대한 내부적 답을 제공하며, 피지컬 AI(Physical AI)가 즉각적인 센서 입력을 넘어 추론하고 항상 부분적으로만 관측할 수 있는 물리적 세계에서 지능적으로 행동할 수 있도록 한다.

## 01.05. State Representation for Physical AI

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

상태 표현(State Representation)은 피지컬 AI(Physical AI) 시스템이 지속적으로 변화하는 물리적 세계(Physical World)를 예측(Prediction), 추론(Reasoning), 계획(Planning), 제어(Control)에 적합한 내부 형태로 변환하는 메커니즘이다. 원시 센서 스트림(Raw Sensor Stream)은 너무 방대하고 불완전하며 작업에 따라 달라지기 때문에 그 자체를 완전한 세계 설명으로 직접 사용하기 어렵다. 따라서 에이전트(Agent)는 미래 행동과 예상되는 환경 변화에 관련된 정보를 포함하는 압축된 표현(Compact Representation)을 구성해야 한다.

유용한 상태 표현(State Representation)은 외부 환경(External Environment)과 그 안에서 작동하는 체화된 에이전트(Embodied Agent)를 모두 설명해야 한다. 환경 상태(Environmental State)에는 기하 구조(Geometry), 자유 공간(Free Space), 점유(Occupancy), 객체(Object), 지형(Terrain), 의미론적 속성(Semantic Property), 동적 개체(Dynamic Entity)가 포함될 수 있으며, 에이전트 상태(Agent State)에는 자세(Pose), 속도(Velocity), 관절 구성(Joint Configuration), 접촉(Contact), 액추에이터 상태(Actuator Condition), 페이로드(Payload), 에너지(Energy)가 포함될 수 있다. 물리적 지능(Physical Intelligence)은 이 두 종류의 상태가 어떻게 상호작용하고 함께 변화하는지를 예측하는 능력에 의존한다.

공간적 정보(Spatial Information)는 상태(State)를 구성하는 주요 요소 중 하나이다. 로봇은 객체, 장애물, 표면, 사람, 다른 에이전트가 자신과 주변 환경을 기준으로 어디에 위치하는지를 표현해야 한다. 응용 분야에 따라 공간 상태(Spatial State)는 좌표(Coordinate), 지도(Map), 포인트 클라우드(Point Cloud), 복셀(Voxel), 점유 격자(Occupancy Grid), 조감도 표현(Bird's-Eye-View Representation), 객체 중심 구조(Object-Centric Structure), 또는 내비게이션과 상호작용에 필요한 관계를 보존하는 학습된 공간 특징(Learned Spatial Feature)을 이용하여 인코딩할 수 있다.

시간적 정보(Temporal Information) 역시 중요하다. 물리적 세계는 서로 독립적인 정적 장면의 집합이 아니라 지속적으로 변화하는 동적 세계이기 때문이다. 상태는 움직임(Motion), 속도, 궤적(Trajectory), 지속성(Persistence), 최근 변화(Recent Change)를 포착하여 에이전트가 정적 구조와 이동 개체를 구별하고 미래의 변화를 추정할 수 있도록 해야 한다. 시간적 표현(Temporal Representation)은 순환 기억(Recurrent Memory), 상태 공간 모델(State-Space Model), 시간적 특징 집계(Temporal Feature Aggregation), 어텐션 메커니즘(Attention Mechanism), 또는 명시적인 객체 및 움직임 추적을 통해 여러 관측을 통합할 수 있다.

의미론적 정보(Semantic Information)는 기하학적 구조와 시간적 구조에 의미를 추가한다. 어떤 영역이 점유되어 있다는 사실을 아는 것도 유용하지만, 그 영역에 벽, 보행자, 차량, 이동 가능한 상자, 계단 또는 주행 가능한 표면이 존재하는지를 아는 것은 적절한 행동을 선택하는 데 큰 차이를 만든다. 따라서 의미론적 상태(Semantic State)는 객체 정체성(Object Identity), 범주(Category), 어포던스(Affordance), 기능적 역할(Functional Role), 관계(Relationship), 작업 관련성(Task Relevance), 그리고 물리적 구조가 행동에 어떤 의미를 갖는지를 해석하는 데 필요한 상황적 정보(Contextual Information)를 인코딩할 수 있다.

물리적 상태 표현(Physical State Representation)은 상호작용과 동역학(Dynamics)에 영향을 주는 속성도 포착해야 한다. 기하 구조만으로는 객체를 밀 수 있는지, 지형이 미끄러운지, 표면이 로봇의 무게를 지탱할 수 있는지, 파지(Grasp)가 안정적으로 유지될지를 설명할 수 없다. 따라서 에이전트가 물리적 결과를 추론해야 하는 경우 질량(Mass), 마찰(Friction), 유연성(Compliance), 접촉(Contact), 힘(Force), 지지 관계(Support Relationship), 운동학적 제약(Kinematic Constraint), 동역학적 속성(Dynamic Property)이 중요한 상태 변수가 될 수 있다.

모든 상태 변수(State Variable)가 명시적으로 해석 가능해야 하는 것은 아니다. 현대의 월드 모델(World Model)은 고차원 관측(High-Dimensional Observation)을 잠재 상태(Latent State) (z_t)로 변환하는 경우가 많으며, 여기에서 학습된 특징(Learned Feature)은 미래 예측에 유용한 정보를 인코딩한다. 잠재 표현(Latent Representation)은 이미지, 포인트 클라우드, 고유수용성 정보(Proprioception), 기타 모달리티(Modality)를 더 작은 계산 공간(Computational Space)으로 압축할 수 있다. 잠재 표현의 효과는 모든 특징이 사람이 이해할 수 있는 의미를 갖는지보다 관련 미래 상태와 행동 결과를 얼마나 신뢰성 있게 예측할 수 있는지에 의해 결정된다.

명시적 표현(Explicit Representation)은 고전 로보틱스(Classical Robotics)와 제어 시스템(Control System)에 자연스럽게 연결될 수 있는 해석 가능한 값을 제공하기 때문에 여전히 중요하다. 로봇 자세, 속도, 객체 위치, 점유, 관절각(Joint Angle), 충돌 기하 구조(Collision Geometry)는 위치추정(Localization), 계획, 최적화(Optimization), 안전 모듈(Safety Module)에서 직접 사용할 수 있다. 또한 명시적 상태는 엔지니어가 월드 모델이 물리적으로 의미 있는 추정값을 포함하고 있는지 직접 확인할 수 있기 때문에 디버깅(Debugging)과 검증(Verification)을 더욱 용이하게 한다.

하이브리드 상태 표현(Hybrid State Representation)은 명시적 정보와 잠재 정보를 결합한다. 피지컬 AI 시스템은 명시적인 조감도 점유 구조(BEV Occupancy Structure)와 추적된 객체 상태(Tracked Object State)를 유지하면서 동시에 외형, 상호작용 패턴, 불확실한 동역학, 상황적 정보를 포착하는 잠재 특징을 학습할 수 있다. 이러한 아키텍처는 공학적으로 설계된 표현의 해석 가능성과 물리적 구조를 유지하면서 사람이 직접 정의하기 어려운 환경 요소를 신경망(Neural Network)으로 모델링할 수 있도록 한다.

객체 중심 표현(Object-Centric Representation)은 또 다른 유용한 추상화 방법을 제공한다. 전체 환경을 균일한 격자(Grid)나 특징 텐서(Feature Tensor)로 처리하는 대신, 세계를 위치, 속도, 크기, 범주, 상태, 관계와 같은 속성을 가진 지속적인 개체(Persistent Entity)의 집합으로 표현할 수 있다. 객체 중심 상태는 식별 가능한 개체 간 상호작용이 계획에 중요한 경우 특히 유용하지만, 식생(Vegetation), 유체(Fluid), 변형 가능한 지형(Deformable Terrain), 복잡한 자유 공간과 같이 명확한 객체 단위로 구분하기 어려운 구조에는 적합성이 낮을 수 있다.

밀집 표현(Dense Representation)은 공간 전체에 걸쳐 환경을 연속적으로 설명함으로써 객체 중심 표현을 보완하는 장점을 제공한다. 점유 격자(Occupancy Grid), 복셀 필드(Voxel Field), 의미론적 점유(Semantic Occupancy), 신경장(Neural Field), 조감도 특징 맵(BEV Feature Map)은 모든 요소에 객체 정체성을 부여하지 않고도 인식된 구조와 인식되지 않은 구조를 모두 표현할 수 있다. 내비게이션(Navigation)과 충돌 회피(Collision Avoidance)에서는 지각 시스템이 장애물의 종류를 정확하게 분류하지 못하더라도 해당 장애물은 여전히 물리적으로 중요하기 때문에 이러한 특성이 매우 중요하다.

상태 표현(State Representation)은 정적 정보(Static Information)와 동적 정보(Dynamic Information)도 구분해야 한다. 건물, 벽, 지형, 영구적인 인프라(Infrastructure)는 일반적으로 천천히 변화하는 반면, 사람, 차량, 조작 가능한 객체, 로봇 자체는 빠르게 변화할 수 있다. 이러한 시간적 특성을 분리하면 계산 효율성과 예측 품질을 향상시킬 수 있다. 천천히 변화하는 월드 메모리(World Memory)는 안정적인 맥락을 제공하고, 빠르게 갱신되는 동적 상태는 단기 예측(Short-Horizon Prediction)과 반응형 제어(Reactive Control)를 지원할 수 있다.

멀티모달 상태 표현(Multimodal State Representation)은 피지컬 AI(Physical AI)가 일반적으로 여러 센싱 시스템으로부터 정보를 받기 때문에 필수적이다. 카메라는 외형 및 의미론적 단서를 제공하고, 라이다는 기하 구조를 제공하며, 레이더는 움직임 정보를 보완하고, 관성측정장치(IMU)는 몸체 동역학(Body Dynamics)을 추정하며, 고유수용성 센서(Proprioceptive Sensor)는 로봇 자체의 상태를 설명한다. 월드 모델은 이러한 관측을 하나의 일관된 상태로 통합하기 전에 공간적·시간적으로 정렬하여 서로 분리된 센서별 설명이 아니라 하나의 물리적 세계를 표현하도록 해야 한다.

불확실성(Uncertainty)은 단순히 상태 추정 이후에 추가되는 오차가 아니라 상태 자체의 일부로 고려되어야 한다. 객체 위치, 속도, 분류(Classification), 지형 특성, 가려진 영역, 미래 의도(Future Intention)는 모두 불확실할 수 있다. 상태 표현은 확률 분포(Probability Distribution), 신뢰도 값(Confidence Value), 다중 가설(Multiple Hypothesis), 앙상블(Ensemble), 잠재 불확실성(Latent Uncertainty)을 인코딩할 수 있다. 이러한 정보를 보존하면 이후의 예측 및 계획 시스템이 신뢰할 수 있는 지식과 주의가 필요한 가정을 구별할 수 있다.

부분 관측 가능성(Partial Observability)은 상태(State)가 기억(Memory)을 포함해야 할 필요성을 더욱 높인다. 현재의 센서 입력만으로는 일시적으로 가려진 객체, 시야 밖의 위치, 이전 상호작용을 통해 추론된 숨겨진 물리적 속성을 설명할 수 없다. 따라서 상태 표현은 중요한 과거 정보를 요약하여 지식이 즉각적인 관측을 넘어 지속되도록 해야 한다. 이러한 의미에서 유용한 상태는 단순히 현재 센서 프레임(Current Sensor Frame)을 인코딩한 것이 아니라 물리적 상황에 대해 시간에 걸쳐 축적된 추정(Accumulated Estimate)이다.

행동 관련성(Action Relevance)은 어떤 정보가 상태에 포함되어야 하는지를 결정하는 중요한 기준을 제공한다. 내비게이션을 위해 설계된 표현은 주행 가능성(Traversability), 충돌(Collision), 움직임, 경로 선택(Route Selection)에 영향을 주는 정보를 보존해야 한다. 조작(Manipulation)을 위한 상태는 도달 가능성(Reachability), 객체 자세(Object Pose), 파지 가능성(Graspability), 접촉, 힘을 강조해야 한다. 따라서 상태 표현은 환경의 모든 측정 가능한 속성을 동일한 정밀도로 모델링하려 하기보다 에이전트가 내려야 하는 의사결정에 충분한 정보를 제공하도록 설계되어야 한다.

동일한 환경에서 서로 다른 로봇이 작동하더라도 체화 형태(Embodiment)에 따라 필요한 상태 정보가 달라진다. 바퀴형 로봇(Wheeled Robot)은 경사(Slope), 바퀴 미끄러짐(Wheel Slip), 지상고(Clearance), 주행 가능성을 필요로 할 수 있으며, 4족 보행 로봇(Quadruped Robot)은 추가적으로 발판 기하 구조(Foothold Geometry), 접촉 안정성(Contact Stability), 몸체 방향(Body Orientation), 지형 지지력(Terrain Support)을 필요로 할 수 있다. 매니퓰레이터는 관절 한계(Joint Limit)와 도달 가능한 구성(Reachable Configuration)이 필요하다. 따라서 상태 표현은 물리적 신체와 독립적이지 않으며 특정 에이전트가 무엇을 감지하고, 예측하고, 제어할 수 있는지를 반영한다.

상태 차원(State Dimensionality)은 중요한 공학적 절충 관계(Engineering Tradeoff)를 만든다. 너무 적은 정보를 포함하는 표현은 정확한 예측에 필요한 변수를 누락할 수 있는 반면, 지나치게 상세한 표현은 메모리, 계산량, 통신량, 학습 요구량을 증가시킨다. 따라서 효과적인 월드 모델은 충분 통계량(Sufficient Statistics)을 추구한다. 즉, 원시 관측에서 중복성과 작업에 불필요한 세부 정보를 제거하면서 미래 변화와 의사결정에 관련된 정보를 보존하는 압축된 내부 상태를 구성해야 한다.

계층적 표현(Hierarchical Representation)은 여러 공간적, 시간적, 의미론적 스케일(Scale)에서 정보를 유지함으로써 이러한 절충 문제를 해결할 수 있다. 세밀한 지역 기하 구조(Local Geometry)는 즉각적인 충돌 회피를 지원할 수 있고, 보다 거친 지도(Coarse Map)는 장거리 내비게이션(Long-Range Navigation)을 지원할 수 있다. 빠르게 변화하는 동적 상태는 주변 이동 객체를 표현하고, 느리게 변화하는 의미론적 기억(Semantic Memory)은 지속적인 환경 지식을 보존할 수 있다. 따라서 서로 다른 예측 시간 범위(Prediction Horizon)가 동일한 구조화된 세계 표현의 서로 다른 계층에서 작동할 수 있다.

상태 표현(State Representation)은 로봇이 세계와 상호작용하는 동안 지속적으로 갱신되어야 한다. 새로운 관측은 객체를 추가하거나, 기하 구조를 수정하거나, 위치추정(Localization)을 보정하거나, 불확실성을 줄이거나, 이전의 가정을 무효화할 수 있다. 행동은 에이전트 상태와 외부 상태 모두를 변화시킬 수 있다. 따라서 유용한 상태 표현은 정적인 데이터베이스(Static Database)가 아니라 자율 작동 과정 전체에서 추정(Estimation), 예측(Prediction), 관측(Observation), 수정(Correction)을 반복하는 동적 계산 기억(Dynamic Computational Memory)이다.

월드 모델 학습(World-Model Learning)에서는 상태 표현의 품질을 복원 정확도(Reconstruction Accuracy)뿐만 아니라 다운스트림 유용성(Downstream Utility)을 기준으로도 평가해야 한다. 센서 픽셀을 정확하게 복원하는 표현이라도 제어에 필요한 변수를 제거할 수 있으며, 반대로 압축된 잠재 상태는 성공적인 계획에 필요한 동역학만 정확하게 보존할 수 있다. 따라서 평가는 상태가 정확한 미래 예측, 행동 조건부 전이(Action-Conditioned Transition), 불확실성 추정, 일반화(Generalization), 강건한 물리적 의사결정(Robust Physical Decision Making)을 지원하는지를 고려해야 한다.

결국 상태 표현(State Representation)은 피지컬 AI(Physical AI) 시스템이 자신의 세계에 대해 무엇을 이해할 수 있는지를 결정한다. 이는 에이전트가 무엇을 기억하고, 무엇을 중요하다고 판단하며, 어떤 동역학을 예측할 수 있고, 행동하기 전에 어떤 대안을 평가할 수 있는지를 정의한다. 강력한 상태 표현은 공간적(Spatial), 시간적(Temporal), 의미론적(Semantic), 물리적(Physical), 체화된(Embodied), 불확실한(Uncertain) 정보를 행동 가능한 내부 상태(Actionable Internal State)로 통합하며, 예측적 월드 모델(Predictive World Model)과 자율적 물리 지능(Autonomous Physical Intelligence)이 구축되는 계산적 기반(Computational Foundation)을 형성한다.

## 01.06. Dynamics and Transition Models

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

동역학 및 전이 모델(Dynamics and Transition Models)은 월드 모델(World Model)의 내부 상태(Internal State)가 시간에 따라 어떻게 변화하는지를 설명한다. 상태 표현(State Representation)이 에이전트(Agent)가 현재 물리적 세계(Physical World)에 대해 무엇을 믿고 있는가에 답한다면, 동역학 모델(Dynamics Model)은 다음에 무엇이 발생할 수 있는가를 다룬다. 이는 움직임(Motion), 상호작용(Interaction), 환경 변화(Environmental Change), 행동의 결과(Action Consequence)를 지배하는 규칙성을 포착하여 피지컬 AI(Physical AI) 시스템 내부에서 시간적 예측(Temporal Prediction)을 가능하게 한다.

전이(Transition)는 일반적으로 현재 상태 (s_t)에서 미래 상태 (s_{t+1})로 변화하는 관계로 표현된다. 행동 조건부 구성(Action-Conditioned Formulation)에서는 이를 개념적으로 (s_{t+1}=f(s_t,a_t))로 나타낼 수 있으며, 여기에서 (a_t)는 에이전트의 행동(Action)을, (f)는 동역학(Dynamics)을 나타낸다. 따라서 모델은 현재 상황과 개입(Intervention)의 조합이 어떻게 새로운 물리적 상황을 만들어내는지를 예측한다.

실제 환경에는 제어된 행동 이외의 영향도 존재하므로 실용적인 전이 모델(Transition Model)은 외부 변수(External Variable), 외란(Disturbance), 확률적 효과(Stochastic Effect)를 포함하는 경우가 많다. 보다 일반적인 형태는 (s_{t+1}=f(s_t,a_t,w_t))로 표현할 수 있으며, 여기서 (w_t)는 바람(Wind), 바퀴 미끄러짐(Wheel Slip), 센서와 무관하게 발생하는 환경 변화, 다른 에이전트가 수행하는 행동과 같은 요소를 나타낸다. 따라서 전이 모델링(Transition Modeling)은 단순히 명령된 움직임을 재현하는 것이 아니라 서로 상호작용하는 원인들을 예측하는 문제이다.

동역학(Dynamics)은 결정론적(Deterministic)이거나 확률적(Probabilistic)일 수 있다. 결정론적 모델(Deterministic Model)은 주어진 상태와 행동에 대해 하나의 미래 상태를 예측하며, 물리적 행동을 높은 수준으로 예측할 수 있는 경우 적합할 수 있다. 반면 확률적 전이 모델(Probabilistic Transition Model)은 (p(s_{t+1}\|s_t,a_t))를 표현하여 여러 결과가 가능하도록 한다. 이는 숨겨진 변수(Hidden Variable), 불확실한 물리적 속성, 환경 외란, 독립적인 에이전트로 인해 겉보기에 유사한 조건에서도 서로 다른 미래가 발생할 수 있을 때 중요하다.

물리적 동역학(Physical Dynamics)은 다양한 추상화 수준(Level of Abstraction)에서 존재한다. 저수준 동역학(Low-Level Dynamics)은 힘(Force), 토크(Torque), 가속도(Acceleration), 접촉(Contact), 바퀴 미끄러짐, 관절 움직임(Joint Motion), 강체 거동(Rigid-Body Behavior)을 설명할 수 있다. 보다 상위 수준의 전이는 객체가 한 영역에서 다른 영역으로 이동하거나, 보행자가 경로를 횡단하거나, 문이 닫힌 상태에서 열린 상태로 바뀌거나, 지형이 주행 불가능한 상태가 되는 것 등을 설명할 수 있다. 유용한 월드 모델은 예측 및 계획 요구사항에 적합한 동역학 수준을 선택한다.

고전 로보틱스(Classical Robotics)는 물리 원리(Physical Principle)에서 유도된 해석적 동역학(Analytical Dynamics)을 자주 사용한다. 강체 역학(Rigid-Body Mechanics), 운동학(Kinematics), 마찰(Friction), 접촉(Contact), 액추에이터 특성(Actuator Characteristic)을 기반으로 하는 방정식은 시스템 파라미터(System Parameter)와 작동 조건을 충분히 알고 있을 때 정확한 예측을 제공할 수 있다. 이러한 모델은 해석 가능성(Interpretability)과 물리적 일관성(Physical Consistency)을 제공하지만 실제 환경에 복잡한 접촉, 불확실한 파라미터, 변형 가능한 물질(Deformable Material), 모델링되지 않은 상호작용이 존재하면 정확도가 저하될 수 있다.

학습된 동역학 모델(Learned Dynamics Model)은 데이터로부터 직접 전이 행동(Transition Behavior)을 추정하는 대안을 제공한다. 신경망(Neural Network)은 모든 물리적 관계를 사람이 직접 명시하지 않고도 기록된 상호작용 시퀀스(Interaction Sequence)로부터 상태, 행동, 미래 상태 사이의 매핑(Mapping)을 학습할 수 있다. 이러한 접근법은 해석적으로 모델링하기 어려운 복잡한 시스템에 유용하지만, 예측 품질은 학습 데이터의 범위(Training Coverage), 표현 품질(Representation Quality), 관측하지 않은 조건에 대한 일반화(Generalization)에 크게 의존한다.

하이브리드 동역학(Hybrid Dynamics)은 해석적 지식(Analytical Knowledge)과 학습된 구성 요소(Learned Component)를 결합한다. 알려진 운동학 또는 물리 모델이 기본적인 예측을 제공하고, 학습된 잔차 모델(Learned Residual Model)이 마찰, 액추에이터 동작, 지형, 페이로드(Payload), 기타 정확하게 설명하기 어려운 효과로 인해 발생하는 체계적인 오차(Systematic Error)를 추정할 수 있다. 이러한 접근법은 실제 세계의 행동에 적응하는 데 필요한 유연성을 유지하면서 데이터 효율성(Data Efficiency)과 물리적 타당성(Physical Plausibility)을 향상시킬 수 있다.

전이 모델(Transition Model)은 명시적 상태 공간(Explicit State Space)에서 직접 작동하거나 학습된 잠재 공간(Latent Space) 내부에서 작동할 수 있다. 명시적 모델은 위치(Position), 속도(Velocity), 점유(Occupancy), 객체 자세(Object Pose)와 같이 해석 가능한 변수를 예측한다. 반면 잠재 동역학(Latent Dynamics)은 (z_t)가 압축된 학습 표현일 때 (z_t)와 (a_t)로부터 (z_{t+1})을 예측한다. 잠재 예측(Latent Prediction)은 미래 의사결정에 필요한 정보를 유지하면서 불필요한 감각적 세부 정보를 복원하지 않아도 되므로 계산 비용을 줄일 수 있다.

시간 해상도(Temporal Resolution)는 동역학 모델이 무엇을 학습하는지에 큰 영향을 미친다. 짧은 시간 간격에서 전이는 위치, 속도, 관절 구성, 접촉의 작은 변화를 표현할 수 있다. 더 긴 시간 간격에서는 모델이 상위 수준의 사건(Event)과 행동 변화(Behavioral Change)에 집중할 수 있다. 따라서 피지컬 AI 시스템은 빠른 모델이 즉각적인 제어를 지원하고 느린 모델이 장기적인 환경 변화와 작업 수준의 결과(Task-Level Consequence)를 포착하는 다중 시간척도 동역학(Multi-Timescale Dynamics)을 활용할 수 있다.

다단계 예측(Multi-Step Prediction)은 전이 모델을 반복적으로 적용하여 얻을 수 있다. (s_t)에서 시작하여 모델은 (s_{t+1})을 예측하고, 그 예측값을 이용하여 (s_{t+2})를 추정하면서 미래 시간 범위(Future Horizon)에 걸쳐 이러한 과정을 계속한다. 이러한 롤아웃(Rollout)을 통해 에이전트는 궤적(Trajectory)을 실제로 실행하기 전에 내부적으로 상상할 수 있다. 그러나 한 단계에서 발생한 오차가 이후 단계의 입력이 되기 때문에 예측 오차가 누적되어 장기 예측 정확도가 크게 저하될 수 있다.

따라서 안정적인 장기 예측(Long-Horizon Prediction)을 위해서는 정확한 단일 단계 전이(One-Step Transition) 이상의 능력이 필요하다. 모델은 시간적 일관성(Temporal Consistency)을 보존하고, 중요한 상태 변수를 유지하며, 불확실성(Uncertainty)을 처리하고, 물리적으로 불가능한 상태로 예측이 표류(Drift)하는 것을 방지해야 한다. 학습 목적함수(Training Objective)에 다단계 예측, 일관성 제약(Consistency Constraint), 물리적 사전 지식(Physical Prior), 궤적 수준 손실(Trajectory-Level Loss)을 명시적으로 포함하여 학습된 동역학이 여러 단계에 걸쳐 반복적으로 전개되더라도 유용성을 유지하도록 할 수 있다.

모델이 계획(Planning)이나 제어(Control)에 사용될 경우 행동 조건화(Action Conditioning)는 필수적이다. 행동 정보가 없으면 동역학 모델은 장면이 일반적으로 어떻게 변화하는지는 예측할 수 있지만 서로 다른 개입으로 인해 발생하는 미래를 구별할 수 없다. 조향(Steering), 가속, 관절 명령(Joint Command), 파지 행동(Grasp Action), 상위 수준 의사결정(High-Level Decision)을 전이의 조건으로 사용하면 월드 모델은 반사실적 질문(Counterfactual Question)에 답하고 로봇이 실제 행동을 실행하기 전에 여러 대안 행동의 결과를 비교할 수 있다.

동역학 모델링(Dynamics Modeling)은 자기 운동(Ego-Motion)과 환경 움직임(Environmental Motion)도 구별해야 한다. 카메라 영상은 로봇이 움직이거나, 객체가 움직이거나, 또는 둘 다 동시에 움직이기 때문에 변화할 수 있다. 따라서 정확한 예측을 위해서는 에이전트 자신의 움직임과 독립적으로 변화하는 환경 개체를 함께 표현해야 한다. 이러한 구분은 센서가 환경을 이동하면서 지속적으로 움직이는 이동 로봇(Mobile Robot), 자율주행차(Autonomous Vehicle), 비행 시스템(Aerial System) 및 기타 체화된 에이전트(Embodied Agent)에서 특히 중요하다.

접촉(Contact)과 상호작용(Interaction)은 피지컬 AI(Physical AI)에서 가장 어려운 전이 중 일부를 만들어낸다. 밀기(Pushing), 파지(Grasping), 보행(Walking), 충돌(Collision), 변형(Deformation), 도구 사용(Tool Use)은 불연속성(Discontinuity)과 강한 비선형 거동(Nonlinear Behavior)을 발생시킬 수 있다. 접촉 위치나 마찰의 작은 차이도 매우 다른 결과를 만들어낼 수 있다. 따라서 조작(Manipulation)이나 이동(Locomotion)을 위한 동역학 모델은 접촉 상태(Contact State), 물리적 제약(Physical Constraint), 상호작용에 따른 전이(Interaction-Dependent Transition)를 포착할 수 있는 표현을 필요로 한다.

지형 상호작용(Terrain Interaction)은 이동 로봇에서도 유사한 문제를 발생시킨다. 동일한 바퀴 명령(Wheel Command)이라도 건조한 포장도로, 느슨한 흙, 진흙, 자갈, 눈, 경사면에서는 서로 다른 변위를 만들어낼 수 있다. 페이로드와 타이어 상태 역시 반응을 변화시킬 수 있다. 지형 특성과 체화 상태(Embodied State)를 표현하는 월드 모델은 이러한 요소를 조건으로 전이 결과를 예측함으로써 바퀴 미끄러짐, 이동성 저하(Reduced Mobility), 불안정성(Instability), 증가된 정지 거리(Increased Stopping Distance)를 미리 예상할 수 있다.

다중 에이전트 환경(Multi-Agent Environment)에서 전이 모델은 제어 가능한 행동과 제어할 수 없는 행동을 모두 예측해야 한다. 에이전트는 자신의 후보 행동(Candidate Action)은 알고 있지만 보행자, 차량, 사람, 다른 로봇을 직접 제어하지는 않는다. 따라서 이들의 미래 행동은 확률적(Probabilistic) 또는 다중 모드 예측(Multimodal Prediction)이 필요할 수 있다. 결과적으로 세계의 전이는 하나의 행동만으로 생성되는 것이 아니라 제어 대상 에이전트, 다른 에이전트, 정적 구조, 환경 동역학 사이의 상호작용을 통해 만들어진다.

불확실성(Uncertainty)은 예측 과정에서 사라지는 것이 아니라 동역학을 통해 전파되어야 한다. 현재 상태에 위치, 속도, 마찰, 객체 정체성(Object Identity), 다른 에이전트의 의도에 관한 불확실성이 존재한다면 미래 상태 역시 이를 반영해야 한다. 전이 불확실성(Transition Uncertainty) 자체도 독립적으로 누적될 수 있다. 따라서 확률적 롤아웃(Probabilistic Rollout)은 분포 또는 여러 개의 가능한 궤적(Plausible Trajectory)을 제공하여 계획 알고리즘이 예상되는 결과뿐만 아니라 발생 가능성은 낮지만 위험한 상황도 함께 추론할 수 있도록 한다.

동역학 모델(Dynamics Model)은 수동적 관측(Passive Observation), 능동적 상호작용(Active Interaction), 시뮬레이션(Simulation), 또는 이들의 조합을 통해 학습할 수 있다. 비디오와 센서 시퀀스는 자연적인 환경 변화를 보여주며, 로봇 행동은 개입과 결과 사이의 인과 관계(Causal Relationship)에 대해 더욱 강한 정보를 제공한다. 시뮬레이션은 대량의 제어된 상호작용 데이터를 생성할 수 있지만, 시뮬레이션과 실제 물리적 행동 사이의 차이를 식별하기 위해서는 실제 세계 경험(Real-World Experience)이 필요하다.

예측 오차(Prediction Error)는 전이 모델(Transition Model)을 학습하기 위한 중요한 학습 신호(Learning Signal)를 제공한다. 모델은 미래 상태를 예측하고 실제로 발생한 결과를 관측한 다음 둘을 비교한다. 그 차이를 이용하여 모델 파라미터(Model Parameter)를 갱신하거나 잔차 동역학(Residual Dynamics)을 추정할 수 있다. 따라서 반복적인 상호작용은 에이전트가 작동 과정에서 경험하는 움직임, 행동 효과, 환경 변동성(Environmental Variability), 물리적 관계에 대한 이해를 점진적으로 향상시키는 지속적 학습 루프(Continuous Learning Loop)를 형성한다.

계획(Planning)에서 전이 모델(Transition Model)은 현실의 모든 세부 사항을 재현할 필요가 없는 내부 시뮬레이터(Internal Simulator)로 기능한다. 목적은 의사결정에 중요한 결과를 보존하는 것이다. 내비게이션 모델(Navigation Model)은 충돌, 움직임, 주행 가능성(Traversability)을 정확하게 예측해야 하며, 조작 모델(Manipulation Model)은 접촉과 객체 움직임을 보존해야 한다. 따라서 계산 자원(Computational Resource)은 미래 행동의 품질이나 안전성을 변화시킬 수 있는 동역학에 집중되어야 한다.

결국 동역학 및 전이 모델(Dynamics and Transition Models)은 세계에 대한 정적인 표현(Static Representation)을 예측적인 표현(Predictive Representation)으로 변화시킨다. 이들은 현재 상태(Current State), 에이전트 행동(Agent Action), 외부 영향(External Influence), 미래 상태(Future State)를 학습되거나 공학적으로 설계된 시간적 관계(Temporal Relationship)를 통해 연결한다. 피지컬 AI 시스템은 이러한 관계를 반복적으로 적용함으로써 여러 대안적 미래(Alternative Future)를 내부적으로 상상하고, 위험을 추정하며, 행동을 선택하고, 새로운 경험을 통해 지속적으로 예측을 수정할 수 있다. 이러한 의미에서 동역학 및 전이 모델은 실제로 작동하는 월드 모델(Operational World Model)의 핵심을 구성하는 시간적 엔진(Temporal Engine)이다.

## 01.07. Observation and Decoder Models

![](images/image7.png){width="7.268055555555556in" height="7.268055555555556in"}

관측 모델(Observation Model)은 세계의 근본적인 상태(Underlying State)와 에이전트(Agent)가 이용할 수 있는 감각 정보(Sensory Information) 사이의 관계를 설명한다. 상태(State)가 물리적으로 실제 발생하고 있는 상황을 표현한다면, 관측(Observation)은 그 현실이 카메라(Camera), 라이다(LiDAR), 레이더(Radar), 촉각 센서(Tactile Sensor), 고유수용성 감각(Proprioception) 또는 기타 센싱 채널(Sensing Channel)을 통해 어떻게 나타나는지를 표현한다. 피지컬 AI(Physical AI) 시스템은 현실에 직접 접근하는 것이 아니라 측정값을 기반으로 추론해야 하므로 이러한 구분은 매우 중요하다.

개념적으로 관측 모델(Observation Model)은 세계 상태 (s_t)와 관측 (o_t) 사이의 관계를 나타낸다. 결정론적 구성(Deterministic Formulation)은 (o_t=g(s_t))로 표현할 수 있으며, 확률적 구성(Probabilistic Formulation)은 (p(o_t\|s_t))로 나타낼 수 있다. 후자는 센서 잡음(Sensor Noise), 환경 조건(Environmental Condition), 시점(Viewpoint), 캘리브레이션 불확실성(Calibration Uncertainty), 가림(Occlusion), 기타 센싱 과정에 영향을 주는 요소로 인해 동일한 물리적 상태에서도 서로 다른 측정값이 생성될 수 있음을 반영한다.

관측 모델(Observation Model)은 부분 관측 가능성(Partial Observability)과 밀접하게 연결되어 있다. 센서는 환경의 일부 속성만을 포착하며 일반적으로 제한된 공간적·시간적 범위 내에서만 정보를 얻는다. 카메라는 완전한 3차원 구조가 아니라 투영된 외형(Projected Appearance)을 기록하고, 라이다는 가시 표면(Visible Surface)의 기하 구조를 샘플링한다. 따라서 관측은 완전한 상태 표현이 아니라 근본적인 물리적 상태에 의해 생성된 불완전한 증거(Incomplete Evidence)로 해석해야 한다.

서로 다른 센싱 모달리티(Sensing Modality)는 근본적으로 서로 다른 관측 공간(Observation Space)을 생성한다. 이미지는 밀집된 외형, 질감(Texture), 색상, 의미론적 단서(Semantic Cue)를 포함하고, 라이다는 희소한 기하학적 측정값을 생성하며, 레이더는 거리 및 움직임 관련 정보를 제공한다. 마이크(Microphone)는 음향 신호(Acoustic Signal)를, 촉각 센서는 접촉(Contact)을, 고유수용성 센서는 에이전트 자신의 상태를 측정한다. 따라서 피지컬 AI 월드 모델(World Model)은 동일한 물리적 상황의 상호보완적 측면을 설명하는 이질적인 관측(Heterogeneous Observation)을 처리할 수 있어야 한다.

인코더(Encoder)와 관측 모델(Observation Model)은 서로 반대 방향에서 바라볼 수 있다. 인코더는 관측 (o_t)를 잠재 상태(Latent State) (z_t)와 같은 내부 표현(Internal Representation)으로 변환하여 예측과 행동에 유용한 정보를 추론한다. 관측 모델 또는 디코더 모델(Decoder Model)은 반대 방향으로 작동하여 내부 상태와 예상되는 감각적 증거(Expected Sensory Evidence)를 연결한다. 이 두 매핑(Mapping)은 고차원 센서 공간(High-Dimensional Sensor Space)과 학습 기반 월드 모델이 사용하는 압축된 내부 상태 공간(Compact Internal State Space)을 연결한다.

디코더(Decoder)는 개념적으로 (\\hat{o}_t=D(z_t))로 표현할 수 있으며, 여기서 (D)는 잠재 상태를 복원되거나 예측된 관측으로 매핑한다. 응용 분야에 따라 디코딩된 출력(Decoded Output)은 RGB 이미지, 깊이 맵(Depth Map), 의미론적 맵(Semantic Map), 점유 표현(Occupancy Representation), 포인트 클라우드(Point Cloud), 고유수용성 신호(Proprioceptive Signal), 또는 다른 작업 관련 정보(Task-Relevant Quantity)가 될 수 있다. 따라서 디코더는 잠재 상태가 관측 가능한 현실에 대해 어떤 정보를 보존하고 있는지를 해석하는 방법을 제공한다.

복원(Reconstruction)은 디코더 모델(Decoder Model)의 중요한 역할 중 하나이다. 학습 과정에서 인코더는 관측을 잠재 표현(Latent Representation)으로 압축하고, 디코더는 원래 관측 또는 그중 중요한 부분을 복원하려 한다. 실제 관측과 복원된 출력 사이의 차이는 학습 신호(Training Signal)를 제공한다. 이를 통해 잠재 상태가 감각 데이터를 설명하는 정보를 유지하도록 유도할 수 있지만, 높은 복원 정확도(Reconstruction Accuracy)만으로 해당 표현이 예측이나 제어에 유용하다는 것이 보장되지는 않는다.

예측 디코딩(Predictive Decoding)은 이러한 개념을 현재 상태의 복원에서 미래 관측(Future Observation)의 생성으로 확장한다. 동역학 모델(Dynamics Model)이 미래 잠재 상태 (z_{t+1})을 예측하면 디코더는 이를 예상 관측 (\\hat{o}_{t+1})로 변환한다. 이 과정을 반복하면 예측된 센서 시퀀스(Predicted Sensor Sequence)를 생성할 수 있다. 이러한 출력은 환경이 변화하거나 에이전트가 특정 행동을 수행했을 때 물리적 장면이 어떻게 나타날 수 있는지를 모델이 시각화하거나 평가하도록 한다.

그러나 월드 모델(World Model)이 항상 완전한 센서 관측을 디코딩해야 하는 것은 아니다. 모든 이미지 픽셀(Image Pixel)이나 라이다 포인트를 복원하는 것은 행동에 중요하지 않은 세부 사항을 유지하면서 상당한 계산 자원을 소비할 수 있다. 내비게이션(Navigation)을 위해 설계된 모델은 대신 점유(Occupancy), 주행 가능성(Traversability), 객체 궤적(Object Trajectory), 충돌 위험(Collision Risk)을 디코딩할 수 있다. 조작 모델(Manipulation Model)은 객체 자세(Object Pose), 접촉, 어포던스(Affordance)를 디코딩할 수 있다. 따라서 디코더의 목표(Decoder Target)는 다운스트림 작업(Downstream Task)에 필요한 정보를 반영해야 한다.

이러한 구분은 작업 지향 디코딩(Task-Oriented Decoding)으로 이어진다. 내부 상태가 센서가 관측한 모든 것을 재현할 수 있는지를 묻는 대신, 시스템은 의사결정(Decision Making)에 필요한 정보를 복원할 수 있는지를 평가한다. 시각적 질감(Visual Texture)을 복원하지 못하는 압축된 상태라도 장애물 움직임, 자유 공간(Free Space), 지형 특성(Terrain Property), 파지 결과(Grasp Outcome)를 정확하게 예측한다면 매우 효과적일 수 있다. 따라서 피지컬 AI에서는 감각적 사실성(Sensory Realism)보다 물리적 유용성(Physical Utility)이 더 중요할 수 있다.

관측 모델(Observation Model)은 센서 기하 구조(Sensor Geometry)를 고려해야 한다. 카메라 측정값은 투영(Projection), 시점(Viewpoint), 시야각(Field of View), 가림(Occlusion)에 따라 달라지며, 라이다 측정값은 빔 기하 구조(Beam Geometry)와 표면 가시성(Surface Visibility)에 따라 달라진다. 동일한 물리적 장면이라도 로봇의 위치나 방향이 달라지면 매우 다른 관측을 생성할 수 있다. 따라서 에이전트 자세(Agent Pose), 환경 구조(Environmental Structure), 예상 관측 사이의 관계를 모델링하는 것은 능동 지각(Active Perception)과 상태 추정(State Estimation)에 중요하다.

센서 잡음(Sensor Noise)과 불확실성(Uncertainty) 역시 관측 모델링(Observation Modeling)의 핵심 요소이다. 측정값은 전자적 잡음(Electronic Noise), 캘리브레이션 오차(Calibration Error), 조명, 날씨, 반사 표면(Reflective Surface), 움직임, 간섭(Interference) 때문에 달라질 수 있다. 확률적 관측 모델(Probabilistic Observation Model)은 가정된 상태(Hypothesized State)가 주어졌을 때 특정 측정값이 나타날 가능성을 표현한다. 이를 통해 에이전트는 여러 경쟁 상태 가설(Competing State Hypothesis)을 비교하고 불완전한 측정값을 지나치게 확신하지 않으면서 어떤 상태가 현재 증거와 가장 일치하는지를 판단할 수 있다.

가림(Occlusion)은 특히 중요한 관측 문제를 발생시킨다. 어떤 객체가 내부 상태(Internal State)에는 존재하지만 다른 구조물이 센서를 가리고 있기 때문에 현재 카메라나 라이다에서는 어떠한 증거도 생성하지 않을 수 있다. 강건한 관측 모델(Robust Observation Model)은 측정값의 부재(Absence of Measurement)와 존재하지 않는다는 증거(Evidence of Absence)를 구분해야 한다. 이러한 구분을 통해 월드 모델은 객체 영속성(Object Permanence)을 유지하고 새로운 관측이 해당 가설을 확인하거나 거부할 때까지 숨겨진 개체(Hidden Entity)에 대한 믿음을 유지할 수 있다.

멀티모달 관측 모델(Multimodal Observation Model)은 서로 다른 센서의 상호보완적인 특성을 활용할 수 있다. 시각적으로 모호한 객체라도 라이다에서는 명확한 기하 구조를 가질 수 있으며, 레이더는 가시성이 좋지 않은 환경에서도 움직임 정보를 제공할 수 있다. 여러 모달리티를 결합하면 모호성(Ambiguity)을 줄이고 강건성(Robustness)을 향상시킬 수 있지만, 성공적인 센서 융합(Sensor Fusion)을 위해서는 공간적 캘리브레이션(Spatial Calibration), 시간 동기화(Temporal Synchronization), 불확실성 처리, 그리고 서로 다른 센싱 메커니즘으로 생성된 측정값을 정렬할 수 있는 표현이 필요하다.

디코더 모델(Decoder Model) 역시 멀티모달(Multimodal) 형태로 구성할 수 있다. 하나의 공유 잠재 상태(Shared Latent State)로부터 이미지 특징(Image Feature), 깊이(Depth), 점유, 객체 상태(Object State), 고유수용성 측정값과 같은 여러 예상 관측을 디코딩할 수 있다. 하나의 잠재 표현이 여러 모달리티를 일관성 있게 예측할 수 있다면 각 센서에 공통으로 존재하는 근본적인 물리적 요소(Underlying Physical Factor)를 포착하도록 유도할 수 있다. 따라서 교차 모달 예측(Cross-Modal Prediction)은 단일 센서 스트림 이상의 세계 정보를 표현하는 상태를 학습하기 위한 강력한 학습 신호가 될 수 있다.

디코딩(Decoding)은 서로 다른 추상화 수준(Level of Abstraction)에서 수행될 수 있다. 저수준 디코더(Low-Level Decoder)는 픽셀, 깊이 값, 포인트 좌표(Point Coordinate), 파형(Waveform)을 복원할 수 있다. 중간 수준 디코더(Intermediate Decoder)는 분할(Segmentation), 옵티컬 플로우(Optical Flow), 점유, 객체 특징을 예측할 수 있다. 상위 수준 디코더(High-Level Decoder)는 의미론적 상태(Semantic State), 궤적(Trajectory), 어포던스, 사건(Event), 작업 결과(Task Outcome)를 출력할 수 있다. 계층적 월드 모델(Hierarchical World Model)은 여러 디코딩 수준을 동시에 지원하여 세부적인 지각과 추상적인 예측 및 계획을 연결할 수 있다.

생성형 디코더 모델(Generative Decoder Model)은 하나의 내부 상태가 여러 개의 가능한 관측이나 미래와 대응할 때 유용해진다. 하나의 평균적인 예측만 생성하는 대신 확률적 또는 생성형 디코더(Probabilistic or Generative Decoder)는 여러 대안적인 결과를 표현할 수 있다. 이는 미래 장면이 불확실한 인간 행동, 숨겨진 객체, 확률적 동역학(Stochastic Dynamics), 모호한 환경 조건에 의존할 때 특히 중요하다. 여러 가능한 예측(Multiple Plausible Predictions)을 유지하면 결정론적 복원(Deterministic Reconstruction)이 숨길 수 있는 불확실성을 보존할 수 있다.

관측 예측(Observation Prediction)은 이상 탐지(Anomaly Detection)와 모델 수정(Model Correction)에도 활용할 수 있다. 월드 모델이 센서가 무엇을 관측해야 하는지를 예측했지만 실제 측정값이 크게 다르다면, 이러한 차이는 예상하지 못한 환경 사건, 부정확한 상태 추정, 센서 고장(Sensor Failure), 잘못된 동역학 예측을 의미할 수 있다. 따라서 예측 오차(Prediction Error)는 학습을 위한 정보뿐만 아니라 내부 모델이 물리적 현실과 계속 일치하는지를 지속적으로 확인하는 정보도 제공한다.

능동 지각(Active Perception)은 관측 모델(Observation Model)을 반대 방향으로 활용한다. 즉, 에이전트는 어떤 행동이 가장 유용한 미래 관측(Informative Future Observation)을 만들어낼지를 추론한다. 장애물 주변으로 이동하면 가려진 영역을 확인할 수 있고, 카메라를 회전하면 객체에 대한 불확실성을 줄일 수 있으며, 표면을 접촉하면 재료 특성(Material Property)을 파악할 수 있다. 따라서 월드 모델은 행동이 물리적 상태를 어떻게 변화시키는지뿐만 아니라 그러한 변화가 이후 에이전트가 무엇을 관측할 수 있는지를 어떻게 변화시키는지도 예측할 수 있다.

잠재 월드 모델(Latent World Model)에서는 실제 배포(Deployment) 과정에서 디코더(Decoder)가 선택적인 구성 요소가 될 수도 있다. 시스템은 관측을 잠재 상태로 인코딩하고, 미래 잠재 상태를 예측하며, 원시 감각 데이터를 다시 복원하지 않고 잠재 공간(Latent Space)에서 직접 계획을 수행할 수 있다. 디코더는 여전히 학습, 디버깅(Debugging), 해석(Interpretation), 보조 예측(Auxiliary Prediction)에 유용할 수 있다. 이러한 분리는 추론 비용(Inference Cost)을 줄이면서 내부 모델의 용량을 행동에 직접 관련된 정보에 집중하도록 할 수 있다.

따라서 관측 모델(Observation Model) 또는 디코더 모델(Decoder Model)의 품질은 전체 피지컬 AI 시스템에서 수행하는 역할을 기준으로 평가해야 한다. 픽셀 수준 복원 품질(Pixel-Level Reconstruction Quality)은 일부 응용 분야에서는 중요할 수 있지만 일반적인 평가 기준으로는 충분하지 않다. 더욱 의미 있는 기준에는 물리적 상태와의 일관성(Consistency), 잡음과 가림에 대한 강건성, 멀티모달 일치성(Multimodal Agreement), 예측 정확도(Predictive Accuracy), 불확실성 보정(Uncertainty Calibration), 그리고 디코딩된 정보가 계획, 제어, 안전(Safety)에 얼마나 유용한지가 포함될 수 있다.

결국 관측 및 디코더 모델(Observation and Decoder Models)은 내부 세계 표현(Internal World Representation)과 측정 가능한 물리적 증거(Measurable Physical Evidence)를 연결한다. 관측 모델은 숨겨진 물리적 상태(Hidden Physical State)가 어떻게 센서 측정값을 생성하는지를 설명하고, 디코더는 내부 상태로부터 관측 가능한 결과를 복원하거나 예측한다. 이들은 인코더(Encoder) 및 동역학 모델(Dynamics Model)과 함께 관측--표현--시간적 예측--예상 감각 증거--현실 기반 수정(Observation--Representation--Temporal Prediction--Expected Sensory Evidence--Reality-Based Correction)의 순환 구조를 형성하며, 월드 모델이 물리적 세계에 지속적으로 기반(Grounded)하도록 한다.

## 01.08. Representation vs Prediction

![](images/image8.png){width="7.268055555555556in" height="7.268055555555556in"}

표현(Representation)과 예측(Prediction)은 월드 모델(World Model)의 핵심을 구성하는 두 가지 상호보완적 기능이다. 표현은 지능형 에이전트(Intelligent Agent)가 현재 세계에 관한 정보를 내부 상태(Internal State)로 어떻게 구성하는지를 결정하고, 예측은 그 상태가 시간에 따라 어떻게 변화할 수 있는지를 결정한다. 유용한 피지컬 AI(Physical AI) 시스템에는 두 기능이 모두 필요하다. 표현이 없으면 추론을 위한 구조화된 기반이 존재하지 않으며, 예측이 없으면 표현은 미래를 예상하기보다 현재를 설명하는 수준에 머무르게 된다.

표현(Representation)은 "에이전트가 현재 상황에 대해 무엇을 알고 있어야 하는가?"라는 질문을 다룬다. 카메라(Camera), 라이다(LiDAR), 레이더(Radar), 고유수용성 감각(Proprioception), 기타 센서에서 들어오는 원시 관측(Raw Observation)은 방대한 정보를 포함하지만 모든 정보가 행동에 필요한 것은 아니다. 표현은 이러한 관측을 압축하여 기하 구조(Geometry), 객체(Object), 움직임(Motion), 의미론(Semantics), 물리적 관계(Physical Relationship), 불확실성(Uncertainty), 체화된 에이전트(Embodied Agent)의 상태와 같은 유용한 속성을 보존하는 변수 또는 특징으로 변환한다.

예측(Prediction)은 다른 질문을 다룬다. 즉, "에이전트가 현재 알고 있는 것을 바탕으로 다음에 무엇이 발생할 수 있는가?"이다. 예측 모델(Predictive Model)은 표현된 상태, 최근 이력(Recent History), 행동(Action), 환경 동역학(Environmental Dynamics)을 이용하여 미래 상태(Future State) 또는 미래 관측(Future Observation)을 추정한다. 하나 또는 여러 미래 시간 단계에 걸쳐 객체 움직임, 로봇 변위(Robot Displacement), 접촉 결과(Contact Outcome), 지형 상호작용(Terrain Interaction), 인간 행동(Human Behavior), 충돌 위험(Collision Risk), 기타 작업 관련 결과(Task-Relevant Consequence)를 예측할 수 있다.

이러한 차이는 상태 (z_t)와 전이 모델(Transition Model) (f)를 통해 개념적으로 표현할 수 있다. 인코더(Encoder)는 이용 가능한 관측과 상호작용 이력(Interaction History)으로부터 (z_t=E(o_{\\leq t},a_{\<t}))를 구성하며, 예측은 (z_{t+1}=f(z_t,a_t))를 추정한다. 따라서 표현은 예측기가 사용할 수 있는 정보를 결정하고, 예측은 그 정보가 미래 행동과 관련된 동역학을 설명하기에 충분한지를 검증한다.

어떤 표현(Representation)은 지각(Perception)에는 유용하지만 반드시 예측(Prediction)에 유용한 것은 아니다. 예를 들어 객체 범주(Object Category)를 인식하도록 최적화된 특징은 자동차, 보행자, 건물을 정확하게 구별하면서도 정밀한 속도, 깊이(Depth), 접촉(Contact), 물리적 상호작용(Physical Interaction) 정보를 제거할 수 있다. 이러한 표현은 정적 인식 벤치마크(Static Recognition Benchmark)에서는 우수한 성능을 보일 수 있지만 행동에 따라 물리적 장면이 어떻게 변화할지를 예측하기에는 충분한 정보를 제공하지 못할 수 있다.

반대로 예측적 표현(Predictive Representation)은 관측 가능한 모든 세부 정보를 보존할 필요가 없다. 벽의 색상 패턴(Color Pattern)은 시각적으로 뚜렷하지만 로봇 움직임에는 중요하지 않을 수 있는 반면, 바닥의 경사(Slope)는 시각적으로 덜 중요해 보여도 주행 가능성(Traversability)에 큰 영향을 미칠 수 있다. 따라서 예측은 모든 감각 정보를 동일하게 중요하게 취급하기보다 미래 변화와 행동 결과에 영향을 미치는 변수를 내부 상태에 보존하도록 유도한다.

이러한 관점은 예측 충분성(Predictive Sufficiency)이라는 개념으로 이어진다. 내부 표현(Internal Representation)은 에이전트의 작업에 필요한 미래의 측면을 예측하기에 충분한 정보를 포함할 때 유용하다. 내비게이션(Navigation)에서는 점유(Occupancy), 움직임, 주행 가능성, 충돌 관계(Collision Relationship)가 포함될 수 있다. 조작(Manipulation)에서는 객체 자세(Object Pose), 접촉, 기하 구조, 물리적 속성이 포함될 수 있다. 따라서 적절한 표현은 시스템이 무엇을 예측하고 제어해야 하는지에 따라 달라진다.

예측(Prediction)은 표현(Representation)을 학습하기 위한 학습 목표(Learning Objective)로도 활용될 수 있다. 모든 상태 변수를 사람이 직접 정의하는 대신, 모델이 미래 관측, 잠재 상태(Latent State), 행동 또는 작업 결과를 예측하도록 하여 내부 표현을 학습할 수 있다. 미래 사건을 지속적으로 예측하는 데 도움이 되는 특징은 유지되는 반면 예측할 수 없거나 관련성이 낮은 세부 정보는 상대적으로 덜 강조될 수 있다. 따라서 자기지도 시간 예측(Self-Supervised Temporal Prediction)은 대규모 센서 데이터셋으로부터 유용한 세계 표현을 학습하는 자연스러운 방법을 제공한다.

그러나 예측(Prediction)만으로 이상적인 표현(Representation)이 자동으로 만들어지는 것은 아니다. 원시 비디오(Raw Video)를 예측하도록 학습된 모델은 물리적 의사결정에 거의 기여하지 않는 질감(Texture), 조명(Lighting), 배경 움직임(Background Motion), 기타 시각적으로 예측 가능한 세부 사항에 상당한 모델 용량(Model Capacity)을 사용할 수 있다. 따라서 무엇을 예측 대상으로 설정하는지가 중요하다. 월드 모델 학습(World-Model Learning)은 계획(Planning), 제어(Control), 안전(Safety), 상호작용(Interaction), 물리적 동역학 이해에 관련된 미래 정보의 정확성을 강조해야 한다.

표현과 예측은 명시적 공간(Explicit Space) 또는 잠재 공간(Latent Space)에서 작동할 수 있다. 명시적 표현(Explicit Representation)은 위치(Position), 속도(Velocity), 점유, 객체 상태(Object State), 지형 분류(Terrain Class)와 같이 해석 가능한 값을 사용하여 이러한 변수의 미래 값을 직접 예측할 수 있도록 한다. 잠재 표현(Latent Representation)은 정보를 학습된 벡터(Learned Vector) 또는 특징 맵(Feature Map)으로 인코딩한다. 잠재 예측(Latent Prediction)은 모든 관련 물리 변수를 사람이 직접 정의하지 않고도 복잡한 동역학을 포착할 수 있다.

명시적 예측(Explicit Prediction)은 해석 가능성(Interpretability)을 제공하며 기존 로보틱스(Conventional Robotics)와 편리하게 통합할 수 있다. 엔지니어는 예측된 궤적(Trajectory), 속도, 점유, 충돌 확률(Collision Probability), 로봇 상태(Robot State)를 직접 확인하고 계획 알고리즘(Planning Algorithm)에 연결할 수 있다. 그러나 미리 정의된 변수에 중요한 정보가 누락될 수 있다는 한계가 있다. 잠재 예측은 표현의 유연성(Representational Flexibility)이 더 높지만 모델이 무엇을 알고 있으며 왜 특정 미래를 예측했는지를 파악하기 어려울 수 있다.

하이브리드 표현(Hybrid Representation)은 실용적인 절충안을 제공한다. 월드 모델은 안전과 제어에 중요한 정보를 명시적으로 표현하면서 복잡한 상황 정보(Contextual Information)나 물리적 정보를 잠재 특징(Latent Feature)으로 유지할 수 있다. 예를 들어 로봇은 자세(Pose), 점유, 추적 객체(Tracked Object), 불확실성을 명시적으로 표현하면서 지형 외형(Terrain Appearance), 상호작용 패턴(Interaction Pattern), 숨겨진 환경 속성(Hidden Environmental Property)을 잠재 특징으로 인코딩하여 전이 예측(Transition Prediction)을 향상시킬 수 있다.

표현(Representation)과 예측(Prediction)의 관계는 부분 관측 가능성(Partial Observability)에서 특히 중요해진다. 현재 관측만으로는 미래를 정확하게 예측하기 위한 충분한 정보가 없을 수 있다. 따라서 표현은 이전 관측과 행동으로부터 얻은 기억(Memory)을 통합해야 한다. 일시적으로 가려진 보행자, 이전에 관측한 지형, 숨겨진 객체에 관한 정보는 현재 센서 측정에서 사라지더라도 내부 상태에 계속 인코딩되어 유지될 수 있다.

예측(Prediction)은 이러한 기억(Memory)의 품질을 검증할 수도 있다. 내부 표현이 중요한 과거 정보를 보존한다면 일시적으로 감각 정보가 사라지더라도 미래 관측과 사건을 계속 예측할 수 있어야 한다. 객체가 가려지거나 시야(Field of View)를 벗어날 때마다 예측이 실패한다면 표현이 현재 관측에 지나치게 의존하고 있을 가능성이 있다. 따라서 시간적 예측(Temporal Prediction)은 모델이 프레임 단위 설명(Frame-by-Frame Description)이 아니라 지속적인 상태(Persistent State)를 형성하도록 유도한다.

불확실성(Uncertainty) 역시 표현과 예측을 연결해야 한다. 현재 상태에는 객체 위치, 지형 마찰(Terrain Friction), 다른 에이전트의 의도(Intention), 숨겨진 영역(Hidden Region)에 관한 불확실성이 포함될 수 있다. 예측은 이러한 불확실성을 하나의 결정론적 결과(Deterministic Outcome)로 성급하게 축소하지 않고 미래 상태로 전파해야 한다. 따라서 강력한 표현은 모델이 무엇을 믿는지뿐만 아니라 무엇이 여전히 모호한지도 인코딩하여 필요한 경우 예측이 여러 개의 가능한 미래(Plausible Future)를 생성할 수 있도록 한다.

예측 시간 범위(Prediction Horizon)는 표현이 어떤 정보를 보존해야 하는지를 변화시킨다. 매우 단기적인 예측은 주로 국소적 움직임(Local Motion)과 동역학에 의존할 수 있지만, 장기 예측에는 의미론적 맥락(Semantic Context), 목표(Goal), 상호작용 이력, 환경 구조(Environmental Structure), 상위 수준 행동(High-Level Behavior)이 필요할 수 있다. 따라서 수 밀리초 이후만을 예측하도록 최적화된 표현은 수 초 또는 수 분 이후의 계획을 지원하도록 설계된 표현과 크게 다를 수 있다.

계층적 월드 모델(Hierarchical World Model)은 여러 스케일에서 표현과 예측을 결합하여 이러한 문제를 해결할 수 있다. 빠르게 변화하는 저수준 상태(Low-Level State)는 움직임, 접촉, 즉각적인 제어를 모델링하고, 느리게 변화하는 상위 수준 상태(High-Level State)는 객체, 사건(Event), 의도, 경로(Route), 작업 진행 상태(Task Progress)를 표현할 수 있다. 이에 대응하는 시간 해상도(Temporal Resolution)에서 예측을 수행함으로써 세밀한 단기 동역학과 추상적인 장기 변화를 하나의 월드 모델 아키텍처 안에서 함께 다룰 수 있다.

예측 오차(Prediction Error)는 표현(Representation)을 개선하기 위한 피드백 메커니즘(Feedback Mechanism)을 제공한다. 예측된 미래가 이후 실제 관측과 다르다면 문제는 동역학 모델(Dynamics Model), 상태 표현(State Representation), 또는 두 요소 모두에 있을 수 있다. 반복적인 오차는 내부 상태에서 중요한 변수가 누락되었다는 사실을 드러낼 수 있다. 예를 들어 로봇이 서로 다른 지형에서 바퀴 움직임을 반복적으로 잘못 예측한다면 표면 특성(Surface Property)이나 미끄러짐 상태(Slip Condition)를 더욱 명시적으로 표현할 필요가 있을 수 있다.

따라서 표현 품질(Representation Quality)은 복원 정확도(Reconstruction Accuracy)나 분류 정확도(Classification Accuracy)만으로 평가해서는 안 된다. 시각적으로 세밀한 내부 표현이라도 행동에 필요한 인과적 정보(Causal Information)를 보존하지 못할 수 있으며, 반대로 압축된 표현이 물리적 결과를 매우 정확하게 예측할 수도 있다. 월드 모델에서는 표현된 상태가 안정적인 다단계 예측(Multi-Step Prediction), 행동 조건부 추론(Action-Conditioned Reasoning), 불확실성 추정(Uncertainty Estimation), 효과적인 다운스트림 계획(Downstream Planning)을 지원하는지를 평가해야 한다.

마찬가지로 예측 품질(Prediction Quality)도 의사결정 관련성(Decision Relevance)과 독립적으로 평가해서는 안 된다. 중요하지 않은 시각적 세부 정보를 완벽하게 예측하더라도 자율 행동(Autonomous Behavior)에 거의 기여하지 않을 수 있다. 가장 유용한 예측기는 의사결정, 안전, 작업 성공(Task Success)을 변화시킬 수 있는 상태 변화에 대해 높은 정확성을 유지한다. 이러한 원리는 선택적 모델링(Selective Modeling)을 유도하며, 계산 자원(Computational Resource)을 체화된 에이전트에게 실제로 중요한 미래 정보의 불확실성과 변화에 집중하도록 한다.

표현(Representation)과 예측(Prediction)은 계획(Planning)과도 상호작용한다. 계획에는 여러 대안 행동(Alternative Action)을 평가할 수 있는 상태와 그 결과를 추정하는 예측 메커니즘(Predictive Mechanism)이 필요하다. 동일한 표현에서 시작하여 모델은 서로 다른 행동 시퀀스(Action Sequence)를 미래로 롤아웃(Rollout)하고 예측된 결과를 비교할 수 있다. 표현은 시작점과 관련 변수를 제공하고, 예측은 후보 행동(Candidate Behavior)을 평가할 수 있는 상상된 미래(Imagined Future)를 생성한다.

따라서 이 관계는 단방향(One-Directional)이 아니라 순환적(Circular)이다. 더 나은 표현은 중요한 인과적·시간적 정보(Causal and Temporal Information)를 보존하기 때문에 예측을 향상시킨다. 더 나은 예측 목표(Predictive Objective)는 미래 변화에 중요한 정보를 모델이 인코딩하도록 유도하기 때문에 표현을 향상시킨다. 계획은 어떤 미래 결과가 행동적으로 중요한지를 정의함으로써 두 요소 모두에 추가적인 영향을 준다. 따라서 월드 모델 설계(World-Model Design)는 표현, 예측, 행동(Action)을 공동으로 최적화되는 하나의 시스템으로 다루어야 한다.

피지컬 AI(Physical AI)의 궁극적인 목표는 현재에 대한 가장 풍부한 설명을 구축하거나 미래에 대한 가장 시각적으로 인상적인 예측을 생성하는 것이 아니다. 목표는 중요한 정보를 포착하는 내부 상태를 구성하고, 행동과 외부 영향(External Influence)에 따라 이러한 관련 요소가 어떻게 변화할 수 있는지를 설명하는 예측 과정을 구축하는 것이다. 표현은 에이전트에게 현재 자신이 어떤 세계에 존재하는지를 알려주고, 예측은 다음에 마주칠 수 있는 세계에 대해 추론할 수 있도록 한다.

따라서 유능한 월드 모델(World Model)은 표현(Representation)과 예측(Prediction) 사이의 균형을 통해 형성된다. 표현은 감각적 경험(Sensory Experience)을 지속적이고 행동 가능한 지식(Actionable Knowledge)으로 압축하고, 예측은 그 지식을 가능한 미래 궤적(Future Trajectory)과 결과로 변환한다. 두 기능은 함께 지각(Perception)을 수동적인 설명에서 선제적 지능(Anticipatory Intelligence)으로 전환하며, 체화된 에이전트가 현재 상황이 미래에 무엇을 의미하는지를 이해하고 그 미래가 현실이 되기 전에 어떤 행동을 취해야 하는지를 판단할 수 있도록 한다.

## 01.09. Spatial Temporal and Semantic State

![](images/image9.png){width="7.268055555555556in" height="7.268055555555556in"}

공간적 상태(Spatial State), 시간적 상태(Temporal State), 의미론적 상태(Semantic State)는 월드 모델(World Model)이 물리적 현실(Physical Reality)을 구성하는 세 가지 상호보완적 차원이다. 공간적 상태는 개체(Entity)와 구조물이 어디에 위치하는지를 설명하고, 시간적 상태는 이들이 시간에 따라 어떻게 지속되고 변화하는지를 설명하며, 의미론적 상태는 이러한 개체가 무엇을 의미하는지를 설명한다. 피지컬 AI(Physical AI)는 위치, 변화, 의미를 동시에 고려해야 지능적인 행동이 가능하므로 이 세 가지 상태의 통합이 필요하다.

공간적 상태(Spatial State)는 환경(Environment)과 그 안에 존재하는 체화된 에이전트(Embodied Agent)의 기하학적 구성(Geometric Organization)을 표현한다. 여기에는 로봇 자세(Robot Pose), 객체 위치(Object Position), 방향(Orientation), 크기(Size), 거리(Distance), 자유 공간(Free Space), 점유 영역(Occupied Region), 표면(Surface), 지형(Terrain), 개체 사이의 관계(Relationship)가 포함될 수 있다. 응용 분야에 따라 이러한 속성은 미터법 좌표(Metric Coordinate), 점유 격자(Occupancy Grid), 포인트 클라우드(Point Cloud), 복셀(Voxel), 메시(Mesh), 조감도 맵(Bird's-Eye-View Map), 객체 상태(Object State), 또는 학습된 공간 특징(Learned Spatial Feature)을 통해 표현할 수 있다.

유용한 공간적 표현(Spatial Representation)은 위치와 움직임을 해석하는 기준 좌표계(Reference Frame)를 설정해야 한다. 정보는 로봇, 로컬 맵(Local Map), 전역 좌표계(Global Coordinate System), 또는 개별 객체를 기준으로 표현할 수 있다. 이러한 좌표계 사이의 변환(Transformation)을 통해 움직이는 센서에서 수집된 관측을 일관성 있게 통합할 수 있다. 이러한 정렬(Alignment)이 없다면 서로 다른 위치와 시간에서 수집된 측정값을 하나의 지속적인 물리적 환경으로 신뢰성 있게 표현하기 어렵다.

공간적 표현(Spatial Representation)은 단순한 기하학적 복원(Geometric Reconstruction)에 한정되지 않는다. 피지컬 AI(Physical AI)에서 기하 구조는 상호작용(Interaction)을 지원할 때 실질적인 의미를 갖는다. 시스템은 자유 공간과 점유 공간, 도달 가능한 영역과 접근할 수 없는 영역, 안정적인 표면과 위험한 지형을 구별해야 한다. 따라서 여유 공간(Clearance), 연결성(Connectivity), 가시성(Visibility), 충돌 관계(Collision Relationship), 지지 영역(Support Region), 주행 가능성(Traversability)이 가능한 행동에 영향을 준다면 공간적 상태의 일부가 될 수 있다.

시간적 상태(Temporal State)는 이러한 공간적 설명에 지속성(Persistence)과 변화(Change)를 추가한다. 하나의 관측은 단지 순간적인 장면(Snapshot)을 제공하지만, 자율 행동(Autonomous Behavior)을 위해서는 이전에 무엇이 존재했는지, 현재 무엇이 움직이고 있는지, 다음에 무엇이 발생할 수 있는지를 이해해야 한다. 시간적 상태에는 속도(Velocity), 가속도(Acceleration), 궤적(Trajectory), 객체 이력(Object History), 접촉 지속시간(Contact Duration), 사건 시퀀스(Event Sequence), 그리고 여러 시간 단계에 걸친 물리적 조건의 변화를 설명하는 기타 변수가 포함될 수 있다.

시간적 표현(Temporal Representation)은 영구적인 구조(Permanent Structure)와 일시적인 조건(Transient Condition)을 구별할 수 있도록 한다. 건물이나 고정된 벽은 장기간 안정적으로 유지될 수 있지만, 보행자, 차량, 이동 가능한 객체, 날씨의 영향, 로봇 구성(Robot Configuration)은 빠르게 변화할 수 있다. 이러한 서로 다른 변화 속도를 표현하면 월드 모델이 계산 자원(Computational Resource)을 적절하게 배분할 수 있으며, 일시적인 관측으로 인해 지속적인 환경 지식(Persistent Environmental Knowledge)이 불필요하게 변경되는 것을 방지할 수 있다.

객체 지속성(Object Persistence)은 특히 중요한 시간적 속성이다. 객체는 가려지거나 센서의 시야(Field of View)를 벗어났다고 해서 일반적으로 존재하지 않게 되는 것은 아니다. 월드 모델은 시간에 걸쳐 관측을 연관시킴으로써 지속적인 개체(Persistent Entity)를 유지하고 새로운 증거가 확보될 때마다 추정 상태를 갱신할 수 있다. 이러한 연속성(Continuity)은 숨겨진 객체(Hidden Object), 다시 나타나는 에이전트, 이동 이력(Motion History), 단일 센서 프레임을 넘어 지속되는 상호작용에 대한 추론을 가능하게 한다.

시간적 상태(Temporal State)는 움직임과 이력이 미래 변화에 관한 증거를 제공하기 때문에 예측(Prediction)과 밀접하게 관련된다. 보행자의 현재 위치만으로는 제한적인 정보를 얻을 수 있지만, 수 초 동안의 궤적을 함께 사용하면 이동 방향과 속도를 파악할 수 있다. 마찬가지로 최근의 바퀴 미끄러짐(Wheel Slip)은 변화하는 지형 상호작용(Terrain Interaction)을 나타낼 수 있다. 따라서 시간적 맥락(Temporal Context)은 고립된 공간 측정값을 예측, 계획(Planning), 선제적 제어(Anticipatory Control)를 지원하는 동적 상태 추정(Dynamic State Estimate)으로 변환한다.

의미론적 상태(Semantic State)는 표현된 세계를 구성하는 요소가 무엇이며 왜 중요한지를 설명한다. 기하 구조(Geometry)는 어떤 영역에 3차원 구조물이 존재한다는 사실을 나타낼 수 있지만, 의미론(Semantics)은 그것을 보행자, 차량, 벽, 문, 팔레트(Pallet), 계단, 도로 또는 식생(Vegetation)으로 식별할 수 있다. 물리적으로 유사한 구조라도 내비게이션(Navigation), 조작(Manipulation), 상호작용, 안전(Safety)에 서로 다른 의미를 가질 수 있으므로 이러한 구별은 행동에 직접적인 영향을 준다.

의미론적 표현(Semantic Representation)은 범주형 레이블(Categorical Label)을 넘어 확장될 수 있다. 속성(Property), 기능(Function), 관계(Relationship), 어포던스(Affordance), 역할(Role), 작업 관련성(Task Relevance)을 인코딩할 수 있다. 예를 들어 문은 단순히 문이라는 객체가 아니라 열 수 있는 통로(Openable Passage)로 표현할 수 있고, 컨테이너(Container)는 객체를 담을 수 있는 대상으로 인식할 수 있으며, 표면은 주행 가능하거나 파지 가능한 대상으로 식별할 수 있다. 따라서 의미론은 지각된 개체를 가능한 행동과 예상되는 물리적 결과에 연결한다.

개체 사이의 관계(Relationship among Entities)는 또 다른 중요한 의미론적 구조(Semantic Structure)를 제공한다. 사람은 차량 내부에 있을 수 있고, 객체는 테이블 위에 놓여 있을 수 있으며, 로봇은 출입구(Doorway)에 접근할 수 있고, 하나의 객체가 다른 객체에 대한 접근을 막을 수도 있다. 내부(Inside), 위(On), 뒤(Behind), 연결됨(Connected To), 지지함(Supporting), 접근함(Approaching), 상호작용함(Interacting)과 같은 관계를 표현하면 개별적인 객체 설명을 구조화된 상황 모델(Structured Situation Model)로 변환할 수 있다.

공간적·시간적·의미론적 정보(Spatial, Temporal, and Semantic Information)는 서로 독립적인 계층으로 다루어서는 안 된다. 이동 로봇 근처에 보행자가 있다고 가정하면, 공간적 상태는 로봇을 기준으로 보행자의 위치를 설명하고, 시간적 상태는 움직임과 최근 궤적을 설명하며, 의미론적 상태는 해당 개체가 행동적으로 중요한 특성을 가진 사람임을 식별한다. 이 세 차원을 결합하면 각각을 독립적으로 사용하는 것보다 훨씬 풍부한 정보를 얻을 수 있다.

이들의 통합은 예측(Prediction)에서 특히 중요하다. 단순히 어떤 영역이 점유되어 있다는 사실만으로는 제한적인 예측 정보만 얻을 수 있다. 그러나 해당 영역에 횡단보도를 향해 움직이는 보행자가 있다는 것을 알면 미래 점유(Future Occupancy)를 예측할 수 있는 훨씬 강력한 기반이 형성된다. 의미론적 정체성(Semantic Identity)은 가능한 행동을 제한하고, 시간적 정보는 현재의 변화를 설명하며, 공간적 정보는 예측된 행동이 로봇의 미래 경로와 교차할지를 결정한다.

동일한 원리는 조작(Manipulation)에도 적용된다. 공간적 상태는 객체의 자세(Object Pose)와 기하 구조를 표현할 수 있고, 시간적 상태는 움직임과 접촉 이력(Contact History)을 설명할 수 있으며, 의미론적 상태는 객체 유형(Object Type), 기능, 어포던스를 설명할 수 있다. 객체를 어떻게 파지하거나 이동할지를 결정하는 로봇은 객체가 어디에 있는지, 어떻게 움직이고 있는지, 어떤 종류의 상호작용이 적절한지를 모두 알아야 하므로 세 가지 상태를 함께 활용하는 것이 유리하다.

밀집 공간 표현(Dense Spatial Representation)과 객체 중심 의미론적 표현(Object-Centric Semantic Representation)은 동일한 월드 모델 안에서 함께 존재할 수 있다. 점유(Occupancy) 또는 조감도 특징(BEV Feature)은 연속적인 자유 공간과 분류되지 않은 장애물을 설명할 수 있으며, 지속적인 객체 상태는 인식된 개체를 표현할 수 있다. 시간적 메커니즘(Temporal Mechanism)은 두 형태의 표현을 모두 갱신할 수 있다. 이러한 하이브리드 구성(Hybrid Organization)은 모든 물리적 구조에 의미론적 정체성을 부여해야만 계획이나 충돌 회피(Collision Avoidance)에 활용할 수 있는 문제를 방지한다.

의미론적 상태(Semantic State)는 여러 추상화 수준(Level of Abstraction)에서도 작동할 수 있다. 저수준 의미론(Low-Level Semantics)은 표면 클래스(Surface Class)와 객체 범주를 설명하고, 상위 수준 의미론(High-Level Semantics)은 활동(Activity), 의도(Intention), 사건(Event), 상황(Situation)을 표현할 수 있다. 차량은 하나의 객체로 표현될 수 있지만, 그 행동은 추가적으로 주차(Parking), 양보(Yielding), 추월(Overtaking), 접근(Approaching)으로 해석될 수 있다. 이러한 상위 수준의 의미는 장기 예측(Long-Horizon Prediction)과 의사결정(Decision Making)을 크게 향상시킬 수 있다.

시간적 추상화(Temporal Abstraction) 역시 여러 시간 스케일(Time Scale)에 걸쳐 구성할 수 있다. 밀리초 수준의 상태는 액추에이터 반응(Actuator Response)과 몸체 움직임(Body Motion)을 설명할 수 있고, 초 단위 상태는 궤적과 상호작용을 표현할 수 있으며, 더 긴 시간 범위에서는 내비게이션 진행 상태(Navigation Progress), 작업 단계(Task Phase), 반복적인 환경 패턴(Recurring Environmental Pattern)을 설명할 수 있다. 계층적 월드 모델(Hierarchical World Model)은 모든 물리적 과정을 하나의 동일한 갱신 주기(Update Frequency)에 맞추는 대신 이러한 여러 시간 스케일을 동시에 유지할 수 있다.

공간적 추상화(Spatial Abstraction) 역시 여러 스케일을 활용할 수 있다. 세밀한 국소 기하 구조(Fine Local Geometry)는 즉각적인 충돌 회피, 발판 선택(Foothold Selection), 조작에 중요하지만, 더 큰 규모의 지도는 경로 계획(Route Planning)과 환경적 맥락(Environmental Context)을 지원한다. 따라서 월드 모델은 에이전트 주변에서는 상세한 상태를 유지하면서 더 먼 영역이나 장기 예측 시간 범위에서는 점차 거친 표현(Coarser Representation)을 사용하여 계산 비용과 의사결정 관련성(Decision Relevance) 사이의 균형을 맞출 수 있다.

불확실성(Uncertainty)은 세 가지 차원 모두에서 표현되어야 한다. 공간적 불확실성(Spatial Uncertainty)은 위치나 기하 구조와 관련될 수 있고, 시간적 불확실성(Temporal Uncertainty)은 움직임과 미래 궤적에 관련될 수 있으며, 의미론적 불확실성(Semantic Uncertainty)은 정체성, 의도, 어포던스에 관련될 수 있다. 이러한 불확실성은 서로 연결되는 경우가 많다. 예를 들어 관측된 개체가 보행자인지 정적 객체인지에 대한 불확실성은 고려해야 하는 가능한 미래 움직임의 범위를 직접 변화시킨다.

부분 관측 가능성(Partial Observability)은 이러한 통합 상태가 본질적으로 기억(Memory)에 의존하도록 만든다. 공간 영역이 가려질 수 있고, 시간적 궤적이 중단될 수 있으며, 의미론적 정체성이 계속 모호하게 남을 수도 있다. 과거 관측(Historical Observation)을 사용하면 추가적인 증거가 확보될 때까지 시스템이 여러 가설(Hypothesis)을 유지할 수 있다. 따라서 결과적으로 형성되는 상태는 단순히 현재 센서 입력을 설명하는 것이 아니라 주변 세계를 시간에 걸쳐 축적하여 해석한 결과(Temporally Accumulated Interpretation)이다.

멀티모달 센싱(Multimodal Sensing)은 이러한 세 가지 차원에 서로 다른 정보를 제공한다. 라이다와 깊이 센싱(Depth Sensing)은 강력한 기하학적 증거(Geometric Evidence)를 제공하고, 카메라는 풍부한 의미론적 단서(Semantic Cue)를 제공하며, 레이더는 움직임 추정(Motion Estimation)을 향상시킬 수 있고, 고유수용성 센서(Proprioceptive Sensor)는 로봇 자체의 공간적·시간적 상태를 설명한다. 센서 융합(Sensor Fusion)은 센싱 모달리티별로 서로 관련 없는 설명을 유지하는 것이 아니라 이러한 상호보완적 신호를 하나의 일관된 표현(Coherent Representation)으로 통합해야 한다.

체화 지능(Embodied Intelligence)을 위해서는 에이전트 자체 역시 공간적·시간적·의미론적으로 표현되어야 한다. 에이전트의 자세와 기하 구조는 공간 관계(Spatial Relationship)를 결정하고, 속도와 행동 이력(Action History)은 시간적 변화를 정의하며, 능력(Capability), 제약(Constraint), 목표(Goal), 역할(Role)은 어떤 환경 특징이 행동적으로 의미가 있는지를 결정한다. 따라서 동일한 환경이라도 서로 다른 체화 형태(Embodiment)와 작업을 가진 로봇에게는 서로 다른 행동 가능한 세계 상태(Actionable World State)가 형성될 수 있다.

적절한 상태 표현(State Representation)은 궁극적으로 미래의 의사결정을 변화시키는 정보를 보존해야 한다. 공간적 세부 정보는 움직임이나 상호작용에 영향을 줄 때 가치가 있고, 시간적 세부 정보는 예측을 향상시킬 때 가치가 있으며, 의미론적 세부 정보는 의미가 가능한 행동을 변화시킬 때 가치가 있다. 관련성이 낮은 정보를 지나치게 표현하면 지능을 반드시 향상시키지 않으면서 계산 비용만 증가시키지만, 중요한 정보가 누락되면 예측과 계획의 신뢰성이 저하될 수 있다.

결국 공간적 상태(Spatial State), 시간적 상태(Temporal State), 의미론적 상태(Semantic State)는 감각 측정(Sensory Measurement)을 동적인 물리적 세계에 대한 구조화된 이해(Structured Understanding)로 변환한다. 공간적 표현은 사물이 어디에 있는지를 설정하고, 시간적 표현은 그것이 어떻게 지속되고 변화하는지를 설명하며, 의미론적 표현은 그것이 무엇이고 행동에 어떤 의미를 갖는지를 식별한다. 이들의 통합은 현재를 이해하고, 과거를 보존하며, 미래를 예상하고, 물리적으로 의미 있는 행동(Physically Meaningful Action)을 선택할 수 있는 월드 모델(World Model)의 기반을 제공한다.

## 01.10. Short vs Long Horizon Prediction

![](images/image10.png){width="7.268055555555556in" height="7.268055555555556in"}

예측 시간 범위(Prediction Horizon)는 월드 모델(World Model)이 내부 상태(Internal State)의 변화를 미래의 어느 시점까지 추정하려 하는지를 결정한다. 단기 예측(Short-Horizon Prediction)은 밀리초 또는 수 초 동안 발생하는 즉각적인 변화에 집중하는 반면, 장기 예측(Long-Horizon Prediction)은 더 먼 미래의 상태(State), 사건(Event), 결과(Consequence)까지 추론을 확장한다. 피지컬 AI(Physical AI)는 두 가지 모두를 필요로 한다. 안전한 제어(Safe Control)는 즉각적인 동역학(Dynamics)에 의존하지만, 목적 지향적인 자율 행동(Autonomous Behavior)은 바로 다음 순간을 넘어선 미래에 대한 예측을 필요로 하기 때문이다.

단기 예측(Short-Horizon Prediction)은 국소적인 물리 동역학(Local Physical Dynamics)과 밀접하게 연결되어 있다. 이 시간 범위에서 모델은 위치(Position), 속도(Velocity), 가속도(Acceleration), 방향(Orientation), 관절 구성(Joint Configuration), 접촉(Contact), 바퀴 미끄러짐(Wheel Slip), 주변 객체의 움직임과 같은 상태 변화를 추정할 수 있다. 현재 상태와 예측 상태 사이의 시간 간격이 비교적 짧기 때문에 즉각적인 물리적 제약(Physical Constraint)이 가능한 결과를 강하게 결정하며, 예측 역시 상대적으로 높은 정밀도를 유지할 수 있다.

이동 로봇(Mobile Robot)의 경우 단기 예측은 수십 또는 수백 밀리초 이후부터 수 초 이내에 로봇과 주변 객체가 어디에 위치할지를 추정할 수 있다. 이러한 예측은 충돌 회피(Collision Avoidance), 제동(Braking), 조향 보정(Steering Correction), 국소 궤적 추종(Local Trajectory Tracking), 동적 장애물 대응(Dynamic Obstacle Response)을 지원한다. 조작(Manipulation)이나 이동 운동(Locomotion)에서는 동일한 시간 범위가 접촉 전이(Contact Transition), 관절 움직임, 파지 안정성(Grasp Stability), 발판 상호작용(Foothold Interaction), 액추에이터 명령(Actuator Command)의 즉각적인 결과를 설명할 수 있다.

장기 예측(Long-Horizon Prediction)은 이와 다른 종류의 문제를 다룬다. 단순히 다음 시간 단계에서 객체가 어디에 위치할지만 묻는 것이 아니라, 상황(Situation), 상호작용(Interaction), 경로(Route), 작업(Task)이 여러 미래 단계에 걸쳐 어떻게 전개될지를 추정할 수 있다. 관련 변수에는 행동 의도(Behavioral Intent), 목적지(Destination), 작업 진행 상태(Task Progress), 환경 변화(Environmental Change), 상호작용 결과(Interaction Outcome), 그리고 순간적인 동역학만으로는 신뢰성 있게 추론하기 어려운 상위 수준 사건(High-Level Event)이 포함될 수 있다.

따라서 단기와 장기 시간 범위의 차이는 단순히 예측하는 시간 단계의 개수가 다르다는 의미가 아니다. 서로 다른 시간 범위에는 서로 다른 정보(Information), 추상화(Abstraction), 모델(Model)이 필요할 수 있다. 단기 예측은 연속적인 물리 동역학(Continuous Physical Dynamics)을 강조하는 경우가 많지만, 장기 예측으로 갈수록 의미론(Semantics), 목표(Goal), 맥락(Context), 기억(Memory), 상호작용 패턴(Interaction Pattern), 그리고 에이전트와 환경이 장시간에 걸쳐 어떻게 행동하는지에 관한 가정이 더욱 중요해진다.

예측 불확실성(Prediction Uncertainty)은 일반적으로 시간 범위가 길어질수록 증가한다. 차량이 0.1초 후에 어디에 위치할지는 현재 움직임을 이용하여 비교적 정확하게 추정할 수 있지만, 수 초 후의 위치는 아직 발생하지 않은 회전, 제동, 교통 상황(Traffic Condition), 의사결정에 따라 달라질 수 있다. 현재 관측(Current Observation)으로부터 더 먼 미래를 예측할수록 상태 추정(State Estimation), 전이 동역학(Transition Dynamics), 숨겨진 변수(Hidden Variable), 미래 의사결정에서 발생하는 불확실성이 누적된다.

이러한 불확실성의 증가는 결정론적 장기 예측(Deterministic Long-Horizon Prediction)을 어렵게 만든다. 여러 미래가 가능한 상황에서 하나의 궤적만 예측하면 실제보다 높은 확신을 가진 것처럼 보일 수 있다. 따라서 확률적 또는 다중 모드 예측(Probabilistic or Multimodal Prediction)은 장기 시간 범위에서 특히 중요하다. 월드 모델은 하나의 미래만 예측하는 대신 여러 가능한 궤적, 사건, 상태 시퀀스(State Sequence)와 함께 어떤 대안이 실제로 발생할지에 대한 불확실성을 표현할 수 있다.

단기 예측 역시 특히 접촉(Contact), 급격한 기동(Rapid Maneuvering), 지형 상호작용(Terrain Interaction), 센서 성능 저하(Sensor Degradation) 상황에서는 불확실할 수 있다. 마찰(Friction), 힘(Force), 지연시간(Latency), 접촉 기하 구조(Contact Geometry)의 작은 변화도 결과를 빠르게 변화시킬 수 있다. 차이는 단기 불확실성이 주로 물리적 상태와 동역학의 영향을 받는 반면, 장기 불확실성에는 의사결정, 의도(Intention), 환경 사건, 여러 에이전트 사이에서 분기되는 상호작용(Branching Interaction)이 점점 더 많이 포함된다는 점이다.

재귀적 롤아웃(Recursive Rollout)은 예측 시간 범위를 확장하는 가장 직접적인 방법을 제공한다. 모델은 (s_t)로부터 (s_{t+1})을 예측하고, 다시 그 예측 상태를 이용하여 (s_{t+2})를 추정하며 이러한 과정을 반복한다. 그러나 각각의 예측에는 일정한 오차가 존재하며, 그 오차가 이후 예측의 입력에 포함된다. 따라서 매우 정확한 단일 단계 모델(One-Step Model)이라도 긴 시간 범위에 걸쳐 반복적으로 적용하면 상당한 표류(Drift)가 발생할 수 있다.

오차 누적(Error Accumulation)은 장기 월드 모델링(Long-Horizon World Modeling)의 핵심적인 문제 중 하나이다. 위치, 속도, 객체 정체성(Object Identity), 지형 특성(Terrain Property), 숨겨진 상태(Hidden State)의 작은 오차도 시간이 지나면서 복합적으로 증가할 수 있다. 결국 예측된 상태가 학습 과정에서 거의 경험하지 못했던 영역으로 진입하면서 추가적인 성능 저하가 발생할 수 있다. 따라서 장기 롤아웃(Long Rollout)은 수치적인 오차 누적뿐만 아니라 실제 상태와 모델 자체가 생성한 상태 사이에서 발생하는 분포 변화(Distribution Shift)도 처리해야 한다.

따라서 단일 단계 정확도(One-Step Accuracy)만을 목표로 학습하는 것은 충분하지 않을 수 있다. 모든 예측이 실제 관측 상태(True Observed State)에서 시작할 때는 좋은 성능을 보이는 모델도 자신의 이전 예측값이 입력으로 사용되면 실패할 수 있다. 다단계 학습(Multi-Step Training), 궤적 수준 목적함수(Trajectory-Level Objective), 일관성 제약(Consistency Constraint), 스케줄된 롤아웃 전략(Scheduled Rollout Strategy), 관측을 통한 주기적인 보정(Periodic Correction)을 이용하면 안정성을 향상시킬 수 있다. 목표는 단순히 다음 상태를 정확하게 예측하는 것이 아니라 필요한 시간 범위 전체에서 유용한 예측을 유지하는 것이다.

상태 표현(Representation)에 대한 요구사항 역시 예측 시간 범위에 따라 달라진다. 즉각적인 예측은 상세한 국소 기하 구조(Local Geometry), 속도, 접촉, 액추에이터 상태(Actuator State)에 의존할 수 있다. 반면 장기 예측에서는 도로 구조(Road Structure), 목적지, 객체 기능(Object Function), 인간 의도(Human Intention), 작업 단계(Task Phase), 환경적 맥락(Environmental Context)과 같은 더욱 추상적인 변수가 유용할 수 있다. 따라서 하나의 세부 수준(Level of Detail)에서 작동하는 단일 표현은 매우 다양한 시간 스케일을 예측하는 데 비효율적일 수 있다.

계층적 월드 모델(Hierarchical World Model)은 이러한 문제에 자연스러운 해결책을 제공한다. 빠른 동역학 계층(Fast Dynamics Layer)은 높은 주파수에서 세밀한 물리적 변화를 예측하고, 더 느린 계층(Slower Layer)은 객체, 상호작용, 사건, 목표 또는 작업 수준 전이(Task-Level Transition)를 예측할 수 있다. 수 밀리초 단위의 모든 상태를 먼 미래까지 재귀적으로 예측하는 대신, 시스템은 예측 시간 범위가 증가함에 따라 점차 더 거친 시간적·의미론적 추상화(Temporal and Semantic Abstraction)로 전환할 수 있다.

시간적 추상화(Temporal Abstraction)는 계산 요구량(Computational Requirement)을 크게 줄일 수 있다. 1밀리초 해상도로 10초 이후를 예측하려면 10,000개의 연속적인 전이(Sequential Transition)가 필요하지만, 그중 상당수는 상위 수준 계획(High-Level Planning)에 불필요한 세부 정보를 포함할 수 있다. 계층적 시스템은 가까운 미래에는 세밀한 해상도(Fine Resolution)를, 국소적 행동에는 중간 해상도(Medium Resolution)를, 먼 미래에는 거친 사건 수준 전이(Coarse Event-Level Transition)를 사용하여 의사결정 관련성(Decision Relevance)에 따라 계산 자원을 배분할 수 있다.

공간 해상도(Spatial Resolution) 역시 예측 시간 범위에 따라 변화할 수 있다. 즉각적인 충돌 회피에는 로봇 주변의 정밀한 기하 구조가 필요하지만, 먼 미래의 계획에는 대략적인 경로(Route), 영역(Region), 객체 그룹(Object Group)만으로 충분할 수 있다. 모든 위치와 모든 미래 시간 단계에서 동일한 기하학적 정밀도를 유지하는 것은 지나치게 많은 계산 비용을 요구할 수 있다. 따라서 다중 스케일 표현(Multi-Scale Representation)을 이용하면 세부 정보가 현재 의사결정에 영향을 주지 않는 영역에서 선택적으로 예측 정밀도를 낮출 수 있다.

의미론적 정보(Semantic Information)는 예측 시간 범위가 길어질수록 더욱 중요해진다. 단기 움직임은 현재 속도를 이용하여 어느 정도 외삽(Extrapolation)할 수 있지만, 장기 행동은 개체가 무엇이며 무엇을 할 가능성이 있는지에 의존한다. 관측된 객체가 보행자, 차량, 문, 자율 로봇(Autonomous Robot)이라는 사실은 가능한 미래 행동의 범위를 제한한다. 따라서 상위 수준 의미론적 해석(High-Level Semantic Interpretation)은 장기적으로 단순한 움직임 외삽의 유용성이 감소하는 문제를 보완할 수 있다.

의도 및 목표 추정(Intent and Goal Estimation)은 다중 에이전트 환경(Multi-Agent Environment)의 장기 예측에서 특히 중요하다. 현재 위치와 속도가 유사한 두 보행자라도 목적지가 다르면 결국 서로 다른 방향으로 이동할 수 있다. 차량 역시 회전하거나, 정지하거나, 양보하거나, 추월할 수 있다. 따라서 장기 월드 모델은 현재 움직임이 무한히 지속된다고 가정하기보다 여러 대안적 의도(Alternative Intention)를 표현해야 한다.

행동 조건화(Action Conditioning)는 예측 시간 범위를 계획(Planning)과 직접 연결한다. 단기 모델은 조향(Steering), 가속(Acceleration), 제동(Braking), 관절 움직임(Joint Motion), 발판 선택(Foothold Selection)과 같은 즉각적인 제어 명령을 평가할 수 있다. 장기 모델은 행동 시퀀스(Action Sequence), 경로, 전략(Strategy), 작업 의사결정을 평가할 수 있다. 그러나 가능한 행동 시퀀스의 수는 시간 범위가 증가함에 따라 급격하게 증가하므로 예측과 계획은 모든 가능한 미래를 전부 시뮬레이션하는 방식을 피해야 한다.

이러한 조합적 증가(Combinatorial Growth)는 선택적 상상(Selective Imagination)의 필요성을 만든다. 월드 모델은 모든 가능성을 평가하는 대신 가능성이 높거나 유망한 미래 궤적(Future Trajectory)의 제한된 집합을 생성할 수 있다. 계획 알고리즘은 이러한 후보를 점진적으로 정제하여 거친 장기 예측으로 유용한 방향을 식별하고, 상세한 단기 예측으로 즉각적인 실행 가능성(Feasibility)과 안전성을 검증할 수 있다. 따라서 예측 정밀도(Prediction Fidelity)는 의사결정 단계에 맞추어 조정될 수 있다.

관측 갱신(Observation Update)은 실제 작동과 개방 루프 상상(Open-Loop Imagination) 사이에 또 다른 중요한 차이를 만든다. 실제 실행 과정에서 로봇은 지속적으로 새로운 감각적 증거(Sensory Evidence)를 받아 예측 오차가 지나치게 커지기 전에 이를 수정할 수 있다. 따라서 장기 예측은 반드시 고정된 미래 예보(Fixed Forecast)로 해석할 필요가 없다. 현재의 의사결정을 안내하는 잠정적인 미래(Provisional Future)로 사용하고, 새로운 관측을 통해 어떤 가능성이 여전히 유효한지를 확인하면서 반복적으로 수정할 수 있다.

이러한 과정은 이동 시간 범위 과정(Receding-Horizon Process)을 형성한다. 에이전트는 미래를 예측하고, 행동을 선택하고, 계획된 시퀀스의 일부만 실행한 다음, 결과로 나타난 세계를 관측하고, 내부 상태를 갱신한 후 다시 미래를 예측한다. 모델 예측 제어(Model Predictive Control)와 관련 접근법은 이러한 원리를 명시적으로 활용한다. 월드 모델은 학습된 환경 행동(Learned Environmental Behavior), 의미론적 상태(Semantic State), 불확실성(Uncertainty), 다중 모드 미래 예측(Multimodal Future Prediction)을 포함함으로써 이를 고전적 동역학 이상으로 확장할 수 있다.

적절한 예측 시간 범위(Prediction Horizon)는 작업(Task)과 체화 형태(Embodiment)에 따라 달라진다. 고속 차량(High-Speed Vehicle)은 긴 제동 거리(Stopping Distance)로 인해 먼 거리의 위험도 현재 행동에 직접적인 영향을 주므로 수 초 이상의 정확한 예측이 필요할 수 있다. 접촉이 많은 작업을 수행하는 매니퓰레이터(Manipulator)는 매우 정밀한 단기 예측을 필요로 할 수 있다. 저속 이동 로봇은 국소적인 충돌 예측과 훨씬 장기적인 경로 수준 추론(Route-Level Reasoning)을 결합할 수 있다. 따라서 피지컬 AI에 보편적으로 최적인 하나의 예측 시간 범위는 존재하지 않는다.

평가(Evaluation) 역시 서로 다른 시간 범위를 구분해야 한다. 단일 단계 정확도가 높다고 해서 장기 안정성(Long-Horizon Stability)이 보장되는 것은 아니며, 장기적인 의미론적 정확성(Semantic Correctness)이 높다고 해서 즉각적인 정밀 제어가 보장되는 것도 아니다. 평가 지표(Metric)는 서로 다른 미래 시간 간격에서 변위 오차(Displacement Error), 충돌 예측, 궤적 일관성(Trajectory Consistency), 사건 정확도(Event Accuracy), 불확실성 보정(Uncertainty Calibration), 작업 성공률(Task Success), 계획 성능(Planning Performance)을 측정할 수 있다. 유능한 월드 모델은 실제 의사결정을 지원해야 하는 시간 스케일에 맞추어 평가되어야 한다.

단기 예측(Short-Horizon Prediction)과 장기 예측(Long-Horizon Prediction)은 서로 경쟁하는 대안이 아니라 상호보완적인 능력으로 작동해야 한다. 단기 시간 범위는 정밀성(Precision), 반응성(Responsiveness), 즉각적인 물리 법칙에 대한 기반(Grounding)을 제공하고, 장기 시간 범위는 맥락(Context), 선제적 예측(Anticipation), 전략적 방향(Strategic Direction), 지연된 결과(Delayed Consequence)에 대한 인식을 제공한다. 계층적 표현(Hierarchical Representation), 불확실성 인식 예측(Uncertainty-Aware Prediction), 지속적인 관측 갱신, 다중 스케일 계획(Multi-Scale Planning)을 통해 이러한 능력을 하나의 월드 모델 안에서 함께 구현할 수 있다.

따라서 성숙한 피지컬 AI(Physical AI) 시스템은 모든 미래 순간을 동일한 세부 수준과 동일한 확신으로 예측하려 하지 않는다. 물리적 결과가 즉각적으로 중요한 가까운 미래는 정밀하게 예측하고, 시간 범위가 확장될수록 증가하는 불확실성을 여러 대안적 미래(Alternative Future)로 표현하며, 상세한 시뮬레이션이 비효율적이거나 신뢰하기 어려워질수록 더 높은 수준의 추상화(Higher-Level Abstraction)로 전환한다. 월드 모델은 이러한 방식으로 즉각적인 동역학과 장기적인 가능성을 연결함으로써 에이전트가 현재는 안전하게 대응하면서도 미래에도 효과적인 행동을 선택할 수 있도록 한다.

## 01.11. World Model Memory

![](images/image11.png){width="7.268055555555556in" height="7.268055555555556in"}

기억(Memory)은 월드 모델(World Model)의 핵심 구성 요소이다. 현재의 관측(Current Observation)만으로는 체화된 에이전트(Embodied Agent)가 자신의 상황을 이해하는 데 필요한 모든 정보를 얻기 어렵기 때문이다. 센서는 매 순간 물리적 세계(Physical World)의 제한된 일부만을 보여주며, 객체는 가려질 수 있고 사건은 시간에 걸쳐 전개되며 중요한 원인은 과거에 존재할 수 있다. 월드 모델 기억(World Model Memory)은 즉각적인 관측을 넘어 관련 정보를 보존함으로써 에이전트가 일관된 내부 세계(Internal World)를 유지할 수 있도록 한다.

기억(Memory)이 없다면 피지컬 AI(Physical AI) 시스템은 각각의 센서 프레임(Sensor Frame)을 마치 환경을 처음 접하는 것처럼 반복적으로 해석해야 한다. 차량 뒤로 사라진 보행자는 내부 표현에서 사실상 사라질 수 있고, 현재 시야(Field of View) 밖에 있는 이전에 탐지된 장애물은 잊힐 수 있으며, 과거의 상호작용 결과가 이후의 의사결정에 영향을 줄 수 없게 된다. 기억은 이렇게 단절된 관측 사이에 시간적 연속성(Temporal Continuity)을 제공한다.

월드 모델 기억(World Model Memory)은 단순히 과거의 원시 센서 데이터(Raw Sensor Data)를 저장하는 것 이상을 의미한다. 모든 카메라 프레임, 라이다 스캔(LiDAR Scan), 제어 명령(Control Command), 내부 활성값(Internal Activation)을 무기한 보존하는 것은 계산 비용이 크고 대부분 불필요하다. 유용한 기억 시스템은 예측(Prediction), 계획(Planning), 상호작용(Interaction), 안전(Safety)에 지속적으로 관련되는 정보를 선택적으로 보존하면서 미래 가치가 낮은 세부 정보는 압축하거나 제거한다.

단기 기억(Short-Term Memory)은 비교적 짧은 시간 간격에 걸쳐 필요한 정보를 유지한다. 최근 관측(Recent Observation), 움직임 이력(Motion History), 이전 행동(Previous Action), 접촉 상태(Contact State), 국소 궤적(Local Trajectory), 빠르게 변화하는 환경 조건을 보존할 수 있다. 이러한 기억은 속도(Velocity)를 추정하고, 시간적 패턴(Temporal Pattern)을 탐지하고, 움직이는 개체를 추적하며, 로봇 자체의 움직임으로 인한 변화와 독립적으로 움직이는 객체에 의한 변화를 구별하는 데 도움을 준다.

장기 기억(Long-Term Memory)은 훨씬 긴 시간 동안 유용하게 유지되는 정보를 보존한다. 여기에는 지속적인 지도(Persistent Map), 객체 위치(Object Location), 의미론적 속성(Semantic Property), 환경의 규칙성(Environmental Regularity), 이전에 학습한 상호작용 결과, 작업 지식(Task Knowledge), 반복적으로 나타나는 패턴(Recurring Pattern)이 포함될 수 있다. 장기 기억을 통해 에이전트는 매번 환경과 행동의 모든 측면을 즉각적인 관측으로부터 다시 구성하지 않고 과거 경험을 활용할 수 있다.

단기 기억과 장기 기억 사이의 경계는 고정되어 있지 않다. 서로 다른 피지컬 AI 시스템은 서로 다른 시간 스케일(Time Scale)에서 작동하며, 정보는 점진적으로 여러 기억 계층 사이를 이동할 수 있다. 일시적인 관측은 처음에는 단기 상태(Short-Term State)에 유지되다가 반복적으로 확인되면 지속적인 정보가 되고, 결국 장기 지식(Long-Term Knowledge)에 기여할 수 있다. 반대로 물리적 환경이 변화하면 저장된 정보는 관련성을 잃을 수 있다.

기억(Memory)은 부분 관측 가능성(Partial Observability)에서 특히 중요하다. 시간 (t)의 내부 상태는 개념적으로 현재 관측과 기억된 이력(Remembered History)의 함수로 이해할 수 있으며, (z_t=E(o_t,m_{t-1}))와 같이 표현할 수 있다. 여기에서 (m_{t-1})은 이전 관측과 행동으로부터 얻은 정보를 요약한다. 이후 기억 갱신(Memory Update)은 미래 예측과 의사결정을 위해 어떤 과거 정보가 (m_t)에 지속적으로 유지되어야 하는지를 결정한다.

순환 신경망(Recurrent Neural Network)은 학습된 기억(Learned Memory)을 유지하는 고전적인 메커니즘 중 하나이다. 새로운 관측이 입력될 때마다 은닉 상태(Hidden State)를 반복적으로 갱신하여 이전 시간 단계의 정보가 현재 처리 과정에 영향을 주도록 한다. 장단기 기억(Long Short-Term Memory)과 게이트 순환 구조(Gated Recurrent Architecture)는 더 긴 시퀀스에 걸쳐 유용한 의존 관계를 유지하기 위해 개발되었지만, 매우 긴 이력과 고차원 멀티모달 관측(High-Dimensional Multimodal Observation)은 여전히 순환 표현에 어려움을 줄 수 있다.

어텐션 기반 아키텍처(Attention-Based Architecture)는 이전 표현들의 집합에서 현재 상황과 관련된 정보를 검색할 수 있도록 하는 또 다른 접근법을 제공한다. 모든 과거 정보를 하나의 순환 은닉 상태에 압축하는 대신, 어텐션(Attention)은 현재 맥락(Context)에 따라 서로 다른 과거 관측이나 기억 토큰(Memory Token)에 선택적으로 접근할 수 있다. 이를 통해 장거리 추론(Long-Range Reasoning)을 향상시킬 수 있지만, 유지되는 맥락의 크기가 커질수록 계산량과 메모리 요구량도 증가한다.

상태 공간 모델(State-Space Model)은 계산 효율성을 유지하면서 긴 시퀀스에 걸쳐 압축된 내부 상태를 전파하는 메커니즘을 제공한다. 모든 과거 관측에 반복적으로 어텐션을 적용하는 대신 구조화된 상태 전이(Structured State Transition)를 통해 시간적 정보를 요약할 수 있다. 지속적으로 작동하는 피지컬 AI 시스템에서는 작동 시간이 증가하더라도 계산 비용이 무한히 증가하지 않으면서 긴 센서 스트림(Long Sensor Stream)을 처리해야 하므로 이러한 접근법이 매력적이다.

외부 또는 명시적 기억(External or Explicit Memory)은 학습된 은닉 상태를 보완할 수 있다. 로봇은 신경 동역학 모델(Neural Dynamics Model) 외부에 기하학적 지도(Geometric Map), 의미론적 지도(Semantic Map), 점유 구조(Occupancy Structure), 객체 데이터베이스(Object Database), 에피소드 기록(Episodic Record), 키-값 기억(Key-Value Memory)을 유지할 수 있다. 이러한 구조는 해석 가능한 정보를 장기간 보존하고 필요한 정보를 선택적으로 검색할 수 있다. 따라서 하이브리드 시스템(Hybrid System)은 암묵적인 패턴을 위한 신경 기억(Neural Memory)과 지속적인 물리적 사실을 위한 구조화된 기억(Structured Memory)을 결합할 수 있다.

공간 기억(Spatial Memory)은 체화된 에이전트에게 특히 중요하다. 로봇이 이동하면 환경의 많은 부분이 현재 센서 시야에서 벗어나지만 물리적으로는 계속 중요한 의미를 가진다. 지도, 객체 위치, 자유 공간 추정(Free-Space Estimate), 지형 특성(Terrain Property), 이전에 관측된 위험 요소(Hazard)를 공간 기억에 유지할 수 있다. 위치추정(Localization)을 이용하면 현재 관측을 기억된 환경 구조와 정렬하여 즉각적인 지각 범위를 넘어 확장되는 지속적인 표현(Persistent Representation)을 구축할 수 있다.

객체 기억(Object Memory)은 또 다른 유용한 구성 방법을 제공한다. 완전한 장면(Scene)만을 저장하는 대신 월드 모델은 개별 개체(Entity)에 대한 지속적인 기록을 유지할 수 있다. 객체 기록에는 정체성(Identity), 위치, 속도, 의미론적 클래스(Semantic Class), 불확실성(Uncertainty), 상호작용 이력, 마지막 관측 시간(Last Observation Time)이 포함될 수 있다. 객체가 가림(Occlusion)으로 사라지더라도 새로운 증거가 저장된 가설을 확인, 갱신 또는 무효화할 때까지 해당 객체의 상태를 계속 예측할 수 있다.

의미 기억(Semantic Memory)은 특정한 하나의 사건에 연결되지 않는 보다 일반적인 지식을 표현한다. 어떤 유형의 객체가 존재하는지, 일반적으로 어떤 속성을 갖는지, 어떤 표면이 주행 가능한지, 특정 도구와 구조물을 어떻게 사용할 수 있는지와 같은 규칙성을 인코딩할 수 있다. 이러한 지식은 월드 모델이 이전 경험을 통해 축적된 패턴과 새로운 관측을 연결함으로써 익숙하지 않은 상황을 해석하는 데 도움을 준다.

반면 일화 기억(Episodic Memory)은 특정 경험에 관한 정보를 보존한다. 로봇은 특정 경로가 막혀 있었던 경험, 특정 위치에서 바퀴 미끄러짐(Wheel Slip)이 발생했던 경험, 이전 상호작용에서 객체가 이동되었던 사실, 또는 과거의 행동 시퀀스(Action Sequence)가 실패했던 경험을 기억할 수 있다. 일화 정보는 에이전트가 유사한 상황을 다시 경험하거나 동일한 환경으로 돌아왔을 때 이후의 의사결정을 위한 맥락을 제공할 수 있다.

절차적 정보(Procedural Information) 역시 월드 모델 기억과 상호작용할 수 있다. 반복적인 경험을 통해 특정 행동이 특정 객체, 지형, 상황에 어떤 영향을 미치는지를 파악할 수 있다. 단순히 무엇을 관측했는지만 기억하는 것이 아니라 효과적인 상호작용 패턴(Interaction Pattern)에 관한 지식을 보존할 수 있다. 이는 저장된 경험이 미래에 유사한 행동을 시도했을 때 어떤 결과가 발생할지를 더욱 정확하게 예측하도록 하기 때문에 기억을 동역학 학습(Dynamics Learning)과 연결한다.

기억(Memory)은 저장하는 메커니즘뿐만 아니라 망각(Forgetting) 메커니즘도 포함해야 한다. 물리적 환경은 변화하고, 객체는 이동하며, 일시적인 장애물은 사라지고, 이전에는 정확했던 정보도 더 이상 유효하지 않을 수 있다. 월드 모델이 모든 과거의 믿음(Belief)을 무기한 유지하면 오래된 정보(Stale Information)가 현재 증거와 충돌할 수 있다. 따라서 정확한 내부 세계를 유지하려면 망각, 감쇠(Decay), 신뢰도 감소(Confidence Reduction), 교체(Replacement), 명시적 무효화(Explicit Invalidation)가 필요하다.

저장된 정보의 중요도는 여러 요소를 통해 결정할 수 있다. 환경 조건이 빠르게 변화하는 경우 최근 정보(Recent Information)에 더 높은 우선순위를 부여할 수 있으며, 비정상적이거나 안전에 중요한 사건(Safety-Critical Event)은 훨씬 오랫동안 중요하게 유지될 수 있다. 예측 오차(Prediction Error)와 관련된 정보 역시 가치가 있을 수 있는데, 예상하지 못한 결과가 현재 모델의 약점을 드러내기 때문이다. 따라서 기억 관리(Memory Management)는 단순히 시간에만 의존하는 것이 아니라 정보의 관련성(Relevance)에 따라 이루어져야 한다.

기억을 유지할 때 불확실성(Uncertainty)은 필수적인 요소이다. 기억된 객체의 위치는 해당 객체가 오랫동안 관측되지 않았는데도 완전히 확실한 상태로 유지되어서는 안 된다. 시간이 지날수록 가능한 움직임에 따라 객체가 존재할 수 있는 위치 범위가 넓어질 수 있다. 마찬가지로 기억된 지형 조건이나 환경 구성(Environmental Configuration)에 대한 신뢰도 역시 감소할 수 있다. 따라서 기억은 정보 자체뿐만 아니라 그 정보가 여전히 유효한지에 대한 불확실성도 함께 보존해야 한다.

예측(Prediction)과 기억(Memory)은 긴밀하게 결합된 시스템을 형성한다. 기억은 미래 상태를 예측하는 데 필요한 과거 맥락(Historical Context)을 제공하고, 예측은 직접적인 관측이 없는 기간 동안 기억된 상태를 시간에 따라 전파할 수 있도록 한다. 객체가 가려지면 월드 모델은 이전 상태와 학습된 동역학을 이용하여 현재의 가능한 상태를 예측할 수 있다. 이후 새로운 관측이 예측을 수정하고 기억을 갱신하면서 지속적인 시간적 추정 루프(Temporal Estimation Loop)가 형성된다.

기억은 장기 예측(Long-Horizon Prediction)도 지원한다. 먼 미래는 현재 관측만으로 추출할 수 없는 정보에 의존하는 경우가 많기 때문이다. 목표(Goal), 이전 상호작용, 경로 이력(Route History), 지속적인 환경 구조, 행동 패턴(Behavioral Pattern)은 여러 단계 이후의 미래에 영향을 미칠 수 있다. 이러한 요소를 지나치게 빠르게 잊어버리는 월드 모델은 즉각적인 예측에서는 좋은 성능을 보이더라도 일관성 있는 장기 예측을 유지하는 데 실패할 수 있다.

계층적 기억(Hierarchical Memory)은 시간적·의미론적 스케일(Temporal and Semantic Scale)에 따라 정보를 구성할 수 있다. 빠른 기억(Fast Memory)은 최근 센서 동역학과 접촉 상태를 보존하고, 중간 수준 기억(Intermediate Memory)은 객체와 진행 중인 상호작용을 유지하며, 느린 기억(Slow Memory)은 지도, 작업 맥락(Task Context), 의미론적 지식, 반복 패턴을 저장할 수 있다. 서로 다른 기억 계층을 서로 다른 주기로 갱신함으로써 적절한 시간 범위의 정보를 보존하면서 계산량을 줄일 수 있다.

기억 검색(Memory Retrieval)은 기억 저장(Memory Storage)만큼 중요하다. 자율 시스템은 방대한 경험을 축적할 수 있지만 현재 상황에 실제로 관련되는 것은 그중 일부에 불과하다. 검색 메커니즘(Retrieval Mechanism)은 공간적 근접성(Spatial Proximity), 의미론적 유사성(Semantic Similarity), 작업 맥락, 예측된 관련성(Predicted Relevance), 불확실성을 기준으로 필요한 기억을 식별해야 한다. 효율적인 검색은 모든 의사결정에서 전체 과거 이력을 처리하지 않고도 대규모 기억을 추론에 활용할 수 있도록 한다.

기억(Memory)은 지속적 적응(Continual Adaptation)도 가능하게 한다. 작동 과정에서 축적된 예측 오차와 상호작용 결과는 새로운 지형 특성, 변화하는 객체 행동, 센서 드리프트(Sensor Drift), 이전에 경험하지 못했던 환경 패턴을 드러낼 수 있다. 선택된 경험을 이용하여 모델을 갱신하거나 예측을 보정(Calibration)할 수 있다. 따라서 월드 모델은 고정된 사전학습 시스템(Pretrained System)에서 지속적인 물리적 경험으로부터 유용한 증거를 통합하는 적응형 모델(Adaptive Model)로 발전할 수 있다.

그러나 지속적 기억(Continual Memory)은 안정성 문제(Stability Challenge)도 발생시킨다. 새로운 경험을 통해 적응 능력을 향상시키면서도 이전에 학습한 중요한 지식이 덮어쓰이지 않도록 해야 한다. 기억 선택(Memory Selection), 재생(Replay), 통합(Consolidation), 파라미터 격리(Parameter Isolation), 기타 지속 학습(Continual Learning) 메커니즘을 통해 가소성(Plasticity)과 안정성(Stability)의 균형을 맞출 수 있다. 이는 수개월 또는 수년에 걸쳐 변화하는 환경에서 작동해야 하는 피지컬 AI 시스템에서 특히 중요하다.

따라서 성숙한 월드 모델(World Model)은 여러 시간 스케일과 여러 형태의 기억을 필요로 한다. 최근의 동역학, 지속적인 공간 구조, 개별 객체, 중요한 일화(Episode), 의미론적 규칙성, 유용한 상호작용 경험을 기억하면서 무엇을 갱신하고, 압축하고, 검색하고, 망각해야 하는지를 지속적으로 결정해야 한다. 기억은 단순히 모델에 부착된 기록 저장소(Archive)가 아니라 상태 추정(State Estimation)과 예측에 적극적으로 참여하는 구성 요소이다.

궁극적으로 월드 모델 기억(World Model Memory)은 체화된 에이전트의 과거(Past), 현재(Present), 미래(Future)를 연결한다. 기억은 서로 단절된 관측을 지속적인 경험(Persistent Experience)으로 변환하고, 감각적 증거가 일시적으로 사라지더라도 숨겨진 상태(Hidden State)를 유지하며, 예측과 계획을 위한 과거 맥락을 제공한다. 표현(Representation) 및 동역학(Dynamics)과 결합된 기억은 피지컬 AI가 현재 보고 있는 것뿐만 아니라 이전에 관측하고, 추론하고, 학습하고, 경험한 것을 바탕으로 현재의 세계를 이해할 수 있도록 한다.

## 01.12. Minimal World Model [w/Code]

![](images/image12.png){width="7.268055555555556in" height="7.268055555555556in"}

최소 월드 모델(Minimal World Model)은 에이전트(Agent)가 현재 상황을 표현하고, 관련된 변화를 예측하며, 그에 따라 행동을 선택할 수 있도록 하는 가장 작은 내부 예측 구조(Internal Predictive Structure)이다. 최소 월드 모델은 물리적 세계(Physical World)의 모든 세부 사항을 복원하려 하지 않는다. 대신 관측(Observation), 내부 상태(Internal State), 행동(Action), 전이(Transition), 미래 결과(Future Consequence)를 일관된 예측 순환(Predictive Loop)으로 연결하는 데 필요한 정보만을 보존한다.

최소성(Minimality)이라는 개념은 현실을 완전하게 표현하는 것이 필요하지도 않고 계산적으로 실용적이지도 않기 때문에 중요하다. 로봇은 시각(Visual), 기하학적(Geometric), 음향(Acoustic), 고유수용성(Proprioceptive), 제어(Control) 정보의 방대한 스트림을 지속적으로 수신하지만, 특정 의사결정에 영향을 미치는 정보는 그중 일부에 불과하다. 따라서 최소 월드 모델은 예측과 행동에 중요한 정보를 보존하는 가장 작은 충분 상태(Smallest Sufficient State)를 추구한다.

가장 단순한 형태에서 모델은 관측 (o_t), 내부 상태 (z_t), 행동 (a_t), 그리고 다음 상태를 추정하는 전이 메커니즘(Transition Mechanism)의 네 가지 요소로 설명할 수 있다. 인코더(Encoder)는 (z_t=E(o_t))를 구성하고, 동역학 모델(Dynamics Model)은 (\\hat{z}_{t+1}=F(z_t,a_t))를 예측한다. 이러한 기본 구조만으로도 에이전트가 특정 행동을 수행하면 무엇이 발생할 수 있는지를 내부적으로 추론할 수 있는 메커니즘을 제공한다.

내부 상태(Internal State)는 이러한 아키텍처(Architecture)의 중심 구성 요소이다. 원시 센서 관측(Raw Sensor Observation)은 일반적으로 차원이 지나치게 높고, 중복적이며, 잡음(Noise)이 많기 때문에 효율적인 예측 상태(Predictive State)로 직접 사용하기 어렵다. 인코더는 이를 작업 관련 정보(Task-Relevant Information)를 포함하는 표현(Representation)으로 압축한다. 응용 분야에 따라 이 상태는 기하 구조(Geometry), 움직임(Motion), 객체(Object), 로봇 구성(Robot Configuration), 접촉 조건(Contact Condition), 자유 공간(Free Space), 또는 학습된 잠재 특징(Learned Latent Feature)을 표현할 수 있다.

최소 상태(Minimal State)는 설명적 완전성(Descriptive Completeness)이 아니라 예측 충분성(Predictive Sufficiency)을 만족해야 한다. 센서에 보이는 모든 것을 재현할 필요는 없으며, 에이전트에게 중요한 결과를 예측하기에 충분한 정보를 포함하면 된다. 이동 로봇(Mobile Robot)의 경우 벽의 정밀한 질감은 불필요할 수 있지만, 장애물 위치, 상대 움직임(Relative Motion), 주행 가능성(Traversability), 로봇 속도는 안전한 미래 움직임을 결정하는 데 필수적일 수 있다.

피지컬 AI(Physical AI)는 단순히 환경을 관측하는 것이 아니라 환경과 상호작용하기 때문에 행동(Action)이 포함되어야 한다. 미래는 현재 상태뿐만 아니라 에이전트가 무엇을 하는지에 따라서도 달라진다. 행동을 조건으로 하는 전이 모델(Action-Conditioned Transition Model)은 이러한 관계를 (p(z_{t+1}\|z_t,a_t))로 표현할 수 있다. 이를 통해 월드 모델은 수동적인 미래 예측 메커니즘에서 제어(Control)와 계획(Planning)을 지원할 수 있는 행동 가능한 예측 모델(Actionable Predictive Model)로 전환된다.

전이 모델(Transition Model)은 유용한 동역학(Dynamics)의 최소 개념을 표현한다. 전이 모델은 행동이 주어졌을 때 관련 상태 변수가 하나의 시간 단계에서 다음 시간 단계로 어떻게 변화하는지를 예측한다. 미래 변화가 충분히 예측 가능하다면 결정론적 모델(Deterministic Model)을 사용할 수 있고, 여러 결과가 가능하다면 확률적 모델(Probabilistic Model)을 사용할 수 있다. 행동에 중요한 물리적 관계를 포착할 수 있다면 작은 전이 모델만으로도 상당한 수준의 지능적 기능을 제공할 수 있다.

디코더(Decoder)는 유용하지만 최소 운영 모델(Minimal Operational Model)에 항상 필요한 것은 아니다. 에이전트가 잠재 상태 공간(Latent State Space)에서 직접 계획한다면 관측을 인코딩하고, 미래 잠재 상태를 예측하며, 카메라 이미지나 다른 원시 센서 신호를 복원하지 않고도 이를 평가할 수 있다. 예측 상태를 해석하거나, 복원하거나, 시각화하거나, 관측과 비교하거나, 복원 기반 목적함수(Reconstruction-Based Objective)를 사용하여 학습해야 하는 경우에는 디코더가 유용해진다.

기억(Memory) 역시 가장 단순한 개념 수준에서는 항상 필요한 요소가 아니라 조건에 따라 필요한 요소이다. 완전 관측 가능한 환경(Fully Observable Environment)에서는 현재 관측만으로 관련 상태를 결정하기에 충분할 수 있다. 그러나 실제 물리적 환경은 일반적으로 부분 관측 가능(Partially Observable)하다. 객체는 가려지고, 센서 범위는 제한되며, 속도나 의도(Intention)를 추정하려면 시간적 맥락(Temporal Context)이 필요한 경우가 많다. 이러한 상황에서는 기억이 최소 충분 모델(Minimal Sufficient Model)의 일부가 된다.

기억이 포함되면 상태 추정기(State Estimator)는 개념적으로 (z_t=E(o_t,m_{t-1}))로 표현할 수 있으며, 여기에서 (m_{t-1})은 관련된 과거 정보(Historical Information)를 요약한다. 기억 갱신(Memory Update)은 현재 관측을 넘어 유지해야 하는 정보를 보존한다. 이는 과거 전체를 저장한다는 의미가 아니다. 최소 기억(Minimal Memory)은 해당 정보가 없을 경우 예측, 상태 추정(State Estimation), 계획 또는 안전 성능이 의미 있게 저하되는 과거 변수만을 유지해야 한다.

믿음 상태(Belief State)는 실제 물리적 상태를 직접 관측할 수 없는 경우 최소 모델을 확률적으로 확장한다. (z_t)가 완벽하게 알려져 있다고 가정하는 대신 시스템은 가능한 여러 상태에 대한 불확실성(Uncertainty)을 유지한다. 새로운 관측은 이러한 믿음을 갱신하고 전이 모델은 이를 미래로 전파한다. 따라서 최소 월드 모델은 결정론적 상태 예측에서 불확실성 인식 추론(Uncertainty-Aware Reasoning)으로 자연스럽게 확장될 수 있다.

예측 시간 범위(Prediction Horizon) 역시 무엇이 최소 모델에 해당하는지를 결정한다. 즉각적인 충돌 회피(Collision Avoidance)만을 위한 모델이라면 위치(Position), 속도(Velocity), 장애물 기하 구조(Obstacle Geometry), 단기 동역학(Short-Term Dynamics)만으로 충분할 수 있다. 그러나 장기적인 내비게이션(Navigation)이나 상호작용을 지원하려면 지속적인 객체(Persistent Object), 의미론적 맥락(Semantic Context), 목표(Goal), 기억, 행동 가설(Behavioral Hypothesis)이 추가적으로 필요할 수 있다. 따라서 최소성은 시스템이 지원해야 하는 시간 범위와 의사결정에 상대적인 개념이다.

동일한 원리는 공간적 스케일(Spatial Scale)에도 적용된다. 즉각적인 국소 제어(Local Control)는 로봇 주변의 상세한 기하 구조만을 필요로 할 수 있으며, 먼 영역은 더 거친 수준으로 표현할 수 있다. 최소 월드 모델은 이러한 정밀도가 현재 또는 예측 가능한 미래 의사결정에 영향을 미치지 않는다면 전체 환경을 균일하게 상세한 표현으로 유지하지 않아야 한다. 따라서 예상되는 행동 관련성(Action Relevance)에 따라 표현 해상도(Representation Resolution)를 배분할 수 있다.

의미론적 정보(Semantic Information) 역시 선택적으로 포함되어야 한다. 로봇이 눈에 보이는 모든 구조에 대해 의미론적 레이블(Semantic Label)을 가질 필요는 없다. 그러나 의미론적 정체성(Semantic Identity)이 예상 동역학이나 적절한 행동을 변화시키는 경우에는 중요해진다. 보행자와 정적 장애물, 문과 벽, 통과 가능한 식생(Traversable Vegetation)과 단단한 장벽(Rigid Barrier)을 구분하면 즉각적인 기하 구조가 유사하더라도 예측과 계획은 크게 달라질 수 있다.

따라서 최소 모델(Minimal Model)은 특정 아키텍처에 의존하는 것이 아니라 작업 의존적(Task-Dependent)인 것으로 이해할 수 있다. 어떤 응용 분야에서는 명시적 상태 변수(Explicit State Variable)를 사용할 수 있고, 다른 분야에서는 학습된 잠재 벡터(Learned Latent Vector)를 사용할 수 있으며, 또 다른 시스템에서는 점유(Occupancy), 객체 상태(Object State), 신경 특징(Neural Feature)을 결합할 수 있다. 모델을 최소 모델로 만드는 것은 특정 신경망 설계가 아니라 불필요한 정보와 메커니즘을 제거하더라도 요구되는 예측 및 의사결정 능력이 저하되지 않는지 여부이다.

이러한 관점은 최소 월드 모델(Minimal World Model)과 완전한 세계 시뮬레이터(Complete World Simulator)를 구분하는 데 유용하다. 시뮬레이터는 다양한 조건에서 상세한 물리적 외형, 동역학, 상호작용을 재현하려 할 수 있다. 반면 최소 월드 모델은 체화된 에이전트에게 필요한 현실의 일부만을 표현한다. 그 목적은 최대한의 사실성(Maximal Realism)이 아니라 지능적인 행동에 충분한 예측 구조(Sufficient Predictive Structure)를 제공하는 것이다.

최소 모델은 계산 자원(Computational Resource), 메모리 대역폭(Memory Bandwidth), 에너지(Energy), 지연시간(Latency)이 제한된 엣지 기반 피지컬 AI(Edge-Based Physical AI)에 특히 매력적이다. 여러 고해상도 카메라의 모든 픽셀을 먼 미래까지 예측하는 것은 그에 비례하는 이점 없이 막대한 계산량을 소비할 수 있다. 압축된 잠재 상태 또는 구조화된 상태 예측(Structured State Prediction)은 내비게이션, 조작, 제어, 안전에 필요한 정보를 유지하면서 추론 비용(Inference Cost)을 줄일 수 있다.

최소성(Minimality)은 학습 효율성(Learning Efficiency)도 향상시킬 수 있다. 예측 목적(Prediction Objective)이 모든 감각적 세부 정보가 아니라 관련된 상태 변화에 집중하면 모델은 행동에 영향을 주는 인과적 관계(Causal Relationship)와 동적 관계(Dynamic Relationship)에 모델 용량(Model Capacity)을 집중할 수 있다. 이를 통해 물리적 결과에 거의 영향을 미치지 않는 예측하기 어려운 질감(Texture), 조명 변화(Illumination Change), 센서 인공물(Sensor Artifact), 배경 변화(Background Variation)를 학습해야 하는 부담을 줄일 수 있다.

그러나 지나친 압축(Excessive Compression)은 그 자체로 위험을 발생시킨다. 표현에서 나중에 중요해지는 정보가 제거되면 전이 모델은 해당 정보를 복구할 수 없다. 직선 도로 주행에는 충분한 상태라도 지형이 변화하거나, 사람이 장면에 등장하거나, 조작 작업이 필요해지면 충분하지 않을 수 있다. 따라서 최소 모델을 설계할 때에는 어떤 변수를 안전하게 제거할 수 있는지와 어떤 변수를 계속 사용할 수 있도록 유지해야 하는지를 신중하게 식별해야 한다.

실용적인 전략 중 하나는 압축된 핵심 상태(Compact Core State)에서 시작하여 예측 오차(Prediction Error)나 작업 실패(Task Failure)가 중요한 정보의 누락을 보여줄 때만 새로운 정보를 추가하는 것이다. 바퀴 움직임 예측이 반복적으로 실패하면 지형이나 미끄러짐(Slip)을 표현해야 한다는 것을 의미할 수 있고, 가려진 보행자를 예측하지 못한다면 객체 기억(Object Memory)이 필요하다는 것을 보여줄 수 있다. 이를 통해 측정 가능한 요구사항에 근거하여 최소 모델에서 더욱 풍부한 아키텍처로 점진적으로 확장할 수 있다.

예측 오차(Prediction Error)는 이러한 과정에서 중요한 진단 신호(Diagnostic Signal)를 제공한다. 특정 조건에서 모델이 반복적으로 실패한다면 그 원인은 불충분한 표현(Insufficient Representation), 부족한 기억(Inadequate Memory), 잘못된 동역학(Incorrect Dynamics), 또는 불확실성 표현의 누락일 수 있다. 모델 크기를 무조건 증가시키는 대신 어떤 정보의 누락이 실패를 발생시켰는지를 분석하여 월드 모델을 선택적으로 확장할 수 있다.

최소 월드 모델(Minimal World Model)은 상상된 롤아웃(Imagined Rollout)을 통해 계획(Planning)을 지원할 수도 있다. 추정된 현재 상태에서 시작하여 모델은 후보 행동(Candidate Action)을 적용하고 제한된 시간 범위에서 그 결과를 예측한다. 계획기는 안전, 진행도(Progress), 에너지, 작업 성공(Task Success), 또는 다른 목적함수(Objective)에 따라 이러한 예측된 미래를 비교한다. 따라서 비교적 작은 예측 모델이라도 지각(Perception)을 선제적 의사결정(Anticipatory Decision Making)으로 전환할 수 있다.

관측(Observation)은 예측과 물리적 현실(Physical Reality) 사이의 순환을 완성한다. 행동을 실행한 후 새로운 센서 측정값은 실제로 무엇이 발생했는지를 보여준다. 시스템은 이 증거를 예측 상태(Predicted State)와 비교하고 내부 표현을 수정한 다음 새로운 예측 순환을 시작한다. 따라서 최소 운영 순환(Minimal Operational Loop)은 관측, 상태 추정, 행동 조건부 예측(Action-Conditioned Prediction), 행동 선택(Action Selection), 실행(Execution), 보정(Correction)으로 요약할 수 있다.

이러한 폐루프 구조(Closed-Loop Structure)는 모델의 복잡성 자체보다 중요하다. 사실적인 미래를 생성하지만 상태 보정(State Correction)이나 행동 선택을 신뢰성 있게 지원하지 못하는 매우 큰 생성 모델(Generative Model)은 작업 관련 물리 상태를 지속적으로 예측하고 수정하는 압축된 모델보다 로보틱스(Robotics)에서 유용성이 낮을 수 있다. 물리적 기반성(Physical Grounding)은 내부 예측과 외부 관측의 반복적인 상호작용을 통해 형성된다.

최소 월드 모델은 계층적 확장(Hierarchical Expansion)을 위한 유용한 기반도 제공한다. 압축된 고속 모델(Compact Fast Model)이 즉각적인 동역학과 안전을 처리하고, 필요할 때 추가 모듈(Module)이 의미론적 추론(Semantic Reasoning), 장기 기억(Long-Term Memory), 멀티모달 예측(Multimodal Prediction), 장기 계획(Long-Horizon Planning)을 도입할 수 있다. 따라서 모든 기능을 항상 최대 복잡도로 작동시키는 대신 작은 예측 핵심(Predictive Core)에서 시작하여 아키텍처를 확장할 수 있다.

궁극적으로 최소 월드 모델(Minimal World Model)은 유용한 내부 상태를 유지하고, 행동에 따른 변화를 예측하며, 새로운 관측을 통해 자신을 수정하는 데 필요한 최소한의 정보와 메커니즘을 포함한다. 구체적인 구성 요소는 체화 형태(Embodiment), 환경(Environment), 작업(Task), 불확실성(Uncertainty), 예측 시간 범위(Prediction Horizon)에 따라 달라진다. 핵심 원칙은 관측할 수 있는 모든 것을 모델링하는 것이 아니라, 제거했을 때 예측이나 행동 능력을 실질적으로 약화시키는 모든 정보를 보존하는 것이다.

피지컬 AI(Physical AI)에서 이러한 원칙은 확장 가능한 월드 모델(Scalable World Model)을 구축하기 위한 실용적인 출발점을 제공한다. 관측은 현재에 대한 증거를 제공하고, 표현(Representation)은 그 증거를 관련 상태로 압축하며, 기억(Memory)은 필요한 과거 정보를 보존하고, 동역학(Dynamics)은 가능한 변화를 예측하며, 행동(Action)은 이러한 예측을 현실에서 검증한다. 이러한 최소 폐루프(Minimal Closed Loop)를 기반으로 공간적(Spatial), 시간적(Temporal), 의미론적(Semantic), 예측적(Predictive) 능력을 실제 측정 가능한 가치를 제공하는 영역에 한해 점진적으로 추가할 수 있다.
