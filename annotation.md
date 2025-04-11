## GenerationType IDENTITY, SEQUENCE, TABLE

[Spring Boot Annotation @GeneratedValue | by Hrishi D | Medium](https://medium.com/@swapnildalimbkar01/spring-boot-annotation-generatedvalue-55e257fbd3d9)

## 양방향 관계

팀과 선수의 관계는 양방향 관계이다. 소유 측(Owning Side)는 데이터베이스에 외래 키를 가지는 쪽이다. 즉 관계를 저장하는 쪽이 소유 측이다. 역방향 측(Inverse Side)는 자바 코드에서만 관계를 표현하고, 실제 데이터베이스에는 영향을 주지 않는다.
팀과 선수에서 선수는 team_id가 존재하므로 관계를 저장하는 소유 측이며, 팀은 선수 목록을 참조하지만 이 관계를 나타내는 컬럼이 존재하지 않는다. mappedBy 속성으로 소유 측을 지정 가능하다.

## @OneToOne, @OneToMany, @ManyToMany

테이블간의 논리적인 연결을 형성한다.

1. @OneToMany

- Inverse Side를 나타낸다.
- parent-child 관계로, 하나의 entity가 여러 entity를 가진다.
- mappedBy, cascade, fetch 속성을 가진다.

[Understanding JPA Relationships: @ManyToMany, @OneToMany, and @OneToOne | by Davoud Badamchi | Feb, 2025 | Medium](https://medium.com/@davoud.badamchi/understanding-jpa-relationships-manytomany-onetomany-and-onetoone-ab84aa1953c1)

## Cascade, FetchType

1. Lazy Fetch Type
   Hibernate가 entity마다 proxy를 생성한다. 관련한 데이터를 호출할 때 가져온다. 대용량 데이터가 존재하는 one-to-many, many-to-many에서 유용하다.

2. Eager Fetch Type
   proxy 없이 곧 바로 데이터를 가져온다. one-to-one 관계에선 이롭다.

[Hibernate Relations, Cascade Types, Fetch Types and Orphan Removal | by Berat Yesbek | Medium](https://beratyesbek.medium.com/hibernate-relations-cascade-types-fetch-types-and-orphan-removal-ad9681758843)

[Working with JPA FetchTypes. When working in SEF, we get many… | by Piumal Rathnayake | Medium](https://piumal1999.medium.com/working-with-jpa-fetchtypes-dc09386cf2ea)

## @email annotation

@Email은 EmailValidator와 연결된다. EmailValidator는 값을 가져와서 pattern matching을 실행한다. null인경우 validation을 건너띄기 때문에 필요에 따라 @NotNull이 존재해야한다.

[How Spring Boot Handles Validation Annotations | Medium](https://medium.com/@AlexanderObregon/how-spring-boot-handles-validation-annotations-33b987c1a5cb)
