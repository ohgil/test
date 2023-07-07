## 1차 요구사항 구현
- [X] 유저가 루트 url로 접속시에 게시글 리스트 페이지가 나온다.
- [X] 리스트 페이지에서는 등록 버튼이 있고 버튼을 누르면 http://주소:포트/article/create 경로로 이동하고 등록 폼이 나온다.
- [X] 등록을 하면 http://주소:포트/article/create로 POST 요청을 보내어 DB에 해당 내용을 저장한다.
- [X] 등록이 되면 해당 게시글 상세 페이지로 리다이렉트 된다. 해당 경로는 http://주소:포트/article/detail/{id} 가 된다.
- [X] 게시글 상세 페이지에는 목록 버튼이 있다. 목록 버튼을 누르면 게시글 리스트 페이지로 이동하게 된다.

## 미비사항 or 막힌 부분
- 결과값만 출력되어 html을 활용하려했으니 생각처럼 되지않음

## MVC 패턴
- 모델-뷰-컨트롤러의 약자로, 디자인 패턴의 하나이다. 비즈니스 처리 로직과 사용자 인터페이스를 구분시켜 서로 영향없이 개발이 가능하다는 장점이 있다(MVC패턴).
- 모델(Model)은 어플리케이션이 "무엇"을 할 지에 대한 정의한다. 처리되는 데이터, 데이터베이스, 내부 알고리즘 등 내부 비즈니스에 관한 로직의 처리를 수행한다. 즉 사용자에게 보이지 않는 로직.
- 뷰(View)는 말 그대로 사용자에게 보여지는 영역이다. JSP등 사용자 인터페이스를 담당한다.
- 컨트롤러(Controller)는 모델에게 "어떻게"할 것인지를 알려주며, 모델과 뷰 사이를 연결하는 역할을 한다. 사용자의 입출력을 받아 데이터를 처리한다.

## 스프링에서 의존성 주입(DI) 방법
1. Field Injection

Field Injection은 의존성을 주입하고 싶은 필드에 @Autowired 어노테이션을 붙여주면 의존성이 주입 됨
@Controller
public class ArticleController {

    @Autowired
    private ArticleService articleService;

}

2. Setter based Injection
setter메서드에 @Autowired 어노테이션을 붙여 의존성을 주입하는 방식

@Controller
public class ArticleController {

    private ArticleService articleService;
    
    @Autowired
    public void setArticleService(ArticleService articleService){
    	this.articleService = ariticleService;
    }

}

3. Constructor based Injection
생성자를 사용하여 의존성을 주입하는 방식.
lombok은 final로 선언된 필드로 생성자를 만들어줌

@RequiredArgsConstructor

@Controller
public class ArticleController {

    private final ArticleService articleService;
    
    public ArticleController(ArticleService articleService){
    	this.articleService = articleService;
    }

}
