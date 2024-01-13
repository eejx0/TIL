# husky

> prettier이나 ESLint 설정 세팅하고 논의해도 팀원 한명이 그걸 적용하지 않는다면..
> 

> **정책들을 강제적으로 지키도록** 하고 지키지 않을 경우 merge, push 같은 과정에서 작업 중단하게 하는 **git hook** 활용
> 

### git hook❔

<aside>
💡 **git과 관련한 어떤 이벤트**가 발생했을 때 특정 **스크립트를 실행**할 수 있도록 하는 기능 
ex) commit, push …

</aside>

### Husky❔

- git hook 설정 도와주는 npm package
- 번거로운 git hook 설정 편리
- npm install 과정에서 사전에 세팅한 git hook을 다 적용 시킬 수 있음
- 따라서 모든 팀원이 git hook 실행이 되도록 하기가 편함

### 설치 및 적용 🔌

1. `npm i husky --save-dev`
2. npx husky install (처음 husky 세팅하는 사람만)
    
    👉🏻 .husky 디렉토리 생성
    
3. package.json에 script문 추가
    
    - 이후에 clone 받아 사용하는 사람은 npm install 후 자동으로 husky install이 될 수 있도록 하는 설정
    
    - `prettier --cache --write .`, `eslint --cache .`
        
        → 모든 파일 검사하지만 이미 검사한 파일이나 항목을 cache에 저장하고 변경사항이 없으면 해당 파일 검사 x
        
        → 따라서 실행 속도 빠름
        
    - npm run format, npm run lint 명령어 통해 좀 더 쉽게 사용하도록 package.json 스크립트 문에 추가
    
    ```json
    // Example
    {
    	"scripts": {
    		"postinstall": "husky install",
    		"format": "prettier --cache --write .",
    		"lint": "eslint --cache .",
    	},
    }
    ```
    
    👉🏻 이 스크립트를 프로젝트 요구 사항에 맞게 수정 가능
    
4.  pre-commit, pre-push hook 추가
    
    `npx husky add .husky/pre-commit “npm run format”`
    
    `npx husky add .husky/pre-push “npm run lint”`
    
    - DMS에선 pre-commit만 되어있음
