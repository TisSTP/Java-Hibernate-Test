# Java Test Hibernate


## Required Libraries
### 1. Hibernate
- [hibernate-core](https://mvnrepository.com/artifact/org.hibernate/hibernate-core)
- [hibernate-osgi](https://mvnrepository.com/artifact/org.hibernate/hibernate-osgi)
- [hibernate-spatial](https://mvnrepository.com/artifact/org.hibernate/spatial)
- [hibernate-envers](https://mvnrepository.com/artifact/org.hibernate/envers)
- [hibernate-hikaricp](https://mvnrepository.com/artifact/org.hibernate/hikaricp)
- [hibernate-c3p0](https://mvnrepository.com/artifact/org.hibernate/c3p0)
- [hibernate-proxool](https://mvnrepository.com/artifact/org.hibernate/proxool)
- [hibernate-infinispan](https://mvnrepository.com/artifact/org.hibernate/infinispan)
- [hibernate-ehcache](https://mvnrepository.com/artifact/org.hibernate/ehcache)

### 2. JDBC Driver
- [mysql-connector-java](https://mvnrepository.com/artifact/mysql/mysql-connector-java)


## Use Hibernate Annotations
1. add hibernate config `resources/hibernate.cfg.xml`
2. Annotate Java Class
> - Option 1 : XML config file(legacy)
> - Option 2 : Java Annotations (modern, preferred)
>> - step 1 : Map class to database table
>> - step 2 : Map fields to database columns

## Code Example

### Sample JDBC Connect DataBase 
```java
    /**
     * useSSL = false :: Get rid of MySQL SSL warnings.
     */
    String jdbcUrl = "jdbc:mysql://localhost:3306/{databasename}?useSSL=false";
    String user = "hbstudent";
    String pass = "hbstudent";

    try {
      Connection myConn = DriverManager.getConnection(jdbcUrl, user, pass);
    }
    catch (Exception exc) {
      exc.printStackTrace();
    }
```

### Sample Entity
```java
// step 1 : Map class to database table
@Entity
@Table(name = "student")
public class Student {
  //step 2 : Map fields to database columns
  @Id
  @Column(name = "id")
  private int id;
  
  @Column(name = "first_name")
  private String firstName;
}
```

### Sample SessionFactory & Session
```java
public static void main(String[] args){
  // create session factory
  SessionFactory factory = new Configuration()
      .configure("hibernate.cfg.xml")
      .addAnnotatedClass(Student.class)
      .buildSessionFactory();

  // create session
  Session session = factory.getCurrentSession();
  
  try {
    // use the session object to save Java Object
  }
  finally {
    factory.close();
  }
}
```

## References
- [luv2code](https://www.youtube.com/playlist?list=PLEAQNNR8IlB7fNkRsUgzrR346i-UqE5CG)