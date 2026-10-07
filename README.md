# 2026 빅콘테스트 — 기후 위기에 따른 취약 상권 영향 분석 (EDA·가설 설정)

제14회 2026 빅콘테스트 AI데이터 분석 분야. 이 저장소는 **EDA부터 가설 설정까지**를 다룬다.

## 진행 절차
| 단계 | 노트북 | 브랜치 | 상태 |
|---|---|---|---|
| 1. 전처리 | `notebooks/01_preprocessing.ipynb` | `ana-prep` | 완료 (카드·유동인구·기상·상가정보) |
| 2. 기술통계 | `notebooks/02_descriptive_stats.ipynb` | `ana-stat` | 완료 |
| 3. EDA | `notebooks/03_eda.ipynb` | `ana-eda` | 완료 |
| 4. 데이터 엔지니어링 (필요 시) | `notebooks/04_feature_engineering.ipynb` | `ana-engin` | 진행 (EDA에서 필요성 확인) |
| 5. 기후에 따른 피해 예측 | `notebooks/05_damage_prediction.ipynb` | `ana-pred` | |
| 6. 피해 지원금 최적화 | `notebooks/06_support_optimization.ipynb` | `ana-opt` | |
| 7. 가설 설정 | `notebooks/07_hypotheses.ipynb` | | |

## 검증할 가설 (초안)
1. 같은 100만원 피해라도 월 매출 규모(100만·500만·1,000만원)에 따라 **실제 타격(피해율)은 다르다.**
2. 그렇다면 피해액이 같은 업체에 **동일한 지원을 하는 것은 효율적이지 않다.**
3. 기후 유형(폭염·호우·한파·대설)에 따라 **업종별 피해 방향과 크기가 다르다.** (예: 폭염에 강한 업종과 약한 업종이 눈·한파에서는 반대로 나타날 수 있다 — 구체 업종은 데이터로 확인)

## 폴더 구조
```
eda_analysis/
├─ data/                 # git 제외 (대회 데이터 외부 공유 금지)
│  ├─ 신한카드_데이터/      # 대회 원본: 데이터1·2 (txt, cp949, 탭 구분)
│  ├─ sk통신인구_데이터/    # 대회 원본: 유동인구 성연령·시간대·요일 × 6개월 (csv, | 구분)
│  ├─ 테이블 정의서/
│  ├─ kma_asos_*.csv      # 외부: 기상청 ASOS 시간자료(2025H2)·일자료(2015~2024) — data/ 또는 data/external/
│  ├─ 소상공인시장진흥공단_상가(상권)정보_20260630/   # 외부: 상가정보 (서울·강원 파일 사용)
│  └─ processed/          # 노트북이 만든 가공 데이터 (언제든 재생성)
├─ references/           # 직접 만든 기준표 (업종 매핑, 공휴일)
└─ notebooks/            # 단계별 분석 노트북 (커널: Python (bigcon))
```

## 환경
```bash
conda activate bigcon
jupyter lab   # 또는 VS Code에서 커널 "Python (bigcon)" 선택
```
노트북은 `notebooks/` 폴더에서 순서대로 실행한다. 앞 단계가 `data/processed/`에 만든 파일을 다음 단계가 읽는다.
