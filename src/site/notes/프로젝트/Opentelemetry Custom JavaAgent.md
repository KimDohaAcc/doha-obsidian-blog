---
{"dg-publish":true,"permalink":"//opentelemetry-custom-java-agent/","dgPassFrontmatter":true}
---


## Javaagent란?

JVM에서 동작하는 Java 애플리케이션으로, JVM에 특별한 기능을 추가하거나 동작을 수정할 수 있는 도구이다. JVM에 동적으로 로드되어 실행 중인 Java 애플리케이션에 영향을 줄 수 있다

### 특징

1. 바이트 코드 조작
    1. 클래스 로더가 클래스를 로드하기 전이나 후에 바이트코드를 동적으로 수정할 수 있다. 이를 통해 기존 클래스의 동작을 변경하거나 새로운 기능을 추가할 수 있다. 대표적인 예로 메소드 실행 시간 측정, 로깅, 성능 모니터링 등을 할 수 있다
2. JVM 이벤트 모니터링
    1. 클래스 로딩, 객체 생성, 가비지 컬렉션 등의 이벤트를 감지하고 원하는 동작을 수행할 수 있따
3. 런타임 정보 수집
    1. 실행 중인 Java 애플리케이션의 런타임 정보를 수집할 수 있다. 힙 메모리 사용량, 스레드 정보, 클래스 히스토그램 등의 정보를 얻을 수 있다

### Javaagent 사용

1. JavaAgent 클래스 작성 클래스 작성 후 premain() 의 메소드를 구현하여 에이전트가 초기화될 때 실행될 코드를 작성한다
2. MANIFEST.MF 파일 작성 jar 파일의 메타데이터를 포함하는 MANIFEST.MF 파일을 작성하고, premain-class 속성을 사용하여 javaagent 클래스를 지정한다
3. jar 파일 생성 및 JVM 옵션 설정

Opentelemetry는 기본적으로 자동 계측 시 사용하는 Javaagent를 제공하기 있기 때문에 따로 클래스를 만들 거나 하진 않았다. 대신 기능을 상속 받아 커스텀한 클래스를 넣어주기 위해서 META-INF에 커스텀한 클래스를 작성해주어 사용했다.

## 커스텀 클래스 등록

### 등록 방법

서비스의 META-INF/services 디렉토리에 인터페이스 구현체를 등록해주면 된다

직접 넣어줘도 되고, @AutoService 어노테이션을 사용하면 자동으로 해당 인터페이스의 구현체로 등록 된다

### DemoAutoConfigurationCustomizerProvider

`AutoConfigurationCustomizerProvider`를 상속 받아서 TracerProvider나 Propagator 등을 설정하는 클래스

### OmegiExtendedInstrumentation & OmegiExtendedInstrumentationModule

`TypeInstrumentation`를 상속 받아서 extension을 구성하는 클래스.

ByteBuddy의 @OnMethodEnter 와 @OnMethodExit를 사용해서 메소드 진입 시 span을 생성하며 exception 발생 시 에러를 상태로 기록해주었다.

`InstrumentationModule`을 상속받고 있는 Module에서 이러한 extension을 등록한다

### OmegiTraceSpanExporter & OmegiTraceSpanExporterFactory

`SpanExporter`를 상속 받아 TraceSpanExporter를 구성하는 클래스.

kafka를 구성해서 span으로 내보낼 수 있게 한다. span은 exception 위주로 속성을 달아주었다. kafka의 bootstrap server는 사용자에게 입력 받을 수 있다

`ConfigurableSpanExporterProvider`

를 상속 받는 OmegiTraceSpanExporterFactory에서 exporter를 등록했다

sampleExporter도 거의 동일한 구성으로 제작하였고, 대신 traceId의 hashcode를 기반으로 설정해 준 샘플의 텀마다 내보내도록 하였다

## build.gradle 의 구성

`com.github.johnrengelman.shadow`를 사용하였다.

shadow는 gradle 플러그인 중 하나로, jar를 생성하는 데 사용하며 모든 종속성을 하나의 jar로 패키징할 때 유용하다.

extendedAgent라는 task를 만들어서 기존의 opentelemetry javaagent를 의존성으로 가져온 후 파일의 내용을 추출한다.

기존 파일의 META-INF/MANIFEST.MF 를 추출해 새로운 JAR 파일의 매니페스트로 사용하도록 설정한다.

이후 shadowJar 태스크에서 생성된 JAR 파일의 내용을 extensions 디렉토리에 추가하면 새로 구성된 custom 클래스의 메타데이터가 들어간 새로운 JavaAgent가 생성된다.

## 트러블 슈팅

1. extendedAgent를 어떻게 적용해야 하는지를 몰라서 계속 일반 build로 시도해 기존 opentelemetry의 javaagent가 베이스로 적용되지 않았다.

extendedAgent를 실행시키는 방법은 간단하다.

1. ./gradlew extendedAgent 를 실행하거나
2. gradle을 열어 Tasks - other - extendedAgent를 실행하면 된다

1. 커스텀을 기존 jar에 적용하는 방법을 몰라 github에서 opentelemetry를 커스텀 한 jar파일을 확인하고 싶었다. jar파일을 열어서 내용을 볼 수 있는 도구 중에 JD-GUI 를 사용했다. 여기서 확인할 수 있었던 것은, 메타데이터 수정이 들어가야 기존 인터페이스 구현체가 들어가지 않고 내가 만든 커스텀 구현체가 들어간다는 것이다.

그리고 커스텀한 것은 아니지만 기본으로 들어가는 설정을 변경하고 싶다면 custom configuration을 구성해서 적용하면 된다. 마찬가지로 configuration 도 메타데이터를 등록해야 한다