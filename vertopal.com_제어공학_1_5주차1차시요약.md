# 제어공학1 5-1차시 강의 요약

## State Variables

### `<The concept of state variables>`{=html}

시스템은 **입력(Inputs)**, **상태(States)**, **출력(Outputs)** 으로
구성된다.\
상태 변수(state variables)는 시스템의 현재 상태를 나타내며, 입력에 따라
시간에 따라 변한다.

------------------------------------------------------------------------

## State Variables Example 1: Spring--Mass--Damper System

### 시스템 설명

-   질량 M, 스프링 상수 k, 감쇠 계수 b로 구성된 시스템\
-   외력 r(t)에 의해 질량이 변위 y(t)로 이동한다.

### 운동 방정식

M \* d²y(t)/dt² + b \* dy(t)/dt + k \* y(t) = r(t)

### 상태 변수 정의

x₁(t) = y(t), x₂(t) = dy(t)/dt

### 상태 방정식

dx₁(t)/dt = x₂(t)\
dx₂(t)/dt = -(b/M)x₂(t) - (k/M)x₁(t) + (1/M)r(t)\
y(t) = x₁(t)

------------------------------------------------------------------------

## State Variables Example 2: R--L--C Circuit System

### 시스템 설명

-   전류원 u(t), 저항 R, 인덕터 L, 커패시터 C로 구성된 회로\
-   출력은 저항 양단의 전압 vₒ(t)

### 상태 변수 정의

x₁(t) = v_c(t), x₂(t) = i_L(t)

### 회로 방정식

KCL: u(t) = C dx₁(t)/dt + x₂(t) → dx₁(t)/dt = (1/C)\[-x₂(t) + u(t)\]\
KVL: L dx₂(t)/dt + R x₂(t) - x₁(t) = 0 → dx₂(t)/dt = (1/L)\[x₁(t) - R
x₂(t)\]

### 상태 방정식

dx₁(t)/dt = (1/C)\[-x₂(t) + u(t)\]\
dx₂(t)/dt = (1/L)\[x₁(t) - R x₂(t)\]\
y(t) = R x₂(t)

------------------------------------------------------------------------

## State Space Equation

### \<1st order state differential equation\> {#1st-order-state-differential-equation}

1차 상태 미분 방정식:\
ẋ(t) = a x(t) + b u(t)

라플라스 변환:\
sX(s) - x(0) = aX(s) + bU(s)\
(s - a)X(s) = x(0) + bU(s)\
X(s) = 1/(s-a)x(0) + 1/(s-a)bU(s)

시간영역:\
x(t) = e\^{at}x(0) + ∫ e\^{a(t-τ)}b u(τ)dτ

Transition from initial state: Φ(t)x(0)\
Effect of input: ∫ Φ(t-τ)b u(τ)dτ

------------------------------------------------------------------------

## State Space Equation

### `<State vector and state space equation>`{=html}

상태 벡터 정의:\
x(t) = \[x₁(t), x₂(t), ..., xₙ(t)\]ᵀ

상태 방정식: ẋ(t) = A x(t) + B u(t)\
출력 방정식: y(t) = C x(t) + D u(t)

예시 (RLC 회로):\
dx₁(t)/dt = (1/C)\[-x₂(t) + u(t)\]\
dx₂(t)/dt = (1/L)\[x₁(t) - R x₂(t)\]\
y(t) = R x₂(t)

행렬 형태:\
ẋ(t) = \[ \[0, -1/C\], \[1/L, -R/L\] \] x(t) + \[ \[1/C\], \[0\] \]
u(t)\
y(t) = \[0, R\] x(t) + \[0\] u(t)

------------------------------------------------------------------------

## State Transition Matrix

상태 전이 행렬 Φ(t)는 시스템의 시간에 따른 상태 변화를 나타낸다.

1차 시스템:\
x(t) = e\^{at}x(0) + ∫ e\^{a(t-τ)}bu(τ)dτ

n차 시스템:\
x(t) = e\^{At}x(0) + ∫ e\^{A(t-τ)}Bu(τ)dτ

라플라스 영역:\
X(s) = \[sI - A\]⁻¹x(0) + \[sI - A\]⁻¹BU(s)

Φ(s) = \[sI - A\]⁻¹\
Φ(t) = L⁻¹{Φ(s)}

x(t) = Φ(t)x(0) + ∫ Φ(t-τ)Bu(τ)dτ

------------------------------------------------------------------------

## State Space Equation  
### <Example 3.1: Two-Cart System>

두 개의 카트 M₁, M₂가 스프링과 감쇠기로 연결되어 있는 시스템이다.  
입력 u(t)는 Cart 1에 작용하며, 각각의 변위는 p(t), q(t)로 표현된다.


M₁·p¨(t) = u(t) − b₁[p˙(t) − q˙(t)] − k₁[p(t) − q(t)]  
M₂·q¨(t) = b₁[p˙(t) − q˙(t)] + k₁[p(t) − q(t)] − b₂q˙(t) − k₂q(t)


x₁(t) = p(t)  
x₂(t) = q(t)  
x₃(t) = p˙(t)  
x₄(t) = q˙(t)


ẋ(t) =  
[ [0, 0, 1, 0],  
 [0, 0, 0, 1],  
 [−k₁/M₁,  k₁/M₁, −b₁/M₁,  b₁/M₁],  
 [ k₁/M₂, −(k₁+k₂)/M₂,  b₁/M₂, −(b₁+b₂)/M₂] ] x(t)  
+ [ [0], [0], [1/M₁], [0] ] u(t)

x(t) = [ x₁(t), x₂(t), x₃(t), x₄(t) ]ᵀ  
  = [ p(t), q(t), p˙(t), q˙(t) ]ᵀ

If y(t) = p(t) and u(t) = 0

y(t) = [ 1  0  0  0 ] x(t)



