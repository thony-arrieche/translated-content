---
title: 데이터 URIs
slug: Web/HTTP/Basics_of_HTTP/Data_URLs
---

{{HTTPSidebar}}

**Data URIs**, `data:` 스킴이 접두어로 붙은 URL은 컨텐츠 작성자가 작은 파일을 문서 내에 인라인으로 삽입할 수 있도록 해줍니다.

## 구문

Data URIs는 접두사(`data:`), 데이터의 타입을 가리키는 MIME 타입, 텍스트가 아닌 경우 사용될 부가적인 `base64` 토큰 그리고 데이터 자체 총 네가지 부분으로 구성됩니다.

```
data:[<mediatype>][;base64],<data>
```

`mediatype`이란, MIME 타입을 말합니다(JPEG 이미지의 경우 `'image/jpeg'`). 만약 생략된다면, 기본 값으로 `text/plain;charset=US-ASCII`이 사용됩니다.``

데이터가 텍스트인 경우, 단순히 텍스트를 (포함된 문서 유형에 따라 적합한 엔티티 혹은 이스케이프를 사용하여) 임베드할 수 있습니다. 그게 아니라면, base64로 인코딩된 이진 데이터를 임베드하기 위해 `base64`를 지정할 수 있습니다.

몇 가지 예제:

- `data:,Hello%2C%20World!`
  - : 간단한 text/plain 데이터
- `data:text/plain;base64,SGVsbG8sIFdvcmxkIQ%3D%3D`
  - : 위 예제의 base64 인코딩 버전
- `data:text/html,%3Ch1%3EHello%2C%20World!%3C%2Fh1%3E`
  - : `<h1>Hello, World!</h1>인 HTML 문서`
- `data:text/html,<script>alert('hi');</script>`
  - : 자바스크립트 얼럿을 실행하는 HTML 문서입니다. 닫기 스크립트 태그가 필요하다는 것을 기억하세요.

## base64 포맷으로 데이터 인코딩하기

리눅스와 Mac OS X 시스템의 명령줄에서 `uuencode` 유틸리티를 사용해 쉽게 인코딩할 수 있습니다:

```
uuencode -m infile remotename
```

`infile` 파라메터는 base64 포맷으로 인코딩하려는 파일의 이름이며, `remotename`는 파일에 대한 원격지 이름으로 `data` URLs내에서는 실제로 사용되지 않습니다.

출력은 다음과 같은 내용일 겁니다:

```
begin-base64 664 test
YSBzbGlnaHRseSBsb25nZXIgdGVzdCBmb3IgdGV2ZXIK
====
```

Data URI는 초기 헤더줄 다음의 인코딩된 데이터를 사용하게 됩니다.

### 웹 페이지에서 JavaScript 사용하기

웹 API는 base64로 인코딩하거나 디코딩하기 위한 프리미티브를 가지고 있습니다: [Base64 인코딩과 디코딩](/ko/docs/Web/JavaScript/Base64_encoding_and_decoding).

## 일반적인 문제점

이 섹션에서는 `data` URIs를 만들고 사용할 때 일반적으로 발생하는 문제점들에 대해 설명합니다.

- 구문
  - : `data` URIs를 위한 문법은 매우 간단하지만, "data" 세그먼트 앞에 콤마를 넣는 것을 쉽게 잊거나 데이터를 base64 포맷으로 부정확하게 인코딩하는 경우가 있습니다.
- HTML 내에 포맷시키기
  - : `data` URI는 동봉된 문서의 너비에 비례할 가능성이 높은 파일 내에 파일을 제공하게 됩니다. URL로 `data`를 공백 문자(라인 피드, 탭 혹은 스페이스)을 사용해 포맷이 가능해야 하지만 [base64 인코딩을 사용할 때](https://bugzilla.mozilla.org/show_bug.cgi?id=73026#c12) 일어나는 실질적인 문제가 있습니다.
- 길이 제한
  - : 파이어폭스는 기본적으로 길이 제한이 없는 `data` URIs를 지원하지만, 브라우저들은 데이터의 개별적인 최대 길이를 제공해야 할 의무가 없습니다. 예를 들어, 오페라 11 브라우저는 `data` URL을 65529 문자로 제한하는 65535 개의 character long으로 제한합니다(MIME 타입을 지정하지 않고 plain `data`를 사용한다면, 소스가 아닌 인코딩된 데이터의 길이는 65529자가 됩니다).
- 오류 처리의 부족
  - : 미디어 내의 유효하지 않은 파라메터들 또는 '`base64`'를 지정할 때 오타들은 무시되지만 오류가 발생하지는 않습니다.
- 쿼리 문자열에 대한 미지원 등

  - : data URI의 data 일부는 불명확해서 데이터 URI를 이용해 쿼리 문자열(`<url>?parameter-data` 문법을 이용한 페이지 특정의 파라메터)을 사용하려는 시도는 URI가 나타내는 데이터 내에 쿼리 문자열을 포함하게 됩니다. 예를 들어:

    ```
    data:text/html,lots of text...<p><a name%3D"bottom">bottom</a>?arg=val
    ```

    이는 내용이 다음과 같은 HTML 리소스를 나타냅니다:

    ```
    lots of text...<p><a name="bottom">bottom</a>?arg=val
    ```

## 명세

{{Specifications}}

## 브라우저 호환성

{{Compat}}

## 함께 참고할 내용

- [Base64 인코딩과 디코딩](/ko/docs/Web/JavaScript/Base64_encoding_and_decoding)
- {{domxref("WindowBase64.atob","atob()")}}
- {{domxref("WindowBase64.btoa","btoa()")}}
- [CSS `url()`](/ko/docs/Web/CSS/uri)
- [URI](/ko/docs/URI)
