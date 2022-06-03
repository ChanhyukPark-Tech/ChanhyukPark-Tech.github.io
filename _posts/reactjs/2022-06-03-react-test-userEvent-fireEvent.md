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

userEvent는 fireEvent 를 사용해서 만들어졌습니다. userEvent의 내부 코드를 보면 fireEvent를 사용하면서 엘리먼트의 타입에 따라서 Label을 클릭했을 때 checkbox, radio 버튼을 클릭했을 때 그 엘리먼트 타입에 맞는 더욱 적절한 반응을 보여줍니다.

### Example

fireEvent 로 버튼을 클릭하면 fireEvent.click(button) 버튼이 focus 되지 않습니다. 하지만 userEvent로 클릭하면 userEvent.click(button) 버튼이 focus 가 됩니다. 이렇게 실제 사용하는 유저가 보기에 실제 버튼을 클릭하는 행위가 더 잘 표현되기에 userEvent를 사용하는 게 더 추천되는 방법입니다.

### Conclusion

userEvent 는 element type 에 적절하게 반응하여 보여준다.
fireEvent 는 어떠한 element type 이든 똑같은 반응을 한다.

실제 테스트를 할때 유저가 실제 클릭할때 처럼 테스트를해야하기때문에 userEvent를 사용하는것을 더 권유한다.

---

<br>

    🌜 주관적인 견해가 담긴 글입니다. 다양한 의견이 있으실 경우
    언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다! 😄

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}
