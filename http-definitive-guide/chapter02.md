## 2.1 인터넷의 리소스 탐색하기

- HTTP 명세에는 URI(하지만 대부분 URL)를 리소스 식별자로 이용하여 탐색
- URL(Uniform Resource Locator): 인터넷 리소스를 가리키는 표준 이름
    - '**스킴://서버위치/경로**' 의 구조로 이루어져 있음
        - 스킴: 웹 클라이언트가 리소스에 어떻게 접근하는지. 예: http 프로토콜 사용
        - 서버 위치: 리소스가 어디에 호스팅 되어있는지
        - 경로: 리소스의 경로로, 서버 내의 리소스 중 어느 리소스인지 판별

### 2.1.1 URL 이전의 암흑시대

- URL이 있기 전에는 애플리케이션마다 각자의 분류 방식 사용
- URL은 브라우저가 정보를 찾는데 필요한 모든 것을 제공하며, 어디에 위치하고 어떻게 가져오는지 정의함

## 2.2 URL 문법

- 대부분의 URL은 URL 문법을 따르며, 스킴에 따라 달라지기도 하지만 형태와 문법면에서 유사.

```
<스킴>://<사용자이름>:<비밀번호>@<호스트>:<포트>/<경로>;<파라미터>?<질의>#<프래그먼트>
```

- **스킴(scheme)**: 리소스를 가져오려면 어떤 프로토콜을 사용하여 서버에 접근해야하는가
- **사용자 이름(user name)**: 일부 스킴은 리소스에 접근하기 위해 사용자 이름 필요
    - 기본 값: anonymous
- **비밀번호(password)**: 사용자의 비밀번호
- **호스트(host)**: 리소스를 호스팅하는 서버의 호스트명이나 IP주소
- **포트(port)**: 리소스를 호스팅하는 서버가 열어 놓은 포트 번호. 많은 스킴이 기본 포트를 가지고 있음(HTTP는 80)
    - 기본 값: 스킴마다 다름.
- **경로(path)**: 서버 내 리소스가 서버에 어디에있는지 가리킴. 경로 컴포넌트의 문법은 서버와 스킴에 따라 다름. HTTP에서는 '/'문자를 기준으로 경로 조각으로 나눔(유닉스 파일 시스템과 유사)
- **파라미터(parameter)**: 특정 스킴(예: ftp)에서 정확한 요청을 위해 입력 파라미터를 기술하는 용도로 사용. 파라미터는 key/value 쌍을 가지며, 여러 쌍을 가질 수 있음.
    - 경로 조각마다 자체 파라미터를 가질 수 있다. 
    예: `http://www.joes-hardware.com/hammers;sale=false/index.html;graphics=true`
- **질의(query)**: 스킴에서 애플리케이션에 패러미터 전달용. 질의 컴포넌트 작성의 공통 포맷은 없음.
    - 편의상 많은 게이트웨이가 '&'로 나뉘는 'key=value' 형식의 질의 문자열을 원한다. 예: `...?item=12731&color=blue`
- **프래그먼트(fragment)**: 리소스를 본래 수준보다 더 작게 나누어, 조각이나 일부를 가리키는 이름. URL이 특정 객체를 가리킬 경우에 프래그먼트 필드는 서버에 전달되지 않고, 클라이언트에서만 사용.
    - 일반적으로 HTTP 서버는 객체 일부가 아닌 전체만 다루므로, 서버에 미전달하고 브라우저가 프래그먼트를 사용하여 보고자 하는 리소스만 보여줌

## 2.3 단축 URL

- URL의 종류: 상대 URL, 절대 URL
- 절대 URL은 우리가 지금까지 본 URL로, 리소스 접근에 필요한 모든 정보를 가지고 있음

### 2.3.1 상대 URL

- 상대 URL은 URL을 짧게 표기하는 방식으로, 리소스 접근에 필요한 모든 정보를 가지고 있지 않으며, 모든 정보를 얻기 위해서는 기저(base)라고 하는 다른 URL을 사용해야 한다.
- 상대 URL 문법에 따르면, HTML 작성자는 스킴, 호스트, 다른 컴포넌트를 입력하지 않아도 되며, 그 정보는 컴포넌트가 포함된 리소스의 기저 URL에서 추출 가능.
- 예시

    ```html
    <!-- http://www.joes-hardware.com/tools.html -->
    ...
    <p>
    ... selection of <a href=".hammers.html">hammers</a>on earth ...
    </p>
    ...
    ```

    - 위의 경우 기저 URL은: `http://www.joes-hardware.com/tools.html`
    - 이 기저 URL로 새로운 절대 URL 만들수 있다: `http://www.joes-hardware.com/hammers.html`
- 상대 URL을 사용하면 리소스 집합(html 페이지 등)을 쉽게 변경할 수 있고, 문서 집합의 위치를 변경하더라도 새로운 기저 URL에 의해 해석되기 때문에 정상적으로 동작한다.
- 상대 URL을 절대 URL로 변환하는 방법
    1. 기저  URL을 찾기
        - 리소스에서 명시적으로 제공 되거나 / 해당 리소스의 URL을 기저 URL로 사용하거나(앞의 예) / 기저 URL이 없는 경우(절대 URL이거나 깨진 URL)
    2. 상대 참조 해석하기
        - 기저 URL과, 상대 URL을 컴포넌트 단위로 분리하여 변환 알고리즘을 통해 절대 경로 형태로 변환한다.

### 2.3.2 URL 확장

어떤 브라우저는 URL입력시에 자동으로 URL을 확장하여 사용자가 URL을 빠르게 입력하도록 도와준다.

- 호스트명 확장
    - 단순한 휴리스틱만을 사용해서 입력한 홋스트명을 전체 호스트명으로 확장
    - 예: `yahoo` 입력 시, 자동으로 `www.yahoo.com` 으로 변환
- 히스토리 확장
    - 과거에 사용자가 방문했던 URL의 기록을 저장하여, URL 입력 시에 입력된 글자를 포함하는 방문한 완결된 형태의 URL중에서 선택하게 함.

## 2.4 안전하지 않은 문자

- 어떤 프로토콜을 통해서든 안전하게 전송 될 수 있도록 URL은 잘 호환되게 설계되었다.
- **안전한 문자**: 문자가 제거되어 정보가 유실되지 않도록 상대적으로 작고 안전한 알파벳 문자만 포함하도록 함
- **안전하지 않은 문자 제외**: 가독성을 위해 출력되지 않거나 보이지 않는 문자를 사용하는 것을 금지
- **이스케이프**: 이진 데이터나 알파벳 외의 문자도 포함할 수 있도록 안전하지 않은 문자를 안전한 문자로 인코딩

### 2.4.1 URL 문자 집합

- URL 문자 집합은 US-ASCII 문자 집합. 7비트를 사용하여 영자판 키와 출력되지 않는 제어문자 표현
    - US-ASCII는 오래된 문자 집합으로, 영어 외 유럽언어 및 비라틴계 언어를 지원하지 않음
- URL로 특정 이진 데이터를 포함해야 하는 경우 존재
- 이스케이프 문자열을 통해 특정 문자나 데이터를 인코딩할 수 있게 함

### 2.4.2 인코딩 체계

- [인코딩](https://en.wikipedia.org/wiki/Percent-encoding)은 안전하지 않은 문자를 퍼센티지 기호(%)로 시작해, ASCII 코드로 표현되는 두개의 16 진수로 이루어진 이스케이프 문자로 변환

### 2.4.3 문자 제한

- URL 내의 예약 문자로, 다른 목적으로 사용하려면 인코딩이 필요하다
    - `%` : 인코딩 된 문자에 사용할 이스케이프 토큰
    - `/` : 경로 컴포넌트에 있는 경로 세그먼트 나누는 용도
    - `.` : 경로 컴포넌트에서 선점
    - `..` : 경로 컴포넌트에서 선점
    - `#` : 프래그먼트 구획 문자
    - `?` : 질의 구획 문자
    - `;` : 파라미터 구획 문자
    - `:` : 스킴, 사용자이름/비밀번호, 호스트/포트의 구획 문자
    - `$`, `,`, `+` : 선점
    - `@`, `&`, `=` : 특정 스킴에서 특별한 의미가 있기때문에 선점
    - `{`, `}`, `|`, `\`, `~`, `[`, `]`, ` : 게이트웨이와 같은 여러 전송 에이전트에서 불안전하게 다룸
    - `<`, `>`, `"` : URL 범위 밖에서 역할이 있는 문자. 안전하지 않음.
    - `0x00` - `0x1F`, `0x7F`: 이 16진수 범위에 속하는 문자는 인쇄되지 않는 US-ASCII
    - `0x7F` < : 이 16진수 범위에 속하는 문자는 7비트 US-ASCII 가 아님

### 2.4.4 좀더 알아보기

- 입력받은 URL에서 어떤 문자를 인코딩해야 하는지는 사용자로부터 최초로 URL을 입력받는 애플리케이션(브라우저)에서 하는 것이 가장 적절
    - URL 구성 컴포넌트마다 사용 가능 문자가 다르며, 스킴에 따라서도 달라지므로
- 보통 URL을 해석하는 애플리케이션은 그것을 처리하기 전에 URL을 디코드해야 함

## 2.5 스킴의 바다

- **http**: 사용자 이름, 비밀번호가 제외된 일반 URL 포맷. 하이퍼 텍스트 전송 프로토콜(Hypertext Transfer Protocol)스킴. 기본 포트값은 80.

    ```
    http://<호스트>:<포트>/<경로>?<질의>#<프래그먼트>
    http://www.joes-hardware.com/index.html
    ```

- **https**: http와 유사하며, HTTP 커넥션의 양 끝단에서 암호화 하기위해 보안 소켓 계층(Secure Sockets Layer, SSL)을 사용하는 점이 다름. 기본 포트값은 443.

    ```
    https://<호스트>:<포트>/<경로>?<질의>#<프래그먼트>
    예: https://www.joes-hardware.com/secure.html
    ```

- **malito**: 이메일 주소를 가리키며, 다른 스킴과 다르게 동작하므로 표준 URL과 다른 포맷을 가진다. [RFC 882](https://tools.ietf.org/html/rfc822),  [RFC 2882](https://tools.ietf.org/html/rfc2822), [RFC 5332](https://tools.ietf.org/html/rfc5322)참조.

    ```
    mailto:<RFC-882-addr-spec>
    예: mailto:joe@joes-hardware.com
    ```

- **ftp**: 파일 전송 프로토콜(File Transfer Protocol)URL은 FTP서버에 있는 파일을 다운로드/업로드하고 디렉터리내의 콘텐츠 목록을 가져오는 데 사용.

    ```
    ftp://<사용자 이름>:<비밀번호>@<호스트>:<포트>/<경로>;<파라미터>
    예: ftp://anonymouse:joe%40joes-hardware.com@prep.ai.mit.edu:21/pub/gnu
    ```

- **rtsp, rtspu**: 실시간 스트리밍 프로토콜(Real Time Streaming Protocol)을 통해서 읽을 수 있는 미디어 리소스(오디오 및 비디오 등) 식별자. rtsp**u**는 리소스를 읽기 위해 UDP 프로토콜을 사용됨을 뜻함

    ```
    rtsp://<사용자 이름>:<비밀번호>@<호스트>:<포트>/<경로>
    rtspu://<사용자 이름>:<비밀번호>@<호스트>:<포트>/<경로>
    예: rtsp:www.joes-hardware.com:554/interview/cto_video
    ```

- **file**: 호스트 기기(로컬디스크, 네트워크 파일시스템, 기타 파일 공유 시스템)에서 바로 접근할 수 있는 파일을 나타냄. 일반적인 URL 포맷을 따르며, 호스트 생략시 URL을 사용하는 기기의 로컬호스트가 기본값

    ```
    file:<호스트>/<경로>
    예: file://OFFICE-FS/policies/casual-fridays.doc
    ```

- **news**: 특정 문서나 뉴스 그룹 접근용(RFC 1036). 해당 리소스 위치에 대한 정보를 포함하지 않으며 애플리케이션이 알아냄. 브라우저는 현재 설명되어있는 뉴스 서버 정보를 사용하여 어떤 서버로부터 뉴스를 가져올지 결정.

    ```
    news:<newsgroup>
    news:<news-article-id>
    예: news:rec.arts.startrek
    ```

- **telnet**: 대화형 서비스 접근용. telnet URL자체는 객체를 가리키지 않지만, 리소스라고 할 수 있는 대화형 애플리케이션이 telnet 프로토콜을 통해 접근 가능.

    ```
    telnet://<사용자이름>:<비밀번호>@<호스트>:<포트>/
    예: telnet:slurp:webhound@joes-hardware.com:23/
    ```
