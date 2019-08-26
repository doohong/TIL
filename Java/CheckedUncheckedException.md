---
title: "[JAVA]자바의 기본 개념 정리-9.Checked,Unchecked Exception"
date: 2019-05-30 22:20:00                             
tags: ["JAVA","Checked","Unchecked","Exception","Error"]
categories: JAVA                                        
---

# Exception Error
Exception은 주로 자바에서 제공하는 java.lang.Exception 클래스와 Exception 클래스의 서브클래스들이 쓰이는 상황을 말한다.

예외(Exception)는 체크 예외(Checked Exception)와 언체크 예외(Unchecked Exception), 두 가지로 나눌 수 있다. 언체크 예외는 RuntimeException을 상속한 것들을 말하고, 체크 예외는 이외의 예외들을 말한다. 물론, RuntimeException 또한 Exception 클래스의 서브 클래스이지만, 프로그램이 동작하는 상황에서 발생하는 예외를 처리한다는 점에서 조금 특별하게 취급한다.

오류(Error)는 시스템에 비정상적인 상황이 생겼을 때 발생한다. 이는 시스템 레벨에서 발생하기 때문에 심각한 수준의 오류이다. 따라서 개발자가 미리 예측하여 처리할 수 없기 때문에, 애플리케이션에서 오류에 대한 처리를 신경 쓰지 않아도 된다.

오류가 시스템 레벨에서 발생한다면, 예외(Exception)는 개발자가 구현한 로직에서 발생한다. 즉, 예외는 발생할 상황을 미리 예측하여 처리할 수 있다. 즉, 예외는 개발자가 처리할 수 있기 때문에 예외를 구분하고 그에 따른 처리 방법을 명확히 알고 적용하는 것이 중요하다.
![java_ExceptionError](/images/java/java_ExceptionError.png)
##  Checked Exception과 Unchecked(Runtime) Exception

![java_ExceptionError](/images/java/java_exception_table.png)

Checked Exception 과 Unchecked Exception의 가장 큰 차이는 '꼭 처리를 해야 하냐' 이다.

Checked Exception이 발생할 가능성이 있는 메소드라면 반드시 로직을 try/catch로 감싸거나 throw로 던져서 처리해야 한다. 

Unchecked Exception은 명시적인 예외처리를 하지 않아도 된다. 이 예외는 피할 수 있지만 개발자가 부주의해서 발생하는 경우가 대부분이고, 미리 예측하지 못했던 상황에서 발생하는 예외가 아니기 때문에 굳이 로직으로 처리를 할 필요가 없도록 만들어져 있다.

그리고 한 가지 더 인지하고 있으면 좋은 것이 있다. 바로 예외발생시 트랜잭션의 roll-back 여부이다. 기본적으로 Checked Exception은 예외가 발생하면 트랜잭션을 roll-back하지 않고 예외를 던져준다. 하지만 Unchecked Exception은 예외 발생 시 트랜잭션을 roll-back한다는 점에서 차이가 있다. 트랜잭션의 전파방식 즉, 어떻게 묶어놓느냐에 따라서 Checked Exception이냐 Unchecked Exception이냐의 영향도가 크다. roll-back이 되는 범위가 달라지기 때문에 개발자가 이를 인지하지 못하면, 실행결과가 맞지 않거나 예상치 못한 예외가 발생할 수 있다. 그러므로 이를 인지하고 트랜잭션을 적용시킬 때 전파방식(propagation behavior)과 롤백규칙 등을 적절히 사용하면 더욱 효율적인 애플리케이션을 구현할 수 있을 것이다.

## 전략

같은 작업이 진행 되더라도 발생하는 Exception에 따라 작업이 rollback(Unchecked Exception이) 될 수도 있고 commit(Checked Exception이)까지 완료될 수가 있다.

기본적으로 Checked Exception는 복구가 가능하다는 메커니즘을 가지고 있다. 그렇기 때문에 Rollback을 진행하지 않는다 생각한다. 

하지만 Checked Exception 예외가 발생했을 경우 복구 전략을 갖고 그것을 복구할 수 있는 경우는 적다.

따라서 복구할 수 없는 경우나 rollback을 시켜줘야 하는 경우 더욱더 구체적인 Unchecked Exception를 만들어 발생 시켜주는 것이 더욱 좋은 처리 방법이라 생각한다.