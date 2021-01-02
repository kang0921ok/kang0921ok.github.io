---
layout: default
title: Gradle 빌드 성능 최적화
parent: Gradle
grand_parent: Build Tool
permalink: /docs/build-tool/gradle/gradle-optimizing-build-time
---

# Gradle 빌드 성능 최적화
{: .no_toc }
```
공식 문서를 기반으로 1차 작성 완료
테스트 후 결과 공유 예정
```

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
## Easy improvements
- 최신 Gradle, JVM버전 사용
- [빌드 캐시](https://docs.gradle.org/nightly/userguide/build_cache.html)
   - ```
    //gradle.properties 
    org.gradle.caching=true 
  ```
- [병렬 실행](https://docs.gradle.org/nightly/userguide/performance.html#parallel_execution)
  - ```
    //gradle.properties 
    org.gradle.parallel=true
  ```
- [파일 시스템 감시 활성화](https://docs.gradle.org/nightly/userguide/gradle_daemon.html#sec:daemon_watch_fs)
   - 증분 빌드를 크게 가속화 시키는 방법
   - 2020.5.29 [파일 시스템 감시 소개글](https://blog.gradle.org/introducing-file-system-watching)
      - 향후 해당 옵션은 default true가 될 수 있음을 밝힘
      - ```
        //gradle.properties 
        //gradle 6.7이상
        org.gradle.vfs.watch=true  
      ```
- [데몬 힙 크기 조정](https://docs.gradle.org/nightly/userguide/performance.html#adjust_the_daemons_heap_size)
   - ```
     //gradle.properties
     //디폴트 1G 
     org.gradle.jvmargs=-Xmx2048M
   ``` 
  
## configuration
- 플러그인을 모든 프로젝트에 적용하는게 아니라 필요 프로젝트에만 적용
   
## dependency
- 동적 및 스냅샵 버전 최소화
   - `2.+`와 같이 +형태 지양
- 불필요하고 사용하지 않는 dependenccy 제거
- repository수 최소화
- 프로파일링을 통해 다운로드 속도가 느린 dependency확인
         
## 프로파일링
- [Grade Enterprise](https://gradle.com/) 빌드 스캔
  - `./gradlew build --scan` 을 수행 
  - `Publishing a build scan to scans.gradle.com requires accepting the Gradle Terms of Service defined at https://gradle.com/terms-of-service. Do you accept these terms? [yes, no]` yes 적고 엔터
  - `https://gradle.com/s/p7ge6o552lumg` 으로 최종 URL이 나옴
  - 페이지에 진입하면 email을 적는 화면이 나옴
  - email을 통해 인증을 하고 나면, 빌드 스캔 결과를 볼 수 있음
  - Grade Enterprise기능으로 30일 무료
- 간단한 프로파일링
  - `./gradlew --profile`  
  
## configuration-cache
- 아직 실험 기능
- [참고](https://docs.gradle.org/nightly/userguide/configuration_cache.html) 
     
## 참고
- [공식 문서 링크](https://docs.gradle.org/nightly/userguide/performance.html)
