# npm install, npm ci
> 모두 **의존성 목록을 설치**하는 커맨드 → “**npm ci가 npm install에 비해 의존성 버전을 더 엄격하게 유지”**
> 

<aside>
🔥

**npm install**은 package.json에 명시된 version range 내에서 **다른 버전 설치할 가능성**이 있음
**npm ci**는 오직 package-lock.json에 **정확하게 표기된 특정 버전**을 따름

---

- 예기치 않게 다른 버전의 의존성을 설치하는 일 방지
- 버전 결정을 위한 연산 수행이 필요 없어서 설치 속도 면에서 유리
</aside>

<aside>
🔥

**npm install**은 **package-lock.json을 변경할 가능성**이 있음
**npm ci**는 절대 **변경하지 않음**

---

- npm ci는 의존성 목록의 버전을 변경없이 일관되게 유지할 수 있게해줌
</aside>

<aside>
🔥

**npm ci**는 매번 **node_modules를 삭제한 후 설치**

---

- 이전에 설치된 의존성과의 충돌로 인한 문제 방지
- 오로지 package-lock.json에 따라 매번 동일한 의존성 설치할 것을 확실히 보장
</aside>

### 로컬 환경에서 npm ci 사용 🤔

> 가능하지만 node_modules를 매번 모두 삭제하고 다시 설치해서 불필요한 시간이 소요될 수 있음
> 

→ **로컬**에선 일반적으로 **npm** **install**, **CI/CD 환경**에서는 **npm** **ci**
