---
title: "WSL2 (Windows Subsystem Linux 2) 환경에서 VSCode 사용하기"
date: 2020-07-31 11:17:00 -0400
categories: dev_tool
---
- 개요  
  윈도우10에서 VSCode와 우분투(Ubuntu) 개발환경을 설정하는 방법  
  기준 환경 : Windows 10 64bit 및 __WSL2__
- 가. 윈도우 최신버전 업데이트  
  윈도우 설정 -> 업데이트 확인 -> 설치 -> (요구시) 재부팅 -> 반복   
  업데이트 더이상 안 뜰 때까지 __반복__   
  완료 시에도 Windows10 Version __2004__ 이상 버전이 아닐 경우 아래 사이트에서 수동 업데이트   
  <https://www.microsoft.com/ko-kr/software-download/windows10>
## 나. WSL2 및 docker for windows 설치
  - 아래 블로그 참조하여 nginx 설치 직전까지 진행
    - <https://www.44bits.io/ko/post/wsl2-install-and-basic-usage>
    - 검증을 위해 nginx를 실습해봐도 좋다
    - docker run hello-world 로 검증하는 방법도 있음
    - WSL 세팅 중에 계정명을 물어보면 임의로 Windows 계정명과 동일하게 설정
## 다. Windows Terminal 편의 설정
  - 기본 탭 WSL로 변경
    - "defaultProfile" 값을 Ubuntu의 guid 값과 일치시켜준다
    - 프로파일 순서를 바꿔서 Ubuntu를 첫번째로 해주는 것도 편하다
  - 기본 디렉토리를 WSL 홈으로 변경
    - Ubuntu 프로파일에 다음사항 추가 ```"startingDirectory": "//wsl$/Ubuntu/home/{유저명}"```
    - <https://github.com/microsoft/terminal/issues/2849> 참조
  - setting.json 예시
```
{
  ...
  "defaultProfile": "{2c4de342-38b7-51cf-b940-2309a097f518}", // 하단 Ubuntu 프로파일과 guid 일치 시켜 줌
  ...
  "profiles":
  {
      ...
      "list":
      [
          {
              "guid": "{2c4de342-38b7-51cf-b940-2309a097f518}",
              "hidden": false,
              "name": "Ubuntu",
              "source": "Windows.Terminal.Wsl",
              "startingDirectory": "//wsl$/Ubuntu/home/kang" // 기본 디렉토리 설정
          },
          {
              "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
              "name": "Windows PowerShell",
              ...
```
## 라. VS Code 설치 및 초기 설정
  - <https://code.visualstudio.com/>
  - 좌측 extension 메뉴 -> remote development extension pack 검색 및 설치
## 마. 지역 설정
  - 한국 로케일 설정 <https://beomi.github.io/2017/07/10/Ubuntu-Locale-to-ko_KR/>
  - 카카오 미러 설정
```
sudo sed -i 's/archive.ubuntu.com/mirror.kakao.com/g' /etc/apt/sources.list \
sudo sed -i 's/security.ubuntu.com/mirror.kakao.com/g' /etc/apt/sources.list \
sudo apt-get update
```
## 바. WSL 원격 개발 환경 구동
  1. 선행 사항 완료 후 Windows terminal 로 WSL 쉘(Ubuntu) 접속
  2. workspace 디렉토리 생성하여 해당 위치로 이동
    - ~/workspace 추천
  3. 해당 디렉토리에서 VS Code 실행 ```code .```
  4. 좌측 하단 __WSL: Ubuntu__ 배너 확인되면 성공
