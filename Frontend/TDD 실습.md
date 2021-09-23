## TDD

1. 테스트에 필요한 테스팅 프레임워크 설치

   - npm install jest

2. 테스트할 파일 작성하기

   - 테스트 파일 양식: `<파일명>.test.js`, `<파일명>.spec.js`

3. 테스트 함수 작성하기

   - TDD: `test("test comment", 함수)`

     ```js
     test("test fail", () => {
       throw new Error()
     })
     ```

4. 테스트 실행하기

   - npx jest



## Describe

여러개의 테스트 케이스를 포함하는 그룹

```js
describe("group comment", () => {
  test("test pass", () => {
    // throw new Error()
  })
    
  test("test fail", () => {
    throw new Error()
  })
})
```



## Assertion

주어진 값이 조건에 부합하면 통과, 부합하지 않으면 에러 반환

> expect(입력값).toBe(예상값)



**입력값의 type을 알기 위해 의존라이브러리 설치**

- npm install @types/jest -D



## 중복 제거

- `beforeEach`/ `afterEach`: 그룹 내의 각 테스트케이스가 실행되기 전/후에 실행됨
- `beforeAll`/ `afterAll`: 그룹 내의 모든 테스트 케이스가 실행되기 전/ 후 단 한번만 실행됨
- `describe.each`/ `test.each`: 인자로 주어진 배열의 길이만큼 테스트 케이스를 반복 실행

