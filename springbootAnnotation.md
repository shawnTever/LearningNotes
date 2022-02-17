# Springboot 注解

- [Springboot 注解](#springboot-注解)
  - [A @Autowired](#a-autowired)
  - [B @Bean](#b-bean)
  - [C @Controller、@Configuration](#c-controllerconfiguration)
  - [D](#d)
  - [E](#e)
  - [F](#f)
  - [G](#g)
  - [H](#h)
  - [I](#i)
  - [J](#j)
  - [K](#k)
  - [L](#l)
  - [M @mapper](#m-mapper)
  - [N](#n)
  - [O](#o)
  - [P @PostConstruct、@PreDestroy](#p-postconstructpredestroy)
  - [Q @Qualifier](#q-qualifier)
  - [R @Repository（@Service、@Controller 和 @Component）、@RequestMapping、@ResponseBody、@RunWith](#r-repositoryservicecontroller-和-componentrequestmappingresponsebodyrunwith)
  - [S @Service、@Scope、@SpringBootTest](#s-servicescopespringboottest)
  - [T](#t)
  - [U](#u)
  - [V @Value](#v-value)
  - [W](#w)
  - [X](#x)
  - [Y](#y)
  - [Z](#z)

- [主页](README.md)

## A @Autowired

@Autowired：自动注入。

## B @Bean

@Bean：一个方法级别上的注解，主要用在@Configuration注解的类里，也可以用在@Component注解的类里。凡是子类及带有方法或属性的类都要加上注册Bean到Spring IoC的注解。方法名即为bean的名字

## C @Controller、@Configuration

@Controller：在tomcat启动的时候，把这个类作为一个控制器加载到Spring的Bean工厂。是一个泛化的概念，仅仅表示一个组件 (Bean) ，可以作用在任何层次。

@Configuration： 用于定义配置类

@ContextConfiguration：Spring整合JUnit4测试时，使用注解引入多个配置文件

## D

## E

## F

## G

## H

## I

## J

## K

## L

## M @mapper

@mapper：给mapper接口自动生成一个实现类，让spring对mapper接口的bean进行管理，并且可以省略去写复杂的xml文件

## N

## O

## P @PostConstruct、@PreDestroy

@PostConstruct：该注解被用来修饰一个非静态的void（）方法。被@PostConstruct修饰的方法会在服务器加载Servlet的时候运行，并且只会被服务器调用一次，类似于Serclet的inti()方法。被@PostConstruct修饰的方法会在构造函数之后，init()方法之前运行。

@PreDestroy：被@PreDestroy修饰的方法会在服务器卸载Servlet的时候运行，并且只会被服务器调用一次，类似于Servlet的destroy()方法。被@PreDestroy修饰的方法会在destroy()方法之后运行，在Servlet被彻底卸载之前。

## Q @Qualifier

@Qualifier：在使用@Autowire自动注入的时候，加上@Qualifier(“test”)可以指定注入哪个对象；可以作为筛选的限定符，我们在做自定义注解时可以在其定义上增加@Qualifier，用来筛选需要的对象。

## R @Repository（@Service、@Controller 和 @Component）、@RequestMapping、@ResponseBody、@RunWith

@Repository：标注数据访问组件，即DAO组件

@Repository、@Service、@Controller 和 @Component 均为将类标识为Bean

@RequestMapping：映射请求，也就是通过它来指定控制器可以处理哪些URL请求。在类的级别上的注解会将一个特定请求或者请求模式映射到一个控制器之上

@ResponseBody：将java对象转为json格式的数据，@ResponseBody是作用在方法上的，在使用 @RequestMapping 后，返回值通常解析为跳转路径，
加上 @Responsebody 表示该方法的返回结果直接写入 HTTP response body 中

@RunWith(SpringRunner.class)：测试启动器，有了它这些类才能实例化到spring容器中。在IDEA里识别为一个JUNIT的运行环境，相当于就是一个自识别的RUNWITH环境配置。但在其他IDE里并没有。

## S @Service、@Scope、@SpringBootTest

@Service：通常作用在业务层，但是目前该功能与 @Component 相同。

@Scope：@Scope注解是springIoc容器中的一个作用域，在 Spring IoC 容器中具有以下几种作用域：基本作用域singleton（单例）、prototype(多例)，Web 作用域（reqeust、session、globalsession）。其中singleton实例的意思不管你使用多少次在springIOC容器中只会存在一个实例

@SpringBootTest：是SpringBoot自1.4.0版本开始引入的一个用于测试的注解。

## T

## U

## V @Value

@Value：将环境变量写在配置文件中，让他根据运行的环境进行读取。

## W

## X

## Y

## Z
