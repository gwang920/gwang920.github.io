---
title: 프로그래머스 프론트엔드 과제관 - ilovecat
toc: true
categories:	
    - programmers
tags:
- 프로그래머스 과제관
- 프론트엔드
last_modified_at: 
---

### 반응형 웹

유저가 사용하는 디바이스의 가로 길이에 따라 검색결과의 row 당 column 갯수를 적절히 변경해주어야 합니다.

```css
.SearchResult {
  margin-top: 10px;
  display: grid;
  grid-template-columns: repeat(4, minmax(250px, 1fr));
  grid-gap: 10px;
}

/* 992px 이하 3개*/
@media (max-width : 992px){
    section .SearchResult{
        grid-template-columns: repeat(3, minmax(250px, 1fr));
    }
}
/* 768px 이하 적용 2개 */
@media (max-width : 768px){
    section .SearchResult{
        grid-template-columns: repeat(2, minmax(250px, 1fr));
    }
}
/* 576px 이하 적용 1개 */
@media (max-width : 576px){
    section .SearchResult{
        grid-template-columns: repeat(1, minmax(250px, 1fr));
    }
}
```

- 미디어쿼리를 적용한다. 
- `minmax(최대값, 최소값)`, `minmax()` 함수를 사용하면 최소값, 최대값 범위 내에서 값을 유연하게 처리한다. 

- 캐스케이딩 등 다른 조건이 같으면 `css`는 나중에 오는 쿼리가 우선순위를 갖는다.
- `.SearchResult`를 가장 아래에 선언하면 `@media` 쿼리가 적용이 안된다.

### 다크모드

다크 모드(Dark mode)를 지원하도록 CSS를 수정해야 합니다.

- 모든 글자 색상은 `#FFFFFF` , 배경 색상은 `#000000` 로 한정합니다. prefers-color-scheme 값은 dark, light 두 가지가 있으며, 브라우저의 모드에 따라서 미디어퀴리가 적용됨.

```
파일명 : darkmode.js
```

```javascript
const STORAGE_KEY = 'user-color-scheme';
const COLOR_MODE_KEY = '--color-mode';

const darkmodeBtn = document.querySelector('.darkmode-btn');

const getCSSCustomProp = (propKey) => {

    /* 
       getComputedStyle 인자로 전달받은 요소의 모든 css 속성값을 담은 객체를 회신
       ref : https://developer.mozilla.org/ko/docs/Web/API/Window/getComputedStyle
    */
    let response = getComputedStyle(document.documentElement).getPropertyValue(propKey);

    // Tidy up the string if there’s something to work with
    if (response.length) {
        response = response.replace(/\'|"/g, '').trim();
    }

    // Return the string response by default
    return response;
};

const applySetting = passedSetting => {
    let currentSetting = passedSetting || localStorage.getItem(STORAGE_KEY);

    if (currentSetting) {
        document.documentElement.setAttribute('data-user-color-scheme', currentSetting);
        setButtonLabel(currentSetting);
    } else {
        setButtonLabel(getCSSCustomProp(COLOR_MODE_KEY));
    }
};

const toggleSetting = () => {
    let currentSetting = localStorage.getItem(STORAGE_KEY);

    switch (currentSetting) {
        case null:
            currentSetting = getCSSCustomProp(COLOR_MODE_KEY) === 'dark' ? 'light' : 'dark';
            break;
        case 'light':
            currentSetting = 'dark';
            break;
        case 'dark':
            currentSetting = 'light';
            break;
    }

    localStorage.setItem(STORAGE_KEY, currentSetting);

    return currentSetting;
};

// 버튼 생성
const setButtonLabel = currentSetting => {
    darkmodeBtn.innerText = currentSetting === 'dark' ? '🌕' : '🌑';
};

darkmodeBtn.addEventListener('click', evt => {
    evt.preventDefault();

    applySetting(toggleSetting());
});

applySetting();
```



**추가**

1. `App.js`에 버튼 생성

```
파일명 : App.js
```

```javascript
const darkmodeBtn = document.createElement('span');
    darkmodeBtn.className = 'darkmode-btn';
    darkmodeBtn.innerText = '🌕';

    $target.appendChild(darkmodeBtn);
```

2. `index.html` 에 `type="module"` 적용

```
파일명 : index.html
```

```html
<script type="module" src="src/utils/darkmode.js"></script>
```

3. `style.css`에 미디어쿼리 `css` 추가

````
파일명 : style.css
````

```css
@media (prefers-color-scheme: dark) {
  :root {
    --color-mode: 'dark';
  }
  
  :root:not([data-user-color-scheme]) {
    --background: var(--color-dark);
    --text-color: var(--color-light);
  }
}

[data-user-color-scheme="dark"] {
  --background: var(--color-dark);
  --text-color: var(--color-light);
}

```

4. `style.css` 전역변수 설정

```css
:root {
  --color-mode: 'light';
  --color-dark: black;
  --color-light: white;
  --background: white;
  --text-color: black;
}
/*
ease-in-out
정해진 시간 동안 요소의 속성값을 부드럽게 변화
*/
body {
  background: var(--background);
  color: var(--text-color);
  transition: background 500ms ease-in-out, color 200ms ease;
}
```



```javascript
import ImageInfo from "./components/ImageInfo.js";
import SearchInput from "./components/SearchInput.js";
import SearchResult from "./components/SearchResult.js";
import Loading from "./components/Loading.js";

import { getItem, setItem } from './utils/sessionStorage.js';
import { api } from "./api/api.js";

export default class App {
  $target = null;
  data = [];

  constructor($target) {
    this.$target = $target;

    this.searchInput = new SearchInput({
      $target,
      onSearch: async keyword => {
        loading.toggleSpinner();
        const response = await api.fetchCats(keyword);
        if(!response.isError){
          setItem('data', response.data);
          console.log(response.data);
          SearchResult.setState(response.data);
          loading.toggleSpinner();
        } else{
          error.setState(response.data);
        }
      }
    });

    this.searchResult = new SearchResult({
      $target,
      initialData: this.data,
      onClick: image => {
        this.imageInfo.setState({
          visible: true,
          image
        });
      }
    });

    this.imageInfo = new ImageInfo({
      $target,
      data: {
        visible: false,
        image: null
      }
    });

    const loading = new Loading({
        $target
    });

    const darkmodeBtn = document.createElement('span');
    darkmodeBtn.className = 'darkmode-btn';
    darkmodeBtn.innerText = '🌕';

    $target.appendChild(darkmodeBtn);
  }

  setState(nextData) {
    console.log(this);
    this.data = nextData;
    this.searchResult.setState(nextData);
  }
}

```



```javascript
const API_ENDPOINT =
  "https://oivhcpn8r9.execute-api.ap-northeast-2.amazonaws.com/dev";


const request = async url =>{
  try {
    const respones = await fetch(url);
    if (reponse.ok) {
        const data= await reponse.json();
        return data;      
    }else{
        const errorData = await respones.json();
        throw errorData;
    }
  } catch (e) {
      throw{
          message: e.message,
          status: e.status
      }
  }
}

const api = {
  fetchCats: async keyword => {
    try{
      const data = await fetch(`${API_ENDPOINT}/api/cats/search?q=${keyword}`);
      const result2=[];
      const result=data.json();
      
      return{
        isError: false,
        data: result2
      }; 
  }catch(err){
      return {
          isError: true,
          data: err
      };
  }
},
  fetchRandomCats: async keyword =>{

  }
};


export { api };
```

### css grid

https://heropy.blog/2019/08/17/css-grid/

### Loading

```v
파일명 : Loading.js
```

```javascript
export default class Loading {
    constructor({ $target }) {
        this.spinnerWrapper = document.createElement('div');
        this.spinnerWrapper.className = 'spinner-wrapper';
        this.spinnerWrapper.classList.add('hidden');

        $target.appendChild(this.spinnerWrapper);

        this.render();
    }

    /*
        toggle 현 상태 = > 반대 상태
    */
    toggleSpinner() {
        const spinner = document.querySelector('.spinner-wrapper');
        spinner.classList.toggle('hidden');
    }

    render() {
        const spinnerImage = document.createElement('img');
        spinnerImage.className = 'spinner-image';
        spinnerImage.src = 'src/img/loading.gif';

        this.spinnerWrapper.appendChild(spinnerImage);
    }
}
```

```
파일명 : App.js
```

```javascript
this.searchInput = new SearchInput({
      $target,
      keywords,
      onSearch: async keyword => {
        loading.toggleSpinner();
        // const response =  await api.fetchCats(keyword);
        // if(!response.isError){
        //   console.log(response.data);
        //   SearchResult.setState(response.data);
        //   loading.toggleSpinner();
        // }else{
        //     console.log(response.data);
        // }


        await api.fetchCats(keyword).then(({ data }) =>{
          setItem('data',data.data);
          this.setState(data.data)
        });
        loading.toggleSpinner();
      }
    });
```





### Api

```javascript
// const API_ENDPOINT =
//   "https://oivhcpn8r9.execute-api.ap-northeast-2.amazonaws.com/dev";

// const api = {
  // fetchCats: async keyword => {
  //   return await fetch(`${API_ENDPOINT}/api/cats/search?q=${keyword}`).then(res =>
  //     res.json()
  //   );
//   }
// };
const API_ENDPOINT =
  "https://oivhcpn8r9.execute-api.ap-northeast-2.amazonaws.com/dev";


const request = async url =>{
  try {
    const reponse = await fetch(url);
    if (reponse.ok) {
        const data= await reponse.json();
        return data;      
    }else{
        const errorData = await respones.json();
        throw errorData;
    }
  } catch (e) {
      throw{
          message: e.message,
          status: e.status
      }
  }
}

const api = {
  fetchCats: async keyword => {
    try{
       const data = await request(`${API_ENDPOINT}/api/cats/search?q=${keyword}`);
      return{
        isError: false,
        data: data
      }; 
  }catch(e){
      return {
          isError: true,
          data: e
      };
  }
},
  fetchRandomCats: async ()=>{
    try {
        const result = await request(`${API_ENDPOINT}/api/cats/search?q=limit=50`);
        return {
          isError: false,
          data: result
        }
    } catch (e) {
      return{
        isError: true,
        data: e
      }
    }
  }
};


export { api };
```



### Keyword 세션 스토리지

```
파일명 : App.js
```

```javascript
import ImageInfo from "./components/ImageInfo.js";
import SearchInput from "./components/SearchInput.js";
import SearchResult from "./components/SearchResult.js";
import Loading from "./components/Loading.js";
import { api } from "./api/api.js";
import { getItem, setItem } from './utils/sessionStorage.js';

export default class App {
  $target = null;
  data = [];

  constructor($target) {
    const keywords = getItem('keywords');
    const data = getItem('data');
    this.$target = $target;

    this.searchInput = new SearchInput({
      $target,
      keywords,
      onSearch: async keyword => {
        loading.toggleSpinner();
        // const response =  await api.fetchCats(keyword);
        // if(!response.isError){
        //   console.log(response.data);
        //   SearchResult.setState(response.data);
        //   loading.toggleSpinner();
        // }else{
        //     console.log(response.data);
        // }


        await api.fetchCats(keyword).then(({ data }) =>{
          setItem('data',data.data);
          this.setState(data.data)
        });
        loading.toggleSpinner();
      }
    });

    this.searchResult = new SearchResult({
      $target,
      initialData: this.data,
      onClick: image => {
        this.imageInfo.setState({
          visible: true,
          image
        });
      }
    });

    this.imageInfo = new ImageInfo({
      $target,
      data: {
        visible: false,
        image: null
      }
    });

    const loading =new Loading({
      $target
    });

    const darkmodeBtn = document.createElement('span');
    darkmodeBtn.className = 'darkmode-btn';
    darkmodeBtn.innerText = '🌕';

    $target.appendChild(darkmodeBtn);

  }

  setState(nextData) {
    console.log(this);
    this.data = nextData;
    this.searchResult.setState(nextData);
  }
}

```

### 

```
파일명 : SearchInput.js
```

```javascript
import { getItem, setItem } from "../utils/sessionStorage.js";
const TEMPLATE = '<input type="text">';

export default class SearchInput {
  constructor({ $target,keywords, onSearch }) {
    // const $searchInput = document.createElement("input");
    // this.$searchInput = $searchInput;
    //this.$searchInput.placeholder = "고양이를 검색해보세요.|";

    //$target.appendChild($searchInput);
    //$searchInput.className = "SearchInput";

        // $searchInput.addEventListener("keyup", e => {
    //   if (e.keyCode === 13) {
    //     onSearch(e.target.value);
    //   }
    // });
    this.recent=keywords;
    this.onSearch=onSearch;
    this.section = document.createElement('section'); 
    this.section.className = 'searching-section';

    $target.appendChild(this.section);

    console.log("SearchInput created.", this);

    this.render();
    this.focusOnSearchBox();
  }

  searchByKeyword(keyword) {
    if (keyword.length == 0) return;

    this.addRecentKeyword(keyword);
    this.onSearch(keyword);
}

  focusOnSearchBox() {
    const searchBox = document.querySelector('.search-box');
    searchBox.focus();
  }

  addRecentKeyword(keyword) {
    if (this.recent.includes(keyword)) return;
    if (this.recent.length == 5) this.recent.shift();

    this.recent.push(keyword);
    setItem('keywords', this.recent);

    this.render();
}

  searchByKeyword(keyword) {
    if (keyword.length == 0) return;

    this.addRecentKeyword(keyword);
    this.onSearch(keyword);
  }

  deleteKeyword() {
      const searchBox = document.querySelector('.search-box');
      searchBox.value = '';
  }

  render() {
    this.section.innerHTML = '';

    const randomBtn = document.createElement('span');
    randomBtn.className = 'random-btn';
    randomBtn.innerText = '🐱';

    const wrapper = document.createElement('div');
    wrapper.className = 'search-box-wrapper';

    const searchBox = document.createElement('input');
    searchBox.className = 'search-box';
    searchBox.placeholder = '고양이를 검색하세요.';
    /*
        div blokc 속성, 블록 처럼 쌓인다.
        span inline 속성, 횡렬로 다닥다닥 붙는다.
    */
    const recentKeywords = document.createElement('div');
    recentKeywords.className = 'recent-keywords';

    this.recent.map(keyword => {
        const link = document.createElement('span');
        link.className = 'keyword';
        link.innerText = keyword;

        link.addEventListener('click', () => { this.searchByKeyword(keyword); });

        recentKeywords.appendChild(link);
    });

    //randomBtn.addEventListener('click', this.onRandom);
    searchBox.addEventListener('focus', this.deleteKeyword);
    searchBox.addEventListener('keyup', event => {
        if (event.keyCode == 13) {
            this.searchByKeyword(searchBox.value);
        }
    });


    wrapper.appendChild(searchBox);
    wrapper.appendChild(recentKeywords);
    //this.section.appendChild(randomBtn);
    this.section.appendChild(wrapper);
  }
}

```



```css
파일명 : style.css
```

```css
.search-box-wrapper {
  display: flex;
  flex-direction: column;
  width: 50%;
}

.search-box {
  font-size: 20px;
}

.recent-keywords {
  margin-top: 10px;
}
```



```
파일명 : SearchResult.js
```

```javascript
import Card from "./Card.js";

export default class SearchResult {

  constructor({ $target, initialData, onClick }) {
    this.$searchResult = document.createElement("div");
    this.$searchResult.className = "SearchResult";
    $target.appendChild(this.$searchResult);

    this.data = initialData;
    this.onClick = onClick;

    this.render();
  }

  setState(nextData) {
    this.data = nextData;
    this.render();
  }

  render() {
    console.log("data :");
    console.log(this.data);

    // Array.from() 메서드는 유사 배열 객체(array-like object)나
    // 반복 가능한 객체(iterable object)를 얕게 복사해새로운Array 객체를 만듭니다.
    this.$searchResult.innerHTML = Array.from(this.data)
      .map(
        cat => `
          <div class="item">
            <img src=${cat.url} alt=${cat.name} />
          </div>
        `
      )
      .join("");

    this.$searchResult.querySelectorAll(".item").forEach(($item, index) => {
      $item.addEventListener("click", () => {
        this.onClick(this.data[index]);
      });
    });
  }
}

```





# Reference

- [woohyeonjo 님 과제관 리뷰](https://github.com/woohyeonjo/ilovecat-javascript)