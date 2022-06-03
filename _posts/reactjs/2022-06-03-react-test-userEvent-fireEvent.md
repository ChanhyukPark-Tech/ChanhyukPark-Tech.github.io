---
title: "[react] test userEvent > fireEvent"

categories:
  - reactjs
tags:
  - [react, test, testing-library]

toc: true
toc_sticky: true

date: 2022-06-03
---

# userEvent vs fireEvent

두괄식 결론
지금까지는 유저의 버튼 클릭을 테스트할때 fireEvent API를 사용했습니다. 이때 fireEvent를 사용해서 잘 처리를 해줬지만 userEvent API를 사용하는게 더 좋은 방법입니다. fireEvent.click(element) < userEvent.click(element)>

## userEvent

userEvent는 fireEvent 를
... WIP

---

<br>

    🌜 주관적인 견해가 담긴 글입니다. 다양한 의견이 있으실 경우
    언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다! 😄

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}
