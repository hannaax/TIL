**Node.js**는 **JavaScript를 브라우저 외부에서 실행할 수 있게 만드는 JavaScript 런타임 환경**입니다. 이는 Chrome의 JavaScript 엔진인 V8이 독립하여 만들어진 프로젝트입니다.

JavaScript는 원래 브라우저에서 동작하는 언어로, 웹페이지 로딩 후에 문서를 변경하거나 브라우저에서 실행되는 로직을 작성하는 등의 작업에 사용됩니다. 그러나 **Node.js의 등장으로 JavaScript는 브라우저에 국한되지 않고, 브라우저 외부에서도 실행**할 수 있게 되었습니다.

**Node.js에서는 일부 브라우저에서 사용되던 API는 삭제되었고, 새로운 API가 추가**되었습니다. 예를 들어, DOM과의 상호작용은 브라우저 환경에서만 가능하므로 Node.js에서는 사용할 수 없습니다. 반면, 브라우저에서는 보안 문제로 파일 시스템 작업이 제한되지만, Node.js에서는 이를 가능하게 하는 API가 추가되었습니다.

**Node.js는 사용자의 브라우저가 아닌, 서버나 다른 기기에서 실행**됩니다. 이를 통해 웹 서버 구축, 데이터베이스와의 통신 등 서버 측 작업을 JavaScript로 처리할 수 있게 되었습니다. 이러한 기능으로 인해 Node.js는 PHP, Java, [ASP.net](http://asp.net/) 등의 서버 사이드 언어를 대체할 수 있는 선택지가 되었습니다.

따라서, **Node.js**는 브라우저 외부에서 JavaScript를 사용할 수 있게 하면서, 동시에 새로운 기능을 추가하고 브라우저에서만 가능했던 기능을 제거하여, **JavaScript의 활용 범위를 확장시킨 도구**라고 할 수 있습니다.

<br/>

---

<br/>

Node.js를 사용하여 프로젝트를 시작하기 위해, 우선 nodejs.org에서 최신 버전의 Node.js를 다운로드하고 설치해야 합니다. 이 과정이 끝나면 시스템에 Node.js와 함께 Node Package Manager(NPM)도 설치됩니다.

이제 Node.js 코드를 작성할 차례입니다. Visual Studio Code와 같은 IDE에서 빈 폴더를 생성하고, app.js라는 새로운 파일을 만들어 JavaScript 코드를 작성합니다. 이 과정에서는 모던 JavaScript 구문(화살표 함수, 구조 분해, 전개 연산자 등)을 사용합니다.

작성한 코드는 Node.js를 통해 실행할 수 있습니다. IDE의 내장된 터미널을 사용하여 'node app.js'라는 명령을 실행하면 됩니다. 그런데 여기서 주의할 점은, 브라우저 환경에서만 사용 가능한 API(예: alert)는 Node.js에서 사용할 수 없다는 점입니다.

대신, Node.js에서는 파일 시스템 작업을 할 수 있도록 지원하는 File system API와 같은 새로운 API를 사용할 수 있습니다. 이를 사용하기 위해서는 **'require' 함수를 통해 File system 모듈을 불러와야** 합니다.

불러온 File system 모듈의 **'writeFile' 메서드를 사용하면, 파일에 데이터를 작성**할 수 있습니다. 이 메서드는 **비동기식으로 동작하며, 작업이 끝나면 지정된 콜백 함수를 호출**합니다.

이렇게 **Node.js**를 사용하면, **브라우저 환경이 아닌 곳에서도 JavaScript 코드를 실행**할 수 있으며, **파일 시스템과 같은 새로운 기능을 사용**할 수 있습니다. 브라우

저 전용 API를 사용할 수 없다는 단점이 있지만, 이를 대신할 수 있는 다양한 API가 제공됩니다.

<br/>

---

<br/>

Node.js 프로젝트를 관리형 프로젝트로 전환하려면 npm(Node Package Manager)을 사용해야 합니다. 이를 위해, 먼저 npm init 명령어를 실행하여 프로젝트를 초기화하고, package.json 파일이 생성됩니다. 이 파일에는 프로젝트의 의존성 정보가 저장됩니다.

Express 라이브러리를 설치하기 위해 npm install express --save 명령어를 사용합니다. **Express**는 웹 서버를 구축하고 HTTP 요청을 처리하는 데 유용한 도구입니다. Express를 사용하면 수신 요청을 더 쉽게 처리하고, 요청에 대한 응답을 단순화할 수 있습니다.

**Express는 미들웨어라는 개념을 사용하여 요청을 처리**합니다. **미들웨어는 요청을 수신하고 처리한 후 응답을 반환하는 일반 함수**입니다. Express 앱에서는 **여러 미들웨어 함수를 설정하고, 이러한 함수들은 순차적으로 실행**됩니다. 각 함수는 요청을 처리하고 **결과를 다음 미들웨어 함수로 전달**합니다.

Express를 사용하면, 서버를 재시작하지 않고도 코드 변경 사항을 적용할 수 있습니다. 이는 개발 과정을 더욱 효율적으로 만들어 줍니다. 그러나, Express를 사용하더라도 데이터 파싱이나 응답 처리와 같은 작업은 여전히 필요합니다. 이러한 작업은 개선이 필요하며, Express 라이브러리의 추가 기능을 활용하여 더욱 간편하게 수행할 수 있습니다.
