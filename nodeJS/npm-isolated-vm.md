# [npm] isolated vm

v8의 "독립된" 인터페이스에 접근하게 해주는 library for nodejs

다른 곳과 완전히 독립된 자바스크립트 환경을 생성한다.

이것은 nodejs 런타임에서 제공하는 관련 기능이 전혀 없는 새로운 자바스크립트 환경에서 코드를 실행하기 위한 매우 강력한 도구이다.

메모리 공간과 CPU 시간 사용이 제한되어있다.

`install --save isolated-vm`

## 보안

신뢰할 수 없는 코드를 실행하는 것은 아주 주의해서 접근해야 하는 엄청 어려운 문제이다. 신뢰할 수 없는 코드를 `isolated-vm`을 이용해 실행하는 것은 자동적으로 어플리케이션을 안전하게 만들어주는 것이 아니다. 이 라이브러리를 부주의하게 사용하거나 오용하는 것은 민감한 데이터를 유출되게할 수 있고 원치 않는 장치에 권한을 부여할 수 있습니다.

적어도 `isolated-vm`의 인스턴스가 외부로 유출되는 것에는 주의를 기울여야 한다. 

잠재적인 공격 코드에 대항하여 v8 untrusted code mitigations를 키는 것을 고려해야한다. 

## Isolate Class

- new ivm.Isolate

- ivm.Isolate.createSnapshot

- isolate.compileScript

- isolate.compileScriptSync

- isolate.compileModule

- isolate.compileModuleSync

- isolate.createContext

- isolate.createContextSync

- isolate.dispose

- isolate.getHeapStatistics

- isolate.getHeapStatisticsSync
...


## Context Class

- context.global
  컨텍스트의 글로벌 객체에 대한 참조값. 각각의 컨텍스트는 자신의 내장 객체와 글로벌 공간을 갖고있다.

- context.eval

- context.evalIgnored

- context.evalSync

## Script class

- script.release

- script.run

- script.runIgnore

- script.runSync

## Module

- module.dependencySpecifiers

- module.namespace
...

## Callback

## Reference

## ExtervalCopy

하지만 `gyp: No Xcode or CLT version detected!` 에러로 과제에 적용하지 못했다..
