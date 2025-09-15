# 실시간 딥페이크 스타일 트랜스퍼 명화 체험 프로젝트 - Artifiction

![프로젝트 소개](ARTIFICTION_소개.png)

## 🎨 프로젝트 개요
**Artifiction**은 딥페이크(Deepfake)와 스타일 트랜스퍼(Style Transfer) 기술을 결합하여, 관객이 실시간으로 명화 속 주인공이 되는 경험을 제공하는 인터랙티브 미디어 아트 프로젝트입니다. 관객은 웹캠 앞에 서면 자신의 얼굴이 명화 속 인물과 합성되고, 동시에 해당 명화의 화풍이 적용되어 마치 자신이 실제 명화의 일부가 된 듯한 몰입감 있는 경험을 하게 됩니다.

본 프로젝트는 3인 팀으로 진행되었으며, 기획 및 디자인 2명, 개발 1명으로 구성되었습니다. 개발 파트를 혼자 담당하며 상당히 고전했지만, 이를 통해 협업의 중요성과 체계적인 프로젝트 관리의 필요성을 깊이 깨닫게 된 의미 있는 프로젝트입니다.

## 💻 기술 스택
- **언어**: Python 3.10+
- **딥러닝 프레임워크**: PyTorch, ONNX Runtime
- **영상 처리**: OpenCV, MediaPipe
- **스타일 트랜스퍼**: Fast Style Transfer (PyTorch 구현)
- **딥페이크**: InsightFace, GFPGAN
- **게임 엔진**: Unity (3D 환경 구축)
- **GUI**: Gradio
- **멀티프로세싱**: multiprocessing, threading

## ✨ 주요 기능
- **실시간 얼굴 스왑**: 웹캠으로 촬영한 관객의 얼굴을 사전 제작된 영상 속 인물의 얼굴과 실시간으로 교체
- **다중 스타일 적용**: 고흐, 모네, 피카소 등 다양한 명화 스타일을 실시간으로 영상에 적용
- **고품질 얼굴 복원**: GFPGAN을 활용한 딥페이크 결과물의 품질 향상
- **Unity 3D 환경 연동**: 명화를 3D 공간으로 재해석한 몰입형 환경 제공
- **프레임 최적화**: GPU 가속 및 멀티스레딩을 통한 실시간 처리 (30FPS 이상)
- **직관적인 UI**: Gradio를 활용한 사용자 친화적 인터페이스

## 🎭 작품 플로우
1. **스타일 학습 단계**: Style Transfer Network에 다양한 명화 스타일을 사전 학습
2. **3D 환경 구축**: Unity로 명화 배경을 3D 맵으로 재구성하고 인물 영상 배치
3. **실시간 얼굴 감지**: MediaPipe를 통한 관객 얼굴 실시간 감지 및 추적
4. **딥페이크 적용**: InsightFace 모델을 활용한 실시간 얼굴 스왑
5. **스타일 변환**: 선택된 명화 스타일을 딥페이크 결과물에 실시간 적용
6. **최종 출력**: 변환된 영상을 대형 스크린에 실시간 송출

## 📂 프로젝트 구조
```
ARTIFICTION/
├── src/                    # 스타일 트랜스퍼 핵심 모듈
│   ├── transform.py        # 스타일 변환 로직
│   ├── optimize.py         # 모델 최적화
│   ├── vgg.py             # VGG 네트워크 구현
│   └── utils.py           # 유틸리티 함수
├── modules/               # 딥페이크 및 얼굴 처리 모듈
│   ├── core.py           # 핵심 처리 로직
│   ├── face_analyser.py  # 얼굴 분석 모듈
│   ├── capturer.py       # 웹캠 캡처 모듈
│   ├── ui.py             # Gradio UI 구현
│   └── processors/       # 각종 처리 모듈
├── final/                # 스타일 및 결과물 저장
│   ├── styles/          # 명화 스타일 이미지
│   ├── targets/         # 타겟 영상
│   └── outputs/         # 변환 결과물
├── models/              # AI 모델 파일 (Git에서 제외)
├── run.py              # 메인 실행 파일
├── style.py            # 스타일 적용 실행 파일
└── transform_video.py  # 비디오 변환 유틸리티
```

## 🚀 실행 방법

### 1. 환경 설정
```bash
# 저장소 클론
git clone https://github.com/yourusername/Artifiction.git
cd Artifiction

# 가상환경 생성 및 활성화
python -m venv venv
source venv/bin/activate  # Linux/macOS
# 또는
.\venv\Scripts\activate  # Windows

# 의존성 설치
pip install -r requirements.txt
```

### 2. 모델 다운로드
다음 모델들을 다운로드하여 `models/` 폴더에 저장:
- **GFPGANv1.4.pth**: [다운로드](https://github.com/TencentARC/GFPGAN/releases/download/v1.3.4/GFPGANv1.4.pth)
- **inswapper_128_fp16.onnx**: [다운로드](https://huggingface.co/hacksider/deep-live-cam/resolve/main/inswapper_128_fp16.onnx)

### 3. 프로그램 실행
```bash
# 기본 실행
python run.py

# GPU 가속 실행 (CUDA)
python run.py --execution-provider cuda

# 스타일 트랜스퍼만 실행
python style.py --style [스타일명] --content [입력영상]
```

## 🔧 개발 상세

### 수행 역할
- **오픈소스 통합**: deep-live-cam과 fast-style-transfer를 결합한 통합 파이프라인 구현
- **실시간 최적화**: GPU 병렬 처리 및 프레임 버퍼링을 통한 30FPS 이상 실시간성 확보
- **Unity 연동**: Python-Unity 소켓 통신을 통한 실시간 데이터 스트리밍
- **모델 학습**: 10개 이상의 명화 스타일 학습 및 최적화

### 기술적 도전과 해결
- **레이턴시 문제**: 멀티스레딩과 프레임 큐잉으로 처리 파이프라인 병렬화
- **메모리 관리**: 모델 경량화 및 선택적 로딩으로 메모리 사용량 50% 감소
- **품질 vs 속도**: GFPGAN 후처리를 선택적으로 적용하여 성능과 품질 균형 유지

## 📝 참고 자료
- [Deep-Live-Cam](https://github.com/hacksider/Deep-Live-Cam) - 실시간 딥페이크 베이스
- [Fast Style Transfer](https://github.com/pytorch/examples/tree/master/fast_neural_style) - 스타일 트랜스퍼 구현
- [GFPGAN](https://github.com/TencentARC/GFPGAN) - 얼굴 복원 모델

## 📄 라이선스
본 프로젝트는 MIT 라이선스 하에 배포됩니다. 자세한 내용은 [LICENSE](LICENSE) 파일을 참조하세요.

## 🤝 기여
프로젝트 개선을 위한 제안이나 버그 리포트는 언제든 환영합니다. Issue를 생성하거나 Pull Request를 보내주세요.

## 📧 문의
프로젝트 관련 문의사항이 있으시면 Issues 탭을 통해 연락 주시기 바랍니다.
