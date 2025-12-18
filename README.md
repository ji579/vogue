# Vogue Website

패션 매거진 VOGUE의 웹사이트를 참고해서 만든 프로젝트입니다.

[Live Demo](https://ji579.github.io/vogue/) | [Figma](https://bit.ly/3MzpaXf) | [GitHub](https://github.com/ji579/vogue.git)

---

## 프로젝트 배경

VOGUE 웹사이트의 구조를 보면서 매거진 사이트를 어떻게 구성하는지 배우기 위해 시작했습니다.  
메인 페이지부터 여러 서브 페이지까지 전체 사이트를 만들면서, 페이지마다 다른 레이아웃을 어떻게 일관성 있게 유지할지 고민했습니다.

특히 헤더와 푸터를 모든 페이지에서 동일하게 유지하면서도 각 페이지의 콘텐츠에 맞는 레이아웃을 설계하는 데 집중했습니다.

---

## 구현 내용

**페이지 구성**
- 메인 / 아티클 목록 / 상세 페이지 / 어바웃
- 각 페이지의 목적에 맞춰 레이아웃 구성
- 공통 헤더/푸터로 사이트 통일성 확보

**디자인 방향**
- 텍스트와 이미지의 균형 있는 배치
- 큰 이미지와 여백으로 고급스러운 느낌 표현
- 가독성 높은 타이포그래피 적용

**기능 구현**
- 네비게이션 메뉴를 통한 페이지 간 이동
- 이미지 호버 시 오버레이 효과
- 스크롤 시 나타나는 부드러운 애니메이션

---

## 기술 스택

**HTML5**  
시맨틱 태그로 각 페이지의 구조를 명확하게 구분했습니다. `<article>`, `<section>`, `<aside>` 등을 적절히 사용해서 콘텐츠의 의미를 코드에 반영했습니다.

**CSS3**  
Flexbox로 전체 레이아웃을 구성했습니다. 복잡한 그리드 배치보다는 Flexbox의 유연함을 활용해서 다양한 화면 크기에 대응했습니다.

**JavaScript (ES6)**  
메뉴 토글, 이미지 슬라이더, 스크롤 애니메이션 같은 기본적인 인터랙션을 구현했습니다. 복잡한 라이브러리 없이 필요한 기능만 직접 작성했습니다.

---

## 주요 구현 사항

### 1. 공통 헤더/푸터 구조
```html
<!-- 모든 페이지에 공통 적용 -->
<header class="site-header">
  <div class="container">
    <h1 class="logo">VOGUE</h1>
    <nav class="main-nav">
      <a href="index.html">Home</a>
      <a href="articles.html">Articles</a>
      <a href="about.html">About</a>
    </nav>
  </div>
</header>
```
```css
.site-header {
  position: sticky;
  top: 0;
  background: white;
  border-bottom: 1px solid #ddd;
  z-index: 100;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}
```
모든 페이지에서 헤더가 일관되게 보이도록 했습니다. 스크롤해도 상단에 고정되어 있어서 언제든 다른 페이지로 이동할 수 있습니다.

### 2. 페이지별 레이아웃 차별화
```css
/* 메인 페이지 - 큰 히어로 이미지 */
.hero-section {
  height: 80vh;
  background-size: cover;
  display: flex;
  align-items: center;
}

/* 아티클 목록 - 그리드 레이아웃 */
.article-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 30px;
}

.article-card {
  flex: 0 0 calc(33.333% - 20px);
}

/* 상세 페이지 - 싱글 컬럼 */
.article-detail {
  max-width: 800px;
  margin: 0 auto;
  line-height: 1.8;
}
```
메인 페이지는 시각적 임팩트를 주고, 목록 페이지는 콘텐츠를 한눈에 볼 수 있게, 상세 페이지는 읽기 편하게 구성했습니다.

### 3. 반응형 네비게이션
```javascript
const menuToggle = document.querySelector('.menu-toggle');
const mainNav = document.querySelector('.main-nav');

menuToggle.addEventListener('click', () => {
  mainNav.classList.toggle('active');
});

// 화면 크기 변경 시 메뉴 상태 초기화
window.addEventListener('resize', () => {
  if (window.innerWidth > 768) {
    mainNav.classList.remove('active');
  }
});
```
```css
@media (max-width: 768px) {
  .main-nav {
    position: fixed;
    top: 60px;
    left: -100%;
    width: 100%;
    background: white;
    transition: left 0.3s ease;
  }
  
  .main-nav.active {
    left: 0;
  }
}
```
모바일에서는 햄버거 메뉴로 전환되고, 클릭하면 사이드에서 슬라이드되어 나타납니다.

### 4. 이미지 오버레이 효과
```css
.article-card {
  position: relative;
  overflow: hidden;
}

.article-card img {
  transition: transform 0.4s ease;
}

.article-card:hover img {
  transform: scale(1.05);
}

.article-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(to top, rgba(0,0,0,0.8), transparent);
  padding: 20px;
  color: white;
}
```
아티클 카드에 마우스를 올리면 이미지가 살짝 확대되고, 하단에서 제목과 설명이 그라디언트와 함께 나타납니다.

### 5. 타이포그래피 시스템
```css
:root {
  --font-display: 'Playfair Display', serif;
  --font-body: 'Open Sans', sans-serif;
}

h1, h2, h3 {
  font-family: var(--font-display);
  font-weight: 400;
  line-height: 1.3;
}

p {
  font-family: var(--font-body);
  font-size: 16px;
  line-height: 1.7;
  color: #333;
}
```
헤드라인은 세리프 폰트로 우아하게, 본문은 산세리프로 읽기 편하게 설정했습니다. 매거진 느낌을 주기 위해 폰트 선택에 신경 썼습니다.

---

## 페이지 구조

**메인 페이지 (index.html)**
- 대형 히어로 이미지
- 주요 아티클 하이라이트
- 카테고리별 콘텐츠 프리뷰

**아티클 목록 (articles.html)**
- 그리드 형태의 카드 레이아웃
- 카테고리 필터 기능
- 페이지네이션

**아티클 상세 (article-detail.html)**
- 싱글 컬럼 레이아웃
- 이미지와 텍스트의 조화
- 관련 아티클 추천

**어바웃 (about.html)**
- 매거진 소개
- 팀 소개
- 연락처 정보

---

## 배운 점

**일관성 있는 디자인**  
여러 페이지를 만들면서 전체적인 통일감을 유지하는 게 생각보다 어렵다는 걸 알았습니다. CSS 변수와 공통 클래스를 미리 정의해두니 작업이 훨씬 수월했습니다.

**콘텐츠 중심 레이아웃**  
매거진 사이트는 콘텐츠가 주인공이어야 한다는 걸 배웠습니다. 화려한 효과보다는 텍스트 가독성과 이미지 품질이 더 중요했습니다.

**페이지 간 자연스러운 전환**  
각 페이지가 독립적이면서도 하나의 사이트처럼 느껴지도록 네비게이션과 푸터를 일관되게 유지하는 게 중요했습니다.

---

## 개선하고 싶은 부분

- 실제 CMS처럼 관리자가 아티클을 추가/수정할 수 있는 기능
- 검색 기능과 태그 기반 필터링
- 댓글 시스템과 소셜 공유 기능
- 더 다양한 레이아웃 템플릿

---

## 프로젝트 구조

```
vogue/
├── index.html              # 메인
├── articles.html           # 아티클 목록
├── article-detail.html     # 아티클 상세
├── about.html              # 어바웃
├── css/
│   ├── reset.css
│   ├── common.css          # 공통 스타일
│   ├── header-footer.css   # 헤더/푸터
│   └── pages.css           # 페이지별 스타일
├── js/
│   ├── main.js
│   └── navigation.js
└── images/
```

---

## 라이선스

이 프로젝트는 학습 목적으로 제작되었습니다.  
VOGUE 브랜드의 저작권은 Condé Nast에 있습니다.