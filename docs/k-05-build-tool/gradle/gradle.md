---
layout: default
title: Gradle
parent: Build Tool
has_children: true
nav_order: 1
permalink: /docs/build-tool/gradle
---

# Gradle
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 설명
- [빌드 자동화 도구](https://stackoverflow.com/questions/7249871/what-is-a-build-tool) 중 하나로, 컴파일 및 링킹등을 통해 [Artifact](https://en.wikipedia.org/wiki/Artifact_(software_development))를 생성합니다.  
- 크게 2가지로 `1.빌드 스크립트를 작성`하고, `2.Gradle Wrapper를 통해 빌드`하여 결과물을 얻습니다. 
- Gradle 빌드 스크립트는 Groovy, Kotlin DSL을 사용하여 작성 됩니다.
- [Gradle Wrapper](https://docs.gradle.org/current/userguide/gradle_wrapper.html#gradle_wrapper)를 통해 Gradle을 따로 설치하지 않아도 사용 할 수 있습니다.
- 해당 문서에서는 어떻게 빌드 스크립트를 작성하고, 어떻게 빌드 할 수 있는지를 설명합니다.
- 추가적으로 멀티모듈을 구성하기 위한 내용도 포함합니다.

---

## 프로젝트 생성
```
대부분 초기 프로젝트 생성 시에 Gradle을 처음 만나게 됩니다.  
다양한 생성 방식이 있으나, Spring 프로젝트 생성 기준으로 적습니다.  
```
- [start.spring.io](https://start.spring.io/)에서 스프링 프로젝트를 생성합니다.
- Java를 선택할 경우 Groovy DSL이 사용되고 Kotlin을 선택할 경우 Kotlin DSL이 디폴트로 사용됩니다.
- <img width="221" alt="Kotlin DSL" src="https://user-images.githubusercontent.com/5463687/103441856-4156a400-4c94-11eb-85d0-87febfb6fe48.png">  
(Kotlin DSL로 생성된 모습)

---

## 구성 요소
```
위 캡쳐 중 빨간색으로 칠한 영역이 Gradle 초기 구성 요소입니다.
```
- .gradle
- gradle/wrapper/gradle-wrapper.jar
   - Gradle Wrapper에 대해서는 [아래 주제](#gradle-wrapper)에서 상세히 설명합니다.
   - Gradle 배포판을 다운로드 하기 위한 코드가 포함 된 Wrapper JAR 파일
- gradle/wrapper/gradle-wrapper.properties
   - Gradle Wrapper 런타임 동작 구성을 담당하는 속성 파일
- gradlew 
   - Gradle Wrapper로 빌드를 시작할 수 있는 쉘 스크립트
- gradlew.bat
   - Gradle Wrapper로 빌드를 시작할 수 있는 윈도우 배치 스크립트
- build.gradle.kts
   - 빌드 스크립트
- settings.gradle.kts
   - 빌드 이름 및 하위 프로젝트를 정의하는 설정 파일

---

## Gradle Wrapper
```
Gradle 빌드를 실행하는 데 권장되는 방법은 Gradle Wrapper (즉, 간단히 "Wrapper")를 사용하는 것입니다.
Wrapper는 Gradle의 선언 된 버전을 호출하여 필요한 경우 미리 다운로드하는 스크립트입니다. 
결과적으로 개발자는 수동 설치 프로세스를 따르지 않고도 Gradle 프로젝트를 빠르게 시작하고 실행할 수 있어 회사의 시간과 비용을 절약 할 수 있습니다.
```
<img width="746" alt="스크린샷 2021-01-02 오전 3 07 07" src="https://user-images.githubusercontent.com/5463687/103443983-9fd94d80-4ca7-11eb-9e2a-41a8a2f515f0.png">
([공식문서 발췌](https://docs.gradle.org/current/userguide/gradle_wrapper.html#gradle_wrapper))

---

## 빌드 & 실행
- gradle wrapper를 활용하여 빌드를 할 수 있습니다.  
   - `./gradlew build`  
- 빌드의 결과를 아래 위치에서 확인할 수 있습니다.  
   - `build/lib/demo-0.0.1-SNAPSHOT.jar`
   - <img width="260" alt="스크린샷 2021-01-02 오전 3 31 07" src="https://user-images.githubusercontent.com/5463687/103444354-fbf1a100-4caa-11eb-8bd1-c3fdb46dccb8.png">  
- 생성된 [jar](https://ko.wikipedia.org/wiki/JAR_(%ED%8C%8C%EC%9D%BC_%ED%8F%AC%EB%A7%B7))는 java로 실행 할 수 있습니다.  
   - `java -jar ./build/libs/demo-0.0.1-SNAPSHOT.jar`

### gradle.properties
- 해당 파일을 만들고 옵션을 정의하면, gradle은 빌드 시 해당 파일을 읽고 정의된 옵션을 활용합니다.
- 주요 옵션
   - org.gradle.caching=true 
   - [빌드 캐시](https://docs.gradle.org/current/userguide/build_cache.html#build_cache) 사용 
- 더 자세한 내용은 [공식 문서 링크](https://docs.gradle.org/current/userguide/build_environment.html#sec:gradle_configuration_properties) 참고
   
   
### 빌드 성능 최적화 
- Gradle Enterprise기능으로 빌드 성능 최적화를 위한 기능들이 제공 될 정도로 굉장히 중요한 부분 입니다.
- Gradle Enterprise는 30일 무료가 제공되나, 그 외에 개발자가 할 수 있는 방법들을 정리 합니다.
- [별도 문서로 작성]({{ site.baseurl }}{% link docs/k-05-build-tool/gradle/gradle-optimizing-build-time.md %})

---

## 빌드 스크립트

---
   
## Kotlin DSL

---

## 멀티 모듈

---

## 참고
[Gradle 공식 레퍼런스](https://docs.gradle.org/current/userguide/what_is_gradle.html)  
[우아한형제들 Kotlin DSL](https://woowabros.github.io/tools/2019/04/30/gradle-kotlin-dsl.html)
