# SFML 식물 키우기 게임

객체지향프로그래밍 기말 프로젝트로 제작한 C++/SFML 식물 키우기 게임입니다.
상점에서 식물을 구매하고 물과 비료를 관리하며 개화시켜 도감을 채웁니다.

## 구현 기능

- 네 개의 식물 슬롯에서 식물별 성장 상태와 수분, 토양 상태를 표시합니다.
- 식물마다 물 주기, 비료 주기, 하루 건너뛰기 중 하나를 선택합니다.
- 식물에 대한 행동을 마치면 다음 날로 진행하며 성장과 고사 여부를 갱신합니다.
- 골드로 식물을 구매하고 개화 보상과 일일 골드를 받습니다.
- 개화한 식물을 도감에 기록하고 식물 설명을 확인합니다.
- 사막, 온대, 열대 스테이지에서 총 12종의 식물을 다룹니다.
- 세 종류의 미니게임을 제공하며 성공 시 물과 비료를 보충합니다.
- 일부 미니게임에서는 점수에 따라 골드를 지급합니다.
- 스테이지별 배경음악과 설정 화면의 음악 재생/정지 기능을 제공합니다.

## 클래스 구성

- `GameState`는 날짜, 스테이지, 골드, 도감과 네 개의 `PlantSlot`, 물/비료 통을 관리합니다.
- `Plant`는 종, 성장 단계, 경과일, 수분과 토양 상태를 관리하고 `PlantSlot`은 식물 포인터를 보관합니다.
- `Bucket`을 상속한 `WaterBucket`과 `FertBucket`은 물과 비료 자원을 표현합니다.
- `BackGround`는 화면 전환을 담당하며 `MainSlot`, `Slot`, `Shop`, `Encyclopedia`, `EncyclopediaInfoView`, `Setting`, `Minigame`을 연결합니다.
- `Resource`는 식물별 가격, 개화일, 설명과 이미지 경로를 제공하며 미니게임은 `Game`, `Game2`, `AvoidPoop`로 구현되어 있습니다.

## 빌드 및 실행

CMake 3.16 이상, C++17 컴파일러와 Git이 필요합니다.
CMake의 FetchContent가 SFML `2.6.x` 브랜치를 내려받고 graphics/audio 모듈을 연결합니다.
CI 설정에는 Windows VS2019/VS2022, Linux GCC/Clang, macOS 구성이 포함되어 있습니다.
Linux 의존성은 CI 기준으로 다음과 같이 설치합니다.

```sh
sudo apt-get update
sudo apt-get install libxrandr-dev libxcursor-dev libudev-dev libopenal-dev libflac-dev libvorbis-dev libgl1-mesa-dev libegl1-mesa-dev
```

저장소 루트에서 다음 명령을 실행합니다.

```sh
cmake -S . -B build -DCMAKE_INSTALL_PREFIX=install
cmake --build build --config Release
cd build/bin
./SIMPLE_GAME
```

리소스 경로가 `../../assets/`와 `../../파일명` 기준이므로 작업 디렉터리는 `build/bin`으로 유지합니다.
Windows 다중 구성 빌드에서는 실행 파일이 `Release/SIMPLE_GAME.exe`에 생성될 수 있으므로 같은 작업 디렉터리에서 해당 경로로 실행합니다.
파일명 대소문자가 코드와 다른 리소스가 있어 대소문자를 구분하는 환경에서는 로딩에 문제가 생길 수 있습니다.
위 내용은 빌드 설정과 소스 기준이며 현재 환경에서 실행 검증한 결과는 아닙니다.

## 저장소 구조

- `src/main/main.cpp`는 실행 진입점이며 `src/lib/`에 게임 상태와 화면, 미니게임 코드가 있습니다.
- `assets/`에는 식물 이미지, 배경과 글꼴 등이 있습니다.
- 루트의 PNG/OGG 파일도 실행 중 사용하므로 기존 위치를 유지합니다.
- `CMakeLists.txt`는 빌드 대상과 의존성을, `.github/workflows/ci.yml`은 CI 빌드 구성을 정의합니다.

## 라이선스

MIT 라이선스를 따릅니다. 자세한 내용은 [LICENSE.md](LICENSE.md)를 참고해 주십시오.
