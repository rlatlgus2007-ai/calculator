# 간단한 Streamlit 계산기

Streamlit을 사용하여 두 정수와 연산자를 입력받고 결과를 출력하는 웹 기반 계산기 프로그램입니다.

## 주요 기능
- **입력**: 첫 번째 정수, 연산자(+, -, *, /), 두 번째 정수를 텍스트 박스로 입력받습니다.
- **예외 처리**: 
  - 사칙연산 기호 외의 값을 입력하면 오류 메시지를 출력합니다.
  - 숫자에 정수가 아닌 값이 입력되거나, 0으로 나누기를 시도할 경우 오류 메시지를 출력합니다.

## 실행 방법

1. Streamlit 라이브러리를 설치합니다.
   ```bash
   pip install streamlit
   ```

2. 아래의 전체 코드를 `app.py`라는 이름의 파이썬 파일로 저장합니다.

3. 터미널(또는 명령 프롬프트)에서 해당 파일이 있는 경로로 이동한 뒤, 다음 명령어를 실행합니다.
   ```bash
   streamlit run app.py
   ```

## 전체 코드 (`app.py`)

```python
import streamlit as st

st.title("간단한 계산기")

# 1. 첫 번째 정수, 연산자, 두 번째 정수를 각각 한 줄씩 입력받음
num1_input = st.text_input("첫 번째 정수")
operator = st.text_input("연산자")
num2_input = st.text_input("두 번째 정수")

# 결과 확인용 버튼
if st.button("결과 확인"):
    try:
        # 2. 입력받은 값을 정수로 변환 (정수가 아니면 ValueError 발생)
        num1 = int(num1_input)
        num2 = int(num2_input)
        
        # 3. 연산자에 따른 계산 수행 및 결과 출력
        if operator == '+':
            result = num1 + num2
            st.success(f"결과: {result}")
        elif operator == '-':
            result = num1 - num2
            st.success(f"결과: {result}")
        elif operator == '*':
            result = num1 * num2
            st.success(f"결과: {result}")
        elif operator == '/':
            # 0으로 나누는 예외 상황 처리
            if num2 == 0:
                st.error("오류: 0으로 나눌 수 없습니다.")
            else:
                result = num1 / num2
                st.success(f"결과: {result}")
        else:
            # 지정된 4가지 연산자 외의 기호가 들어왔을 때의 예외 처리
            st.error("오류: +, -, *, / 연산자만 사용할 수 있습니다.")
            
    except ValueError:
        # 입력값이 없거나, 소수, 문자 등 정수가 아닌 값이 입력된 경우의 예외 처리
        st.error("오류: 올바른 정수를 입력해주세요.")
```