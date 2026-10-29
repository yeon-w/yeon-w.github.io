---
layout: post
title: "작게 만들고 검증하기: 보안 실습용 로그 요약기"
date: 2026-10-29 00:00:00 +0900
description: "표준 라이브러리만으로 JSON Lines 로그를 요약하며, 보안 도구 개발에서 입력 검증과 재현성을 챙기는 방법을 정리합니다."
categories: ['개발']
tags: [python, logging, security]
toc: true
---

보안 도구를 만들 때는 화려한 기능보다 **입력이 무엇이고, 출력이 무엇이며, 실패하면 어떻게 되는지**가 먼저다. 아래는 외부 서비스에 접속하지 않고 로컬의 가상 로그만 읽는 작은 연습이다. 실제 시스템 로그에는 계정·IP·토큰이 들어갈 수 있으므로 공개 글에는 반드시 합성 데이터를 사용한다.

## 입력과 기대 결과

한 줄에 JSON 객체 하나를 담은 `sample.jsonl`을 준비한다.

```json
{"event":"login_failed","source":"web"}
{"event":"login_failed","source":"web"}
{"event":"login_success","source":"ssh"}
```

목표는 이벤트 종류별 개수를 출력하고, 깨진 줄은 몇 개였는지 별도로 알리는 것이다. 원본 행을 다시 출력하지 않아 불필요한 정보 노출도 줄인다.

```python
# summarize.py — Python 3 표준 라이브러리만 사용
import argparse
import json
from collections import Counter
from pathlib import Path


def summarize(path: Path) -> tuple[Counter, int]:
    counts = Counter()
    invalid = 0

    with path.open(encoding="utf-8") as stream:
        for line in stream:
            try:
                record = json.loads(line)
            except json.JSONDecodeError:
                invalid += 1
                continue

            if not isinstance(record, dict) or not isinstance(record.get("event"), str):
                invalid += 1
                continue
            counts[record["event"]] += 1

    return counts, invalid


if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Count event names in a JSONL file")
    parser.add_argument("file", type=Path)
    args = parser.parse_args()

    counts, invalid = summarize(args.file)
    for event, count in sorted(counts.items()):
        print(f"{event}: {count}")
    print(f"invalid_lines: {invalid}")
```

```text
$ python3 summarize.py sample.jsonl
login_failed: 2
login_success: 1
invalid_lines: 0
```

## 이 예제에서 확인할 것

1. **입력 경계:** JSON 파싱 성공과 필요한 필드의 존재는 다른 문제다. 둘 다 검사한다.
2. **재현성:** 예시 입력과 예상 출력을 함께 두면 도구를 수정한 뒤 결과를 비교할 수 있다.
3. **실패 범위:** 깨진 한 줄 때문에 전체 처리가 멈추지 않는다. 다만 파일이 없거나 읽을 권한이 없는 경우는 사용자에게 오류를 보여 준다.
4. **공개 범위:** 보안 글에서는 실제 로그보다 합성 데이터를 사용한다.

다음 단계로는 빈 파일, 빈 줄, 배열 형태의 JSON, 매우 큰 파일을 시험할 수 있다. 기능을 추가할 때마다 입력과 예상 결과를 같이 기록하는 습관이 도구의 신뢰도를 높인다.
