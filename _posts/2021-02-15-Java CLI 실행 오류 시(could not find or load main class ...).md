매번 Java는 이클립스에서만 컴파일하고 실행했었다.
이번에 WSL2로 `리눅스(우분투)` 환경을 구축하고 `CLI` 환경에 익숙해질겸 
Java를 컴파일 및 실행을 해보았다.

- VSCODE 상 파일은 다음과 같았다.

![04_vscode file list](\assets\ImagesForPosts\04_vscode file list.png)

 

```java
javac SinglyLinkedList.java
```

![04_vscode javac](\assets\ImagesForPosts\04_vscode javac.png)

- 컴파일 후 class파일들이 생성되었다.

![04_vscode file list2](\assets\ImagesForPosts\04_vscode file list2.png)



- 여기서 실행을 해보았다.

```java
java SinglyLinkedList
```

그랬더니 아래와 같이 오류가 난다.

![04_vscode java](\assets\ImagesForPosts\04_vscode java.png)

Could not find or load main class

- 아직 리눅스에 익숙치 않아서 생긴 문제인가 싶어서 윈도우의 cmd로도 해보지만 결과는 같았다.
-  다른 운영체제에서 같은 오류가 발생하는 것이라면 OS문제는 아니였다.
- 그래서 구글링을 하기 시작했다.
- 환경설정 CLASSPATH 문제라거나 VSCODE에서 Clean the java language server workspace를 해보랬지만 해결되지 않았다.
- 그러던 중 해결책을 발견했다.



해결책은 의외로 간단했고 평소 IDE로만 실행해서 간과하고 있었던 부분이었다.

> java는 full class name을 가지고 클래스 파일들을 찾기 때문에 
>
> parent directory(package root directory)에서 실행해야 한다고한다.



- 쉽게 말해서 Package명.클래스명 or Package명/클래스명 으로 해줘야 한다.

  ```java
  java LinkedList.SinglyLinkedList
  ```

![04_solution](\assets\ImagesForPosts\04_solution.png)



### 결론적으로 다음과 같이 습관을 들이면 좋을 것 같다.

**1. 패키지안으로 들어가지말고 패키지밖의 경로에서 컴파일하고 **

```java
javac LinkedList/SinglyLinkedList.java
```



**2. 실행시에는 패키지명.클래스파일 or 패키지명/클래스파일로 실행**

```java
java LinkedList/SinglyLinkedList
    		or
java LinkedList.SinglyLinkedList
```



