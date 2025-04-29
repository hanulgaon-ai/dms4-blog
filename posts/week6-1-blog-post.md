---
title: Week 6-1 Blog
published_at: 2025-04-22
snippet:
disable_html_sanitization: true
allow_math: true
---

## Week 6-1 blog

1. 아래 JS 라이브러리 3개를 조사하세요:
   q5.js

c2.js

svg.js

각 라이브러리는 어떤 용도인가요?
q5.js

p5.js에서 영감을 받은 창의적 코딩용 JS 라이브러리

신호, 진폭, 시간 제어 같은 음향·시각 효과를 위한 "신호 처리 도구" 포함

"Envelope", "Signal", "Oscillator" 등 시간에 따른 변화 구현에 유리함

c2.js

창의적 코딩을 수학적으로 표현할 수 있도록 도와주는 라이브러리

기하학적 형태, 벡터 연산, 수학 기반 표현에 특화됨

아름다운 수학적 시각화를 쉽게 만들 수 있음

svg.js

SVG(Scalable Vector Graphics)를 쉽게 조작하고 애니메이션 할 수 있는 라이브러리

웹에서 벡터 그래픽을 생성, 조작, 변형하는 데 적합

DOM 기반 애니메이션 처리 가능

2. 이 라이브러리들은 어떻게 다른가요?

라이브러리 주요 목적 특징 적합한 상황
q5.js 신호/시간 변화 기반 효과 Envelope, Signal 등 음향/인터랙션 시각화
c2.js 수학 기반 시각화 벡터·함수 중심 추상 기하학, 계산적 미학
svg.js SVG 그래픽 제어 DOM 기반, 애니메이션 가능 웹 기반 UI / 아이콘 / 애니메이션

3. 이 라이브러리들을 JS 모듈(JavaScript Module)에서 사용할 수 있나요?
   사용 가능 여부는 각 라이브러리의 구조에 따라 다릅니다.

설명:
JS 모듈에서 쓰려면 해당 라이브러리가 ESM (ES Modules) 형식으로 작성되어 있어야 함

일부는 CDN (예: esm.sh) 또는 번들러(Vite, Webpack)를 통해 모듈 형태로 사용 가능

4. esm.sh는 어떤 상황에서 유용한가요?
   라이브러리가 ESM 형식이 아닐 때, esm.sh는 이를 ES 모듈로 변환하여 사용 가능하게 해 줍니다.

복잡한 NPM 설치 없이, 브라우저에서 모듈처럼 바로 import 가능하게 해주는 도구입니다.

예:

js
복사
편집
import \* as q5 from 'https://esm.sh/q5.js';

5. 블로그에 데모 만들기
   위 세 가지 라이브러리 중 하나를 선택해,

"signal" 또는 "envelope" 기능을 사용하여,

시간에 따라 변화하는 효과(예: 색상 변화, 진동, 확대/축소 등)를 블로그에서 구현하세요.

6. 읽기 요약 (자신의 말로)
   📖 Michel Serres - Information & Thinking
   "정보"란 단순한 데이터가 아니라 생각(사고)을 유도하는 유동적인 흐름이다.

기술적 신호(소음 포함)가 어떻게 인간의 인지와 연결되는지를 탐구함.

정보화 시대의 지식 생산 방식의 변화를 철학적으로 고찰함.

📖 Merlin Sheldrake - What Is It Like to Be A Fungus?
균류(fungi)의 삶을 인간 중심 시각이 아닌 그 자체로 이해하려는 시도.

균은 분산된 지능, 비인간적 존재 방식, 생태계와의 상호 연결성의 상징.

우리가 인식하지 못하는 다른 형태의 의식/지각 가능성을 상상하게 함.

📖 Laboria Cuboniks - Xenofeminism: A Politics for Alienation
젠더 해방, 기술, 사이보그 페미니즘을 하나로 결합한 선언적 텍스트.

인간성·자연성을 고정된 것이 아니라 재구성 가능한 것으로 본다.

소외(alienation)를 부정적이 아닌, 변화 가능성의 원천으로 재정의함.
