# infra
[코드] → [빌드] → [테스트] → [배포] → [모니터링]
                ↘
               [인프라 프로비저닝]


Terraform + Jenkins 기반 DevOps 셋업
기능	도구
Git 저장소	GitHub
빌드/배포 자동화	Jenkins
인프라 관리	Terraform
이미지 빌드	Docker
이미지 저장	GitHub Container Registry
배포	ECS, EKS 또는 EC2
시크릿 관리	AWS Secrets Manager
모니터링	CloudWatch + Grafana
알림	Slack (Jenkins 연동)





1. 개발자 Git push

2. Jenkins가 파이프라인 실행
코드 검사 (SonarQube, Lint)
유닛/통합 테스트 (pytest 등)
Docker 이미지 빌드 → 레지스트리 푸시
Terraform으로 AWS 인프라 관리
Helm/Kubernetes로 앱 배포
Slack으로 배포 알림 전송

3. 실행 중인 서비스
Grafana + Prometheus로 상태 모니터링
Loki나 ELK로 로그 확인
AWS Secrets Manager로 민감 정보 관리


---
핵심 DevOps 구성 요소 & 도구 추천
분야	도구	설명 및 역할	비고
소스 저장소	GitHub, GitLab	코드 버전 관리	PR 기반 협업
CI/CD	Jenkins	빌드, 테스트, 배포 자동화	핵심
GitHub Actions	Jenkins 대안 또는 보완용	사용 간편
IaC	Terraform	인프라 선언형 구성	이미 사용 중
컨테이너화	Docker	앱/ML 모델 패키징	배포 표준화
오케스트레이션	Kubernetes (EKS, k3s 등)	컨테이너 관리	고가용성/확장 필요 시
도커 레지스트리	Docker Hub, GitHub Container Registry	이미지 저장소	Jenkins에서 푸시
시크릿 관리	AWS Secrets Manager, HashiCorp Vault	민감 정보 안전 관리	인증서, 키 등
로그/모니터링	Grafana, Prometheus, Loki, ELK	로그 수집 및 상태 모니터링	장애 대응 필수
알림/통합	Slack, Discord, Email, Opsgenie	배포 성공/실패 알림	Jenkins 연동
코드 품질 검사	SonarQube, ESLint, PyLint	정적 분석	PR에 자동 실행 가능
테스트 자동화	pytest, JUnit, Selenium	유닛/통합/UI 테스트	CI에 포함해야 함
보안	Trivy, Snyk	이미지/패키지 취약점 분석	자동 스캔
