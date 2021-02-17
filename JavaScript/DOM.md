# DOM
## DOM(Document Object Model)이란?
  HTML 태그를 자바스크립트에서 이용할 수 있게 객체로 만든 것. 
  - 웹 페이지(HTML)를 스크립트 또는 프로그래밍 언어들에서 사용될 수 있게 객체로 만든 것. 연결시켜주는 역할을 담당한다. 
  - 태그를 조작하고, 삭제하고, 이벤트를 추가할 수 있다.
  - 정적인 웹페이지에 접근하여 동적으로 웹페이지를 변경하기 위한 유일한 방법은 메모리 상에 존재하는 DOM을 변경하는 것이고, 이때 필요한 것이 DOM에 접근하고 변경하는 프로퍼티와 메소드의 집합인 
  DOM API이다.
  - DOM(Document Object Model)은 HTML, XHTML, XML 문서의 객체를 나타내고 상호작용하기 위한, 언어에 제약되지 않는 크로스 플랫폼 협약
  DOM 트리의 객체는 해당 객체의 메서드를 사용해 조작할 수 있습니다.
  W3C는 HTML와 XML 문서를 객체로 추상화하는 Core Document Object Model을 표준화하고, 추상화를 조작하기 위한 방법도 정의합니다. DOM에 정의된 내용 중 일부는 다음과 같습니다.
  - DOM은 프로그래밍 언어와 독립적으로 디자인되었다. 주로 자바스크립트와 연관이 있지만, 다른 프로그래밍 언어로도 사용 가능
  ```
  # python DOM example
import xml.dom.minidom as m
doc = m.parse("C:\\Projects\\Py\\chap1.xml");
doc.nodeName # DOM property of document object;
p_list = doc.getElementsByTagName("para");
  ```
  ### DOM의 기능
  DOM은 HTML, ECMAScript에서 정의한 표준이 아닌 별개의 W3C의 공식 표준이며 플랫폼/프로그래밍 언어 중립적이다. DOM은 다음 두 가지 기능을 담당한다.
   1. HTML 문서에 대한 모델 구성 <br> 
      브라우저는 HTML 문서를 로드한 후 해당 문서에 대한 모델을 메모리에 생성한다. 이때 모델은 객체의 트리로 구성되는데 이것을 DOM tree라 한다.
   2. HTML 문서 내의 각 요소에 접근 / 수정 <br>
      DOM은 모델 내의 각 객체에 접근하고 수정할 수 있는 프로퍼티와 메소드를 제공한다. DOM이 수정되면 브라우저를 통해 사용자가 보게 될 내용 또한 변경된다.



## DOM tree
![dom-tree](https://user-images.githubusercontent.com/46726709/108145606-11157880-710f-11eb-9301-fd5b07a25f97.png)
  ### Dom tree의 네가지 노드
  - 문서 노드(Document Node)
  트리의 최상위에 존재하며 각각 요소, 어트리뷰트, 텍스트 노드에 접근하려면 문서 노드를 통해야 한다. 즉, DOM tree에 접근하기 위한 시작점(entry point)이다.
  - 요소 노드(Element Node)
  요소 노드는 HTML 요소를 표현한다. HTML 요소는 중첩에 의해 자손 관계를 가지며 이 관계를 통해 정보를 구조화한다. 따라서 요소 노드는 문서의 구조를 서술한다고 말 할 수 있다. 어트리뷰트, 텍스트 노드에 접근하려면 먼저 요소 노드를 찾아 접근해야 한다. 모든 요소 노드는 요소별 특성을 표현하기 위해 HTMLElement 객체를 상속한 객체로 구성된다. (그림: DOM tree의 객체 구성 참고)
  - 어트리뷰트 노드(Attribute Node)
  어트리뷰트 노드는 HTML 요소의 어트리뷰트를 표현한다. 어트리뷰트 노드는 해당 어트리뷰트가 지정된 요소의 자식이 아니라 해당 요소의 일부로 표현된다. 따라서 해당 요소 노드를 찾아 접근하면 어트리뷰트를 참조, 수정할 수 있다.
  - 텍스트 노드(Text Node)
  텍스트 노드는 HTML 요소의 텍스트를 표현한다. 텍스트 노드는 요소 노드의 자식이며 자신의 자식 노드를 가질 수 없다. 즉, 텍스트 노드는 DOM tree의 최종단이다.

  ### 정적생성과 동적생성
    - 웹 페이지를 처음 실행 할 때 HTML 태그로 생성 : 정적생성
    - 웹 페이지 실행 중 JavaScript로 문서 객체 생성 : 동적생성
    
   #### 문서의 동적 구성
    - DOM 객체 동적 생성 : document.createElement("태그이름");
      ```
      var newDiv = document.createElement("div");
      newDiv.innerHTML = "새로 생성된 DIV입니다.";
      newDiv.setAttribute("id","myDiv");
      newDiv.style.backgroundColor = "yellow";
      ```
    - DOM 트리에 삽입 : 부모.appendChild(DOM객체)
    - DOM 객체의 삭제 : 
  
  ## DOM의 핵심 interfaces
  document.getElementById(id)
  document.getElementsByTagName(name)
  document.createElement(name)
  parentNode.appendChild(node)
  element.innerHTML
  element.style.left
  element.setAttribute
  element.getAttribute
  element.addEventListener
  window.content
  window.onload
  window.dump
  window.scrollTo
  
  
  
  
  
  
  
 ### 참고
 [DOM (Document Object Model) ](https://poiemaweb.com/js-dom)<br>
 [DOM 소개 - Web API](https://developer.mozilla.org/ko/docs/Web/API/Document_Object_Model/%EC%86%8C%EA%B0%9C)<br>
