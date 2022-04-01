# 접근성
### 접근성이 필요한 이유
웹 접근성은 모두가 사용할 수 있도록 웹사이트를 디자인, 개발하는 것을 의미한다. Assistive technology들이 웹페이지들을 해석할 수 있도록 접근성을 갖추는 것이 필요하다.
React는 접근성을 갖춘 웹사이트를 만들 수 있도록 모든 지원을 하고 있으며, 대부분은 표준 HTML 기술이 사용된다.

### 표준 및 지침
### WCAG
Web Content Accessibility Guidelines는 접근성을 갖춘 웹사이트를 만드는데 필요한 지침을 제공한다.

### WAI-ARIA
Web Accessibility Initiative - Accessible Rich Internet Applications 문서에는 접근성을 갖춘 JavaScript 위젯을 만드는데 필요한 기술들이 담겨 있다.

참고로, JSX에서는 모든 aria-* HTML 어트리뷰트를 지원하고 있다. React에서 대부분의 DOM 프로퍼티와 어트리뷰트에 대한 값이 캐멀 케이스로 지원되는 반면, aria-* 와 같은 어트리뷰트는 일반적인 HTML과 마찬가지로 hypen-case(혹은 kebab-case, lisp-case 등)로 작성해야 한다.
```
<input
  type="text"
  aria-label={labelText}
  aria-required="true"
  onChange={onchangeHandler}
  value={inputValue}
  name="name"
/>
```

# 시맨틱 HTML
시맨틱 HTML은 웹 애플리케이션에 있어 접근성의 기초이다. 정보의 의미가 강조되는 HTML 엘리먼트를 웹 사이트에서 사용하면 자연스럽게 접근성이 갖추어지곤 한다.

가끔 React로 구성한 코드가 돌아가게 만들기 위해 &lt;div>와 같은 엘리먼트를 사용해 HTML의 의미를 깨트리곤 합니다. 특히, 목록(&lt;ol>, &lt;ul>, &lt;dl>)과 HTML %lt;table>을 사용할 때 문제가 두드러진다. 이 경우에는, React Fragment를 사용하여 여러 엘리먼트를 하나로 묶어주는 것이 권장된다.
```
import React, { Fragment } from 'react';

function ListItem({ item }) {
  return (
    <Fragment>
      <dt>{item.term}</dt>
      <dd>{item.description}</dd>
    </Fragment>
  );
}

function Glossary(props) {
  return (
    <dl>
      {props.items.map(item => (
        <ListItem item={item} key={item.id} />
      ))}
    </dl>
  );
}
```
다른 엘리먼트와 마찬가지로, Fragment는 배열의 각 항목을 매핑할 때에도 사용할 수 있다.
```
function Glossary(props) {
  return (
    <dl>
      {props.items.map(item => (
        // 항목을 매핑할 때 Fragment는 반드시 `key` 프로퍼티가 있어야 합니다.
        <Fragment key={item.id}>
          <dt>{item.term}</dt>
          <dd>{item.description}</dd>
        </Fragment>
      ))}
    </dl>
  );
}
```
Fragment 태그에 어떤 props도 필요하지 않고, 사용하고 있는 도구에서 지원한다면, 아래와 같이 짧게 줄여 쓸 수 있다.
```
function ListItem({ item }) {
  return (
    <>
      <dt>{item.term}</dt>
      <dd>{item.description}</dd>
    </>
  );
}
```

