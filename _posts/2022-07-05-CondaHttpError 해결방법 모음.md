---
title: "CondaHttpError 해결방법 모음"
date: 2022-07-05T18:08:30-04:00
categories:
  - '2022-07 TIL'
tags:
  - '20220705'
  - 'TIL'
  - 'Pytorch'
  - 'Anaconda'
  - 'CondaHttpError'
---

# 개요

* MMSkeleton 모듈 관련해서 예제 파일을 실행하려 했다.

* 하지만 pytorch 설치가 말썽을 일으켰고, 근 2일 가까이를 인터넷을 뒤져 얻어낸 답들을 정리하기로 했다.

# CondaHttpError

## 개요

* conda install fails - HTTP 000 CONNECTION FAILED라는 경고문과 함께, conda를 통한 몇몇 패키지의 설치가 진행되지 않는 현상이다.

## 통상적으로 알려진 해결법

1. openssl 설치

    * 종종 openssl 모듈이 가상환경에 설치되지 않아 발생된다고도 한다.
      ```
      conda install openssl
      ```

    * 다만, 이렇게 설치하는 과정 자체가 CondaHttpError로 막히는 경우 역시 존재했다.

2. conda에서 ssl 사용 옵션 꺼보기

    * 기본적으로 ssl 인증서에 관련한 문제인 만큼, conda의 ssl 기능을 꺼버리는 방법이다.

      ```
      conda config --set ssl_verify no
      ```

    * 보안에 관해 문제가 발생할수 있다.
    * 또한, 80%의 인터넷 사이트에서 1번과 2번 방법을 제시하고 있었다.

3. [정해영님의 방법](http://blog.genoglobe.com/2019/04/ssl-conda.html)

    * 위의 2번 방법과 원리는 같지만, 보안 인증서를 별도로 생성하여 conda 설정파일에 먹임으로서 ssl 인증을 우회한다.

      ```
      # echo quit | openssl s_client -showcerts -servername "www.anaconda.com" -connect www.anaconda.com:443 > cacert.pem
      depth=1 C = KR, O = Somansa, CN = Somansa Root CA
      verify error:num=19:self signed certificate in certificate chain
      DONE
      # conda config --set ssl_verify cacert.pem 
      # conda update conda
      Collecting package metadata: done
      Solving environment: done

      # All requested packages already installed.

      # conda install -c bioconda trimmomatic
      ...성공!
      ```

    * 단, echo로 시작하는 명령문에서 볼수 있듯, Linux 계열에서 인증서 파일을 생성하는 법이기에 Windows를 사용중인 나는 사용할수 없는 방법이었다.

## 나의 해결방법

* 나는 우선 노트북으로 여태 작업을 수행하고 있었고, 노트북은 기본적으로 와이파이를 통해 연결되기에 방화벽이 어느정도 일을 하고있다고 생각했다.

* PIP를 통해 pytorch를 받는 방법도 실험해봤는데, 받던 중간에 443번 포트에서 무언가 이상이 생겼다며 다운로드를 거부하는것을 발견했다.

* 아마 443번이 SSL인증에 관련된 포트일것이라 확신하고, <U>방화벽의 인바운드 규칙을 수정해서 443번 포트에 한해 방화벽을 꺼버리기로 했다.</U>

  1. [제어판 - 시스템 및 보안 - Windows Defender 방화벽 - 고급 설정] 으로 들어간다.

  2. 인바운드 규칙 메뉴 우클릭 - 새 규칙

  3. 포트 - 특정 로컬 포트(443) - 연결 허용 - 도메인&개인&공용 모두 체크

  4. 해당 인바운드 규칙의 이름을 정해주고 마침을 눌러 마무리.

* 방화벽의 새 규칙이 적용된 후, 다시 다운로드를 실행해보니 잘 되는것을 확인할수 있었다.

* 다만, 이 방식은 보안에 대단히 안좋은 방식이므로, 사용후 만들었던 인바운드 규칙을 제거해야 한다는 단점이 있다.




