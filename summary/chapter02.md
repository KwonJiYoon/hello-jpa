### Chpaer02 - JPA 시작



<b> @Entity </b> <br>
해당 클래스를 테이블과 매핑한다는 것을 JPA에 알려주고, @Entity가 사용된 클래스를 엔티티 클래스라고 한다.
<br><br>

<b> @Table </b> <br>
엔티티 클래스에 매핑할 테이블 정보를 알려줌.<br>
name 속성을 사용하여 테이블과 매핑하였고, 이 어노테이션을 생략하면 엔티티 이름으로 테이블과 매핑한다.
<br><br>

<b> @Id </b> <br>
엔티티 클래스의 필드를 테이블의 기본키 (Primary Key)에 매핑하고, @Id가 사용된 필드를 식별자 필드라고 한다.
<br><br>

<b> @Column </b> <br>
필드를 컬럼에 매핑하고 name 속성을 사용해서 컬럼과 매핑.
매핑 어노테이션을 생략한 경우, 필드명을 사용해서 컬럼명과 매핑한다.<br>
만약 대소문자를 구분하는 데이터베이스를 사용하는 경우 name 속성을 사용하여 명시적으로 매핑해야한다.
<br><br>

><b> 엔티티 매니저 팩토리 생성 </b> <br>
JPA를 시작하려면 persistence.xml의 설정 정보를 사용해 엔티티 매니저 팩토리를 생성해야한다. <br>
이때 사용하는 Persistence 클래스는 엔티티 매니저 팩토리를 생성해서 JPA를 사용할 수 있게 준비한다. <br>
```
EntityManagerFactory emf = Persistence.createEntityManagerFactory("jpabook");
```
META-INF/persistence.xml에서 이름이 jpabook인 영속성 유닛을 찾아서 엔티티 매니저 팩토리를 생성한다.<br>
persistence.xml의 설정 정보를 읽어서 JPA를 동작시키기 위한 기반 객체를 만들고, <br>
JPA 구현체에 따라서 데이터베이스 커넥션 풀도 생성하므로 엔티티 매니저 팩토리는 애플리케이션 전체에서 딱 한 번만<br>
생성하고 공유하여 사용해야한다.
<br><br>

><b> 엔티티 매니저 생성 </b> <br>
```
EntityManager em = emf.createEntityManager();
```
엔티티 매지너 팩토리에서 엔티티 매니저 생성<br>
JPA의 기능 대부분이 이 엔티티 매니저가 제공하고, 대표적으로는 엔티티를 데이터베이스에 등록/수정/삭제/조회할 수 있다.<br>
내부의 데이터소스(데이터베이스 커넥션)를 유지하며 데이터베이스와 통신하며, 데이터베이스 커넥션과 밀접한 관계가 있으므로 스레드간에 공유하고나 재사용하면 안 된다.
<br><br>

><b> 종료 </b> <br>
```
em.close();
```
사용이 끝난 엔티티 매니저는 반드시 종료해야한다.
```
emf.close(); 
```
애플리케이션을 종료할 때 엔티티 매니저 팩토리도 종료해야한다.
<br><br>

><b> 등록 </b> <br>
```
em.persist(member);
```
엔티티를 저장하려면 엔티티 매니저의 persist() 메소드에 저장할 엔티티를 넘겨준다.
<br><br>

><b> 수정 </b> <br>
```
member.setAge(20);
```
JPA는 어떤 엔티티가 변경되었는지 추적하는 기능을 갖추고 있기 때문에, 엔티티의 값만 변경하면 update SQL을 
생성해서 데이터베이스의 값을 변경한다. 따라서 update 메소드가 없다.
<br><br>

><b> 삭제 </b> <br>
```
em.remove(member);
```
엔티티를 삭제하려면 엔티티 매니저의 remove() 메소드에 삭제할 엔티티를 넘겨준다.
<br><br>

><b> 한견 조회 </b> <br>
```
Member findMember = em.find(Member.class, id);
```
find() 메소드는 조회할 엔티티 타입과 @Id로 데이터베이스 테이블의 기본 키와 매핑한 식벽자 값으로 엔티티 하나를<br>
조회하는 가장 단순한 조회 메소드이다.
<br><br>

><b> JPQL </b> <br>
```
List<Member> members = em.createQuery("select m from Member m", Member.class)
                        .getResultList();
```
JPA는 엔티티 객체를 중심으로 개발하기에 검색을 할 때도 테이블이 아닌 엔티티 객체를 대상으로 검색해야하는 문제가 있다.<br>
애플리케이션이 필요한 데이터만 데이터베이스에서 불러오려면 결국 검색 조건이 포함된 SQL을 사용해야한다.<br>
JPQL이라는 객체지향 쿼리 언어로 위 문제를 해결할 수 있다.<br>
JPQL은 <b>엔티티 객체</b>가 대상이고 SQL은 <b>데이터베이스 테이블</b>을 대상으로 한다.<br>

위 코드에서 from Member은 MEMBER 테이블이 아닌 Member 엔티티 객체이고 <b>JPQL은 데이터베이스 테이블을 전혀 알지 못한다.</b><br>
JPQL을 사용하려면 em.createQuery(JPQL, 반환타입) 메소드로 쿼리 객체를 생성한 후 getResultList() 메소드를 호출하면 된다.
<br><br>
