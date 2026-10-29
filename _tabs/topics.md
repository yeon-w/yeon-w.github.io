---
title: 연구 분야
icon: fas fa-layer-group
order: 2
---

## 여섯 갈래의 기록

한 번의 실험이 코드, 문제 풀이, 문서, 연구 읽기로 이어지도록 주제를 나누었습니다. 각 카드는 해당 카테고리의 실제 글 목록으로 이동합니다.

{% assign development = '개발' | slugify | url_encode %}
{% assign ctf = 'CTF/Wargame' | slugify | url_encode %}
{% assign bounty = 'Bug Bounty' | slugify | url_encode %}
{% assign writing = '블로그/기술문서' | slugify | url_encode %}
{% assign papers = '논문/컨퍼런스' | slugify | url_encode %}
{% assign awards = '공모전/자격증' | slugify | url_encode %}

<div class="topic-grid">
  <a class="topic-card" href="{{ '/categories/' | append: development | append: '/' | relative_url }}"><span class="topic-index">01 / BUILD</span><strong>개발</strong><span>작은 보안 도구, 입력 검증, 자동화의 재현성</span></a>
  <a class="topic-card" href="{{ '/categories/' | append: ctf | append: '/' | relative_url }}"><span class="topic-index">02 / EXPLORE</span><strong>CTF/Wargame</strong><span>포너블과 워게임 풀이의 관찰·가설·검증</span></a>
  <a class="topic-card" href="{{ '/categories/' | append: bounty | append: '/' | relative_url }}"><span class="topic-index">03 / REPORT</span><strong>Bug Bounty</strong><span>허가된 범위의 재현, 영향 분석, 책임 있는 제보</span></a>
  <a class="topic-card" href="{{ '/categories/' | append: writing | append: '/' | relative_url }}"><span class="topic-index">04 / DOCUMENT</span><strong>블로그/기술문서</strong><span>다시 따라 할 수 있는 실습 글과 문서 작성</span></a>
  <a class="topic-card" href="{{ '/categories/' | append: papers | append: '/' | relative_url }}"><span class="topic-index">05 / RESEARCH</span><strong>논문/컨퍼런스</strong><span>주장과 증거, 위협 모델, 연구의 한계 읽기</span></a>
  <a class="topic-card" href="{{ '/categories/' | append: awards | append: '/' | relative_url }}"><span class="topic-index">06 / GROW</span><strong>공모전/자격증</strong><span>학습 계획과 준비 과정, 검증된 결과 기록</span></a>
</div>

> 모든 실습은 허가된 환경을 전제로 합니다. 실제 성과와 공개 가능한 프로젝트 내용은 확인 후 기록합니다.
