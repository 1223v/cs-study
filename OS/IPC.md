### IPC (Inter-Process Communication)

### IPC란 무엇이며, 왜 필요한가요?

- IPC(Inter-Process Communication)는 프로세스 간 통신을 의미.
- 운영 체제 내에서 실행되는 프로세스들이 데이터를 교환하고 협력 가능.
- 격리성을 보장 ⇒ 각 프로세스가 독립적으로 실행되어 보안 취약점의 영향을 최소화.

- **필요성**:
  - 데이터를 공유해야 하는 애플리케이션 구성 요소들 간의 협력
  - 병렬 처리로 성능 향상
  - 다중 프로세스 기반 애플리케이션 설계

### 파이프, 메시지 큐, 공유 메모리 비교

| **특징**         | **파이프**                           | **메시지 큐**                           | **공유 메모리**             |
| ---------------- | ------------------------------------ | --------------------------------------- | --------------------------- |
| 데이터 전달 방식 | 단방향(익명) 또는 양방향(Named Pipe) | 메시지 단위로 데이터 전송               | 메모리 공간 공유            |
| 속도             | 상대적으로 느림                      | 중간 수준                               | 빠름                        |
| 복잡성           | 간단                                 | 중간 수준                               | 구현 복잡                   |
| 지속성           | 부모-자식 관계에서만 사용 가능       | 프로세스 독립적으로 메시지 큐 접근 가능 | 별도의 동기화 메커니즘 필요 |
| 사용 사례        | 단순 데이터 스트림                   | 프로세스 간 구조화된 메시지 교환        | 대용량 데이터 공유          |

### 브라우저에서 IPC를 활용한 주요 사례

### **멀티프로세스 아키텍처**

- **브라우저 구조**

  - **Browser Process**: 브라우저의 UI, 네트워크 요청, 탭 관리 등 총괄.
  - **Renderer Process**: 웹 페이지 렌더링, 자바스크립트 실행, HTML/CSS 처리.
  - **GPU Process**: 하드웨어 가속 및 그래픽 처리를 담당.
  - **Plugin Process**: 플러그인(예: Flash, PDF 뷰어) 처리.
  - **Utility Process**: 미디어 디코딩, 네트워크 서비스 등 보조 작업.

- **IPC 역할**
  - 각 프로세스 간 데이터를 교환하여 페이지 로드, 스크롤, 클릭 이벤트 등 사용자 작업을 수행.
  - 프로세스 간 데이터를 안전하게 전달하며 보안 격리를 유지.

---

### **웹 페이지와 브라우저 간 통신 (DOM 접근 및 이벤트)**

- **DOM 이벤트 전파**:
  - 사용자가 클릭, 키 입력 등을 수행하면 Renderer Process가 이를 처리하고 필요 시 Browser Process로 전달.
  - IPC를 통해 Renderer와 Browser 간의 이벤트 동기화.
- **Web APIs 호출**:
  - 예: `window.open()` 같은 호출이 Renderer에서 실행되면 IPC를 통해 Browser Process에서 새로운 탭 또는 창을 생성.

---

### **Web Workers와 Shared Workers**

- **Web Workers**:
  - 자바스크립트 코드에서 멀티스레드를 활용해 백그라운드 작업을 수행.
- **Shared Workers**:
  - 여러 브라우저 탭이 동일한 작업자를 공유.
- **IPC 활용**:
  - 워커와 메인 스레드 간 **Message Passing**으로 데이터를 주고받음.
  - `postMessage()`와 `onmessage` 이벤트를 통해 메시지를 교환.

---

### **브라우저 확장 프로그램 (Browser Extensions)**

- **동작 원리**:
  - 확장 프로그램(Extension)은 브라우저 API를 사용하여 기능을 확장.
- **IPC 활용**:
  - 확장 프로그램의 콘텐츠 스크립트(Content Script)와 백그라운드 스크립트 간 통신.
  - 예: 확장 프로그램이 웹 페이지에서 데이터를 수집하고 이를 백그라운드 프로세스로 전달.
  - `chrome.runtime.sendMessage`와 같은 메서드를 사용.

---

### **네트워크와 렌더링 간 데이터 전달**

- **네트워크 요청**:
  - Browser Process가 HTTP 요청을 처리하고, Renderer Process로 데이터를 전달.
- **IPC 역할**:
  - 요청의 결과(HTML, CSS, JS 파일)를 렌더링 프로세스에 전달.
  - 네트워크 프로세스와 렌더링 프로세스 간 데이터 전달을 최적화.

---

### **멀티미디어 처리**

- **비디오/오디오 스트리밍**:
  - 비디오 디코딩 작업은 GPU Process 또는 Utility Process에서 실행.
  - IPC를 통해 디코딩된 데이터를 Renderer Process로 전달.
- **웹캠/마이크 접근**:
  - 사용자 권한 요청과 데이터 처리가 각기 다른 프로세스에서 이루어지며 IPC로 동기화.

---

### **크로스-오리진 통신 (CORS 및 Cross-Origin Messaging)**

- **Cross-Origin Messaging**:
  - 서로 다른 출처의 웹 페이지가 데이터를 주고받는 경우.
  - `postMessage()` API를 사용하여 안전한 IPC를 구현.
- **CORS 요청 처리**:
  - Browser Process가 CORS 정책을 확인하고, Renderer Process와 데이터를 교환.

### IPC의 중요성 및 효과

**안정성**: 프로세스 간 격리를 통해 한 프로세스의 충돌이 브라우저 전체에 영향을 주지 않음.

**보안성**: 각 프로세스가 독립적으로 실행되어 보안 취약점의 영향을 최소화.

**성능**: 멀티프로세스 구조와 IPC를 활용해 작업 부하를 분산.
