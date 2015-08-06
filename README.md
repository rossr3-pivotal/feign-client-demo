# feign-client-demo

A simple Spring Feign Client Demo that runs locally:

```
gradle clean build
java -jar build/libs/demo-0.0.1-SNAPSHOT.jar
```

but not when it is pushed to PWS.

```
cf push feigntest -p build/libs/demo-0.0.1-SNAPSHOT.jar
```

For some reason, the application does not start, giving the following stacktrace:

OUT org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'myController': Injection of autowired dependencies failed; nested exception is org.springframework.beans.factory.BeanCreationException: Could not autowire field: private io.pivotal.demo.RepairClient io.pivotal.demo.MyController.repairClient; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'repairClient': FactoryBean threw exception on object creation; nested exception is java.lang.NullPointerException: encoder
OUT 	at org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor.postProcessPropertyValues(AutowiredAnnotationBeanPostProcessor.java:334)
OUT 	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.populateBean(AbstractAutowireCapableBeanFactory.java:1210)
OUT 	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:537)
OUT 	at org.springframework.beans.factory.support.AbstractBeanFactory$1.getObject(AbstractBeanFactory.java:303)
OUT 	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:230)
OUT 	at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:299)
OUT 	at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:194)
OUT 	at org.springframework.beans.factory.support.DefaultListableBeanFactory.preInstantiateSingletons(DefaultListableBeanFactory.java:755)
OUT 	at org.springframework.context.support.AbstractApplicationContext.finishBeanFactoryInitialization(AbstractApplicationContext.java:757)
OUT 	at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:480)
OUT 	at org.springframework.boot.context.embedded.EmbeddedWebApplicationContext.refresh(EmbeddedWebApplicationContext.java:118)
OUT 	at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:686)
OUT 	at org.springframework.boot.SpringApplication.run(SpringApplication.java:320)
OUT 	at org.springframework.boot.SpringApplication.run(SpringApplication.java:957)
OUT 	at org.springframework.boot.SpringApplication.run(SpringApplication.java:946)
OUT 	at io.pivotal.demo.FeignApplication.main(FeignApplication.java:12)
OUT 	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
OUT 	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
OUT 	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
OUT 	at java.lang.reflect.Method.invoke(Method.java:497)
OUT 	at org.springframework.boot.loader.MainMethodRunner.run(MainMethodRunner.java:53)
OUT 	at java.lang.Thread.run(Thread.java:745)
OUT Caused by: org.springframework.beans.factory.BeanCreationException: Could not autowire field: private io.pivotal.demo.RepairClient io.pivotal.demo.MyController.repairClient; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'repairClient': FactoryBean threw exception on object creation; nested exception is java.lang.NullPointerException: encoder
OUT 	at org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor$AutowiredFieldElement.inject(AutowiredAnnotationBeanPostProcessor.java:561)
OUT 	at org.springframework.beans.factory.annotation.InjectionMetadata.inject(InjectionMetadata.java:88)
OUT 	at org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor.postProcessPropertyValues(AutowiredAnnotationBeanPostProcessor.java:331)
OUT 	... 22 common frames omitted
OUT Caused by: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'repairClient': FactoryBean threw exception on object creation; nested exception is java.lang.NullPointerException: encoder
OUT 	at org.springframework.beans.factory.support.FactoryBeanRegistrySupport.doGetObjectFromFactoryBean(FactoryBeanRegistrySupport.java:175)
OUT 	at org.springframework.beans.factory.support.FactoryBeanRegistrySupport.getObjectFromFactoryBean(FactoryBeanRegistrySupport.java:103)
OUT 	at org.springframework.beans.factory.support.AbstractBeanFactory.getObjectForBeanInstance(AbstractBeanFactory.java:1517)
OUT 	at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:251)
OUT 	at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:194)
OUT 	at org.springframework.beans.factory.support.DefaultListableBeanFactory.findAutowireCandidates(DefaultListableBeanFactory.java:1120)
OUT 	at org.springframework.beans.factory.support.DefaultListableBeanFactory.doResolveDependency(DefaultListableBeanFactory.java:1044)
OUT 	at org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor$AutowiredFieldElement.inject(AutowiredAnnotationBeanPostProcessor.java:533)
OUT 	... 24 common frames omitted
OUT Caused by: java.lang.NullPointerException: encoder
OUT 	at feign.Util.checkNotNull(Util.java:95)
OUT 	at feign.ReflectiveFeign$ParseHandlersByName.<init>(ReflectiveFeign.java:132)
OUT 	at feign.Feign$Builder.target(Feign.java:166)
OUT 	at org.springframework.cloud.netflix.feign.FeignClientFactoryBean.loadBalance(FeignClientFactoryBean.java:126)
OUT 	at org.springframework.cloud.netflix.feign.FeignClientFactoryBean.getObject(FeignClientFactoryBean.java:136)
OUT 	at org.springframework.beans.factory.support.FactoryBeanRegistrySupport.doGetObjectFromFactoryBean(FactoryBeanRegistrySupport.java:168)
OUT 	... 32 common frames omitted
