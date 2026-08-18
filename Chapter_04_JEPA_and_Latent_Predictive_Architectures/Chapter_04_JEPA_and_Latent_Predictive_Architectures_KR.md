**Volume 07. World Models for Physical AI**

# Chapter 04. JEPA and Latent Predictive Architectures

## 04.01. Joint Embedding Predictive Architectures

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

공동 임베딩 예측 아키텍처(Joint Embedding Predictive Architectures)는 원시 감각 입력(raw sensory input)의 모든 세부 정보를 재구성하는 대신, 인코딩된 관측(encoded observations) 사이의 관계를 예측함으로써 유용한 세계 표현(world representation)을 학습한다. 모델이 픽셀(pixel), 파형(waveform), 기타 고차원 측정값(high-dimensional measurements)을 그대로 재현하도록 요구하는 대신, 관측을 임베딩 공간(embedding space)으로 변환하고 그 공간에서 의미 있는 표현을 예측하도록 학습한다. 이를 통해 학습의 초점은 구조(structure), 동역학(dynamics), 미래 상태(future states)를 이해하는 데 유용한 정보로 이동한다.

핵심 아이디어는 서로 관련된 상황의 다양한 관측이 공통 잠재 공간(common latent space)에서 표현되어야 하며, 그 공간에서는 관측 사이의 근본적인 관계를 보다 쉽게 모델링할 수 있다는 것이다. 인코더(encoder)는 문맥 관측(context observation)을 압축된 표현(compact representation)으로 변환하고, 또 다른 인코딩 과정은 목표 관측(target observation)의 표현을 생성한다. 이후 예측기(predictor)는 문맥 임베딩(context embedding)으로부터 목표 임베딩(target embedding)을 추정하여 원래 관측 공간이 아닌 표현 공간(representation space)에서 직접 예측 학습 문제를 구성한다.

이 접근법은 물리적 환경(physical environment)이 에이전트(agent)에게 불필요할 수 있는 방대한 세부 정보를 포함하기 때문에 월드 모델(world model)에서 특히 중요하다. 질감(texture), 조명 변화(illumination variation), 센서 잡음(sensor noise), 배경 패턴(background pattern), 개별 픽셀을 정확하게 재구성하는 것은 의사결정을 개선하지 않으면서도 상당한 모델 용량(model capacity)을 소비할 수 있다. 공동 임베딩 예측(joint embedding prediction)은 대신 객체 정체성(object identity), 기하 구조(geometry), 움직임(motion), 공간적 관계(spatial relationship), 상호작용 가능성(interaction possibility), 미래 행동에 중요한 변화와 같은 지속적인 특성을 강조할 수 있다.

일반적인 아키텍처(architecture)는 예측기(predictor)를 통해 연결되는 문맥(context) 및 목표(target) 인코딩 경로를 포함한다. 문맥 인코더(context encoder)는 에이전트가 사용할 수 있는 정보를 처리하고, 목표 표현(target representation)은 해당 문맥으로부터 추론되어야 하는 정보를 나타낸다. 학습 과정에서 예측기는 문맥 표현(context representation)을 목표 표현의 추정값으로 변환한다. 학습 목적(training objective)은 예측된 목표와 인코딩된 목표 사이의 차이를 줄이는 동시에, 아키텍처 또는 최적화 메커니즘(optimization mechanism)을 통해 단순하고 무의미한 표현이 학습 목표를 만족시키는 것을 방지한다.

문맥(context)과 목표(target)의 의미는 매우 다양하게 정의될 수 있다. 동일한 이미지의 서로 다른 영역, 하나의 장면에 대한 서로 다른 시점(view), 시간적으로 분리된 관측, 서로 다른 센서 모달리티(sensor modality), 또는 물리 시스템의 현재 상태와 미래 상태가 될 수 있다. 이러한 유연성으로 인해 공동 임베딩 예측은 특정 데이터 유형에 제한된 기술이 아니라 일반적인 아키텍처 원리(architectural principle)가 된다. 어떤 규칙성을 표현이 학습해야 하는지는 문맥과 목표 사이에 정의된 예측 관계(predictive relationship)에 의해 결정된다.

시간적 예측(temporal prediction)은 이러한 아키텍처를 피지컬 AI(Physical AI)에 특히 적합하게 만든다. 로봇은 현재의 감각 문맥(sensory context)을 인코딩하고 미래 관측과 관련된 표현을 예측할 수 있다. 이러한 예측에 성공하려면 잠재 표현(latent representation)이 움직임, 객체 지속성(object persistence), 환경 변화(environmental change), 시간적 의존성(temporal dependency)에 관한 정보를 포함해야 한다. 더 긴 시간 간격을 대상으로 예측하면 모델이 단기적인 시각적 유사성에만 의존하는 대신 환경의 보다 느리고 의미 있는 특성을 표현하도록 유도할 수 있다.

공동 임베딩 아키텍처(joint embedding architecture)는 공간적 예측(spatial prediction)도 활용할 수 있다. 관측의 일부 영역을 숨기거나 문맥에서 제외한 뒤, 예측기가 보이는 정보로부터 해당 영역의 표현을 추정하도록 만들 수 있다. 이를 통해 모델은 객체, 표면(surface), 장면 영역(scene region), 더 큰 공간 구조 사이의 관계를 학습한다. 로보틱스(robotics)에서는 장애물, 조작 가능한 객체(manipulable object), 사람 또는 주행 가능 영역(traversable region)이 일시적으로 가려지거나 센서 시야(field of view) 밖에 있는 부분 관측 환경(partially observed environment)을 추론하는 데 이러한 표현을 활용할 수 있다.

중요한 문제 중 하나는 표현 붕괴(representation collapse)이다. 이는 인코더가 서로 다른 많은 입력을 동일하거나 거의 동일한 임베딩으로 변환하는 현상이다. 이러한 해법은 예측을 인위적으로 쉽게 만들지만 환경에 관한 유용한 정보를 제거한다. 따라서 공동 임베딩 시스템(joint embedding system)은 정보성과 다양성을 유지하는 표현을 위한 메커니즘을 필요로 한다. 이러한 메커니즘에는 비대칭 네트워크 업데이트(asymmetric network update), 정교하게 설계된 정규화(normalization), 정규화 기법(regularization), 아키텍처 제약(architectural constraint), 또는 인코딩된 관측 사이의 변동성을 보존하는 학습 목적 등이 사용될 수 있다.

전통적인 생성형 예측(generative prediction)과 달리 공동 임베딩 예측은 미래에 발생할 수 있는 모든 감각적 결과를 반드시 표현하려고 하지 않는다. 많은 물리적 상황에는 시각적으로 서로 다르지만 행동 관점에서는 동등한 여러 결과가 존재한다. 추상 표현(abstract representation)을 예측하면 모델은 예측하기 어려운 저수준 세부 정보(low-level detail)를 무시하면서 상태 전이(state transition)에 중요한 정보를 유지할 수 있다. 이러한 특성은 예측 지평(prediction horizon)이 길어지고 정확한 감각 예측의 불확실성이 증가할수록 더욱 중요해진다.

피지컬 AI 시스템(Physical AI system)에서 임베딩(embedding)은 이용 가능한 증거로부터 예측 가능한 세계의 측면을 학습한 내부 표현(internal representation)으로 해석할 수 있다. 카메라 이미지(camera image), 라이다 측정값(LiDAR measurement), 고유수용감각(proprioception), 레이더(radar), 기타 관측 정보가 궁극적으로 장면 구조(scene structure)와 동역학을 설명하는 표현에 기여할 수 있다. 적절하게 학습된 이러한 표현은 원시 센서 측정값(raw sensor measurement)을 반복적으로 직접 처리하지 않고도 후속 지각(perception), 기억(memory), 예측(prediction), 계획(planning), 제어(control)를 위한 압축된 기반을 제공한다.

이 아키텍처는 목표(target)를 감각 데이터 스트림(sensory data stream) 자체에서 구성할 수 있기 때문에 자기지도학습(self-supervised learning)을 위한 자연스러운 기반도 제공한다. 로봇은 모든 객체, 움직임, 상호작용, 미래 상황에 대해 사람이 직접 작성한 주석(annotation)을 필요로 하지 않는다. 공간 영역(spatial region), 시간적 관측(temporal observation), 대체 시점(alternative viewpoint), 다중 모달 측정(multimodal measurement)을 이용해 예측 관계를 자동으로 구성할 수 있다. 따라서 대규모의 레이블 없는 체화 경험(unlabeled embodied experience)을 물리적 세계의 규칙성을 학습하는 훈련 데이터로 활용할 수 있다.

월드 모델링(world modeling)의 관점에서 공동 임베딩 예측은 단순한 표현 압축(representation compression) 이상으로 이해해야 한다. 예측기(predictor)는 잠재 상태(latent state) 사이의 관계 모델을 도입한다. 문맥과 목표가 서로 다른 시점에 대응하면 예측 과정은 환경 동역학(environmental dynamics)의 일부를 암묵적으로 학습한다. 서로 다른 시점(view)이나 공간 영역에 대응하면 공간적 의존성(spatial dependency)을 학습한다. 이러한 관계를 시간, 공간, 모달리티(modality), 그리고 궁극적으로 행동(action)까지 확장하면 표현 학습(representation learning)은 점차 구조화된 잠재 월드 모델링(latent world modeling)으로 발전할 수 있다.

행동(action)은 중요한 후속 확장 요소이다. 물리적 에이전트는 단순히 환경의 상태 전이를 관찰하는 것이 아니라 자신의 행동을 통해 상태 변화를 직접 발생시킨다. 표현 공간 예측기(representation-space predictor)는 모터 명령(motor command)이나 상위 수준 행동(high-level action)을 포함하도록 확장할 수 있으며, 이를 통해 예측된 임베딩이 현재 문맥과 의도된 개입(intervention)에 모두 의존하도록 만들 수 있다. 모델은 자연적으로 발생할 가능성이 높은 변화와 로봇이 이동, 회전, 파지(grasp), 밀기(push) 등의 행동을 수행함으로써 발생하는 변화를 구분할 수 있게 된다.

따라서 공동 임베딩 예측 학습(joint embedding predictive learning)은 수동적 지각(passive perception)과 완전한 예측 월드 모델링(predictive world modeling) 사이에서 중요한 위치를 차지한다. 이는 관측 가능한 세계의 모든 세부 정보를 재구성할 필요 없이 대규모 감각 경험으로부터 추상 상태(abstract state)를 학습하는 메커니즘을 제공한다. 이렇게 생성된 표현은 이후 마스킹 예측(masked prediction), 시간적 JEPA 모델(temporal JEPA model), 행동 조건부 아키텍처(action-conditioned architecture), 체화 지능(embodied intelligence)을 위한 잠재 계획 시스템(latent planning system)의 기반이 될 수 있다.

보다 광범위한 피지컬 AI 아키텍처에서 이러한 학습 표현은 지각(perception)을 예측(prediction), 그리고 궁극적으로 의사결정(decision making)과 연결할 수 있다. 인코더는 복잡한 관측을 구조화된 잠재 정보(structured latent information)로 변환하고, 예측기는 이러한 표현 사이의 관계를 학습하며, 후속 구성요소는 예측된 잠재 상태를 이용해 미래의 여러 가능성을 평가할 수 있다. 핵심 목표는 현실의 완벽한 감각적 복제본을 생성하는 것이 아니라, 물리적 세계가 어떻게 변화하는지를 이해하는 데 필요한 구조를 보존하는 내부 표현을 학습하는 것이다.

## 04.02. Prediction in Representation Space

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

표현 공간에서의 예측(prediction in representation space)은 예측 모델(predictive model)의 목표를 원시 관측(raw observation)을 그대로 재현하는 것에서 의미 있는 구조를 인코딩한 잠재 표현(latent representation)을 추정하는 것으로 전환한다. 미래의 픽셀(pixel), 라이다 반환값(LiDAR return), 센서 측정값(sensor measurement)이 정확히 어떻게 나타날지를 예측하는 대신, 모델은 세계를 인코딩한 표현이 어떻게 변화할지를 예측한다. 이를 통해 물리적 상태(physical state)와 그 변화를 이해하는 데 중요한 정보에 예측을 집중할 수 있다.

원시 관측 공간(raw observation space)은 방대한 양의 정보를 포함하며, 그중 상당 부분은 예측하기 어렵거나 예측할 필요가 없다. 조명(illumination), 질감(texture), 반사(reflection), 센서 잡음(sensor noise), 시점(viewpoint)의 작은 변화도 실제 물리적 상황은 거의 동일한 상태에서 픽셀 수준에서는 큰 차이를 발생시킬 수 있다. 표현 공간 예측(representation-space prediction)은 인코더(encoder)가 관측을 보다 지속적이고 행동적으로 의미 있는 특성을 강조하는 잠재 변수(latent variable)로 변환함으로써 이러한 부담을 줄인다.

기본 과정은 인코더(encoder)가 관측 (x_t)를 잠재 표현(latent representation) (z_t)로 매핑하는 것에서 시작한다. 이후 예측기(predictor)는 다른 관측, 영역, 시점(viewpoint) 또는 미래 시간과 관련된 목표 표현(target representation)을 추정한다. 재구성된 픽셀과 실제 관측 픽셀 사이의 오차를 최소화하는 대신, 예측된 표현 (\\hat{z})와 목표 표현 (z) 사이의 차이를 최소화한다. 따라서 예측은 학습된 의미적·구조적 공간(semantic and structural space) 내부에서 이루어진다.

유용한 표현(representation)은 물리적 상황을 구별하는 데 필요한 정보를 유지하면서 예측이나 행동에 중요하지 않은 변화를 제거해야 한다. 학습 목적(training objective)에 따라 잠재 변수는 객체 존재(object presence), 기하 구조(geometry), 상대적 위치(relative position), 움직임(motion), 장면 구성(scene organization), 주행 가능성(traversability), 상호작용 관련 특성(interaction-relevant property)을 인코딩할 수 있다. 인간이 정의한 변수와 명시적으로 일치할 필요는 없으며, 환경 내부의 중요한 관계를 모델링하는 데 필요한 정보를 보존하면 된다.

이러한 추상화(abstraction)는 미래 관측이 본질적으로 불확실하기 때문에 미래 예측에서 특히 중요하다. 장면을 이동하는 차량은 높은 수준의 장면 변화가 예측 가능하더라도 약간 다른 조명, 보행자의 자세, 식생의 움직임, 이미지 세부 정보를 경험할 수 있다. 잠재 예측기(latent predictor)는 픽셀 생성 모델(pixel-generative model)이 재현하려고 하는 모든 예측 불가능한 감각적 세부 정보에 계산 자원을 소비하지 않고도 미래의 안정적인 특성을 표현할 수 있다.

표현 공간 예측은 시간적 동역학(temporal dynamics)을 학습하는 자연스러운 메커니즘도 제공한다. 인코딩된 관측 시퀀스(sequence) (z_t, z_{t-1}, \\ldots)가 주어지면 모델은 (t+1) 또는 더 먼 미래 시점에 해당하는 표현을 예측할 수 있다. 성공적인 예측을 위해 잠재 상태(latent state)는 시간에 걸쳐 지속되고 관측 사이의 변화를 설명하는 정보를 포함해야 한다. 따라서 시간적 학습(temporal learning)은 움직임, 객체 지속성(object persistence), 장면 변화(scene evolution), 월드 모델링(world modeling)에 중요한 기타 동적 특성을 포함하는 표현의 학습을 촉진할 수 있다.

예측 목표(prediction target)가 반드시 전체 미래 관측을 표현할 필요는 없다. 마스킹된 영역(masked region), 다른 카메라 시점(camera view), 서로 다른 센서 모달리티(sensor modality), 또는 잠재 상태의 선택된 일부가 목표가 될 수 있다. 이러한 목표를 예측하면 모델은 문맥(context)에 이미 존재하는 관계로부터 누락된 정보를 추론해야 한다. 따라서 표현 공간 예측은 하나의 공통 아키텍처 프레임워크(architectural framework) 안에서 공간 추론(spatial reasoning), 다중모달 학습(multimodal learning), 시간 예측(temporal forecasting), 부분 관측 환경(partially observable environment)에 적용될 수 있다.

피지컬 AI(Physical AI)에서는 세계의 물리적 상태를 하나의 센서만으로 완전히 관측하기 어렵기 때문에 다중모달 표현 공간(multimodal representation space)이 특히 중요하다. 카메라는 풍부한 외형 및 의미 정보(semantic information)를 제공하고, 라이다(LiDAR)는 기하 구조를 제공하며, 레이더(radar)는 거리와 움직임 정보를 포착한다. IMU와 고유수용감각(proprioception)은 에이전트 자신의 동역학을 설명한다. 인코더는 이러한 이질적인 측정값을 원래 형식 그대로 재현하지 않고도 예측 관계를 학습할 수 있는 표현으로 변환할 수 있다.

잠재 공간(latent space)에서의 예측은 계산 효율성(computational efficiency)도 향상시킬 수 있다. 원시 감각 데이터 스트림(raw sensory stream)은 하나의 관측마다 수백만 개의 값을 포함할 수 있지만, 유용한 잠재 상태는 훨씬 더 압축된 형태로 표현될 수 있다. 압축된 표현에서 작동하는 예측기는 고차원 감각 출력을 반복적으로 생성하는 대신 관계와 동역학을 모델링하는 데 계산 자원을 집중할 수 있다. 이는 지연시간(latency), 메모리(memory), 전력(power), 엣지 컴퓨팅(edge computing)의 제약 아래 지속적으로 예측해야 하는 로봇 시스템에서 특히 유용하다.

그러나 단순한 압축(compression)만으로 유용한 예측 표현이 보장되는 것은 아니다. 인코더가 미래 상태를 구분하는 데 필요한 정보를 제거하면 예측기는 이를 복구할 수 없다. 반대로 지나치게 많은 불필요한 세부 정보를 유지하면 예측 문제가 불필요하게 어려워질 수 있다. 따라서 공동 학습(joint training)은 잠재 공간이 예측 가능하고 과업 관련성이 높은 구조를 유지하면서 세계 동역학 이해에 기여하지 않는 방해 변동(nuisance variation)에는 둔감해지도록 적절한 정보 병목(information bottleneck)을 형성해야 한다.

또 다른 핵심 문제는 무의미한 해법(trivial solution)을 방지하는 것이다. 문맥 표현(context representation)과 목표 표현(target representation)이 거의 일정한 벡터로 붕괴하면 모델이 의미 있는 정보를 학습하지 않았음에도 예측 오차가 작아질 수 있다. 따라서 표현 공간 아키텍처는 임베딩(embedding)의 다양성과 정보를 유지하는 메커니즘이 필요하다. 비대칭 인코더 업데이트(asymmetric encoder update), 정규화(normalization), 분산 제약(variance constraint), 정규화 기법(regularization), 교사-학생 메커니즘(teacher-student mechanism) 등의 목적 함수를 통해 예측 학습 과정에서도 구조화된 잠재 공간을 유지할 수 있다.

학습된 표현 공간(representation space)의 기하 구조(geometry) 자체도 중요하다. 유사한 물리적 상황은 이상적으로 서로 가까운 영역에 위치해야 하며, 상태의 의미 있는 차이는 구별 가능한 표현으로 나타나야 한다. 잠재 변수의 변화는 임의적인 감각 변동이 아니라 환경에서 의미 있는 변환(transformation)을 반영해야 한다. 따라서 잘 구성된 표현 공간은 모델이 관측 사이의 관계를 설명하고 변화하는 물리적 상태의 궤적(trajectory)을 예측할 수 있는 내부 좌표계(internal coordinate system)가 된다.

장기 예측(long-horizon prediction)은 추상화의 가치를 더욱 높인다. 시간이 길어질수록 불확실성이 누적되기 때문에 정확한 미래 감각 정보를 예측하기는 점점 어려워지지만, 높은 수준의 구조는 훨씬 오랫동안 예측 가능할 수 있다. 로봇은 움직이는 사람의 미래 픽셀 구성을 정확히 알 수 없더라도 그 사람이 복도를 계속 이동하거나 특정 영역으로 진입할 가능성을 예측할 수 있다. 잠재 예측(latent prediction)은 하나의 정확한 감각적 결과에 불필요하게 고정되지 않으면서 이러한 유용한 규칙성을 유지할 수 있다.

표현 공간 예측은 지각(perception)과 계획(planning)을 연결하는 중요한 가교 역할을 한다. 관측이 잠재 상태(latent state)로 인코딩되면 예측된 미래 표현을 모든 후보 미래마다 이미지나 다른 센서 측정값으로 다시 디코딩(decoding)하지 않고도 평가할 수 있다. 계획기(planner)는 가능한 잠재 궤적(latent trajectory)을 비교하고 바람직하거나 위험한 결과를 추정한 뒤 이에 따라 행동을 선택할 수 있다. 따라서 예측은 가능한 미래의 물리적 상태에 대한 압축 표현에서 수행되는 내부 시뮬레이션(internal simulation) 과정이 된다.

월드 모델이 행동 조건부(action-conditioned) 형태로 발전하면 잠재 예측은 현재 표현뿐 아니라 후보 행동(candidate action)까지 함께 포함할 수 있다. 모델은 에이전트가 특정 명령을 실행할 경우 표현된 세계가 어떻게 변화할지를 추정한다. 서로 다른 행동 시퀀스(action sequence)는 물리적으로 실행하기 전에 비교할 수 있는 대안적인 잠재 미래(alternative latent future)를 생성한다. 이는 모든 가상 결과를 완전한 감각 데이터로 생성하지 않고도 반사실적 추론(counterfactual reasoning), 모델 기반 제어(model-based control), 상상된 궤적(imagined trajectory)을 통한 계획을 수행하는 기반이 된다.

따라서 표현 공간에서의 예측은 월드 모델의 목적을 미래 관측의 정확한 복사본을 생성하는 것에서 현실에 대한 유용한 예측적 추상화(predictive abstraction)를 유지하는 것으로 변화시킨다. 핵심 목표는 중요한 정보를 인코딩하고, 그 정보가 어떻게 변화하는지를 예측하며, 예측된 상태를 추론(reasoning)과 제어(control)에 활용할 수 있도록 만드는 것이다. JEPA와 관련 잠재 예측 아키텍처(latent predictive architecture)에서 이러한 원리는 자기지도 지각(self-supervised perception)에서 예측적이고 행동 인식적인 내부 모델(action-aware internal model)로 발전하기 위한 확장 가능한 경로를 피지컬 AI에 제공한다.

## 04.03. Context Target and Predictor Networks

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

문맥, 목표, 예측기 네트워크(Context, Target, and Predictor Networks)는 공동 임베딩 예측 아키텍처(Joint Embedding Predictive Architectures)의 핵심 계산 구조를 형성한다. 이들은 이용 가능한 관측이 어떻게 잠재 표현(latent representation)으로 변환되고, 누락되거나 숨겨져 있거나 미래에 존재하는 정보가 어떻게 추론되는지를 함께 정의한다. 세 구성요소를 분리함으로써 모델은 현재 알고 있는 정보, 예측해야 할 정보, 그리고 두 표현을 연결하는 데 필요한 변환을 명확하게 구분할 수 있다.

문맥 네트워크(context network)는 모델이 직접 이용할 수 있는 정보를 처리한다. 관측(observation), 시퀀스(sequence), 보이는 이미지 영역, 센서 측정값 또는 다중모달 입력(multimodal input)은 먼저 잠재 문맥 표현(latent context representation)으로 변환된다. 문맥 인코더(context encoder)는 원래 신호의 모든 세부 정보를 보존하기보다 객체, 기하 구조(geometry), 움직임, 공간적 관계, 시간적 의존성, 환경의 지속적인 특성과 같이 예측을 지원할 수 있는 구조적 정보를 포착하도록 학습된다.

문맥(context)은 반드시 하나의 관측에만 대응할 필요가 없다. 시간적 월드 모델링(temporal world modeling)에서는 장면이 어떻게 변화했는지를 함께 설명하는 여러 과거 관측을 포함할 수 있다. 공간 예측(spatial prediction)에서는 마스킹된 영역(masked region) 주변의 보이는 영역으로 구성될 수 있다. 다중모달 피지컬 AI(multimodal Physical AI)에서는 카메라, 라이다(LiDAR), 레이더(radar), IMU, 고유수용감각(proprioception)을 결합할 수 있다. 따라서 모델이 학습해야 하는 예측 관계에 따라 문맥을 정의할 수 있다.

목표 네트워크(target network)는 예측기(predictor)가 추정하도록 학습되는 표현을 제공한다. 목표 인코더(target encoder)는 선택된 목표 관측(target observation)을 학습의 기준으로 사용되는 잠재 임베딩(latent embedding)으로 변환한다. 목표는 미래 관측, 숨겨진 영역, 다른 시점(viewpoint), 다른 센서 모달리티(sensor modality), 또는 동일한 물리적 상황의 다른 일부를 나타낼 수 있다. 예측은 원시 관측 공간(raw observation space)에서 목표를 재구성하는 대신 예측기의 출력과 이렇게 인코딩된 목표를 비교하여 평가된다.

문맥(context)과 목표(target)의 분리는 모델이 어떤 지식을 추론해야 하는지를 결정하기 때문에 중요하다. 목표가 미래 프레임(future frame)에 대응하면 시스템은 시간적 관계와 장면 동역학(scene dynamics)을 학습해야 한다. 목표가 마스킹된 공간 영역이라면 공간 구조와 객체 관계를 학습해야 한다. 목표가 다른 센서 또는 시점에서 제공되면 예측 과정은 실제 물리 환경에 대해 모달리티 간(cross-modal) 또는 시점 일관적(viewpoint-consistent) 표현을 학습하도록 유도한다.

예측기 네트워크(predictor network)는 문맥 표현(context representation)과 목표 표현(target representation)을 연결한다. 예측기의 역할은 단순히 문맥 임베딩(context embedding)을 복사하는 것이 아니라, 문맥에서 이용할 수 있는 정보로부터 목표를 추론하는 데 필요한 변환(transformation)을 모델링하는 것이다. 아키텍처에 따라 예측기는 다층 네트워크(multilayer network), 어텐션 메커니즘(attention mechanism), 트랜스포머(Transformer), 순환 구조(recurrent structure), 또는 시공간 관계를 표현할 수 있는 다른 잠재 동역학 모듈(latent dynamics module)로 구현될 수 있다.

유용한 예측기(predictor)는 문맥과 목표가 서로 다른 위치, 시간, 시점 또는 모달리티에 존재할 수 있다는 점을 고려해야 한다. 따라서 위치 정보(positional information), 시간 인덱스(temporal index), 마스크 정보(mask information), 목표 설명자(target descriptor)를 제공하여 무엇을 예측해야 하는지 지정할 수 있다. 하나의 문맥 표현으로 여러 예측 질의(prediction query)를 지원할 수 있으므로 전체 관측을 반복적으로 인코딩하지 않고도 서로 다른 영역, 미래 지평(future horizon), 시점 또는 잠재 변수를 추정할 수 있다.

학습 신호(learning signal)는 예측된 목표 표현과 목표 인코더가 생성한 표현 사이의 차이에서 발생한다. 유사도(similarity), 거리(distance), 회귀 기반 목적 함수(regression-based objective)를 사용하여 예측 임베딩(predicted embedding)이 목표 임베딩에 가까워지도록 학습할 수 있다. 이러한 최적화가 잠재 공간(latent space)에서 수행되기 때문에 시스템은 정확한 질감, 조명 변화, 센서 잡음처럼 예측하기 어려운 저수준 세부 정보를 재구성하지 않고도 의미 있는 특성을 예측하도록 학습할 수 있다.

문맥 인코더(context encoder)와 목표 인코더(target encoder) 사이의 관계는 신중하게 설계되어야 한다. 두 네트워크가 모두 쉬운 해법을 향해 자유롭게 최적화되면 표현이 붕괴(representation collapse)하여 의미 있는 변동성을 잃을 수 있다. 따라서 JEPA 방식 아키텍처(JEPA-style architecture)는 일반적으로 두 경로 사이에 비대칭성(asymmetry)을 도입한다. 목표 표현은 제어된 업데이트(controlled update) 또는 관련 메커니즘을 통해 생성되어 충분히 안정적인 학습 신호를 제공하고, 문맥 경로는 이를 예측할 수 있는 표현을 학습한다.

이러한 비대칭성은 전통적인 인간 레이블링(human labeling)과 달리 변화하는 표현적 지도 신호(representational supervision)의 한 형태로 이해할 수 있다. 목표 네트워크는 관측 자체로부터 학습 목표를 생성하고, 문맥 네트워크와 예측기는 그 목표에 맞추도록 학습한다. 따라서 시스템은 대규모의 레이블 없는 감각 경험(unlabeled sensory experience)으로부터 학습할 수 있으며, 모든 물리적 상태를 사람이 직접 주석 처리하기 어려운 환경에서 문맥-목표 예측(context-target prediction)은 자기지도학습(self-supervised learning)에 특히 적합하다.

목표 선택(target selection)은 어떤 종류의 세계 표현(world representation)이 형성되는지에 큰 영향을 준다. 지나치게 쉬운 목표를 예측하면 모델이 의미 있는 구조를 학습하지 않고 국소적 상관관계(local correlation)에만 의존할 수 있다. 반대로 지나치게 어렵거나 예측 불가능한 목표는 약한 학습 신호를 제공할 수 있다. 따라서 효과적인 학습에서는 추상화(abstraction)를 요구하면서도 주어진 문맥으로부터 충분히 예측 가능한 공간적, 시간적 또는 다중모달 관계를 목표로 선택해야 한다.

시간적 분리(temporal separation)는 월드 모델(world model)을 위한 특히 중요한 학습 차원을 제공한다. 단기 목표(short-term target)는 즉각적인 움직임과 국소적 연속성(local continuity)의 표현을 촉진하는 반면, 장기 목표(long-term target)는 객체, 장면 구성, 환경 동역학에 관한 더욱 지속적인 정보를 요구한다. 여러 예측 지평(prediction horizon)을 결합하면 빠른 상태 변화와 느린 구조적 변화 모두를 지원하는 표현을 학습할 수 있으며, 이를 통해 피지컬 AI를 위한 더욱 풍부한 내부 모델(internal model)을 형성할 수 있다.

로봇 시스템(robotic system)에서 문맥 네트워크는 궁극적으로 환경 관측과 함께 에이전트 자신의 상태를 포함할 수 있다. 고유수용감각(proprioception), 속도(velocity), 자세(orientation), 이전 행동(previous action), 감각 측정값이 문맥 표현에 기여할 수 있다. 이후 예측기는 가능한 미래 물리 상태를 설명하는 목표 표현을 추정할 수 있다. 이를 통해 아키텍처는 시각적 표현 학습(visual representation learning)에서 체화된 에이전트(embodied agent)가 환경과 상호작용하는 내부 예측 모델(internal predictive model)로 확장된다.

행동 조건화(action conditioning)는 또 다른 중요한 확장이다. 행동 표현(action representation)이 예측기에 제공되면 예측된 목표는 수동적인 환경 변화뿐 아니라 로봇이 무엇을 하려고 하는지에 따라 달라질 수 있다. 따라서 동일한 문맥에서도 서로 다른 후보 행동(candidate action)은 서로 다른 예측 잠재 상태(predicted latent state)를 생성할 수 있다. 이러한 구조는 반사실적 예측(counterfactual prediction), 잠재 롤아웃(latent rollout), 모델 기반 계획(model-based planning), 내부적으로 시뮬레이션된 결과에 기반한 제어의 토대를 제공한다.

세 구성요소는 궁극적으로 예측 월드 모델(predictive world model)에서 상호보완적인 역할을 수행한다. 문맥 네트워크는 시스템이 현재 무엇을 알고 있는지 나타내고, 목표 네트워크는 어떤 의미 있는 표현을 예측해야 하는지를 정의하며, 예측기는 한 표현이 다른 표현과 어떻게 연결되는지를 학습한다. 이들의 상호작용은 원시 경험(raw experience)을 자기지도 예측 문제(self-supervised prediction problem)로 변환하며, 공간, 시간, 시점, 모달리티, 그리고 궁극적으로 행동 사이의 관계로부터 유용한 추상 표현이 형성되도록 한다.

피지컬 AI에서 이러한 아키텍처는 지각(perception)에서 예측 지능(predictive intelligence)으로 발전하기 위한 확장 가능한 경로를 제공한다. 문맥 인코더는 다중모달 관측을 지속적으로 요약하고, 목표 인코더는 미래 또는 숨겨진 경험으로부터 구조화된 학습 신호를 제공하며, 예측기는 잠재 상태 사이의 변환을 학습한다. 이러한 구성요소가 더 긴 시간 지평과 행동 조건부 전이(action-conditioned transition)로 확장되면 이해(understanding), 예측(anticipation), 계획(planning), 제어(control)를 지원하는 월드 모델의 핵심 구성요소가 된다.

## 04.04. Masked Latent Prediction

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

마스킹된 잠재 예측(masked latent prediction)은 문맥(context)에서 의도적으로 숨겨진 정보의 표현을 추론하도록 모델을 학습한다. 누락된 내용을 픽셀(pixel)이나 센서 공간(sensor space)에서 직접 재구성하는 대신, 모델은 마스킹된 영역 또는 관측에 대응하는 잠재 임베딩(latent embedding)을 예측한다. JEPA 방식 아키텍처(JEPA-style architecture)에서 이러한 방법은 마스킹(masking)을 정확한 감각 재구성보다 의미 있는 구조에 초점을 맞춘 자기지도 예측 문제(self-supervised prediction problem)로 전환한다.

이 과정은 관측(observation)이나 시퀀스(sequence)를 그대로 보이는 부분과 예측 목표(prediction target)가 될 부분으로 나누는 것에서 시작한다. 보이는 정보는 문맥 인코더(context encoder)에 의해 처리되어 문맥 표현(context representation)을 생성하고, 숨겨진 정보는 학습 과정에서 목표 인코더(target encoder)에 의해 별도로 처리된다. 예측기(predictor)는 문맥 표현과 마스킹된 위치를 설명하는 정보를 입력받아 숨겨진 목표에 대응하는 잠재 표현(latent representation)을 추정한다.

이는 누락된 픽셀, 토큰(token), 센서 값을 직접 재현하려는 마스킹 재구성 방법(masked reconstruction method)과 근본적으로 다르다. 원시 공간 재구성(raw-space reconstruction)은 모델이 질감(texture), 조명(illumination), 잡음(noise), 기타 저수준 세부 정보를 모델링하는 데 많은 용량을 사용하도록 만들 수 있다. 반면 마스킹된 잠재 예측은 주변 문맥과 일관된 누락 정보의 표현이 무엇인지를 추론하도록 하여 외형 변화에도 유용하게 유지되는 더 높은 수준의 관계를 학습하도록 유도한다.

마스킹(masking)은 모델이 입력을 단순히 복사하지 못하도록 정보 격차(information gap)를 만든다. 숨겨진 영역을 성공적으로 예측하려면 시스템은 보이는 객체, 기하 구조(geometry), 장면 배치(scene layout), 시간적 문맥(temporal context), 기타 관측 사이의 관계를 활용해야 한다. 따라서 마스크(mask)의 크기, 형태, 위치, 밀도, 분포를 통해 과제의 난이도를 조절할 수 있다. 적절하게 설계된 마스크는 예측 문제를 지나치게 쉽거나 불가능하게 만들지 않으면서 추론(inference)을 촉진한다.

공간적 마스킹(spatial masking)은 마스킹된 잠재 예측의 가장 직접적인 형태 중 하나이다. 이미지, 조감도 표현(BEV representation), 점유 지도(occupancy map), 포인트 클라우드 기반 특징 맵(point-cloud-derived feature map), 기타 공간 표현의 일부 영역을 문맥에서 제거할 수 있다. 모델은 주변 증거로부터 누락된 영역의 표현을 추론해야 한다. 이를 통해 객체 연속성(object continuity), 공간 구성, 기하학적 관계, 가림(occlusion), 그리고 피지컬 AI(Physical AI)에 중요한 더 큰 장면 구조에 대한 이해를 촉진할 수 있다.

시간적 마스킹(temporal masking)은 동일한 원리를 시간 축으로 확장한다. 시퀀스 내 하나 이상의 관측을 숨기고 이전, 이후 또는 주변 관측을 문맥으로 사용할 수 있다. 마스킹된 시간적 표현을 예측하려면 모델이 움직임과 환경 동역학(environmental dynamics)을 추론해야 한다. 미래 관측을 마스킹하고 과거 문맥만 제공하는 경우, 모델이 미래 잠재 상태(latent future state)를 추정해야 하므로 이 과제는 자연스럽게 예측 월드 모델링(predictive world modeling)에 가까워진다.

시공간 마스킹(spatiotemporal masking)은 여러 프레임(frame)이나 시간 단계(time step)에 걸쳐 선택된 영역을 숨김으로써 공간과 시간 차원을 결합한다. 움직이는 객체가 일부 관측에서는 사라지지만 궤적(trajectory)의 다른 부분은 보일 수 있다. 예측기는 공간적 관계와 시간적 연속성(temporal continuity)을 모두 이용해 누락된 표현을 추론해야 한다. 이러한 학습은 고립된 시각 특징이 아니라 지속적인 객체, 움직임 패턴, 장면 기하 구조, 동적 상호작용(dynamic interaction)을 인코딩하는 잠재 상태의 학습을 촉진할 수 있다.

마스킹된 예측은 센서 모달리티(sensor modality) 사이에서도 수행할 수 있다. 카메라 특징(camera feature)을 문맥으로 사용하면서 선택된 라이다(LiDAR) 표현을 목표로 설정하거나, 기하학적 관측을 이용해 누락된 시각 표현을 예측할 수 있다. 레이더(radar), 고유수용감각(proprioception), IMU 신호와 기타 모달리티에도 동일한 관계를 적용할 수 있다. 교차 모달 마스킹(cross-modal masking)은 서로 다른 감지 방식으로 관측되는 공통의 물리적 구조를 모델이 발견하도록 유도한다.

목표 표현(target representation)은 예측기가 실제로 무엇을 복원하도록 요구받는지를 결정하기 때문에 매우 중요하다. 목표 인코더(target encoder)는 숨겨진 관측을 잠재 임베딩으로 변환하여 수작업 레이블(manual label) 없이 지도 신호(supervisory signal)를 생성한다. 예측기는 숨겨진 원시 관측 자체에 접근할 필요가 없다. 인코딩된 목표에 가까운 표현을 생성하도록 학습하면 되므로 대규모의 레이블 없는 로봇 및 환경 데이터(unlabeled robot and environmental data)를 자기지도 표현 학습(self-supervised representation learning)에 활용할 수 있다.

마스킹 전략(masking strategy)은 표현 품질(representation quality)에 큰 영향을 미친다. 지나치게 작거나 쉽게 예측할 수 있는 마스크는 국소적 보간(local interpolation)만으로 해결될 수 있어 피상적인 상관관계를 학습하게 만들 수 있다. 반대로 지나치게 큰 마스크는 너무 많은 문맥을 제거하여 목표 자체가 근본적으로 모호해질 수 있다. 따라서 효과적인 학습은 이용 가능한 증거와 누락된 정보 사이의 균형을 유지해야 한다. 가변 마스크(variable mask)를 사용하면 다양한 난이도에 모델을 노출시켜 국소적 의존성과 전역적 의존성(global dependency)을 모두 추론할 수 있는 표현을 학습하도록 할 수 있다.

아키텍처는 서로 다른 입력이 거의 동일한 잠재 임베딩을 생성하여 예측 과제가 무의미해지는 표현 붕괴(representation collapse)도 방지해야 한다. 비대칭 문맥 및 목표 경로(asymmetric context and target pathways), 제어된 목표 네트워크 업데이트(controlled target-network update), 정규화(normalization), 분산 보존 목적 함수(variance-preserving objective), 기타 정규화 메커니즘(regularization mechanism)을 통해 정보성이 높은 표현을 유지할 수 있다. 마스킹만으로 유용한 학습이 보장되는 것은 아니며, 잠재 공간은 의미 있는 물리적 상태를 구별할 수 있을 정도의 다양성을 유지해야 한다.

장기 월드 모델링(long-horizon world modeling)에서 마스킹된 잠재 예측은 불확실성이 증가할수록 추상화(abstraction)의 수준을 높일 수 있는 방법을 제공한다. 시간이 길어질수록 다양한 저수준 결과가 가능하기 때문에 정확한 미래 관측을 예측하는 것은 점점 어려워진다. 그러나 잠재 표현을 예측하면 모델은 하나의 정확한 미래 감각 결과에 고정되지 않으면서 장면 구성, 객체 행동, 움직임 경향(motion tendency), 가능한 상호작용에 관한 안정적인 정보를 유지할 수 있다.

피지컬 AI에서 마스킹 개념은 단순히 인위적인 학습 연산(training operation) 이상의 의미를 가진다. 실제 로봇은 가림(occlusion), 제한된 시야(field of view), 센서 성능 저하(sensor degradation), 통신 손실(communication loss), 부분 관측성(partial observability)으로 인해 지속적으로 누락된 정보를 경험한다. 따라서 마스킹된 표현을 추론하도록 모델을 학습하는 것은 실제 배치(deployment) 환경에서 발생하는 조건과 유사하다. 학습된 세계 표현은 물리 환경의 일부를 직접 관측할 수 없는 상황에서도 유용한 내부 상태(internal state)를 유지하는 능력을 향상시킬 수 있다.

마스킹된 잠재 예측은 기억(memory)으로 확장되는 자연스러운 연결 고리도 제공한다. 이전 시점에 보이던 정보가 나중에 가려질 수 있지만, 시간적 문맥 표현(temporal context representation)은 해당 정보의 존재와 동역학에 관한 증거를 유지할 수 있다. 현재 관측과 저장된 문맥으로부터 숨겨진 상태를 예측하도록 학습하면 시스템이 지속적인 개체(persistent entity)의 표현을 유지하도록 촉진한다. 이러한 능력은 내비게이션(navigation), 조작(manipulation), 자율주행(autonomous driving), 동적 환경에서의 상호작용에 중요하다.

행동(action)을 포함하면 마스킹된 예측은 행동 조건부 잠재 예측(action-conditioned latent prediction)으로 발전할 수 있다. 모델은 현재 문맥과 의도된 로봇 행동을 함께 입력받고, 학습 과정에서 숨겨진 미래 상태의 잠재 표현을 예측할 수 있다. 서로 다른 행동은 서로 다른 목표 상태(target state)를 의미할 수 있으므로 예측기는 개입(intervention)이 환경을 어떻게 변화시키는지를 학습해야 한다. 이를 통해 아키텍처는 수동적인 완성(passive completion)에서 인과적이고 제어 가능한 세계 예측(causal and controllable world prediction)으로 발전한다.

따라서 마스킹된 잠재 예측은 물리 환경의 내부 표현(internal representation)을 학습하기 위한 강력한 자기지도 메커니즘(self-supervised mechanism)으로 기능한다. 선택된 정보를 숨기고 이용 가능한 문맥으로부터 그 표현을 추론하도록 함으로써 모델은 공간, 시간, 시점(viewpoint), 모달리티, 그리고 궁극적으로 행동 사이의 관계를 학습한다. JEPA 기반 월드 모델(JEPA-based world model)에서 이는 표현 학습에서 강건한 잠재 동역학(robust latent dynamics), 부분 관측 추론(partial-observation reasoning), 미래 예측, 계획(planning), 제어(control)로 발전하기 위한 확장 가능한 경로를 제공한다.

## 04.05. Self Supervised Latent World Modeling

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

자기지도 잠재 월드 모델링(self-supervised latent world modeling)은 지능형 에이전트(intelligent agent)가 밀집된 인간 주석(dense human annotation) 없이 대규모 감각 경험(sensory experience)으로부터 물리 세계의 내부 표현(internal representation)을 직접 학습할 수 있도록 한다. 모든 객체, 상태, 움직임, 상호작용에 명시적인 레이블(label)을 부여하는 대신, 데이터에 이미 존재하는 관계로부터 지도 신호(supervisory signal)를 생성한다. 예측(prediction), 마스킹(masking), 시간적 연속성(temporal continuity), 다중 시점(multiple viewpoints), 센서 간 대응 관계(sensor correspondence)가 학습을 위한 지도 정보가 된다.

핵심 목표는 원시 관측(raw observation)을 환경이 어떻게 구성되어 있으며 어떻게 변화하는지를 이해하는 데 필요한 정보를 보존하는 잠재 상태(latent state)로 변환하는 것이다. 카메라, 라이다(LiDAR), 레이더(radar), IMU, 고유수용감각(proprioception), 기타 센서는 매우 고차원의 데이터 스트림을 생성하지만, 월드 모델(world model)이 모든 측정값을 재현할 필요는 없다. 대신 인코더(encoder)는 지속적인 기하 구조(geometry), 객체, 움직임, 의미 정보(semantics), 상호작용 관련 구조를 강조하는 압축된 표현을 학습할 수 있다.

자기지도(self-supervision)는 관측 자체로부터 예측 문제를 구성함으로써 발생한다. 이미지의 일부를 숨기고 주변 영역으로부터 예측하거나, 과거 문맥(context)으로부터 미래 관측을 예측하거나, 하나의 센서 표현으로부터 다른 모달리티(modality)의 표현을 추론할 수 있다. 문맥과 목표(target)가 모두 자연스럽게 수집된 데이터에서 생성되므로, 모든 관측에 대한 올바른 의미 해석을 사람이 직접 지정하지 않고도 시스템은 지속적으로 학습 사례를 생성할 수 있다.

잠재 예측(latent prediction)은 모델이 무엇을 학습해야 하는지를 변화시킨다. 픽셀 공간 예측(pixel-space prediction)은 질감(texture), 조명(illumination), 반사(reflection), 잡음(noise), 그리고 행동에는 중요하지 않지만 예측하기 어려운 수많은 세부 요소를 고려해야 한다. 반면 잠재 월드 모델(latent world model)은 방해 변동(nuisance variation)을 제거하면서 물리적 상황의 안정적인 특성을 유지할 수 있는 인코딩된 표현을 예측한다. 따라서 학습 문제는 감각적 외형을 재구성하는 것에서 환경의 예측 가능한 구조를 발견하는 것으로 전환된다.

시간적 자기지도(temporal self-supervision)는 월드 모델이 정적인 외형뿐 아니라 변화를 표현해야 하기 때문에 특히 중요하다. 서로 다른 시간에 수집된 관측은 현재 상태와 미래 상태 사이의 자연스러운 관계를 제공한다. 미래 잠재 표현(future latent representation)을 예측하면 모델이 움직임, 객체 지속성(object persistence), 환경 전이(environmental transition), 시간적 의존성(temporal dependency)을 포착하도록 유도할 수 있다. 더 긴 예측 지평(prediction horizon)은 오랜 시간 동안 안정적으로 예측 가능한 정보만 남기 때문에 더욱 높은 수준의 추상화(abstraction)를 촉진할 수 있다.

마스킹된 잠재 예측(masked latent prediction)은 또 다른 강력한 학습 신호를 제공한다. 선택된 영역, 시간 단계(time step), 특징 그룹(feature group)을 문맥에서 제거하고 해당 영역의 인코딩된 표현을 목표로 사용한다. 모델은 남아 있는 정보로부터 누락된 내용을 추론해야 한다. 공간 마스크(spatial mask)는 장면 구성과 기하 구조에 대한 이해를 촉진하고, 시간 마스크(temporal mask)는 동역학 학습(dynamics learning)을 촉진한다. 시공간 마스크(spatiotemporal mask)는 이러한 두 요구사항을 하나의 학습 과정에서 결합할 수 있다.

다중모달 감각 데이터 스트림(multimodal sensory stream)은 피지컬 AI(Physical AI)를 위한 추가적인 자기지도 형태를 제공한다. 서로 다른 센서는 동일한 물리적 상태의 서로 다른 측면을 관측한다. 시각 관측은 외형과 의미 단서(semantic cue)를 포함하고, 라이다는 기하 구조를 제공하며, 레이더는 거리와 움직임 정보를 제공하고, 고유수용감각은 에이전트 자신의 상태를 설명한다. 이러한 잠재 표현 사이의 관계를 예측하면 서로 다른 센싱 모달리티(sensing modality)에 걸친 물리적 일관성에 기반한 공유 세계 표현(shared world representation)을 학습하도록 유도할 수 있다.

다중 시점(multiple viewpoints) 역시 명시적인 레이블 없이 지도 정보를 제공할 수 있다. 여러 카메라 또는 서로 다른 위치에서 얻은 관측이 동일한 환경을 바라보는 경우, 모델은 시점이 변화하더라도 일관성을 유지하는 표현을 학습할 수 있다. 이를 통해 잠재 공간(latent space)은 특정 센서 이미지의 우연한 특성이 아니라 세계 자체에 속하는 특성을 인코딩하도록 학습된다. 이러한 불변성(invariance)은 위치와 방향이 지속적으로 변화하는 이동 로봇(mobile robot)에 특히 중요하다.

자기지도 잠재 월드 모델은 일반적으로 표현 공간(representation space)에서 동작하는 예측 메커니즘(predictive mechanism)과 인코더를 결합한다. 문맥 관측은 잠재 변수(latent variable)로 매핑되고, 예측기(predictor)는 숨겨지거나 미래에 존재하거나 현재 이용할 수 없는 정보에 대응하는 목표 표현을 추정한다. 학습 과정에서는 목표 인코딩(target encoding)이 기준 신호(reference signal)를 제공한다. 예측 표현과 목표 표현 사이의 차이가 학습을 유도하므로 모든 예측을 원래 감각 영역으로 다시 디코딩(decoding)할 필요가 없다.

잠재 상태(latent state)는 단순히 압축된 센서 데이터 이상의 것으로 이해해야 한다. 이상적으로는 여러 형태의 추론(inference)을 지원할 수 있는 내부 상태 표현(internal state representation)이 된다. 객체, 자유 공간(free space), 기하 구조, 움직임, 에이전트 상태(agent state), 환경 동역학에 관한 정보가 표현 전체에 분산되어 포함될 수 있다. 중요한 것은 물리 세계를 이해하는 데 의미 있게 기여하지 않는 세부 정보는 제거하면서 예측과 미래 행동에 필요한 구별 정보를 보존하는 것이다.

표현 붕괴(representation collapse)를 방지하는 것은 여전히 근본적인 요구사항이다. 인코더가 서로 다른 관측을 거의 동일한 잠재 상태로 매핑하면 모델은 유용한 구조를 학습하지 않고도 예측 목적을 만족시킬 수 있다. 따라서 자기지도 잠재 아키텍처(self-supervised latent architecture)는 임베딩(embedding)의 정보와 다양성을 유지하는 메커니즘을 필요로 한다. 비대칭 문맥 및 목표 경로(asymmetric context and target pathways), 제어된 목표 업데이트(controlled target update), 정규화(normalization), 분산 제약(variance constraint), 기타 정규화 전략(regularization strategy)을 통해 학습을 안정화할 수 있다.

관측이 불완전한 환경에서는 기억(memory)이 점점 더 중요해진다. 물리적 에이전트는 객체의 가림(occlusion), 센서의 제한된 시야(field of view), 로봇 이동에 따른 정보 소실 때문에 한 순간에 전체 환경을 관측하기 어렵다. 시간적 잠재 표현(temporal latent representation)은 이전 관측의 증거를 유지하면서 현재 감각 입력과 결합할 수 있다. 따라서 시간에 걸친 자기지도 예측은 부분 관측성(partial observability)에서도 유용한 내부 상태를 유지하도록 모델을 학습할 수 있다.

다음의 중요한 확장은 행동 조건부 잠재 월드 모델링(action-conditioned latent world modeling)이다. 수동적인 관측은 환경이 일반적으로 어떻게 변화하는지를 학습하게 하지만, 체화된 에이전트(embodied agent)는 자신의 행동이 이러한 변화에 어떤 영향을 미치는지도 학습해야 한다. 잠재 상태와 모터 명령(motor command) 또는 상위 수준 행동(high-level action)을 결합하면 예측기가 그 결과로 나타날 미래 상태의 표현을 추정할 수 있다. 상호작용을 통해 생성된 경험은 상태-행동-전이 관계(state-action-transition relationship)를 학습하기 위한 자기지도 사례를 제공할 수 있다.

행동 조건부 동역학(action-conditioned dynamics)이 학습되면 월드 모델은 내부 롤아웃(internal rollout)을 지원할 수 있다. 서로 다른 후보 행동(candidate action) 또는 행동 시퀀스를 현재 잠재 상태에 적용하여 여러 대안적 미래(alternative future)를 예측할 수 있다. 이러한 미래는 실제 물리 환경에서 행동을 실행하기 전에 과업 목표(task objective), 안전 제약(safety constraint), 비용(cost), 기대 보상(expected reward)에 따라 평가할 수 있다. 따라서 잠재 월드 모델은 지각(perception), 예측(prediction), 계획(planning), 제어(control)를 연결하는 계산적 기반(computational substrate)이 된다.

대규모 자기지도학습(large-scale self-supervised learning)은 로봇이 잠재적으로 막대한 양의 운용 데이터(operational data)를 축적할 수 있다는 점에서 피지컬 AI에 특히 매력적이다. 주행(driving), 내비게이션(navigation), 조작(manipulation), 검사(inspection), 인간-로봇 상호작용(human-robot interaction)은 공간적, 시간적, 다중모달, 행동 의존적 구조를 포함하는 관측을 지속적으로 생성한다. 잠재 월드 모델링을 이용하면 이러한 데이터 대부분을 레이블이 없어 사용할 수 없는 데이터로 취급하는 대신, 일반적인 체화 경험(embodied experience)을 지속적인 학습 신호의 원천으로 전환할 수 있다.

따라서 자기지도 잠재 월드 모델링은 방대한 수작업 주석 없이 감각 데이터에서 예측 가능한 내부 표현으로 발전하기 위한 경로를 제공한다. 마스킹된 정보, 시간적 전이(temporal transition), 다중 시점, 센서 간 관계, 그리고 궁극적으로 행동으로부터 학습함으로써 모델은 물리적 경험에 존재하는 재사용 가능한 구조(reusable structure)를 발견할 수 있다. JEPA 및 관련 잠재 예측 아키텍처(latent predictive architecture)에서 이러한 접근법은 지각, 예측(anticipation), 추론(reasoning), 계획, 제어가 가능한 확장형 월드 모델(scalable world model)의 기반을 형성한다.

## 04.06. JEPA vs Generative World Models

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

JEPA와 생성형 월드 모델(generative world model)은 환경에 대한 예측 모델(predictive model)을 학습하기 위한 서로 다른 두 가지 전략을 나타낸다. 생성형 접근법(generative approach)은 미래의 감각 데이터(sensory data)를 재구성하거나 생성할 수 있을 정도로 관측을 모델링하려는 반면, 공동 임베딩 예측 아키텍처(Joint Embedding Predictive Architectures)는 미래 또는 숨겨진 정보 가운데 중요한 부분의 표현(representation)을 예측하는 데 초점을 둔다. 두 접근법의 차이는 예측을 수행하는지 여부가 아니라 세계를 어느 수준에서 예측하도록 요구하는지에 있다.

생성형 월드 모델은 일반적으로 이미지, 비디오 프레임(video frame), 점유 구조(occupancy structure), 센서 측정값(sensor measurement), 또는 가능한 미래 상태를 설명하는 기타 데이터를 생성하도록 학습한다. 아키텍처에 따라 자기회귀 모델(autoregressive model), 변분 방법(variational method), 확산 모델(diffusion model), 또는 관련 기법을 사용할 수 있다. 따라서 모델은 센서가 실제로 관측할 수 있는 것과 유사한 현실적인 결과를 합성할 수 있도록 관측 분포(observation distribution)를 충분히 표현하려고 한다.

이러한 생성 능력(generative capability)은 생성된 관측을 사람이 직접 해석할 수 있기 때문에 매우 유용할 수 있다. 예측 비디오(predicted video)는 예상되는 객체 움직임을 보여줄 수 있고, 생성된 점유 정보(occupancy)는 미래의 공간 구조를 설명할 수 있으며, 시뮬레이션된 관측(simulated observation)은 에이전트가 가능한 결과를 평가할 수 있는 환경을 제공한다. 따라서 생성형 모델은 현실적인 감각 예측 자체가 학습, 평가, 시각화 또는 합성 경험 생성(synthetic experience generation)에 중요한 경우 학습된 시뮬레이터(learned simulator)로 기능할 수 있다.

그러나 원시 감각 예측(raw sensory prediction)은 상당한 불확실성과 불필요한 세부 정보를 포함한다. 장면의 미래 외형은 조명(illumination), 질감(texture), 그림자(shadow), 반사(reflection), 식생의 움직임, 센서 잡음(sensor noise), 그리고 에이전트의 의사결정에는 거의 영향을 미치지 않는 수많은 변수에 따라 달라질 수 있다. 생성형 모델은 현실적인 관측을 생성하기 위해 이러한 요소까지 모델링해야 하므로 물리적 동역학(physical dynamics)을 이해하는 데 필수적이지 않더라도 상당한 모델 용량(model capacity)을 할당할 수 있다.

JEPA는 원래 관측을 재구성하도록 요구하는 대신 표현 공간(representation space)에서 예측한다는 점에서 다른 접근법을 취한다. 문맥 관측(context observation)은 잠재 표현(latent representation)으로 인코딩되고, 예측기(predictor)는 목표 관측(target observation), 영역 또는 미래 상태의 표현을 추정한다. 따라서 학습 목표는 감각 신호에 나타날 수 있는 모든 관측 가능한 세부 정보를 예측하는 것이 아니라 목표 네트워크(target network)에 의해 인코딩된 의미 있는 추상 정보를 예측하는 것이다.

이러한 차이는 외형의 예측(prediction of appearance)과 추상화의 예측(prediction of abstraction)으로 이해할 수 있다. 생성형 모델은 미래가 어떻게 보일 것인가를 예측하려는 반면, JEPA 방식 모델(JEPA-style model)은 그 미래를 특징짓는 의미 있는 상태나 구조가 무엇인지를 추정하려고 한다. 생성형 모델 역시 잠재 공간(latent space)에서 동작할 수 있기 때문에 이러한 경계가 절대적인 것은 아니지만, JEPA는 예측된 표현을 완전한 감각 결과로 디코딩(decoding)하는 것을 주요 학습 목표로 요구하지 않는다.

이러한 차이는 미래가 다중양상적(multimodal)일 때 특히 중요해진다. 서로 다른 많은 감각적 결과가 본질적으로 동일한 물리적 상황에 대응할 수 있다. 보행자는 동일한 경로를 계속 이동하면서도 매우 다양한 자세를 취할 수 있으며, 실외 장면은 동일한 내비게이션 구조(navigational structure)를 유지하면서 수많은 픽셀 수준의 변화를 보일 수 있다. 표현 예측(representation prediction)은 이러한 변화를 부차적인 것으로 처리하면서 추론(reasoning)과 행동(action)에 중요한 상위 수준 정보를 보존할 수 있다.

장기 예측(long-horizon prediction)은 이러한 장점을 더욱 확대한다. 일반적으로 예측 지평(prediction horizon)이 길어질수록 픽셀 수준의 불확실성이 빠르게 증가하여 정확한 미래 생성이 점점 어려워진다. 반면 객체 지속성(object persistence), 대략적인 움직임, 장면 위상(scene topology), 주행 가능성(traversability), 상호작용 가능성(interaction possibility)과 같은 상위 수준 특성은 훨씬 오랫동안 예측 가능할 수 있다. JEPA 방식 잠재 예측은 불확실성이 증가하는 감각적 세부 정보를 반복적으로 생성하는 대신 이러한 지속적인 구조에 모델링 능력을 집중할 수 있다.

그럼에도 생성형 모델은 명시적인 미래 관측(explicit future observation)이 필요한 경우 중요한 장점을 가진다. 로봇 개발 시스템은 시각화(visualization), 합성 데이터 생성(synthetic data generation), 시뮬레이션(simulation), 인간에 의한 검사(human inspection), 또는 후속 지각 모델(downstream perception model)의 학습을 위해 현실적인 미래 이미지가 필요할 수 있다. 비디오 생성(video generation)은 수작업으로 정의하기 어려운 풍부한 환경의 가능성을 표현할 수도 있다. 이러한 경우 세계 상태를 실제 관측 가능한 감각 결과로 디코딩하는 능력은 불필요한 계산 부담이 아니라 중요한 기능이 된다.

계산 요구량(computational requirement)에서도 차이가 존재한다. 고해상도 생성형 예측(high-resolution generative prediction)은 여러 미래 단계에서 많은 수의 픽셀, 복셀(voxel), 포인트(point), 토큰(token)을 생성해야 하기 때문에 높은 계산 비용을 요구할 수 있다. 표현 공간 예측은 훨씬 작은 잠재 상태에서 동작하면서 각각의 예측된 미래를 디코딩하지 않아도 된다. 따라서 JEPA 방식 아키텍처는 엄격한 지연시간(latency), 메모리(memory), 에너지(energy), 엣지 컴퓨팅(edge computing) 제약에서 동작하는 피지컬 AI(Physical AI) 시스템에 매력적인 선택이 될 수 있다.

두 접근법은 방해 정보(nuisance information)를 처리하는 방식에서도 차이를 보인다. 생성형 목적 함수(generative objective)는 일반적으로 관측 분포를 재현하는 데 필요한 모든 정보를 정확하게 모델링하도록 보상한다. 반면 JEPA 방식 목적 함수는 목표 표현을 일치시키는 데 필요하지 않다면 인코더가 예측 불가능하거나 행동적으로 중요하지 않은 변동을 제거하도록 허용할 수 있다. 따라서 생성된 잠재 공간은 예측에 유용한 구조를 강조하면서 세계 이해에 기여하지 않는 세부 정보를 억제하는 정보 병목(information bottleneck)으로 작동할 수 있다.

그러나 어느 접근법도 자동으로 유용한 월드 모델을 생성하는 것은 아니다. 생성형 시스템은 인과적 또는 제어 가능한 동역학(causal or controllable dynamics)을 충분히 포착하지 못한 채 피상적인 외형만 학습할 수 있으며, 표현 기반 시스템(representation-based system)은 잠재 공간이 지나치게 압축될 경우 필수 정보를 잃을 수 있다. 또한 JEPA 아키텍처는 표현 붕괴(representation collapse)의 문제를 가지므로 정보성이 높은 임베딩(embedding)을 유지하기 위한 메커니즘이 필요하다. 따라서 월드 모델의 품질은 단순히 예측 형식만이 아니라 학습 목적, 아키텍처, 데이터, 시간적 구조, 행동 조건화(action conditioning)에 의해 결정된다.

피지컬 AI에서 행동(action)은 결정적인 요구사항을 추가한다. 유용한 월드 모델은 단순히 다음에 무엇이 일어날지를 예측하는 것뿐만 아니라 가능한 미래가 에이전트의 행동에 따라 어떻게 달라지는지도 예측해야 한다. 생성형 모델과 JEPA 방식 모델 모두 행동 조건부(action-conditioned) 모델로 확장될 수 있다. 생성형 모델은 후보 행동(candidate action)에 따른 미래 관측을 합성할 수 있으며, JEPA 모델은 이에 대응하는 미래 잠재 상태(future latent state)를 예측할 수 있다. 따라서 두 접근법 모두 서로 다른 표현 수준에서 반사실적 추론(counterfactual reasoning)을 지원할 수 있다.

계획(planning)은 이러한 실질적인 상충관계(tradeoff)를 잘 보여준다. 생성형 계획기(generative planner)는 세부적인 감각적 미래를 상상하고 평가할 수 있지만, 수많은 후보 행동 시퀀스(candidate action sequence)에 대해 고차원 관측을 반복적으로 생성하면 높은 계산 비용이 발생할 수 있다. 반면 잠재 예측 계획기(latent predictive planner)는 압축된 표현을 롤아웃(rollout)하고 잠재 공간에서 비용(cost), 보상(reward), 위험(risk), 목표 적합성(goal compatibility)을 직접 추정한 뒤 필요한 경우에만 디코딩할 수 있다. 이는 실시간 로봇 의사결정(real-time robotic decision making)을 위한 효율적인 내부 상상 메커니즘(internal imagination mechanism)을 제공할 수 있다.

따라서 JEPA와 생성형 월드 모델의 관계를 서로 배타적인 아키텍처 중 하나를 선택해야 하는 문제로 볼 필요는 없다. 하나의 시스템은 효율적인 상태 추정(state estimation)과 장기 추론(long-horizon reasoning)을 위해 표현 예측을 사용하면서, 세부적인 감각 결과가 필요한 경우 생성형 구성요소(generative component)를 사용할 수 있다. 잠재 예측은 계획을 안내하고, 디코더(decoder) 또는 생성형 모델은 필요한 단계에서 시각화, 시뮬레이션, 재구성 또는 고해상도 예측을 제공할 수 있다.

이러한 하이브리드 아키텍처(hybrid architecture)는 다중모달 피지컬 AI(multimodal Physical AI)에서 특히 중요하다. 압축된 공유 잠재 상태(shared latent state)는 카메라, 라이다, 레이더, 고유수용감각(proprioception), 기타 관측을 통합할 수 있으며, 예측 동역학(predictive dynamics)은 이 상태가 어떻게 변화하는지를 추정할 수 있다. 이후 필요할 때 선택된 생성 헤드(generative head)를 통해 특정 모달리티를 재구성하거나 합성할 수 있다. 이를 통해 세계를 이해하고 예측하는 계산 문제와 그 이해를 바탕으로 세부 관측을 렌더링(rendering)하는 선택적 문제를 분리할 수 있다.

결국 JEPA와 생성형 월드 모델은 서로 보완적인 능력을 강조한다. 생성형 접근법은 풍부하고 관측 가능한 미래와 학습된 시뮬레이션(learned simulation)을 제공하는 반면, JEPA는 추상화(abstraction), 효율적인 표현 공간 예측, 경험으로부터 지속적인 구조를 추출하는 능력을 강조한다. 피지컬 AI를 위한 가장 효과적인 월드 모델은 이러한 원리를 결합하여 확장 가능한 추론과 계획에는 잠재 예측을 사용하고, 명시적인 감각적 미래가 추가적인 가치를 제공하는 경우에는 생성(generation)을 활용하는 형태로 발전할 수 있다.

## 04.07. Video JEPA and Temporal Prediction

![](images/image7.png){width="7.268055555555556in" height="7.268055555555556in"}

비디오 JEPA(Video JEPA)는 공동 임베딩 예측 아키텍처(Joint Embedding Predictive Architectures)의 원리를 개별 관측에서 시각적 관측의 시퀀스(sequence)로 확장한다. 각 비디오 프레임(video frame)을 독립적인 이미지로 처리하는 대신, 시간에 따라 시각 정보가 어떻게 변화하는지를 포착하는 표현을 학습한다. 핵심 목표는 미래의 모든 픽셀을 재구성하는 것이 아니라 미래 또는 숨겨진 비디오 상태(video state)의 의미 있는 잠재 표현(latent representation)을 예측하는 것이다. 이를 통해 시간적 예측(temporal prediction)은 잠재 월드 모델링(latent world modeling)의 자연스러운 구성요소가 된다.

비디오 시퀀스(video sequence)는 인접한 프레임들이 물리적 연속성(physical continuity)에 의해 서로 연결되어 있기 때문에 풍부한 시간적 구조(temporal structure)를 제공한다. 객체는 일반적으로 지속되고, 카메라와 로봇은 일관된 궤적(coherent trajectory)을 따라 움직이며, 환경의 변화는 무작위로 발생하기보다 일정한 패턴을 따른다. 비디오 JEPA는 시간적 문맥(temporal context)을 인코딩하고 이후 관측에 대응하는 표현을 예측함으로써 이러한 관계를 활용할 수 있다. 결과적으로 잠재 공간(latent space)은 움직임, 지속성, 장면 변화(scene evolution), 시간적 의존성(temporal dependency)을 표현할 수 있다.

비디오 예측(video prediction)의 문맥은 하나의 이미지가 아니라 여러 개의 연속된 프레임으로 구성될 수 있다. 인코더(encoder)는 이 시퀀스를 공간과 시간에 걸쳐 분포된 정보를 포함하는 압축된 표현(compact representation)으로 변환한다. 이후 예측기(predictor)는 미래 프레임, 미래 세그먼트(segment), 또는 선택된 시간적 목표(temporal target)의 표현을 추정한다. 목표 표현(target representation)은 학습 과정에서 별도로 생성될 수 있으므로, 시스템은 완전한 픽셀 수준 재구성(pixel-level reconstruction) 없이 예측 임베딩(predicted embedding)과 목표 임베딩(target embedding)을 비교할 수 있다.

시간적 예측은 여러 예측 지평(prediction horizon)에서 수행될 수 있다. 단기 예측(short-horizon prediction)은 국소적인 움직임(local motion)이나 객체 이동(object displacement)과 같은 즉각적인 변화를 다루는 반면, 장기 예측(long-horizon prediction)은 장면의 더욱 지속적인 특성을 보존하도록 요구한다. 예측 지평이 길어질수록 정확한 픽셀 예측은 가능한 시각적 미래가 다양하기 때문에 점점 더 불확실해진다. 잠재 예측(latent prediction)은 객체 정체성(object identity), 대략적인 궤적, 공간적 관계(spatial relationship), 장면 구조(scene structure)와 같은 안정적인 정보에 집중함으로써 유용성을 유지할 수 있다.

비디오 JEPA는 마스킹된 시간적 예측(masked temporal prediction)도 사용할 수 있다. 전체 시퀀스를 제공하는 대신 선택된 프레임, 패치(patch), 시간적 영역을 문맥에서 숨길 수 있다. 모델은 보이는 정보로부터 이들의 잠재 표현을 추론해야 한다. 이를 통해 표현은 시간에 걸친 관계를 포착하도록 강제되며, 예측기가 바로 이전 프레임을 단순히 복사하는 것을 방지한다. 따라서 시간적 마스킹(temporal masking)은 움직임과 장면 동역학(scene dynamics)에 대한 더욱 깊은 이해를 촉진할 수 있다.

공간적 마스킹(spatial masking)과 시간적 마스킹을 결합하여 시공간 예측(spatiotemporal prediction) 과제를 구성할 수도 있다. 모델은 여러 프레임에 걸쳐 미래의 특정 영역이 숨겨진 상태에서 그 영역을 예측해야 할 수 있으며, 이를 위해 객체가 어디에 있는지와 어떻게 움직이고 있는지를 동시에 이해해야 한다. 이는 물리적 AI(Physical AI)에서 특히 중요하다. 환경의 미래 상태는 공간 구조와 시간적 변화에 동시에 의존하기 때문이다. 이러한 예측은 움직이는 객체, 변화하는 점유 상태(occupancy), 상호작용 패턴, 동적 장면 기하 구조(dynamic scene geometry)를 표현하는 데 활용될 수 있다.

비디오 JEPA는 반드시 하나의 결정론적 미래(deterministic future)를 가정할 필요가 없다. 물리적 환경에는 특히 사람, 차량, 동물 또는 기타 에이전트가 포함될 경우 여러 가지 가능한 결과가 존재한다. 표현 공간 예측기(representation-space predictor)는 모든 저수준 시각 세부 정보를 하나로 선택하지 않고 여러 가능한 미래에 공통적으로 존재하는 특징을 학습할 수 있다. 이는 불확실성(uncertainty)을 다루는 데 유용한 추상화를 제공하며, 모델은 예측 가능한 구조를 유지하면서 하나의 정확한 픽셀 수준 결과에 불필요하게 고정되지 않을 수 있다.

시간적 표현 학습(temporal representation learning)은 서로 다른 시간적 규모가 서로 다른 종류의 정보를 포함하기 때문에 더 긴 시퀀스를 사용할 때도 이점을 얻는다. 매우 짧은 시간 간격에서는 빠른 움직임과 국소적 상호작용이 나타나는 반면, 긴 시퀀스에서는 지속적인 행동, 경로 구조(route structure), 환경 변화, 반복적인 패턴이 나타난다. 따라서 계층적 또는 다중 지평 접근법(hierarchical or multi-horizon approach)을 사용하면 월드 모델이 빠른 동역학과 느린 변화를 모두 표현할 수 있다. 이는 예측, 기억(memory), 계획(planning), 제어(control)를 위한 더욱 강력한 기반을 제공한다.

로보틱스(robotics)에서 비디오 JEPA는 시각 프레임 이상의 정보를 통합할 수 있다. 카메라 관측은 깊이(depth), 라이다(LiDAR), 고유수용감각(proprioception), IMU 측정값, 행동(action), 기타 시간적 신호와 결합될 수 있다. 모델은 시각적 변화가 로봇 자신의 움직임 및 환경 동역학과 연결되는 공유 잠재 표현(shared latent representation)을 학습할 수 있다. 이는 로봇이 움직일 때 카메라 이미지가 크게 변할 수 있지만 실제 물리적 환경 자체는 동일하게 유지될 수 있기 때문에 중요하다.

행동 조건화(action conditioning)는 시간적 예측을 확장하는 또 하나의 중요한 방법이다. 과거 관측만으로 미래를 예측하는 대신 모델은 현재 잠재 상태와 함께 후보 행동 시퀀스를 입력받을 수 있다. 이후 서로 다른 행동에 따라 잠재적 미래가 어떻게 달라지는지를 추정할 수 있다. 이를 통해 수동적인 시간적 예측(passive temporal prediction)은 행동을 인식하는 예측 모델(action-aware predictive model)로 발전하며, 반사실적 롤아웃(counterfactual rollout), 계획(planning), 모델 기반 제어(model-based control)를 지원할 수 있다. 더 넓은 월드 모델 구조에서 행동 조건부 예측(action-conditioned prediction)은 JEPA 아키텍처의 후속 확장으로 포함된다.

비디오 JEPA는 주요 목표가 시각적 렌더링(visual rendering)이 아니라 추론(reasoning)인 경우 완전한 생성형 비디오 예측(full generative video prediction)에 대한 효율적인 대안이 될 수 있다. 모든 미래 프레임을 생성하려면 모델이 질감, 조명, 세부적인 외형, 기타 의사결정에 중요하지 않을 수 있는 요소를 표현해야 한다. 압축된 잠재 상태(compact latent state)를 예측하면 미래 행동에 필요한 정보를 유지하면서 계산량과 메모리 요구량을 줄일 수 있다. 세부적인 시각화나 감각 재구성(sensory reconstruction)이 필요한 경우에는 생성형 디코더(generative decoder)를 추가할 수도 있다.

학습 신호(training signal)는 대규모의 레이블 없는 비디오(unlabeled video) 데이터에서 직접 생성할 수 있다. 로봇 궤적(robot trajectory), 자율주행 시퀀스(autonomous driving sequence), 시뮬레이션 데이터(simulation data), 기타 시간적 시각 경험은 자연스럽게 문맥-목표 관계(context-target relationship)를 포함한다. 모델은 프레임 단위의 의미 레이블(semantic label)을 요구하지 않고 이러한 관계로부터 학습할 수 있다. 따라서 대규모 자기지도 시간 학습(large-scale self-supervised temporal learning)은 일반적인 물리 동역학과 환경 변화에 대한 표현을 학습하기 위한 훈련 데이터로 일반적인 비디오 경험을 전환할 수 있다.

중요한 과제 중 하나는 모델이 피상적인 시간적 상관관계(superficial temporal correlation)를 학습하는 것을 방지하는 것이다. 단순히 다음 프레임을 예측하는 것은 모델이 근본적인 물리적 상태를 이해하지 않고 저수준의 시각적 연속성에 의존하도록 만들 수 있다. 따라서 효과적인 비디오 JEPA 학습은 의미 있는 시간적 추상화(temporal abstraction)를 요구하는 예측 과제를 구성해야 한다. 마스킹, 여러 예측 지평, 다양한 문맥, 신중하게 선택된 목표 관계를 사용하면 모델이 국소적인 외형을 단순히 기억하는 대신 지속적인 구조를 학습하도록 유도할 수 있다.

학습된 시간적 표현(temporal representation)은 더 넓은 월드 모델을 위한 기반이 될 수 있다. 현재 관측은 잠재 상태로 인코딩되고, 시간적 예측기는 미래의 잠재 상태를 추정하며, 기억 메커니즘(memory mechanism)은 시간에 걸쳐 정보를 보존한다. 이후 계획 구성요소(planning component)는 가능한 잠재 미래를 평가하고, 제어 시스템(control system)은 선택된 예측을 이용하여 행동을 결정할 수 있다. 이러한 구조에서 비디오 예측은 독립적인 컴퓨터 비전 과제가 아니라 물리적 세계가 어떻게 변화하는지를 학습하는 메커니즘이 된다.

따라서 비디오 JEPA는 시각 표현 학습(visual representation learning)과 시간적 월드 모델링(temporal world modeling)을 연결한다. 시간에 걸쳐 잠재 표현을 예측함으로써 모델은 모든 감각적 세부 정보를 재현할 필요 없이 움직임, 지속성, 공간적 관계, 환경 동역학, 미래 구조를 학습할 수 있다. 더 넓은 JEPA 구조에서 이는 표현 공간 예측과 자기지도 잠재 모델링(self-supervised latent modeling)에서 로봇 지각(robot perception), 동역학 이해(dynamics understanding), 행동 조건부 월드 모델(action-conditioned world model)로 발전하는 자연스러운 연결고리를 제공한다.

## 04.08. JEPA for Robot Perception and Dynamics

![](images/image8.png){width="7.268055555555556in" height="7.268055555555556in"}

JEPA는 로봇 지각(robot perception)과 동역학(dynamics)을 위한 유용한 기반을 제공할 수 있다. 이는 현재의 물리적 상태를 이해하는 문제와 그 상태가 어떻게 변화할지를 예측하는 문제를 분리하기 때문이다. 로봇 시스템에서는 카메라, 라이다(LiDAR), 레이더(radar), IMU, 고유수용감각(proprioception)에서 얻은 관측을 압축된 잠재 표현(latent representation)으로 변환할 수 있다. 이후 예측기(predictor)는 시간에 따른 이러한 표현 사이의 관계를 학습하여 지각(perception)과 미래 상태 예측(future-state prediction)에 모두 유용한 내부 상태(internal state)를 형성할 수 있다. 이 주제는 JEPA와 잠재 예측 아키텍처(latent predictive architecture)를 다루는 장에서 일반적인 표현 학습(representation learning)에서 물리적 로봇 월드 모델(physical robot world model)로 발전하는 연결고리 역할을 한다.

로봇 지각(robot perception)은 개별 프레임에서 단순히 객체를 식별하는 일반적인 이미지 인식(image recognition)과 근본적으로 다르다. 로봇은 객체가 어디에 있는지, 어떻게 움직이는지, 환경이 어떻게 구성되어 있는지, 어떤 영역을 주행할 수 있는지, 그리고 자신의 움직임이 관측에 어떤 영향을 미치는지를 이해해야 한다. JEPA 방식 표현 학습(JEPA-style representation learning)은 이러한 요구사항을 하나로 결합할 수 있다. 즉, 관련 없는 시각적 변동에는 둔감하면서도 지속적인 공간적(spatial), 의미적(semantic), 기하학적(geometric), 동적(dynamic) 정보를 보존하는 잠재 상태(latent state)를 학습할 수 있다.

다중모달 로봇 지각 시스템(multimodal robot perception system)은 카메라 이미지와 라이다, 레이더, IMU, 고유수용감각 측정값을 하나의 공유 또는 조정된 잠재 표현(shared or coordinated latent representation)으로 인코딩할 수 있다. 각 센서는 물리적 상태의 서로 다른 측면을 관측하며, 여러 센서를 결합하면 단일 모달리티보다 더 강력한 정보를 얻을 수 있다. 잠재 표현은 모든 센서 측정값을 그대로 재현할 필요가 없다. 대신 로봇 상태 추정(robot state estimation), 환경 이해(environment understanding), 미래 변화 예측(future change prediction)에 유용한 관계를 보존해야 한다.

시간적 구조(temporal structure)는 로봇 지각이 정적인 특성과 동적인 사건을 구별해야 하기 때문에 필수적이다. 하나의 관측은 객체의 위치를 보여줄 수 있지만, 시퀀스(sequence)는 객체가 정지해 있는지, 접근하고 있는지, 회전하고 있는지, 가속하고 있는지, 또는 다른 객체와 상호작용하고 있는지를 보여줄 수 있다. JEPA는 관측 시퀀스를 문맥(context)으로 인코딩하고 이후 상태에 대응하는 잠재 표현을 예측함으로써 이러한 시간적 관계를 학습할 수 있다. 결과적으로 잠재 표현은 현재 상태에 관한 정보와 환경 동역학(environmental dynamics)에 관한 증거를 모두 포함할 수 있다.

이동 로봇(mobile robot)에서는 자기 운동(ego-motion)이 동역학 이해에서 특히 중요한 구성요소이다. 로봇이 움직인다는 이유만으로 카메라와 라이다 관측이 크게 변할 수 있으며, 주변 환경 자체는 물리적으로 동일하게 유지될 수 있다. 유용한 잠재 표현은 로봇 자신의 움직임에 의해 발생한 변화와 객체 또는 환경 과정(environmental process)에 의해 발생한 변화를 구별해야 한다. 시각 관측을 IMU, 오도메트리(odometry), 고유수용감각 및 기타 움직임 정보와 결합하면 실제 세계의 보다 안정적인 표현을 형성하는 데 도움이 될 수 있다.

JEPA 방식 예측(JEPA-style prediction)은 모든 객체에 명시적으로 레이블을 부여하지 않고도 객체 중심(object-centric) 및 장면 수준(scene-level) 동역학을 학습하는 데 활용될 수 있다. 미래 관측에서 목표 표현(target representation)을 선택하면 예측기는 상태 전이(state transition) 과정에서도 계속 유용한 정보를 포착해야 한다. 지속적인 객체, 공간적 관계, 대략적인 궤적(trajectory), 자유 공간(free space), 장면 구조(scene structure)가 잠재 상태에 인코딩될 수 있다. 이를 통해 모델은 사람이 미리 정의한 의미적 범주(semantic category)에 전적으로 의존하지 않고 경험으로부터 물리적 규칙성을 학습할 수 있다.

마스킹된 예측(masked prediction)은 로봇 지각을 위한 또 하나의 유용한 메커니즘이다. 장면, 센서 표현 또는 시간적 시퀀스의 일부를 숨긴 뒤 모델이 보이는 문맥으로부터 그 잠재 표현을 예측하도록 할 수 있다. 이는 실제 로봇에서 자연스럽게 발생하는 조건과 유사하다. 센서는 가림(occlusion), 제한된 시야(field of view), 일시적인 성능 저하, 측정 누락을 자주 경험한다. 따라서 숨겨진 표현을 추론하도록 학습하면 부분 관측성(partial observability) 상황에서도 유용한 상태 정보를 유지하는 내부 모델의 능력을 향상시킬 수 있다.

잠재 표현은 지각과 동역학 모델링(dynamics modeling)을 연결하는 가교 역할도 할 수 있다. 기존 지각 시스템은 객체와 기하학적 특징을 추정한 후 이를 별도의 동역학 모델에 전달할 수 있다. JEPA 기반 아키텍처에서는 표현 자체가 미래 상태를 예측하는 데 필요한 정보를 보존하도록 학습될 수 있다. 따라서 지각과 동역학은 잠재 상태를 통해 결합되며, 모델은 환경이 어떻게 변화할지를 예측하는 데 실제로 중요한 지각 정보가 무엇인지 학습할 수 있다.

예측 지평(prediction horizon)은 표현이 어떤 종류의 동역학을 포착해야 하는지를 결정한다. 단기 예측(short-horizon prediction)은 즉각적인 움직임, 국소적 상호작용(local interaction), 빠르게 변화하는 센서 정보에 집중할 수 있다. 장기 예측(long-horizon prediction)은 객체 정체성(object identity), 장면 구성, 경로 수준 정보(route-level information), 환경 제약(environmental constraint)과 같은 더욱 지속적인 구조를 요구한다. 로봇 월드 모델(robot world model)은 여러 예측 지평을 사용하여 즉각적인 반응과 장기적인 예측을 동시에 지원하는 잠재 표현을 형성할 수 있다.

동일한 원리는 다양한 로봇 플랫폼에도 적용될 수 있다. 자율 이동 로봇(autonomous mobile robot)은 자유 공간, 장애물, 위치 추정(localization), 이동하는 에이전트에 중점을 둘 수 있다. 매니퓰레이터(manipulator)는 객체 자세(object pose), 접촉 관계(contact relationship), 파지 가능한 표면(graspable surface), 상호작용 동역학(interaction dynamics)을 중요하게 다룰 수 있다. 4족 보행 로봇(quadruped)은 지형 구조(terrain structure), 신체 움직임(body motion), 발 디딤 관계(foothold relationship), 안정성(stability) 정보를 필요로 할 수 있다. 기본적인 JEPA 원리는 동일하게 유지된다. 즉, 불필요한 감각 세부 정보를 피하면서 관련 미래 상태를 예측하는 데 필요한 정보를 포함하는 표현을 학습하는 것이다.

행동 정보(action information)는 완전한 로봇 동역학 모델(robot dynamics model)로 발전하기 위한 다음 단계이다. 수동적인 관측은 환경이 일반적으로 어떻게 변화하는지를 보여줄 수 있지만, 로봇은 자신의 행동이 그 변화에 어떤 영향을 미치는지도 이해해야 한다. 잠재 예측기(latent predictor)는 현재 표현과 함께 행동 또는 행동 시퀀스를 입력받고 그 결과로 발생하는 미래 표현을 추정할 수 있다. 이는 잠재 공간에서 행동 조건부 전이 모델(action-conditioned transition model)을 형성하며, 반사실적 예측(counterfactual prediction), 계획, 모델 기반 제어(model-based control)의 기반을 제공한다.

잠재 동역학(latent dynamics)은 완전한 미래 이미지나 센서 스트림을 생성하지 않고도 내부 롤아웃(internal rollout)을 수행할 수 있도록 한다. 현재 잠재 상태에서 시작하여 서로 다른 행동 시퀀스에 따른 여러 가능한 미래 상태를 예측할 수 있다. 이러한 잠재 궤적은 내비게이션 목표(navigation goal), 충돌 위험(collision risk), 작업 진행도(task progress), 안정성(stability), 에너지 소비(energy consumption) 등의 기준으로 평가할 수 있다. 따라서 로봇은 실제 행동을 실행하기 전에 후보 미래를 비교하는 일종의 내부 상상(internal imagination)을 수행할 수 있다.

JEPA는 로봇 지각과 동역학이 엄격한 계산 제약(computational constraint) 아래에서 작동한다는 점에서 특히 매력적이다. 로봇은 여러 센서 스트림을 지속적으로 처리하면서 낮은 지연시간(low latency)과 제한된 전력 소비(power consumption)를 유지해야 할 수 있다. 압축된 잠재 상태를 예측하면 고차원 미래 관측을 생성하는 데 필요한 계산 부담을 줄일 수 있다. 그렇다고 생성형 모델(generative model)이 불필요하다는 의미는 아니다. 세부적인 감각 재구성(sensory reconstruction)은 시뮬레이션, 시각화 또는 특정 지각 작업에 여전히 유용할 수 있다. 잠재 예측기는 대신 예측 시스템의 효율적인 핵심 역할을 수행할 수 있다.

중요한 과제는 잠재 표현이 물리적으로 의미 있는 상태(physically meaningful state)를 유지하도록 하는 것이다. 표현이 지나치게 압축되면 안전한 주행이나 제어에 필요한 정보가 손실될 수 있다. 반대로 지나치게 많은 저수준 세부 정보를 유지하면 예측이 비효율적이고 방해 변동(nuisance variation)에 민감해질 수 있다. 따라서 학습 과정은 정보 보존(information preservation)과 추상화(abstraction) 사이에서 균형을 유지해야 한다. 잠재 표현 붕괴(representation collapse), 시간적 불일치(temporal inconsistency), 센서 정렬 오류(sensor misalignment), 장기 예측 과정에서의 누적 예측 오차(accumulated prediction error) 역시 해결해야 한다.

피지컬 AI(Physical AI)에서 가장 중요한 결과는 단순히 지각 정확도(perception accuracy)를 높이는 것이 아니라, 지각, 동역학 이해, 예측, 그리고 궁극적으로 행동을 지원할 수 있는 통합 내부 표현(unified internal representation)을 형성하는 것이다. JEPA 기반 로봇 월드 모델은 다중모달 관측을 잠재 물리 상태(latent physical state)로 변환하고, 그 상태가 시간에 따라 어떻게 변화하는지를 학습하며, 이후 로봇의 행동에 따라 이러한 변화를 조건화할 수 있다. 이는 센서 표현(sensor representation)에서 예측 월드 모델링(predictive world modeling), 그리고 궁극적으로 계획과 제어로 이어지는 자연스러운 발전 경로를 제공한다.

따라서 로봇 지각과 동역학을 위한 JEPA(JEPA for robot perception and dynamics)는 수동적인 인식(passive recognition)에서 예측적 물리 지능(predictive physical intelligence)으로 발전하는 중요한 전환을 나타낸다. 로봇은 단순히 지금 무엇이 보이는지를 묻는 것이 아니라, 현재 상태의 어떤 측면이 다음에 무엇이 일어날지를 예측하는 데 중요한지를 학습한다. 다중모달 지각, 시간적 예측, 잠재 동역학, 부분 관측 추론, 그리고 궁극적으로 행동 조건화를 결합함으로써 이 접근법은 감각(sensing)과 예측(anticipation), 행동(behavior)을 연결하는 압축된 내부 모델을 형성할 수 있다. 이는 JEPA를 확장 가능한 로봇 월드 모델과 보다 광범위한 피지컬 AI 시스템을 위한 강력한 아키텍처 구성요소로 만든다.

## 04.09. Action Conditioned JEPA

![](images/image9.png){width="7.268055555555556in" height="7.268055555555556in"}

행동 조건부 JEPA(action-conditioned JEPA)는 공동 임베딩 예측 아키텍처(Joint Embedding Predictive Architectures)를 수동적인 예측(passive prediction)에서 에이전트의 행동에 따라 환경이 어떻게 변화하는지를 예측하는 모델링으로 확장한다. 수동적인 JEPA는 문맥(context)과 미래 표현(future representation) 사이의 관계를 학습하는 반면, 행동 조건부 JEPA는 행동 또는 행동 시퀀스를 추가로 입력받아 그 결과로 예상되는 잠재 상태(latent state)를 예측한다. 이를 통해 하나의 표현 공간 안에서 지각(perception), 잠재 동역학(latent dynamics), 반사실적 예측(counterfactual prediction), 계획(planning), 제어(control)를 직접 연결할 수 있다.

핵심 아이디어는 물리적 시스템의 미래 상태가 현재 상태뿐만 아니라 에이전트가 무엇을 하는지에도 의존한다는 것이다. 객체를 관찰하는 로봇은 로봇이 객체를 향해 이동하는지, 밀어내는지, 잡는지, 또는 아무것도 하지 않는지를 고려하지 않고서는 객체의 미래 위치를 정확하게 예측하기 어렵다. 따라서 행동 조건부 JEPA는 (z_{t+1}=f(z_t,a_t))와 같은 관계를 모델링한다. 여기서 (z_t)는 현재 잠재 상태를 나타내고 (a_t)는 행동을 나타낸다. 예측기는 행동이 표현된 세계를 어떻게 변화시키는지를 학습한다.

현재 문맥(current context)은 카메라, 라이다(LiDAR), 레이더(radar), IMU, 고유수용감각(proprioception), 기타 센서에서 얻은 다중모달 관측(multimodal observation)을 포함할 수 있다. 이러한 관측은 관련된 공간적(spatial), 의미적(semantic), 기하학적(geometric), 동적(dynamic), 로봇 상태(robot-state) 정보를 설명하는 압축된 잠재 표현(compact latent representation)으로 인코딩된다. 행동 인코더(action encoder)는 모터 명령(motor command)이나 상위 수준 행동(high-level action)을 별도로 행동 임베딩(action embedding)으로 변환할 수 있다. 이후 잠재 상태와 행동 표현은 예측 네트워크(predictive network)에 의해 결합되어 하나 이상의 미래 잠재 상태를 추정한다.

행동(action)은 서로 다른 수준의 추상화(abstraction)에서 표현할 수 있다. 저수준 행동(low-level action)은 모터 명령, 조향(steering), 휠 속도(wheel velocity), 관절 토크(joint torque), 액추에이터 목표값(actuator target) 등을 설명할 수 있다. 중간 수준 행동(intermediate action)은 내비게이션 명령(navigation command), 파지 동작(grasp motion), 조작 프리미티브(manipulation primitive) 등을 나타낼 수 있다. 더 높은 수준의 행동은 접근(approach), 파지(grasp), 이동(move), 놓기(release), 추종(follow)과 같은 작업 지향적 의사결정(task-oriented decision)을 표현할 수 있다. 적절한 행동 표현은 로봇 플랫폼과 제어 아키텍처(control architecture)에 따라 달라지지만, 예측 원리는 동일하다. 즉, 선택된 개입(intervention)에 따라 잠재적 미래가 달라져야 한다.

하나의 행동은 즉각적인 다음 잠재 상태(next latent state)를 예측하는 데 사용할 수 있으며, 행동 시퀀스(action sequence)는 다단계 예측(multi-step prediction)을 지원할 수 있다. (z_t)와 (a_t,a_{t+1},\...,a_{t+H-1})가 주어지면 예측기는 (\\hat{z}\*{t+1},\\hat{z}\*{t+2},\...,\\hat{z}_{t+H})를 추정할 수 있다. 이를 통해 모델은 행동의 결과가 시간에 따라 어떻게 누적되는지를 표현할 수 있다. 단기 예측(short-horizon prediction)은 반응형 제어(reactive control)를 지원할 수 있고, 장기 롤아웃(longer rollout)은 계획과 의사결정에 필요한 정보를 제공할 수 있다.

학습 목표(training target)는 실제 또는 시뮬레이션 로봇 운용에서 수집된 미래 관측으로부터 얻을 수 있다. 목표 인코더(target encoder)는 관측된 미래 상태를 잠재 표현으로 변환하고, 예측기는 이전 문맥과 해당 행동으로부터 그 표현을 추정한다. 따라서 학습 목적은 잠재 공간(latent space)에서 적용되며, 모델이 미래의 모든 픽셀이나 센서 측정값을 재구성하도록 요구하지 않는다. 이는 행동에 따른 상태 전이를 도입하면서도 JEPA의 핵심 원리를 유지한다.

행동 조건부 학습(action-conditioned learning)은 로봇 경험으로부터 자연스러운 자기지도(self-supervision) 형태도 제공한다. 기록된 모든 궤적(trajectory)은 관측, 행동, 그리고 그 결과로 발생한 미래 상태를 포함한다. 시스템은 이러한 상태-행동-전이 관계(state-action-transition relationship)를 사용하여 각 행동의 인과적 효과(causal effect)에 대해 사람이 직접 주석을 달지 않고도 학습 신호를 구성할 수 있다. 따라서 대규모 운용 데이터(operational data)는 예측 동역학 지식(predictive dynamics knowledge)의 원천이 될 수 있으며, 특히 다양한 행동과 환경 조건이 포함된 데이터에서 더욱 유용하다.

중요한 차이는 수동적 예측(passive prediction)과 행동 조건부 예측(action-conditioned prediction) 사이에 있다. 수동적 예측은 지금까지 관측된 정보를 바탕으로 세계가 어떻게 변화할 가능성이 높은지를 묻는다. 행동 조건부 예측은 에이전트가 특정 행동을 수행한다면 세계가 어떻게 변화할 가능성이 높은지를 묻는다. 두 번째 형태는 서로 다른 개입(intervention)을 비교할 수 있기 때문에 의사결정(decision making)에 더욱 직접적으로 유용하다. 따라서 월드 모델(world model)은 단순히 예측적인 모델을 넘어 실제 행동을 실행하기 전에 결과를 평가하는 데 사용할 수 있는 모델로 발전한다.

이러한 능력은 반사실적 행동 롤아웃(counterfactual action rollout)을 가능하게 한다. 동일한 잠재 상태 (z_t)에서 시작하여 예측기는 서로 다른 후보 행동 (a\^1,a\^2,\...,a\^N)을 평가하고 각각에 대응하는 미래 잠재 궤적(future latent trajectory)을 추정할 수 있다. 따라서 로봇은 실제 환경에서 모든 행동을 직접 수행하지 않고도 내부적으로 서로 다른 선택이 어떤 결과를 가져올지를 물어볼 수 있다. 이렇게 상상된 궤적(imagined trajectory)은 작업 목표(task objective), 안전성(safety), 비용(cost), 에너지, 안정성(stability), 예상 진행도(expected progress) 등의 기준에 따라 비교할 수 있다.

다중 행동 시퀀스 예측(multi-action sequence prediction)은 이러한 개념을 개별 의사결정에서 더 긴 행동 계획(behavioral plan)으로 확장한다. 후보 시퀀스는 (A\^i=(a_t\^i,\...,a_{t+H-1}\^i))로 표현할 수 있으며, 예측기는 이에 대응하는 잠재 롤아웃(latent rollout)을 생성할 수 있다. 계획기(planner)는 이러한 궤적을 평가하고 가장 바람직한 예측 결과를 생성하는 시퀀스를 선택할 수 있다. 이는 모든 후보에 대해 미래 감각 관측을 완전히 생성할 필요 없이 잠재 상태에서 계획을 수행하는 압축된 내부 시뮬레이션 메커니즘(internal simulation mechanism)을 형성한다.

행동 조건부 예측의 품질은 잠재 상태의 품질에 크게 의존한다. 표현은 행동이 환경에 미치는 영향을 결정하는 물리적 정보를 보존해야 한다. 객체 위치, 접촉 상태(contact state), 지형 기하 구조(terrain geometry), 속도(velocity), 로봇 구성(robot configuration) 등이 제거되면 예측기는 행동의 결과를 정확하게 추정할 수 없다. 동시에 관련 없는 외형 정보가 표현을 지배해서도 안 된다. 따라서 잠재 상태는 추상화(abstraction)와 물리적 정보(physical information) 사이에서 적절한 균형을 유지해야 한다.

장기 행동 조건부 예측(long-horizon action-conditioned prediction)은 반복되는 잠재 전이(latent transition) 과정에서 작은 오류가 누적될 수 있기 때문에 추가적인 문제를 발생시킨다. 한 단계에서 발생한 부정확한 예측은 다음 단계의 입력이 되어 상상된 궤적(imagined trajectory)이 실제 시스템에서 점점 벗어날 수 있다. 다중 지평 학습(multi-horizon training), 시간적 일관성 목적 함수(temporal consistency objective), 안정적인 잠재 표현(stable latent representation), 불확실성 추정(uncertainty estimation), 적절한 롤아웃 전략(rollout strategy)을 통해 이러한 문제를 줄일 수 있다. 안전이 중요한 로보틱스에서는 행동 선택 시 예측 불확실성(prediction uncertainty)도 고려해야 한다.

행동 조건부 JEPA는 다양한 형태의 로봇 제어(robot control)를 지원할 수 있다. 반응형 제어에서는 예측기가 매우 짧은 미래 지평만을 추정하고 즉각적인 행동 선택에 사용할 수 있는 압축된 표현을 제공할 수 있다. 모델 예측 제어(model predictive control)에서는 여러 후보 행동 시퀀스를 롤아웃하고 새로운 관측이 들어올 때마다 반복적으로 평가할 수 있다. 상위 수준 계획에서는 더 긴 잠재 궤적을 통해 작업 진행과 환경에 미치는 결과를 표현할 수 있다. 따라서 동일한 예측 표현이 여러 시간 규모와 의사결정 수준에서 활용될 수 있다.

이 아키텍처는 지각과 강화학습(reinforcement learning) 사이의 자연스러운 연결고리도 제공한다. 학습된 잠재 동역학 모델(latent dynamics model)은 가치 추정(value estimation), 정책 평가(policy evaluation), 모델 기반 강화학습(model-based reinforcement learning)을 지원하는 예측된 전이를 생성할 수 있다. 실제로 실행된 행동으로부터만 학습하는 대신 에이전트는 월드 모델을 이용하여 추가적인 가상 궤적(hypothetical trajectory)에 대해 추론할 수 있다. 이러한 접근법의 품질은 학습된 모델이 정책(policy)이 탐색하는 상태-행동 공간(state-action space)의 영역에서 충분히 정확하게 유지되는지에 따라 달라진다.

피지컬 AI(Physical AI)에서 행동 조건부 JEPA는 결국 세계가 어떻게 보이는지를 학습하는 것에서 에이전트의 개입에 세계가 어떻게 반응하는지를 학습하는 것으로의 전환을 의미한다. 다중모달 관측은 현재의 잠재 상태를 제공하고, 행동은 가능한 개입을 지정하며, 예측기는 그 결과로 발생할 미래 잠재 상태를 추정한다. 이러한 예측은 반사실적 추론(counterfactual reasoning), 내부 롤아웃, 계획, 제어를 지원할 수 있다. 이러한 형태에서 JEPA는 감지(sensing), 이해(understanding), 예측(prediction), 의사결정(decision making), 물리적 행동(physical behavior)을 연결하는 행동 인식 월드 모델(action-aware world model)의 핵심 구성요소가 된다.

## 04.10. Minimal JEPA World Model [w/Code]

![](images/image10.png){width="7.268055555555556in" height="7.268055555555556in"}

최소 JEPA 월드 모델(minimal JEPA world model)은 현재의 물리적 상황을 표현하고 의미 있는 미래 상태를 예측하는 데 필요한 잠재 정보(latent information)만을 유지하도록 설계된다. 관측의 모든 세부 정보를 재구성하는 대신 다중모달 감각 입력(multimodal sensory input)을 압축된 잠재 상태(compact latent state)로 변환하고, 그 상태가 어떻게 변화하는지를 학습한다. 이 장의 구조에서 최소 모델은 JEPA 표현 공간 예측(representation-space prediction)과 자기지도 학습(self-supervised learning)에서 시작하여 시간적 예측(temporal prediction), 로봇 지각(robot perception), 동역학(dynamics), 행동 조건부 예측(action-conditioned prediction)으로 발전하는 흐름을 따른다.

모델은 카메라 이미지, 라이다(LiDAR), 레이더(radar), IMU, 고유수용감각(proprioception) 또는 기타 이용 가능한 감각 정보가 포함된 관측(observation)으로 시작한다. 이러한 신호는 인코더(encoder)에 의해 잠재 상태 (z_t)로 변환된다. 여기서 인코딩의 목적은 단순한 압축이 아니라 선택적 표현(selective representation)을 만드는 것이다. 객체, 공간 구조, 기하 구조, 움직임, 로봇 상태(robot state), 예측에 필요한 기타 특성은 유지되어야 하며, 관련성이 낮은 외형 변화와 센서별 잡음(sensor-specific noise)은 감소시킬 수 있다.

잠재 상태(latent state)는 지각(perception)과 예측(prediction) 사이의 핵심 인터페이스를 제공한다. 대규모 원시 관측(raw observation)을 이후의 모든 계산에 직접 전달하는 대신 시스템은 물리 세계의 압축된 표현(compact representation)을 사용하여 동작한다. 이를 통해 잠재 상태는 현재 시점에서 중요한 것이 무엇인지를 설명하는 실용적인 내부 표현(internal description)이 된다. 좋은 표현은 예측과 의사결정(decision making)을 지원할 수 있을 만큼 충분히 풍부하면서도 미래 행동에 거의 영향을 주지 않는 세부 정보에 계산 자원을 낭비하지 않을 정도로 충분히 추상적이어야 한다.

예측 구성요소(predictive component)는 잠재 상태가 시간에 따라 어떻게 변화하는지를 학습한다. 가장 단순한 형태에서 모델은 (\\hat{z}_{t+1}=F(z_t))와 같은 미래 표현을 추정한다. 예측기는 완전한 미래 이미지나 모든 센서 측정값을 생성할 필요가 없다. 대신 미래 상태를 특징짓는 잠재 구조를 추정한다. 이를 통해 지각이 상태를 생성하고, 동역학이 그 변화를 예측하며, 이후 새로운 관측이 다시 보정 정보를 제공하는 최소한의 예측 루프(predictive loop)가 형성된다.

JEPA 학습 원리(JEPA training principle)는 미래 관측을 직접 재구성하도록 요구하는 대신 목표 표현(target representation)을 도입한다. 학습 과정에서 목표 인코더(target encoder)는 미래 또는 숨겨진 관측을 목표 잠재 상태 (z_{t+k})로 변환한다. 예측기는 이용 가능한 문맥(context)으로부터 (\\hat{z}_{t+k})를 추정하고, 잠재 공간 목적 함수(latent-space objective)는 예측 표현과 목표 표현이 서로 가까워지도록 유도한다. 이를 통해 밀집된 수작업 레이블(dense manual label)이나 픽셀 수준 재구성(pixel-level reconstruction) 없이 자연스럽게 발생하는 관측으로부터 모델을 학습할 수 있다.

시간적 예측(temporal prediction)은 최소 JEPA 모델에 월드 모델(world model)의 특성을 부여한다. 하나의 잠재 상태는 현재 표현된 내용을 설명하고, 잠재 상태의 시퀀스는 그 표현이 어떻게 변화하는지를 설명한다. 짧은 예측 지평(short prediction horizon)은 즉각적인 움직임과 국소적인 상태 전이(local state transition)를 포착할 수 있는 반면, 긴 예측 지평(long prediction horizon)은 더욱 지속적인 정보를 보존하도록 요구한다. 따라서 다중 지평 예측(multi-horizon prediction)은 잠재 표현이 빠르게 변화하는 동역학과 느리게 변화하는 환경의 구조적 특성을 동시에 포함하도록 유도할 수 있다.

기억(memory)은 아키텍처를 불필요하게 복잡하게 만들지 않으면서도 통합할 수 있다. 각각의 관측을 독립적으로 처리하는 대신 모델은 이전 관측으로부터 얻은 정보를 포함하는 시간적 잠재 상태(temporal latent state)를 유지할 수 있다. 이는 환경이 부분적으로만 관측되는 경우 특히 중요하다. 객체가 장애물 뒤로 사라질 수 있고, 센서의 시야가 제한될 수 있으며, 측정값을 일시적으로 이용할 수 없게 될 수도 있다. 압축된 잠재 기억(compact latent memory)은 이전에 관측된 상태에 대한 유용한 증거를 유지하고 이를 새로운 정보와 결합할 수 있도록 한다.

마스킹된 잠재 예측(masked latent prediction)은 최소 모델을 학습하는 또 다른 방법을 제공한다. 관측, 시퀀스 또는 시간적 상태의 일부를 숨기고 예측기가 남아 있는 문맥으로부터 그 잠재 표현을 추정하도록 할 수 있다. 이를 통해 표현은 단순히 보이는 정보를 복사하는 것이 아니라 관계를 인코딩하도록 강제된다. 공간적 마스킹(spatial masking)은 기하 구조와 장면 이해(scene understanding)를 촉진하고, 시간적 마스킹은 동역학 학습(dynamics learning)을 촉진하며, 시공간적 마스킹(spatiotemporal masking)은 모델이 공간과 시간 모두에 걸쳐 물리적 구조가 어떻게 변화하는지를 추론하도록 유도할 수 있다.

최소 JEPA 모델은 다중모달 일관성(multimodal consistency)도 통합할 수 있다. 카메라, 라이다, 레이더, IMU, 고유수용감각은 동일한 물리적 시스템에 대해 서로 다른 관측을 제공한다. 각 모달리티를 독립적으로 유지하도록 요구하는 대신 인코더는 여러 모달리티에 공통으로 존재하는 정보를 포착하는 잠재 상태를 학습할 수 있다. 이를 통해 표현은 특정 센서의 특성이 아니라 underlying physical situation, 즉 실제 물리적 상황을 반영하도록 유도된다. 이후 센서가 누락되거나 성능이 저하되는 경우에도 이러한 상황을 불완전한 증거(incomplete evidence)로 처리하여 내부 표현이 이를 보완하도록 할 수 있다.

로보틱스(robotics)에서는 행동 조건화(action conditioning)를 통해 최소 예측 모델을 수동적 동역학(passive dynamics)에서 제어 가능한 동역학(controllable dynamics)으로 확장할 수 있다. 예측기는 현재 잠재 상태와 행동 표현을 함께 입력받아 (z_{t+1}=F(z_t,a_t))에 따라 미래 상태를 추정할 수 있다. 행동은 모터 명령, 조향, 속도, 관절 움직임, 조작 프리미티브(manipulation primitive), 내비게이션 명령, 또는 상위 수준의 의사결정을 나타낼 수 있다. 중요한 원리는 예측된 미래가 로봇이 선택한 개입(intervention)에 따라 달라져야 한다는 것이다.

행동이 잠재 동역학(latent dynamics)을 조건화하면 동일한 압축 모델을 내부 롤아웃(internal rollout)에 사용할 수 있다. (z_t)에서 시작하여 서로 다른 후보 행동(candidate action)을 평가하고 각각의 미래 잠재 상태를 예측할 수 있다. 행동 시퀀스(action sequence)는 일련의 예측 상태를 생성할 수 있으므로 로봇은 실제로 행동을 수행하기 전에 가능한 미래를 비교할 수 있다. 이는 미래 감각 관측을 완전히 생성하지 않고도 반사실적 추론(counterfactual reasoning), 잠재 공간 계획(latent-space planning), 모델 예측 제어(model predictive control)를 수행하기 위한 기반을 제공한다.

따라서 최소 아키텍처(minimal architecture)는 일방향 예측 네트워크(one-way prediction network)가 아니라 폐루프 시스템(closed-loop system)으로 볼 수 있다. 로봇은 환경을 관측하고, 관측을 (z_t)라는 잠재 상태로 인코딩하고, 가능한 미래 상태를 예측하며, 행동을 선택하거나 실행하고, 그 결과로 변화한 환경을 다시 관측하여 내부 상태를 업데이트한다. 새로운 관측은 예측 오차(prediction error)를 보정한다. 이러한 관측--예측--행동--보정(observe--predict--act--correct) 루프를 통해 월드 모델은 개방 루프 잠재 롤아웃(open-loop latent rollout)에 무한히 의존하지 않고 실제 물리적 경험에 계속 연결될 수 있다.

최소 JEPA 월드 모델은 무엇을 표현해야 하고 무엇을 제거할 수 있는지도 구별해야 한다. 정확한 질감, 조명 변화, 센서 잡음 및 기타 저수준 외형 정보는 내비게이션(navigation), 조작(manipulation), 제어(control)가 주된 목표라면 필요하지 않을 수 있다. 반면 객체 움직임, 자유 공간(free space), 접촉 상태(contact state), 지형 구조(terrain structure), 로봇 구성(robot configuration), 불확실성(uncertainty)은 매우 중요할 수 있다. 따라서 모델은 예측 가능하고 행동과 관련된 물리적 구조에 표현 용량을 집중하는 정보 병목(information bottleneck)을 학습해야 한다.

이 최소 아키텍처의 주요 장점은 계산 효율성(computational efficiency)이다. 잠재 상태는 원시 이미지, 포인트 클라우드 또는 다중모달 센서 스트림보다 훨씬 작을 수 있으므로 더 적은 메모리, 지연시간(latency), 에너지로 예측을 수행할 수 있다. 이는 엣지 또는 온보드 컴퓨팅(edge or onboard computing) 플랫폼에서 지속적으로 동작해야 하는 피지컬 AI(Physical AI) 시스템에 특히 중요하다. 최소 모델은 모든 특수 지각 모듈이나 생성형 구성요소(generative component)를 대체하려는 것이 아니다. 대신 이러한 구성요소들이 연결될 수 있는 압축된 예측 핵심(predictive core)을 제공한다.

따라서 최소 JEPA 월드 모델은 가능한 한 적은 수의 신경망 계층(neural-network layer)을 갖는 것으로 정의되는 것이 아니라, 지능적인 행동에 필요한 구조는 보존하면서 예측해야 하는 정보의 양을 최소화하는 것으로 정의된다. 핵심 루프는 관측에서 잠재 상태로, 잠재 상태에서 예측된 미래로, 행동에서 조건부 전이(action-conditioned transition)로, 그리고 새로운 관측에서 보정으로 이어진다. 자기지도 잠재 예측, 시간적 기억, 다중모달 표현, 행동 조건화를 통해 이러한 압축된 구조는 지각, 동역학, 예측, 계획, 제어를 하나의 통합된 내부 모델(unified internal model)로 연결한다.
