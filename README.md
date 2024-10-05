# 🚀 1단계 - 상품 카테고리
## 진행 방식
미션은 과제 진행 요구 사항, 기능 요구 사항, 프로그래밍 요구 사항 세 가지로 구성되어 있다.
세 개의 요구 사항을 만족하기 위해 노력한다. 특히 기능을 구현하기 전에 기능 목록을 만들고, 기능 단위로 커밋 하는 방식으로 진행한다.
기능 요구 사항에 기재되지 않은 내용은 스스로 판단하여 구현한다.
## 과제 진행 요구 사항
기능을 구현하기 전 README.md에 구현할 기능 목록을 정리해 추가한다.
Git의 커밋 단위는 앞 단계에서 README.md에 정리한 기능 목록 단위로 추가한다.
AngularJS Git Commit Message Conventions을 참고해 커밋 메시지를 작성한다.
## 기능 요구 사항
상품 정보에 카테고리를 추가한다. 상품과 카테고리 모델 간의 관계를 고려하여 설계하고 구현한다.

상품에는 항상 하나의 카테고리가 있어야 한다.
상품 카테고리는 수정할 수 있다.
관리자 화면에서 상품을 추가할 때 카테고리를 지정할 수 있다.
카테고리는 1차 카테고리만 있으며 2차 카테고리는 고려하지 않는다.
카테고리의 예시는 아래와 같다.
교환권, 상품권, 뷰티, 패션, 식품, 리빙/도서, 레저/스포츠, 아티스트/캐릭터, 유아동/반려, 디지털/가전, 카카오프렌즈, 트렌드 선물, 백화점, ...
아래 예시와 같이 HTTP 메시지를 주고받도록 구현한다.

Request
```
GET /api/categories HTTP/1.1
Response
HTTP/1.1 200 
Content-Type: application/json

[
  {
    "id": 91,
    "name": "교환권",
    "color": "#6c95d1",
    "imageUrl": "https://gift-s.kakaocdn.net/dn/gift/images/m640/dimm_theme.png",
    "description": ""
  }
]
```
프로그래밍 요구 사항
구현한 기능에 대해 적절한 테스트 전략을 생각하고 작성한다.
힌트
아래의 DDL을 보고 유추한다.
```
create table category
(
    color       varchar(7)   not null,
    id          bigint       not null auto_increment,
    description varchar(255),
    image_url   varchar(255) not null,
    name        varchar(255) not null,
    primary key (id)
) engine=InnoDB

create table product
(
    price       integer      not null,
    category_id bigint       not null,
    id          bigint       not null auto_increment,
    name        varchar(15)  not null,
    image_url   varchar(255) not null,
    primary key (id)
) engine=InnoDB

alter table category
    add constraint uk_category unique (name)

alter table product
    add constraint fk_product_category_id_ref_category_id
        foreign key (category_id)
            references category (id)
```
