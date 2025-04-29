---
title: Week 5-2 Blog
published_at: 2025-04-18
snippet:
disable_html_sanitization: true
allow_math: true
---

## Week 5-2 blog

1. Three.js 예제 선택 및 블로그 구현
   Three.js 예제 페이지에서 마음에 드는 예제 하나를 고르세요.

선택한 예제를 자신의 블로그에 직접 구현하세요.

주의! 해당 예제를 구현하려면:

다양한 JavaScript 모듈 및 자산(import)을 불러와야 합니다.

이들은 보통 CDN 링크 또는 직접 저장한 static 폴더에서 불러올 수 있어야 합니다.

예: import \* as THREE from 'https://cdn.skypack.dev/three';

2. 글리치 아트 분석: Sabato Visconti – flower-01C_giphy-1.gif

이 글리치 아트에서는 3D 형태(또는 이미지)가 의도적으로 왜곡되어 디지털 오류처럼 보입니다.

미학적(Aesthetic) 효과:

형태가 "망가진 듯한" 느낌은 디지털 매체의 불안정성, 오류 가능성을 드러냅니다.

기계적, 차가운 디지털 공간을 감정적이고 혼란스럽게 바꾸는 효과가 있습니다.

Post-Digital 미학의 핵심: 완벽하지 않은 디지털, 우연성과 노이즈의 미학

복잡도(Effective Complexity):

의도된 오류는 무질서와 질서가 혼합된 상태를 만들어냅니다.

이는 관객의 시선을 붙잡고, 예측 불가능한 상호작용을 유도합니다.

기술적으로 어떻게 작동할까? (Under the Hood):

이미지나 3D 모델의 텍스처 좌표(uv mapping)를 조작

또는 정점(vertex) 위치 데이터를 랜덤하게 섞거나 왜곡

셰이더(Shader) 코드를 사용해 실시간 글리치를 구현할 수 있음

보너스 라운드: 세션 4b 개념 적용
세션 4b에서는 다음과 같은 글리치 생성 방법을 다루었습니다:

랜덤 노이즈 삽입 (예: Perlin noise, Simplex noise)

셰이더(ShaderMaterial)를 이용한 정점 및 픽셀 왜곡

이미지 데이터 해킹 (예: getImageData() / putImageData())

선택한 Three.js 예제에 이 중 하나 이상을 적용해보세요:

예: vertex displacement, glitchPass, custom shader, Noise function, fragment shader distortion 등
